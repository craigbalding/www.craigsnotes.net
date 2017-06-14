+++
title = "RPi with USB external drive"
date = "2014-01-23"
tags = ["rpi"]
+++

To attach an external USB harddrive *without* a USB hub, check the maximum power requirements of the drive are less than 120mA.

One way to find this out is using `lsusb -v`, locating your drive and check the MaxPower field.  Full output below for future reference:

    Bus 001 Device 005: ID 0bc2:2300 Seagate RSS LLC Expansion Portable
    Device Descriptor:
      bLength                18
      bDescriptorType         1
      bcdUSB               2.00
      bDeviceClass            0 (Defined at Interface level)
      bDeviceSubClass         0 
      bDeviceProtocol         0 
      bMaxPacketSize0        64
      idVendor           0x0bc2 Seagate RSS LLC
      idProduct          0x2300 Expansion Portable
      bcdDevice            1.30
      iManufacturer           1 Seagate 
      iProduct                2 Portable        
      iSerial                 3 2GH5XXXX    
      bNumConfigurations      1
      Configuration Descriptor:
	bLength                 9
	bDescriptorType         2
	wTotalLength           32
	bNumInterfaces          1
	bConfigurationValue     1
	iConfiguration          0 
	bmAttributes         0x80
	  (Bus Powered)
	MaxPower              100mA  # this is the field!
	Interface Descriptor:
	  bLength                 9
	  bDescriptorType         4
	  bInterfaceNumber        0
	  bAlternateSetting       0
	  bNumEndpoints           2
	  bInterfaceClass         8 Mass Storage
	  bInterfaceSubClass      6 SCSI
	  bInterfaceProtocol     80 Bulk-Only
	  iInterface              0 
	  Endpoint Descriptor:
	    bLength                 7
	    bDescriptorType         5
	    bEndpointAddress     0x81  EP 1 IN
	    bmAttributes            2
	      Transfer Type            Bulk
	      Synch Type               None
	      Usage Type               Data
	    wMaxPacketSize     0x0200  1x 512 bytes
	    bInterval               0
	  Endpoint Descriptor:
	    bLength                 7
	    bDescriptorType         5
	    bEndpointAddress     0x02  EP 2 OUT
	    bmAttributes            2
	      Transfer Type            Bulk
	      Synch Type               None
	      Usage Type               Data
	    wMaxPacketSize     0x0200  1x 512 bytes
	    bInterval               0
    Device Qualifier (for other device speed):
      bLength                10
      bDescriptorType         6
      bcdUSB               2.00
      bDeviceClass            0 (Defined at Interface level)
      bDeviceSubClass         0 
      bDeviceProtocol         0 
      bMaxPacketSize0        64
      bNumConfigurations      1
    Device Status:     0x0000
      (Bus Powered)

If I plug this drive in whilst the RPi is running, the power draw of the USB drive spinning up can sometimes cause the RPi to reboot. If I boot the Pi with the drive plugged in, I haven't experienced any problems.

Performance is reasonable for media storage/serving.  Here's the output of `dd`:
 
    [craigb@alarmpi scratch]$ dd if=/dev/zero of=test bs=64k count=16k conv=fdatasync
    16384+0 records in
    16384+0 records out
    1073741824 bytes (1.1 GB) copied, 52.7311 s, 20.4 MB/s

Here's the partition table.  A single partition set as Linux LVM:

    Disk /dev/sdb: 698.7 GiB, 750156374016 bytes, 1465149168 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xf81530c3

    Device    Boot Start        End    Blocks  Id System
    /dev/sdb1       2048 1465149167 732573560  8e Linux LVM

And the LVM layout, courtesy of `lvdisplay`:

    --- Logical volume ---
    LV Path                /dev/rpi/photos
    LV Name                photos
    VG Name                rpi
    LV UUID                L7AQ9s-crZP-uV4Z-czMy-2TEe-DIzy-QSAhxN
    LV Write Access        read/write
    LV Creation host, time microserver, 2014-01-14 00:23:24 +0100
    LV Status              available
    # open                 1
    LV Size                400.00 GiB
    Current LE             102400
    Segments               1
    Allocation             inherit
    Read ahead sectors     auto
    - currently set to     256
    Block device           253:0

    --- Logical volume ---
    LV Path                /dev/rpi/music
    LV Name                music
    VG Name                rpi
    LV UUID                oHsoV9-zopM-5Deh-dkRs-WNZt-pNhO-1PCzlb
    LV Write Access        read/write
    LV Creation host, time microserver, 2014-01-14 00:23:38 +0100
    LV Status              available
    # open                 1
    LV Size                200.00 GiB
    Current LE             51200
    Segments               1
    Allocation             inherit
    Read ahead sectors     auto
    - currently set to     256
    Block device           253:1

    --- Logical volume ---
    LV Path                /dev/rpi/scratch
    LV Name                scratch
    VG Name                rpi
    LV UUID                rI4dc2-2YEN-Y9lA-B0Af-QuO5-0t8N-BTbNoJ
    LV Write Access        read/write
    LV Creation host, time alarmpi, 2014-01-14 16:06:14 +0100
    LV Status              available
    # open                 1
    LV Size                50.00 GiB
    Current LE             12800
    Segments               1
    Allocation             inherit
    Read ahead sectors     auto
    - currently set to     256
    Block device           253:2
   
The LVM metadata gives away that I created "music" and "photos" when the drive was attached to my HP Microserver N36L (to copy the data quickly).  The "scratch" volume was only added I after attached the drive to the RPi.
