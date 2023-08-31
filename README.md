# simcom module

SIM8380G:

chipset: ?

* GNSS: GPS/Gallileo/QZSS/GLONASS/Beidou

* 5G Sub-6G Speeds: 4Gbps(DL)/1Gbps(UL)

* 5G mmWave Speeds: 7Gbps(DL)/3Gbps(UL)

* Supports R16 and 5G dual mode (NSA/SA)

# Build
	make
# Load driver
	# require usbnet, cdc_wdm
	modprobe usbnet
	modprobe cdc_wdm
	insmod qmi_wwan_simcom

# Get operation mode: 
	at+cusbcfg=? 
	gives the following: 9001,9003,9011,901e

# usage
	sudo apt install libqmi-utils
	qmicli
	sudo qmi-network /dev/cdc-wdm1 start
	# check It’s either qmi_wwan (if it’s in QMI mode) or cdc_mbim (if it’s in MBIM mode)
	basename $(realpath /sys/class/usbmisc/cdc-wdm0/device/driver)

	sudo apt install modemmanager
# Mobile Broadband Interface Model (MBIM) Interface.
	Microsoft request cellular module vendors to include the MBIM interface for good compatibility with Windows 8, 8.1, 10 and later systems. The Windows built-in connection manager also rely on MBIM interface for control of the cellular modules.
	cdc_mbim, 

https://techship.com/faq/how-to-set-up-a-simple-data-connection-over-the-mbim-interface-using-libmbim-and-driver-cdc-mbim-in-linux/

# kernel path
	/drivers/net/usb/qmi_wwan.c
