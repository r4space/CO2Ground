This is a project wide readme relating to far more than just the attached code
#Connecting CO2 to Pis:
- Script will try connect to as many Co2 meters on as many USB ports as you tell it starting from 0.  Therefore plug in as many CO2 meters into USB ports on the Pi as wanted starting with port 0 and counting up.  When you run the script tell it how many CO2 meters are connected - i.e 1, 2, 3 or 4

- Connect the other end of the USB-to-serial cable to the CO2meter as follows:
    - Pin0 is the tiny little square hole in the back row of holes along the side with the most holes (2 rows)
    - Counting left to right:
        - Pin1 = White wire (RX to TX on CO2 board)
        - Pin2 = Green wire (Tx to RX on CO2 board)
        - Pin3 = Red wire (5V supply)
        - Pin4 = Black wire (Ground)

#CollectingData
1. Power up Pi-Sensor systems
2. Wait ~15minutes for sensors to warm up
3. While waiting:
    - Turn on laptop wifi hotspot
    - ssh into each Pi:
        - $ ssh VT<number>  //0,1,2,3,4...
        - A new folder will be created in /home/pi/DATA/ every time you run the data collection script.  If you want a clean start and have already captured the data from previous uses remove the contents of this folder to make it easier to keep track of capture instances.

#How to configure a new Pi
- Create new SD card image:
    ## Format SDcard
        - Format new card with gparted to be 1 blank FAT32 partition, suggest labeling VT1 or something both digitally and with a sharpie on the outside:
            - Find the SD card on laptop
                $ df-h 
            - format it
                $ sudo gparted  //perform formating in GUI
            - Eject SD card and reinsert
    ## Write new image to formated SD card 
        $ umount </dev/sdb1>    #Or whatever the location is sdb<x>
        $ sudo dd bs=4M if=~/SDCardBackup.img of=/dev/sdb status=progress   #Note: Don't include any partition number. And, this will take quite a while (tens of minutes perhaps)
        $ sudo sync

- Boot and configure new image:
    - Boot new card in a Pi
    - ssh into new image:
        $ ssh pi@192.168.0.12   #Password is Vermont
        $ sudo raspi-config
        - follow instructions in the GUI that comes up to give it a new name, suggest VT<x> where x is an incremental number

