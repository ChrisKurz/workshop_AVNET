# AVNET/Nordic Semiconductor Workshop: <br>_Newcomer's Zephyr RTOS Seminar_

## Workshop Dates/Locations
>  24.June 2026, Rothrist <br>
>  23.January 2026, Leinfelden-Echterdingen <br>

## Code Snippets for Hands-On Sessions
In this repository, you will find the files you need for the hands-on session. 

1) __lps22hb__: the LPS22hb demo.

2) __lps22hb\_shell__:  this project should be modified to enable I2C and sensor Shell. See the corresponding slide.

3) __lps22hb\_sensorSim__: as described in the slide, the simulated sensor must be activated in the DeviceTree overlay file and the simSensor node must be selected in the code.

4) __lps22bh\_thread__: this project is identical to the lps22hb project. It should serve as a starting point and sensor handling should be implemented via thread.

## Workshop Slides
- Introduction to Zephyr
- [_nRF Connect SDK_: How Nordic uses Zephyr](presentations/2-AVNET_ZephyrWorkshop_nrfConnectSDK.pdf)
- [Configure software without changing source code: Kconfig and DeviceTree](3-AVNET_ZephyrWorkshop_Kconfig_DeviceTree.pdf)
- Visual Studio Code and useful tools]()
- Hands-on session: Unboxing the nRF54L15DK, QuickStart, Board Configurator, Connecting an ST LPS22 pressure sensor, Configure Zephyr to read sensor data, Running I2C shell]()
- Introduction to the Nordic Tech Academy for self-learning]()
- Nordic Developer Academy - Multithreaded applications: Tread creation & priorities, Time slicing, Workqueue creation & work item submission]()
