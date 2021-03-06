## Uploading code using DFU-OTA

* Download latest release of [Python 2](https://www.python.org/downloads/)

* Install Python

* Add python to environment variables. **python.exe** can be found in `<Python2x_Install_Direc>`

* Add pip to environment variables. **pip.exe** and **pip2.exe** can be found in `<Python2x_Install_Direc>\Scripts`

* Run: `pip install nrfutil` or `pip2 install nrfutil`

![](images/nrfutil-install.png)

* Check for updates: `pip install nrfutil --upgrade` or `pip2 install nrfutil --upgrade`

![](images/nrfutil-upgrade.png)

* **nrfutil.exe** can be found in `<Python2x_Install_Directory>\Scripts`. So, it is automatically included in environment variables.

* Run: `nrfutil --help` to check whether the package is installed properly.

![](images/nrfutil-check.png)

* Using Windows Explorer, open: `nRF5_SDK_12.2.0_f012efa\examples\ble_peripheral\ble_app_hrs\pca10040\s132\armgcc`.

* In command prompt, run: `cd nRF5_SDK_12.2.0_f012efa\examples\ble_peripheral\ble_app_hrs\pca10040\s132\armgcc`

* Run: `make`, to generate hex file.

![](images/make-hrs.png)

* Copy ***private.key*** file provided in the repository.

* Paste ***private.key*** file in `nRF5_SDK_12.2.0_f012efa\examples\ble_peripheral\ble_app_hrs\pca10040\s132\armgcc\_build`

* In command prompt, Run: `cd _build` to access the directory where hex file is stored.

* Run: `nrfutil pkg generate --hw-version 52 --application-version 1 --application nrf52832_xxaa.hex --sd-req 0x8C --key-file private.key app_dfu_hrs_package.zip`

![](images/generate-package.png)

_Note!: --sd-req = 0x8C for s132_nrf52_3.0.0 and --sd-req = 0x98 for s132_nrf52_4.0.2. Find complete list [here](https://github.com/NordicSemiconductor/pc-nrfutil)

* Once the zip package has been created, transfer the file to your mobile or save it to Google Drive. The file should be accessible from the smartphone.

* Connect **bluey** to the PC.

* Enter bootloader mode: Press SW3 switch followed by RST switch. Release RST switch. Once LED is red, release SW3 switch.

* Scan for bluey using nRF Connect or nRF Toolbox. The device should advertise as ***DfuTarg***

![](images/DfuTarg.png)

* Connect: ***DfuTarg***

* Press the **DFU** symbol.

![](images/dfu.png)

* Select Distribution packet (ZIP) option.

![](images/zip.png)

* Select the package that was transferred to the smartphone earlier.

![](images/package-select.png)

* Wait for the update to reach 100%.

![](images/dfu-uploading.png)

* Wait for the device to disconnect.

![](images/dfu-disconnecting.png)

* The device resets once the upload is complete and should advertise as ***Nordic_HRM***

![](images/dfu-app-updated.png)
