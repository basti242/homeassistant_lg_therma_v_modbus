
[Description](#description)  
[Basics](#basics)  
[How to install](#howtoinstall)  
> [Gateway](#gateway)  
> [Homeassistant](#homeassistant)  
> [Heatpump](#heatpump) 

# Description <a name="description"></a>
This package is for connecting and controlling an LG Therma V heat pump with Homeassistant via modbus.  
This manual is tested with:
- LG Therma V Monoblock 9kW (@basti242)

# Basics  <a name="basics"></a>
The LG Heatpump is only availiable to communicate via RS485/Modbus TCP . The best way to connect them with Homeassistant is a Modbus TCP Gateway.
For example a [Waveshare Industrial RS232/RS485 to Ethernet Converter](https://www.waveshare.com/rs232-485-to-eth-for-eu.htm).

![Converter](https://github.com/user-attachments/assets/36b88e14-a3f1-4fcb-9d65-a4cfd5b065c2)


With this integration, you are able to controll nearly all settings of your heatpump.  

**Examples**  

![image](https://github.com/user-attachments/assets/85a27c31-40ee-468f-ba29-5d5f2826946a)  ![image](https://github.com/user-attachments/assets/2667a9a6-823b-4b5f-9487-f319fcc84b4f)



# How to install  <a name="howtoinstall"></a>
### Gateway <a name="gateway"></a>
![IMG_4261](https://github.com/user-attachments/assets/59bbd424-c406-4b6a-b33f-670361443392)

## Homeassistant <a name="homeassistant"></a>
Download the [*modbus_lg_heatpump.yaml*](https://github.com/basti242/homeassistant_lg_therma_v_modbus/blob/main/modbus_lg_heatpump.yaml)

Put the file in a folder named *integrations*. Create the folder if not exist.



![image](https://github.com/user-attachments/assets/b85ebb60-3963-4d8f-8c68-fa098d60591b)


Add a reference to your integration folder in your *configuration.yaml*. The *homeassistant:* line should be still there.
```yaml
homeassistant:
  packages: !include_dir_named integrations
```

Set the secrets in your *secrets.yaml* file

```yaml
# LG Heatpump
#-----------------------------------------------
lg_heatpump_modbus_host_ip: 10.10.1.xxx #change it to the IP adress from your gateway
lg_heatpump_modbus_port: 502
lg_heatpump_modbus_slave: 1
```
Restart your Homeassistant

Here is a code example for the UI.
```yaml
type: entities
entities:
  - entity: input_select.hp_set_operation_mode
    name: Operation Mode
  - entity: input_select.hp_set_control_method
    name: Control Mode
  - entity: input_number.hp_dhw_target_temperatur
    name: Brauchwasser
    icon: kuf:sani_water_hot
```
should look like this  
![image](https://github.com/user-attachments/assets/ee8e1ee6-e58f-4d5e-a39d-bf918f096a0c)

## Heatpump <a name="heatpump"></a>
**Hardware settings**  
Wire connection between heatpump and gateway.  
Inside the heatpump you will find a connector named "3rd PARTY CONTROLLER". This is the connector for the modbus wire. The wire must be connected to contact A (+) and B(-).  

![connection_heatpump](https://github.com/user-attachments/assets/258c3483-5fb1-4e9a-a41a-709377e070ff)



Dip switch inside the heatpump
*Settings for 4er series*  
On the main bord of the heatpump are 2 dip switch banks, SW1 and SW2.
For us are the settings from SW1 important.  

SW1 dip 1 - ON --> The heat pump is set as a Modbus slave device.  
SW1 dip 2 - ON --> The heat pump is using a open protokoll.

![image](https://github.com/user-attachments/assets/9759fe76-785b-43c3-9957-14483a88a61e)



**Software settings**  
It is also required to set some options on the inside LG head unit (LG RS3). 
  
![image](https://github.com/user-attachments/assets/b78ce590-2876-4b27-9264-40c5444da8b5)

1. Navigate to Settings
2. ...

![image](https://github.com/user-attachments/assets/8f63e8f5-6eb2-4a65-a723-41daf5b122db)



**That’s it! You can now control the heat pump from Homeassistant.**


