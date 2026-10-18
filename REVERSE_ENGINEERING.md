# M-VAVE FM1 Hardware Architecture, Protocol & Reverse Engineering Reference

Technical reference and reverse-engineering findings for the **M-VAVE FM1** synthesizer (powered by the **JieLi AC791N** processor / WL82 series) — covering hardware analysis, bootloader memory maps, OTA MIDI SysEx protocol specifications, binary offsets, recovery vectors, and disassembly tooling.

> Part of the [M-VAVE FM1 Resource Hub](README.md).

---

## 1. Hardware & Device Ecosystem Overview

### 1.1. Target Device & Processor
* **Target Device:** **M-VAVE FM1** (FM Synthesizer / MIDI Controller).
* **Processor SoC:** **JieLi AC791N Series** (WL82 family, dual-core 32-bit `pi32v2` RISC core with FPU, DC–320 MHz, integrated Wi-Fi 802.11b/g/n and Bluetooth 2.1+EDR / BLE 5.3).
* **Exact IC Model on PCB:** **JieLi AC7912AB** (marking code `C156211-11A-B` on PCB, package **QFN-68**, 7 × 7 mm, 68 pins, internal 4M×16-bit / 8 MB SDRAM, external SPI NOR Flash).
* **Official Development Board:** **JL_AC79_DevKit V1.0** (AC791N evaluation kit).
  * [JL_AC79_DevKit V1.0 Official Documentation](https://doc.zh-jieli.com/AC79/zh-cn/release_v1.0.3/board_description/board_overview/index.html)
  * Note: In retail/marketplace listings, this devboard has been found available for purchase primarily on **Taobao**.
  
  ![JL_AC79_DevKit V1.0](photos/devboard.webp)

* **Datasheets & Reference Schematics:**
  * Official repository upstream: [amitv87/fw-AC79_AIoT_SDK doc/datasheet](https://github.com/amitv87/fw-AC79_AIoT_SDK/tree/release/AC79NN_SDK_V1.2.0/doc/datasheet)
  * Reference schematics: [AC791N Schematics (GitHub)](https://github.com/amitv87/fw-AC79_AIoT_SDK/tree/release/AC79NN_SDK_V1.2.0/doc/datasheet/AC791N%E8%A7%84%E6%A0%BC%E4%B9%A6/schematic)
    * `AC7912AB智能WiFi摄像头（IPC）V1.0_20220606.pdf` (Direct schematic reference for AC7912AB QFN68)
    * `JL_AC79_DevKitBoard V1.0原理图.pdf` & `JL_AC79_WIFI V1.0原理图.pdf`
    * `AC7916A_四声道+推屏+DVP摄像头+麦+SD卡参考原理图V1.0-20230323.pdf`
    * `AC7911BA_WIFI音箱参考原理图(双MIC)-V1.2-20220429.pdf`
  * Chip Selection Guide & Datasheets:
    * `AC791N选型表231122.xlsx` (Complete chip comparison and feature matrix)
    * `AC7912A_Datasheet_V1.2_20230303.pdf` (AC7912AB QFN-68 7×7 mm datasheet)
    * `AC7916A_Datasheet_V2.1_20230418.pdf` (AC7916A QFN-76 9×9 mm datasheet)
    * `AC7915A_Datasheet_V1.2_20230303.pdf` / `AC7915B6A_Datasheet_V1.2_20230303.pdf` (QFN-52)
    * `AC7911B_Datasheet_V1.3_20230303.pdf` (QFN-48)
    * `AC7913A0_Datasheet_V1.2_20230303.pdf` / `AC7913A6` / `AC7913B8` (QFN-40)

* **Synthesizer Product Page:** [Cuvave / M-VAVE FM-1 Product Page](http://www.cuvave.com/product?id=fm-1)
* **Latest Available Synthesizer Firmware:** [FM-1.fwsc (v15 2026-07-30)](https://yms-file-store.oss-cn-hongkong.aliyuncs.com/software/firmware/FM-1.fwsc)
* **Firmware v15 Entropy Analysis:** ([Source Issue #1](https://github.com/aroum/fm1-custom-fw/issues/1))
  
  ![Firmware v15 Entropy Analysis](photos/firmware_entropy.png)

* **M-VAVE Ecosystem:** Many other M-VAVE audio products (MIDI foot controllers, audio interfaces, and digital pedals) use the same JieLi AC791N / AC69xx processor platform and share similar OTA firmware architectures. Notably, the **M-VAVE SMK-37 Pro** keyboard controller uses the identical AC791N (WL82) SoC, second-stage bootloader, update loader, and chip key, making FM-1 custom firmwares portable to it via board HAL adaptors (see [fm1-to-smk37](https://github.com/genkigenki/fm1-to-smk37) and [Snoop37](https://github.com/genkigenki/Snoop37)). Note: SMK-37 Pro flash contains unique factory key/pad calibration (`0xC1000` USRTRIM `trimdat`) that must never be overwritten.

### 1.2. Complete Hardware Pinout Mapping & Free GPIOs (AC7912AB QFN-68)

Verified from SLOOP/Felucca hardware HAL drivers (`fm1_gpio.h`, `fm1_lcd_hw.h`, `fm1_input.h`, `fm1_audio.h`, `fm1_adc.h`, `fm1_uart.h`, `fm1_usb.h`), high-resolution PCB teardown photography, and the official `AC7912A_Datasheet_V1.2` specification:

#### 1. Display (Color TFT LCD 240 × 240)
* **SPI Controller:** Hardware SPI1 master interface.
* **Pin 5 (`PC10`):** SPI1 MOSI (`DO`) — LCD serial data out.
* **Pin 6 (`PC9`):** SPI1 SCK (`CLK`) — LCD serial clock.
* **Pin 7 (`PC8`):** GPIO OUT — LCD Data/Command select (`D/C`: Low = Command, High = Data).
* **Pin 8 (`PC7`):** GPIO OUT — LCD Chip Select (`CS`, active low).
* **Pin 47 (`PA2`):** GPIO OUT — LCD Backlight power control (`BL`, active low / low = ON).

#### 2. Key Matrix, Rotary Encoders & LEDs
* **Matrix Architecture:** 11-column × 6-row diode-isolated matrix driven by a cascaded dual shift register chain:
  * **Shift Registers:** Two 74HC595 ICs (U2 and U3 on PCB) driving 11 active column lines.
  * **Pin 45 (`PA4`):** 74HC595 Serial Data Input (`SER`).
  * **Pin 46 (`PA3`):** 74HC595 Shift Clock (`SRCLK`).
  * **Pin 48 (`PA1`):** 74HC595 Storage Latch Clock (`RCLK`).
* **Matrix Input Rows (Inputs with internal Pull-Up, active low):**
  * **Pin 49 (`PA0`):** Row 0 — Rotary Encoders 0 to 5 (Knobs 1–4, ALGORITHM, etc.).
  * **Pin 44 (`PA5`):** Row 1 — Button Matrix row.
  * **Pin 43 (`PA6`):** Row 2 — Button & Key Matrix row.
  * **Pin 42 (`PA7`):** Row 3 — Note Key Matrix row.
  * **Pin 41 (`PA8`):** Row 4 — Note Key Matrix row.
  * **Pin 16 (`PB7`):** Row 5 — Rotary Encoder 6.
* **Matrix Column LED Drivers (High-Drive Push-Pull Outputs):**
  * **Pin 40 (`PA9`):** LED Row 1 driver (lights LEDs across active columns matching row PA5).
  * **Pin 39 (`PA10`):** LED Row 2 driver (lights LEDs across active columns matching row PA6).
  * **Pin 58 (`PH6`):** LED Row 3 driver (lights LEDs across active columns matching row PA7).
  * **Pin 55 (`PH9`):** LED Row 4 driver (lights LEDs across active columns matching row PA8).

#### 3. Audio & External DAC/Codec
* **Audio Bus:** JieLi `ALNK0` I2S / Left-Justified 24-bit DMA engine running into an external audio codec / headphone amp.
* **Pin 15 (`PC0`):** Codec Control Line (`MCLK` / configuration line).
* **Pin 14 (`PC1`):** Codec Control Line (`BCLK` / bit clock).
* **Pin 13 (`PC2`):** Codec Control Line (`LRCK` / word select).
* **Pin 9 (`PC6`):** Codec Power & Reset control line (active high).
* **Pin 50 (`DACFL`):** On-chip 16-bit analog DAC Left channel output (auxiliary line).

#### 4. Analog Inputs (10-bit SAR ADC)
* **Pin 17 (`PB6` / `ADC4`):** MASTER Volume Potentiometer analog wiper voltage (`ch 4`).
* **Pin 27 (`PB1` / `ADC3`):** Li-Po Battery Voltage divider input (`ch 3`).

#### 5. Communications & USB
* **Pin 56 (`PH8`):** UART1 RX input mapped via IOMAP crossbar for **3.5 mm TRS MIDI IN** (31,250 baud, DMA ring buffer).
* **Pin 36 (`FUSBDM`):** USB Full-Speed D- (connected to USB-C port).
* **Pin 37 (`FUSBDP`):** USB Full-Speed D+ (connected to USB-C port, with software 1.5 kΩ pull-up attach).
* **Pin 68 (`WFRF`):** 2.4 GHz RF Antenna pin (soldered directly to the internal insulated red wire antenna on PCB marked `天线`).

#### 6. Power & System Pins
* **Pin 33 (`VBAT`):** Battery power input.
* **Pin 34 (`SW`):** DC-DC switching node connected to external inductor `L2` (10 µH, marked `100`).
* **Pin 35 (`PGND`):** Power Ground.
* **Pin 32 (`DCVDD14`):** DC-DC 1.4V Core Power supply.
* **Pin 21 (`DVDD`):** Digital Core 1.2V LDO supply.
* **Pin 4, 38, 45 (`IOVDD`):** 3.3V Digital I/O Power supply rails.
* **Pin 51 (`DACVDD`):** DAC 3.3V supply.
* **Pin 54 (`AHVDD`):** Analog 3.3V supply.
* **Pin 52 (`VCM`):** Audio common mode bias voltage filter capacitor.
* **Pin 53 (`HPVSS`):** Headphone/Audio Ground.
* **Pin 2, 3 (`XOSCI`, `XOSCO`):** 24.000 MHz system crystal oscillator (Y1).
* **Pin 30, 31 (`PR1`, `PR0`):** Power management / RTC pins.
* **Pin 1, 66 (`WFVDD14`), Pin 67 (`WFVDD33A`), Pin 65 (`WFVSS`):** Wi-Fi/Bluetooth RF power and ground pins.

#### 7. Free / Unused Pins Available for Hardware Mods
Out of 68 physical pins on the AC7912AB SoC, **18 GPIO lines** and **2 High-Speed USB differential lines** are currently unused and free for expansion:

| Pin No. | Pin Name | Peripheral Capabilities | Mod Potential / Recommended Usage |
|:---:|:---:|:---|:---|
| **10** | `PC5` | GPIO / ALNK0_DAT2A / SPI1_DOA / UART0_TXA | Extra digital I/O, UART debug TX, extra SPI |
| **11** | `PC4` | GPIO / ALNK0_DAT1A / SPI1_CLKA / UART0_RXA | Extra digital I/O, UART debug RX, extra SPI |
| **12** | `PC3` | GPIO / ALNK0_DAT0A / SPI1_DIA | Extra digital I/O, secondary I2S audio data in/out |
| **18** | `PB5` | GPIO / SPI1_DOB / UART2_TXC | Additional serial comms or SPI peripheral |
| **19** | `PB3` | GPIO / UART1_TXC / SPI1_DIB | **UART1 TX (Hardware MIDI OUT)** mod pin |
| **20** | `PB2` | GPIO / UART1_RXC / PWM output | Extra PWM or digital control line |
| **22** | `PD5` | GPIO / SD0_DAT3A / SPI2_DO | SD card interface (DAT3) / SPI2 |
| **23** | `PD4` | GPIO / SD0_DAT2A / SPI2_CLK | SD card interface (DAT2) / SPI2 |
| **24** | `PD6` | GPIO / SD0_DAT1A / SFGAT | SD card interface (DAT1) |
| **25** | `PD1` | GPIO / SD0_DAT0A / I2C SDA | **MicroSD Card Mod** (DAT0) or hardware I2C SDA |
| **26** | `PD0` | GPIO / SD0_CLK / I2C SCL | **MicroSD Card Mod** (CLK) or hardware I2C SCL |
| **28** | `HUSBDM` | USB 2.0 High-Speed D- | High-speed USB host / PHY expansion |
| **29** | `HUSBDP` | USB 2.0 High-Speed D+ | High-speed USB host / PHY expansion |
| **57** | `PH7` | GPIO / PAP_D7 / ADC ch 7 | Extra ADC channel / analog input mod |
| **59** | `PH5` | GPIO / EMI_D21 / ADC ch 6 | Extra ADC channel / analog sensor mod |
| **60** | `PH4` | GPIO / EMI_D20 / ADC ch 5 | Extra ADC channel / analog sensor mod |
| **61** | `PH3` | GPIO / PAP_D3 / PWM | Extra PWM timer output |
| **62** | `PH2` | GPIO / PAP_D2 / Timer capture | General Purpose Digital I/O |
| **63** | `PH1` | GPIO / PAP_D1 / Timer capture | General Purpose Digital I/O |
| **64** | `PH0` | GPIO / PAP_D0 / Touch input | Capacitive touch pad expansion or Digital I/O |

> [!TIP]
> **Key Hardware Modding Opportunities:**
> * **Hardware MIDI OUT (`PB3`):** The FM-1 possesses physical 3.5 mm TRS MIDI IN (driven via `PH8` / UART1 RX), but lacks a hardware MIDI OUT jack. Pin 19 (`PB3`) can be configured as UART1 TX to drive a standard MIDI OUT / THRU circuit.
> * **MicroSD Card Slot (`PD0`, `PD1`, `PD4`, `PD5`, `PD6`):** The JieLi SD0 hardware controller is fully routed to Port D pins (`PD0`–`PD6`). Adding a MicroSD card breakout would allow reading GBs of samples, soundfonts, and tracker songs directly.
> * **I2C Bus Expansion (`PD0`/`PD1`):** Can be used to interface external OLED displays, sensors, or I2C expanders without interfering with the internal LCD and 74HC595 shift registers.

### 1.3. Hardware PCB Characteristics & Recovery Vector
* **No Debug Ports / Jumpers:** The M-VAVE FM1 PCB contains **no exposed debug headers** (JTAG, SWD, or UART debug pads).
* **No Recovery Buttons:** There are **no hidden jumper pins or physical recovery buttons** on the board for forcing bootloader / DFU mode.
* **Firmware Update & Recovery Vectors:**
  * **Standard User-Mode Flashing:** MIDI SysEx over USB is the official, application-level firmware update channel available on the device.
  * **Software-Bricked Recovery over Plain USB (Mask-ROM `WL82 UBOOT1.00` mode):**
    * When a firmware flash is corrupt, incomplete, or fails to boot, the JieLi AC791N mask-ROM automatically drops into its built-in USB recovery mass-storage mode: **`WL82 UBOOT1.00 USB Device`** (`VID: 0x4C4A`, `PID: 0x8057`, SCSI / Mass Storage interface).
    * In this state, **no extra hardware or case opening is required**: a standard USB data cable and [`jl-uboot-tool`](https://github.com/kagaimiq/jl-uboot-tool) on Windows/Linux (or automated via [`MvaveFM1Unbricker`](https://github.com/Quixotic7/MvaveFM1Unbricker)) are sufficient to communicate directly with the SPI flash via SCSI pass-through.
    * **Triggering ROM Boot without Hardware Dongles ([MvaveFM1Unbricker Troubleshooting](https://github.com/Quixotic7/MvaveFM1Unbricker#the-fm-1-does-not-show-up-as-wl82-uboot100-at-all)):**
      * **Two-minute Watchdog Wait:** Felucca-family firmwares arm a watchdog and boot-loop guard; leaving a crashing unit on for two minutes lets the guard automatically enter ROM boot after two consecutive reset loops.
      * **Update-Mode Key Hold:** Switch off, hold **OCT- and OCT+** simultaneously, switch on, and keep holding for 10 seconds. If the firmware boots enough to reach input polling, this forces update mode.
      * **Three Quick Restarts:** Turn on for 10 s, off; on for 10 s, off; on. If each boot crashes, the third consecutive failure forces the processor into ROM boot.
    * **Crucial Flash Addressing Rules:**
      * **Bootloader / Head (`0x00000000` – `0x00003FFF`):** NEVER overwrite or erase this 16 KB region. It holds the partition header and boot vector.
      * **App Code Area (`0x00004000` – `0x00092FFF`):** Extracted application binaries (e.g., from `FM-1.fwsc` via [`fm1_extract_app.py`](https://gist.github.com/Acrawf1/ae2b9930b49231db397568cfc2abc2a8)) MUST be written starting at offset **`0x4000`**, never at `0x0`.
      * **Felucca 0.9 → 1.0.x Upgrade Brick Fix:** Upgrading from Felucca 0.9-beta to 1.0.x can soft-brick due to incompatible legacy preset structures. Erasing `0x97000 0x8000` and `0xFC000 0x2000` via `jl-uboot-tool` resolves this issue.
    * Full step-by-step unbricking guide: [Reddit: Unbricking a soft-bricked FM-1 (black screen / "WL82 UBOOT1.00") over plain USB](https://www.reddit.com/r/MVaveFM1/comments/1wz48t7/guide_unbricking_a_softbricked_fm1_black_screen/).
  * **Hardware Recovery Vector (Forcing Mask-ROM via USB_KEY Dongle):**
    * If the processor hangs without falling into `WL82 UBOOT1.00` automatically (e.g., due to an interrupted write mid-flash from a depleted battery), the mask-ROM download mode can be forced via an external RP2040 dongle ([FM-1 Transporter](https://github.com/kurogedelic/FM-1-transporter) / [mvave-fm1-open-firmware](https://github.com/ip2k/mvave-fm1-open-firmware) / [MvaveFM1Unbricker](https://github.com/Quixotic7/MvaveFM1Unbricker)).
    * The dongle pulses the JieLi hardware boot key (`0x16EF` at ~50 kHz) over USB D+/D- lines during power-up, allowing SPI flash recovery and unbricking through the external USB-C port without opening the enclosure.
    * A practical community wiring guide using a Seeed Studio XIAO RP2040 or Raspberry Pi Pico (Green to D6, White to D7, Black to GND; red disconnected) is documented on [Reddit: Unbricking after a hard brick using a RP2040 and the FM-1 Transporter](https://www.reddit.com/r/MVaveFM1/comments/1x5lifu/mvave_fm1_unbricking_after_a_hard_brick_using_a/).

### 1.4. Device Disassembly & Case Opening Instructions
To open the physical enclosure of the M-VAVE FM1:
1. **Remove Bottom Screws:** Unscrew **6 self-tapping screws** from the bottom casing.
   * **Hidden Screw:** 5 screws are visible on the bottom surface; **1 screw is hidden in the center under the product sticker**.
   * **Rubber Feet:** The rubber feet do **NOT** need to be unglued or peeled off (no screws are hidden under the rubber pads).
2. **Separate Housing Latches:** After removing all 6 screws, carefully unclip the internal **plastic retaining latches/snaps** running along the bottom enclosure seam to separate the case halves.

* **Teardown & Internal PCB Photos:**
  * High-resolution disassembly photos of the PCB and internal components are available locally in the [photos/](photos/) directory.
  * Teardown photo discussion and community analysis can also be viewed on [Reddit r/synthdiy](https://www.reddit.com/r/synthdiy/comments/1vgotwe/comment/p3gk1ko/).

---

## 2. Core Technical Findings

### 2.1. Does the firmware update occur over MIDI?
**Yes, the firmware update occurs entirely over the MIDI SysEx protocol.**

The application does not use dedicated USB DFU/CDC emulation or direct low-level raw flash access during standard operation. The entire process (from handshake to streaming every byte of firmware and preset data) is executed via **USB MIDI SysEx messages** using the **RtMidi** library on top of macOS **CoreMIDI**.

### 2.2. Where is the firmware file stored?
**The firmware binary is embedded directly inside the native executable file.**

There are no external `.bin` or `.hex` files in the resources directory. Inside the executable file [M-UPGRADE-FM1](M-UPGRADE-FM1.app/Contents/MacOS/M-UPGRADE-FM1), the firmware image is stored as an embedded Qt resource package:
* **Qt Resource Length Prefix:** `0x47EB4` (`0x000ABC14` = 704,052 bytes).
* **Package Span:** `0x47EB8` – `0xF3CEC` (704,052 bytes). Contains stock V14 (`FM-1_014`).
* **Container Signatures:** `@JMUA` (offset `0xF3BB8`), `JLUFW` (offset `0xF3CDC`), and target CPU tag `AC791N` at `+0x424`.

### 2.3. Is Signature Verification implemented?
**Asymmetric cryptographic signature verification (RSA/ECDSA/AES) is NOT implemented.**

Security checks include:
1. **Container Header & Signature Validation:** Verification of `@JMUA` / `JLUFW` signatures, target device type, and version strings.
2. **Size Boundaries Validation:** `Embedded firmware too small: %1 bytes (min %2)`.
3. **Checksums (CRC/Byte Checksums):** Every block transmitted via SysEx is accompanied by a byte checksum.

---

## 3. M-UPGRADE-FM1 Application Architecture

* **UI Framework:** Qt6 (`MainView`, `SelectFile`, `LoadingWidget`).
* **MIDI Stack:** RtMidi (`RtMidiIn`, `RtMidiOut`, `MidiInCore`, `MidiOutCore`).
* **OTA Update Worker Modules:**
  * `OtaUpgradeWorker`: Background worker managing the two-step firmware flashing process.
  * `PresetUpdateWorker`: Background worker handling preset bank uploads.
  * `OtaFormat`: Utility class responsible for packing (`pack`), parsing (`parse`, `tryParse`), and building metadata frames (`buildMetaSequence`).

---

## 4. MIDI SysEx Commands & Verified OTA Protocol

### 4.1. Handshake & Device Detection Trace
* **Purpose:** Query connected devices for FM1 identity and status.
* **Handshake Query (Host → Device):** `F0 00 32 45 00 00 00 40 7F F7`
* **Incoming Response Frame (41 bytes wire, 34 bytes unpacked):**
  `F0 00 32 45 58 01 00 00 23 4D 5A 44 XX XX XX ... 40 [chk] F7`
  * Unpacks (7-bit LSB-first) on channel `00 59 11` to a 34-byte ID block containing model identity (`FM-1_015` or `FM-1_014`).
* **Parameter Query Fuzzing Note:** Exhaustive read scanning confirmed that the M-VAVE FM1 synthesizer responds **exclusively to Parameter ID `0x40` (64)**. Queries sent to all other Parameter IDs produce no response.

### 4.2. Verified Two-Step Session Flow (Device-Pull Protocol)
Analysis of the hardware verifier (`AL-255/FM-1-RE`, `docs/io/11-ota-protocol.md`, Issue #2) confirms that the firmware update is a **device-pull** architecture rather than host-push:

1. **Step 1: Verification Mode**
   * Host sends enter-upgrade command: `F0 22 24 35 7F F7`.
   * The device begins *pulling* file chunks via read requests. After entry reads pass verification, the device writes a JieLi `UPDATA_PARM` boot record and soft-resets into the OTA loader.
   * Device re-enumerates as USB device `4D4A:4155` (`ota-FM-1`).

2. **Step 2: OTA Flash Upgrade Mode**
   * Host sends handshake query and `F0 22 24 35 7F F7` again to the OTA loader.
   * The device pulls the complete image with read requests (header reads, entry-list reads descending from the top, then bulk data ascending).
   * Upon reaching completion, the device requests address `0xF0000000` (length 8); host replies with `"success\0"` on channel `00 32 41 01`. The device then reboots into the new firmware.

### 4.3. Wire Framing: Read-Request and Data-Response
All payload data between the host and device is framed as:
```text
F0 00 32 41 41 [f1:4][addr:4][len:4] [pack7(data)...] F7
```
* **Header:** `00 32 41 41` (7-bit wire packing of internal channel `00 59 30`).
* **Fields:** `f1`, `addr`, and `len` are 32-bit little-endian integers encoded as 4×7-bit groups (`b0 | b1<<7 | b2<<14 | b3<<21`).
  * `len` encodes `(length << 4) | flashtype`.
  * In requests (Device → Host): `f1 = 0`.
  * In responses (Host → Device): `f1 = length >> 4`.
* **Data Encoding:** Continuous **8→7 LSB-first bitstream** (7 wire bytes per 8 data bytes). The payload contains `length` data bytes plus 1 checksum byte:
  ```python
  checksum = ~(flashtype + sum(data) + sum(addr_LE4) + sum(len_LE3)) & 0xFF
  ```

---

## 5. Memory Map, Bootloader & Custom Firmware Development

### 5.1. Bootloader Layout & Memory Offsets
In JieLi microcontrollers (AC791N / WL82 series):
1. **Mask ROM (ROM0):** Hardwired ROM initiating chip reset.
2. **UBOOT (Bootloader):** Located at SPI Flash physical address **`0x00000000`** (size 16 KB – 64 KB).
3. **Partition Table & Header (`app_dir_head` / `isd_config.ini`):** Partition table and pin definitions (Power Pin, UART, SD).
4. **App Code Offset (`app.bin`):** User application code starts at Flash offset **`0x4000`** (16 KB) or **`0x10000`** (64 KB) as specified by `isd_config.ini`.

### 5.2. Custom Firmware Support & CRITICAL Bootloader Re-entry Requirement

**Flashing custom firmware via this protocol is fully supported, BUT requires strict adherence to bootloader re-entry logic:**

> [!CAUTION]
> **CRITICAL BOOTLOADER RE-ENTRY REQUIREMENT:**  
> Because the M-VAVE FM1 PCB lacks physical recovery buttons or debug pads, **any custom firmware MUST retain or implement a mechanism to enter the bootloader / OTA mode** (e.g. by listening for the SysEx verification/upgrade commands `0x01` / `0x02` or handling a button combination during startup).  
> **If custom firmware is flashed without a bootloader entry handler, the device will be permanently soft-locked against future MIDI updates or rollback to stock firmware.**

**Requirements for compiling custom firmware:**
1. **Toolchain:** Official JieLi GCC toolchain targeting **Pi32v2 / q32s** architecture.
2. **Linker Script:** Code must be linked at the target partition offset (`origin Flash: 0x4000` / `0x10000`).
3. **Bootloader Handler:** Include the SysEx parser / OTA transition handler in the custom application code.
4. **Container Packaging (`isd_tools`):** Package output binaries using `isd_download` / `fw_pack` into a UFW container with `@JMUA` / `JLUFW` headers.
5. **Flashing:** The resulting UFW file can be transmitted via `M-UPGRADE-FM1` or the custom Python script ([fm1_flasher.py](fm1_flasher.py)).

---

## 6. Binary References & Offsets

Binary offsets extracted from analysis:

1. **Native Application Binary:**
   * Binary Path: [M-UPGRADE-FM1](M-UPGRADE-FM1.app/Contents/MacOS/M-UPGRADE-FM1)
   * **Offset `0xEEDDC`**: Resource path string `usb_hid_ota.bin`.
   * **Offset `0xF14AD`**: Bootloader configuration block `isd_config.ini`, `app_dir_head`, `uboot`, `POWER_PIN`.
   * **Offset `0xF3BB8`**: Container signature `@JMUA`.
   * **Offset `0xF3CDC`**: JieLi firmware container magic `JLUFW`.
   * **Offset `0x14C010`**: SysEx header data symbol `_s_arrSysexHead`.

2. **Supported Hardware & UBOOT Documentation:**
   * JieLi Chip Series List (WL82 / AC791N): [README.md:L84](jl-uboot-tool/README.md#L84)
   * UBOOT Architecture: [what-is-uboot.md](jl-uboot-tool/docs/what-is-uboot.md)

---

## 7. Firmware Size Boundaries

Firmware size is constrained by three factors:

### 7.1. SPI Flash Capacity
AC791N chips feature **4 MB (32 Mbit)** or **8 MB (64 Mbit)** internal/external SPI Flash.
* **Layout:**
  * **UBOOT (Bootloader):** First `16 KB` – `64 KB` (`0x00000000` – `0x00010000`).
  * **VM / Flash DB (Settings):** Final `16 KB` – `64 KB` of Flash.
  * **User App Partition:** Remaining space between UBOOT and VM.
* **Maximum Image Size:** For 4 MB Flash, the maximum compiled image size is approximately **~3.9 MB**.

### 7.2. Application Boundary Validation
* **Lower Limit:** `Embedded firmware too small: %1 bytes (min %2)` (requires valid `@JMUA` header and >64 KB size).
* **Upper Limit:** Protocol size field is 32-bit (up to 4 GB payload support).

### 7.3. Execution Model (XIP)
Code runs via **XIP (Execute-In-Place)** directly from SPI Flash via the MCU hardware cache. SRAM size limits dynamically allocated memory (`.bss` / `.data`), but does not restrict binary code size in Flash.

---

## 8. Python Firmware Utility (`fm1_flasher.py`)

A standalone CLI tool [fm1_flasher.py](fm1_flasher.py) provides firmware extraction and experimental protocol tooling. Project environment is managed via [`uv`](https://github.com/astral-sh/uv) (configured in [`pyproject.toml`](pyproject.toml)).

> [!WARNING]
> **FLASHING STATUS & PROTOCOL DISCLAIMER (Issue #2):**  
> Direct firmware flashing implemented in [fm1_flasher.py](fm1_flasher.py) is **experimental and non-functional** on physical hardware because it assumes a host-push packet structure, whereas the actual synthesizer hardware runs a **device-pull protocol** with 8→7 LSB-first bitstream encoding (documented in [Section 4: MIDI SysEx Commands & Verified OTA Protocol](#4-midi-sysex-commands--verified-ota-protocol)).  
> **For verified, byte-exact firmware flashing on physical hardware, use `tools/fm1_ota.py` from [AL-255/FM-1-RE](https://github.com/AL-255/FM-1-RE).**

### Features:
* **Firmware Extraction (`--extract`):** Fully functional. Carves the exact 704,052-byte `.fwsc` package (`0x47EB8`–`0xF3CEC`, stock V14) from the macOS `M-UPGRADE-FM1` binary by resolving the big-endian Qt resource length prefix and verifying the `AC791N` marker.
* **MIDI Port Discovery (`--list`):** Scans and enumerates available MIDI inputs and outputs.
* **Experimental Flash Tooling (`--file`):** Research skeleton for protocol analysis.

### Example Commands:
```bash
# List available MIDI ports
uv run fm1-flasher --list

# Extract embedded .fwsc firmware from macOS updater app
uv run fm1-flasher --extract FM-1_014.fwsc --app M-UPGRADE-FM1.app/Contents/MacOS/M-UPGRADE-FM1

# Flashing on physical hardware (use AL-255's verified tool):
python3 tools/fm1_ota.py flash FM-1.fwsc
```

---

## 9. Firmware Disassembly & Reverse Engineering

Reverse-engineering JieLi microcontrollers (AC791N / WL82 / AC69x series) requires specialized tools due to JieLi's proprietary 32-bit RISC processor architectures (**Pi32**, **Pi32v2**, **q32s**).

### 9.1. Disassembly Tools & Ghidra Plugin

* **Ghidra Processor Module ([ghidra-jieli](https://github.com/kagaimiq/ghidra-jieli)):**
  An open-source Ghidra processor module targeting JieLi CPU architectures:
  * `pi32`: Functional disassembly support for older JieLi chips.
  * `pi32v2`: Processor definition for **AC791N (WL82 series)**. Enables Ghidra to parse function boundaries, construct control flow graphs (CFG), and trace MMIO register addresses (`JL_PORTA`, `JL_PORTB`, `JL_PORTC`).
  * `q32s`: Processor definition for BD19/BD29 series.

* **JieLi Official Toolchain (`pi32v2-elf-objdump`):**
  Provides 100% accurate instruction decoding from the vendor SDK, used in combination with Ghidra for verifying complex instruction groups.

---

## 10. Firmware Security & BadUSB Threat Modeling

With the rise of custom community firmwares, community discussions have raised valid threat models regarding unsigned firmware execution on host computers (e.g. [Reddit: Security concern: BadFM1 Exploit Theory](https://www.reddit.com/r/MVaveFM1/comments/1x816h9/security_concern_badfm1_exploit_theory/)):

* **Absence of Cryptographic Firmware Signing:** The JieLi AC791N SoC and the stock bootloader do not enforce cryptographic digital signatures on application firmware images (`.fwsc`). Any binary matching the container format and vector table will execute.
* **USB Class Reconfiguration (BadUSB Attack Surface):**
  * The JieLi AIoT SDK allows configuring the device's USB descriptor to any standard USB class via `#define USB_DEVICE_CLASS_CONFIG`.
  * Legitimate custom firmwares (such as [Trireme FM-1](README.md#13-gaming-emulators--non-audio-ports-games--experiments) and [FM-1 Macropad Patch](README.md#14-stock-firmware-patchers--binary-mods)) intentionally demonstrate switching the USB interface into a standard Human Interface Device (HID) keyboard/composite device.
  * In a theoretical rogue or compromised firmware scenario, a malicious binary flashed over WebMIDI could reboot and act as a BadUSB/Rubber Ducky device, injecting keystrokes into the host operating system (e.g., opening a terminal or executing curl/powershell downloaders) immediately upon connecting.
  * If a rogue firmware eliminates USB-MIDI descriptors entirely, subsequent recovery via standard WebMIDI browser flashers may become disabled, necessitating low-level mask-ROM recovery (`WL82 UBOOT1.00` via plain USB or hardware `USB_KEY` dongle).
* **Mitigation Best Practices:**
  * Only flash firmware built from public, verifiable open-source repositories with clean revision histories.
  * Audit build actions, releases, and source diffs before flashing unknown binaries.
  * On sensitive host workstations, connect experimental USB devices through isolated USB hubs, dedicated non-privileged test machines, or VMs with USB passthrough controls.
