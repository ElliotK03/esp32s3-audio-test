# Using ESP-ADF with Generic ESP32-S3 board

This repo contains adapted code from the [play-mp3-control](https://github.com/espressif/esp-adf/tree/release/v2.x/examples/get-started/play_mp3_control) example in the [ESP-ADF](https://github.com/espressif/esp-adf) repo

## Prerequisites

1. ESP-IDF v5.1 or newer (see [supported IDF versions](https://github.com/espressif/esp-adf/tree/release/v2.x?tab=readme-ov-file#idf-version))
2. ESP-ADF (cloned from ESP-ADF github repo, follow the [official guide](https://docs.espressif.com/projects/esp-adf/en/latest/get-started/index.html))
3. An ESP32-S3 board, and ES8311 DAC

These frameworks will take up quite a lot of space so do make sure you have enough storage available for them.

## Hardware setup
| ES8311 Pin | ESP32 GPIO Pin |
|------------|----------------|
|     SDA    |       17       |
|     SCL    |       18       |
|     BCK    |       9        |
|     WS     |       45       |
|     DIN    |       8        |
|     DOUT   |       10       |
|     MCK    |       16       |

Don't forget to connect your speaker to the DAC's output, and connect your ES8311 to 5V (if that's what your module uses) and GND

## How to use
1. Start ESP-IDF shell, CMD, Powershell or whatever you use
2. Add the `ADF_PATH` environment variable (`set "ADF_PATH=C:\path\to\your\esp-adf"` in CMD)
3. `cd` to the root folder of the this project
4. Run `idf.py set-target esp32s3`
5. Run `idf.py menuconfig`
   1. In `menuconfig root --> Audio HAL --> Audio board` select `Custom audio board`
   2. In `menuconfig root --> Component config --> ESP PSRAM` enable `Support for external, SPI-connected RAM`
   3. In `menuconfig root --> Component config --> ESP PSRAM --> SPI RAM Config -> Mode` select `Octal`
   4. (Optional) In `menuconfig root --> Component config --> ESP PSRAM --> SPI RAM Config -> Set RAM clock speed` select `80MHz`

6. Press `s` to save, then `q` to close the menuconfig
7. Run `idf.py build`
8. Connect your ESP32-S3 and run `idf.py flash`

If it works, you'll hear it.
