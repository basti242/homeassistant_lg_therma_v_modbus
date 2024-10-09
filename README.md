### Description
This package is for connecting an LG Therma V heat pump with Homeassistant via Modbus.

### Basics
The LG Heatpump is only availiable to communicate via RS485/Modbus TCP . The best way to connect them with Homeassistant is a Modbus TCP Gateway.
In my case, i use a [Waveshare Industrial RS232/RS485 to Ethernet Converter](https://www.waveshare.com/rs232-485-to-eth-for-eu.htm).

![converter](https://github.com/user-attachments/assets/c2cadb83-e3a9-4593-92a9-ddbca321a4e0)



### How to install
***

Download the modbus_lg_heatpump.yaml

Put the file in a folder named integrations. Create the folder if not exist.

![image](https://github.com/user-attachments/assets/b85ebb60-3963-4d8f-8c68-fa098d60591b)


Add a reference to your integration folder in your configuration.yaml.

![image](https://github.com/user-attachments/assets/be2b6c9a-6929-47da-984c-66d7c3457f64)

Set the secrets in your secrets.yaml file

Restart your Homeassistant