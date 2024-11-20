
[Description](#description)  
[Basics](#basics)  
[How to install](#howtoinstall)  
> [Gateway](#gateway)  
> [Homeassistant](#homeassistant)  
> [Heatpump](#heatpump)

[Dashboard](#dashboard)

# Description <a name="description"></a>
This package is for connecting and controlling an LG Therma V heat pump with Homeassistant via modbus.  
This manual is tested with:

Heat pump                        | Tested by                                
--------                         | --------                                 
LG Therma V Monoblock 9kW        | [basti242](https://github.com/basti242)  


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

Tested Gateways:

Device                          | Type                | Tested by                                   | Link
--------                        | --------            | --------                                    | --------
Waveshare RS485 To ETH          | tabletop device     | [basti242](https://github.com/basti242)     | [Amazon](https://amzn.eu/d/9hwIM75)
Waveshare RS485 To ETH (B)      | top-hat rail        | [fRiMMi83](https://github.com/gRiMMi83)     | [Amazon](https://amzn.eu/d/4nqkfNH)
WaveShare RS232-485-TO-WIFI-ETH | tabletop device     | [BigCabbage](https://github.com/BigCabbage) | [Amazon](https://amzn.eu/d/2aOHsr5)


## Homeassistant <a name="homeassistant"></a>

[Overview availiable Modbus Register](https://docs.google.com/spreadsheets/d/1nzYJzj6M_eGvW1HD7guehZE_RDtn0w31KEogzJ0uoaY/edit?usp=sharing)

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

# Dashboard <a name="dashboard"></a>
**Examples**  
required HACS packages for these examples
- mushroom
- card_mod
- Multiple-Entity-Row

![image](https://github.com/user-attachments/assets/85a27c31-40ee-468f-ba29-5d5f2826946a)

```yaml
type: entities
entities:
  - type: custom:mushroom-chips-card
    chips:
      - type: template
        content: Steuerungen
        card_mod:
          style: |
            ha-card {
              border: none !important;
              box-shadow: none !important; 
              padding: 3px !important;
              background: none !important;
              margin-bottom: -10px !important;
              font-size: 3.5rem !important;
            }
  - entity: input_select.hp_set_operation_mode
    name: Operation Mode
  - entity: input_select.hp_set_control_method
    name: Control Mode
  - entity: input_number.hp_dhw_target_temperatur
    name: Brauchwasser
    icon: kuf:sani_water_hot
```
```yaml
type: conditional
conditions:
  - condition: state
    entity: sensor.hp_operation_mode
    state: "3"
card:
  type: entities
  entities:
    - type: custom:mushroom-chips-card
      chips:
        - type: template
          content: Sollwertverschiebungen
          card_mod:
            style: |
              ha-card {
                border: none !important;
                box-shadow: none !important; 
                padding: 3px !important;
                background: none !important;
                margin-bottom: -10px !important;
                font-size: 3.5rem !important;
              }
    - entity: input_number.hp_shift_value_in_auto_mode_circuit1
      name: HK₁
      secondary_info: last-changed
      icon: kuf:sani_heating
    - entity: input_number.hp_shift_value_in_auto_mode_circuit2
      name: HK₂
      secondary_info: last-changed
      icon: mdi:heating-coil
    - entity: sensor.hp_target_temp_circuit1
      type: custom:multiple-entity-row
      show_state: false
      name: Status
      icon: mdi:thermometer-chevron-up
      secondary_info: HK₁ & HK₂
      entities:
        - entity: sensor.hp_shift_value_in_auto_mode_circuit1
          name: HK₁
        - entity: sensor.hp_shift_value_in_auto_mode_circuit2
          name: HK₂
```

![image](https://github.com/user-attachments/assets/2667a9a6-823b-4b5f-9487-f319fcc84b4f)

```yaml
type: entities
entities:
  - entity: switch.hp_hauptschalter
    secondary_info: last-changed
    type: custom:multiple-entity-row
    name: Wärmepumpe
    state_color: true
    icon: mdi:heat-pump
    show_state: false
    entities:
      - entity: sensor.power_heatpump
        name: false
      - entity: switch.hp_silent_mode
        name: Silent Mode
        toggle: true
      - entity: switch.hp_hauptschalter
        name: Ein/Aus
        toggle: true
  - entity: binary_sensor.hp_dhw_heating_status
    secondary_info: last-changed
    type: custom:multiple-entity-row
    name: Brauchwasser (DHW)
    state_color: true
    icon: mdi:coolant-temperature
    show_state: false
    entities:
      - entity: sensor.hp_dhw_target_temp
        name: Soll
      - entity: sensor.hp_dhw_water_temp
        name: Ist
      - entity: switch.hp_dhw
        name: false
        toggle: true
  - type: custom:mini-graph-card
    animate: true
    decimals: 1
    hours_to_show: 24
    line_width: 2
    entities:
      - entity: sensor.hp_dhw_water_temp
        show_state: false
        color: "#FFBF00"
        name: Temperatur
    show:
      state: false
      icon: false
      name: false
      labels: true
      icon_adaptive_color: true
      extrema: false
      average: false
    icon: mdi:thermometer
    card_mod:
      style: |-
        ha-card {
          border: none !important;
        }
  - entity: switch.zirkulationspumpe
    secondary_info: last-changed
    type: custom:multiple-entity-row
    name: Zirkulationspumpe
    state_color: true
    icon: mdi:pump
    show_state: false
    entities:
      - entity: automation.heizung_zirkulationspumpe
        name: Automation
        toggle: true
      - entity: switch.zirkulationspumpe
        name: Ein/Aus
        toggle: true
````


![image](https://github.com/user-attachments/assets/d077df93-140c-454e-8df8-8f80f9b4d5c1)

````yaml
type: entities
entities:
  - type: custom:mushroom-template-card
    primary: Heizkreis 1 (Radiatoren)
  - type: custom:bar-card
    positions:
      icon: "off"
      indicator: inside
      name: outside
    width: 80%
    height: 25px
    text-align: right
    padding-left: 4px
    bar-card-border-radius: 2px
    entities:
      - entity: sensor.hp_target_temp_circuit1
        name: Soll
      - entity: sensor.hp_outlet_temp
        name: Ist
    entity_row: false
  - type: custom:mushroom-template-card
    primary: Heizkreis 2 (Fußboden)
  - type: custom:bar-card
    positions:
      icon: "off"
      indicator: inside
      name: outside
    width: 80%
    height: 25px
    text-align: right
    padding-left: 4px
    bar-card-border-radius: 2px
    entities:
      - entity: sensor.hp_target_temp_circuit2
        name: Soll
      - entity: sensor.hp_flow_temp_circle_2
        name: Ist
    entity_row: false
  - type: section
  - entity: sensor.hp_target_temp_circuit1
    type: custom:multiple-entity-row
    show_state: false
    name: Sollwertverschiebungen
    icon: mdi:thermometer
    secondary_info: HK₁ & HK₂
    entities:
      - entity: sensor.hp_shift_value_in_auto_mode_circuit1
        name: HK₁
      - entity: sensor.hp_shift_value_in_auto_mode_circuit2
        name: HK₂
  - entity: sensor.hp_outside_temp
    name: Außentemperatur (Heatpump)
  - type: section
  - entity: sensor.hp_inlet_temp
    type: custom:multiple-entity-row
    show_state: false
    name: Wärmepumpe
    icon: mdi:thermometer-water
    secondary_info: Inlet / Outlet
    entities:
      - entity: sensor.hp_inlet_temp
        name: Eingang
      - entity: sensor.hp_outlet_temp
        name: Ausgang
  - entity: sensor.vorlauf_hk1_esp
    type: custom:multiple-entity-row
    show_state: false
    name: Heizkreis 1 (ESP)
    icon: mdi:thermometer
    secondary_info: Heizkörper
    entities:
      - entity: sensor.vorlauf_hk1_esp
        name: Vorlauf
      - entity: sensor.ruecklauf_hk1_esp
        name: Rücklauf
  - entity: sensor.vorlauf_hk2_esp
    type: custom:multiple-entity-row
    show_state: false
    name: Heizkreis 2 (ESP)
    icon: mdi:thermometer
    secondary_info: Fußbodenheizung
    entities:
      - entity: sensor.vorlauf_hk2_esp
        name: Vorlauf
      - entity: sensor.ruecklauf_hk2_esp
        name: Rücklauf
  - type: section
  - entity: sensor.temp_before_vaporiser
    type: custom:multiple-entity-row
    show_state: false
    name: Temperaturen Verdampfer
    icon: mdi:thermometer
    entities:
      - entity: sensor.temp_before_vaporiser
        name: vor
      - entity: sensor.temp_after_vaporiser
        name: nach
  - entity: sensor.temp_liquid_gas
    name: Temperatur Flüssiggas
````



