# AVNET/Nordic Semiconductor Workshop: <br>_Newcomer's Zephyr RTOS Seminar_

## Workshop Dates/Locations
>  24.June 2026, Rothrist <br>
>  23.January 2026, Leinfelden-Echterdingen <br>

## The LPS22HB Sensor Project
Please download following ZIP file and extract it into your Workspace folder, e.g. C:/Nordic/Workspace

[Download ZIP file](lps22hb.zip)

> Right mouse click on above link, and click on _Save link as..._.

## Code Snippets for Hands-On Sessions
Here you will find the code snippets you will add to the LPS22HB Sensor project. 

- [__lps22hb\_shell__: Adding I2C shell to your project](HandsOn/i2cshell.md)

- __lps22hb\_sensorSim__: as described in the slide, the simulated sensor must be activated in the DeviceTree overlay file and the simSensor node must be selected in the code.

- __lps22bh\_thread__: this project is identical to the lps22hb project. It should serve as a starting point and sensor handling should be implemented via thread.

## Workshop Slides
- Introduction to Zephyr
- [_nRF Connect SDK_: How Nordic uses Zephyr](presentations/2-AVNET_ZephyrWorkshop_nrfConnectSDK.pdf)
- [Configure software without changing source code: Kconfig and DeviceTree](presentations/3-AVNET_ZephyrWorkshop_Kconfig_DeviceTree.pdf)
- [Visual Studio Code and useful tools](presentations/4-AVNET_ZephyrWorkshop_VSCode.pdf)
- [Hands-on session: Unboxing the nRF54L15DK, QuickStart, Board Configurator, Connecting an ST LPS22 pressure sensor, Configure Zephyr to read sensor data, Running I2C shell](presentations/5-AVNET_ZephyrWorkshop_HandsOn_Unboxing_SensorDemo.pdf)
- [Hands-on session: Multi-Threaded Applications](presentations/6-AVNET_ZephyrWorkshop_HandsOn_Threads.pdf)
