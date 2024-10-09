
# This is under construction!!!

## Table of Contents
[Description](#description)  
[Basics](#basics)  
[How to install](#howtoinstall)  
  [Gateway](#gateway)  

## Description <a name="description"></a>
This package is for connecting and controlling an LG Therma V heat pump with Homeassistant via modbus.  
This manual is tested with:
- LG Therma V ...

## Basics  <a name="basics"></a>
The LG Heatpump is only availiable to communicate via RS485/Modbus TCP . The best way to connect them with Homeassistant is a Modbus TCP Gateway.
In my case, i use a [Waveshare Industrial RS232/RS485 to Ethernet Converter](https://www.waveshare.com/rs232-485-to-eth-for-eu.htm).

![converter](https://github.com/user-attachments/assets/c2cadb83-e3a9-4593-92a9-ddbca321a4e0)

## How to install  <a name="howtoinstall"></a>
### Gateway <a name="gateway"></a>
![IMG_4261](https://github.com/user-attachments/assets/59bbd424-c406-4b6a-b33f-670361443392)

### Homeassistant
Download the *modbus_lg_heatpump.yaml*

Put the file in a folder named *integrations*. Create the folder if not exist.

![image](https://github.com/user-attachments/assets/b85ebb60-3963-4d8f-8c68-fa098d60591b)


Add a reference to your integration folder in your *configuration.yaml*.

![image](https://github.com/user-attachments/assets/be2b6c9a-6929-47da-984c-66d7c3457f64)

Set the secrets in your *secrets.yaml* file


### Heatpump
#### Hardware settings
##### Wire connection between heatpump and gateway.  
Inside the heatpump you will find a connector named "3rd PARTY CONTROLLER". This is the connector for the modbus wire. The wire must be connected to contact A (+) and B(-).  

![connection_heatpump](https://github.com/user-attachments/assets/258c3483-5fb1-4e9a-a41a-709377e070ff)



##### Dip switch inside the heatpump. 
*Settings for 4er series*  
On the main bord of the heatpump are 2 dip switch banks, SW1 and SW2.
For us are the settings from SW1 important.  

SW1 dip 1 - ON --> The heat pump is set as a Modbus slave device.  
SW1 dip 2 - ON --> The heat pump is using a open protokoll.

![image](https://github.com/user-attachments/assets/9759fe76-785b-43c3-9957-14483a88a61e)



#### Software settings
It is also required to set some options on the inside head unit. 
  
![image](https://github.com/user-attachments/assets/b78ce590-2876-4b27-9264-40c5444da8b5)

1. Navigate to Settings
2. ...

![image](https://github.com/user-attachments/assets/8f63e8f5-6eb2-4a65-a723-41daf5b122db)



Restart your Homeassistant
