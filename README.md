# Allwinner V3s SBC

![board_render](/assets/front.png)

This board embeds a SIP (single core 1GHz Cortex-A7 with 64MB DDR2) with AXP203 PMIC, IO headers and microSD/eMMC storage.

Board overview (draft):
[TBD]

## Board features
| Characteristic | Description |
| --- | --- |
| Dimensions | 60mm x 40mm |
| Processor | Allwinner V3s Cortex-A7 @1GHz |
| Oscillators | 32.768kHz slow click, 24MHz main clock |
| RAM | 512Mb embedded DDR2 memory |
| Storage | SPI Flash/microSD |
| USB | 1 microUSB OTG |
| Ethernet | 10/100M PHY with pins on header |
| Supply | Power path between USB/Vin/Battery, 5V max |

## Notes and observations

### Expansions
The board features a number of connectors. They expose various buses for expansions:
 * 1 SPI port
 * 2 UART ports
 * 1 I2C port
 * 2 ADC enabled pins
 * 18bit parallel LCD interface
 * Ethernet signals with status LEDs

The connectors are organized in consistent locations present on the other SBCs i have developed.
 * J100 connector - 2.54mm 2x18 header with standard Apollo IoT pinout
 * J200 connector - 1.27mm 2x04 header with ethernet signals
 * J300 connector - 1.27mm 2x05 header with analog audio I/O signals
 * J500 connector - 1.27mm 2x20 header with parallel LCD interface signals

Check expansions section for example daughter cards with added functionality

### Boot process
The board has two boot strategies depending on component configuration. If the SPI flash memory is not used, the BROM uses the MicroSD as boot source and loads UBoot from there.
If the SPI flash is populated, UBoot with a minimal Kernel and Busybox can be stored as recovery environment or main application.

### LCD connector
Most of port D signals are mapped to the LCD connector. if LCD is not used they can be muxed as GPIO or other functions upon editing the DT overlay.

### AXP203
AXP203 is pin to pin compatible with the more popular AXP209, so they can be easily swapped.

### 1.2V Rail
Two different 1.2V rails are provided to the CPU. This is a deliberate decision to allow fixed CPU internal rail at 1.2V and provide DVFS cappability to 1.2V rail for CPU core.

### Signals on headers
All the signals on the headers, with their initial functions are detailed on the silkscreen on the bottom layer

### Battery usage
The board schematic uses a Diodes AP9211 battery protection IC for safety protections when used toghether with a LiIon battery. If a battery pack with embedded protection and thermistor is used, TH1 and AP9211 can be left unpopulated.

### Expansions
 The board can be combined with several predefined capes that add functionality.
 * [LCD cape](https://github.com/vd-rd/hw_cape_lcd) can be used to add a 3inch LCD/Touch with 800x480px resolution.
 * [GPS cape](https://github.com/vd-rd/hw_cape_gps) adds GPS/GNSS/GLONAS capabilities
 * [GSM cape](https://github.com/vd-rd/hw_cape_gsm) adds GPRS connectivity. 


## Resources
You can find all necesary information to build or evaluate the module here:
   - [View 3D board render](https://a360.co/2GTPupk)
   - [Fabrication files](https://github.com/vd-rd/sbc_alw_v3s/releases)
