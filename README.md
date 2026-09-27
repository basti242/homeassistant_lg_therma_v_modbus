# LG Therma V ↔ Home Assistant (Modbus)

Connect and control an LG Therma V heat pump in Home Assistant via Modbus — no cloud, no vendor bridge, just a Modbus TCP gateway and this package.

Tested with:

| Heat pump | Tested by |
|---|---|
| LG Therma V Monoblock 9 kW | [basti242](https://github.com/basti242) |

With this integration you can read and control nearly all settings of your heat pump: operation mode (cooling/auto/heating), control method, DHW target temperature, heating circuit setpoints, silent mode, SG-ready/energy-state input, and read out temperatures, pressures, flow rate, compressor status and more.

![Examples](https://github.com/user-attachments/assets/85a27c31-40ee-468f-ba29-5d5f2826946a) ![Examples](https://github.com/user-attachments/assets/2667a9a6-823b-4b5f-9487-f319fcc84b4f)

## Contents

- [Hardware](#hardware)
- [Installation](#installation)
- [Heat pump setup](#heat-pump-setup)
- [Dashboard examples](#dashboard-examples)
- [Register documentation](#register-documentation)

## Hardware

The LG heat pump only exposes RS485/Modbus. The easiest way to bridge that into Home Assistant is a Modbus TCP gateway.

![Gateway](https://github.com/user-attachments/assets/59bbd424-c406-4b6a-b33f-670361443392)

Tested gateways:

| Device | Type | Tested by | Link |
|---|---|---|---|
| Waveshare RS485 To ETH | tabletop device | [basti242](https://github.com/basti242) | [Amazon](https://amzn.eu/d/9hwIM75) |
| Waveshare RS485 To ETH (B) | top-hat rail | [gRiMMi83](https://github.com/gRiMMi83) | [Amazon](https://amzn.eu/d/4nqkfNH) |
| Waveshare RS232-485-TO-WIFI-ETH | tabletop device | [BigCabbage](https://github.com/BigCabbage) | [Amazon](https://amzn.eu/d/2aOHsr5) |

**Wiring.** Inside the heat pump there is a connector labeled "3RD PARTY CONTROLLER" — this is the Modbus connection. Wire it to contact **A (+)** and **B (-)**.

![Wiring](https://github.com/user-attachments/assets/258c3483-5fb1-4e9a-a41a-709377e070ff)

**DIP switches** (4th-generation units). The main board has two DIP switch banks, SW1 and SW2 — only SW1 matters here:

- SW1, switch 1 → **ON**: heat pump acts as a Modbus slave device
- SW1, switch 2 → **ON**: use the open protocol

![DIP switches](https://github.com/user-attachments/assets/9759fe76-785b-43c3-9957-14483a88a61e)

**LG head unit (RS3) settings.** Also enable Modbus on the indoor head unit itself:

![Head unit settings](https://github.com/user-attachments/assets/b78ce590-2876-4b27-9264-40c5444da8b5)

1. Navigate to Settings
2. Enable the third-party/Modbus controller option

![Head unit settings 2](https://github.com/user-attachments/assets/8f63e8f5-6eb2-4a65-a723-41daf5b122db)

That's it on the hardware side — the heat pump can now be controlled from Home Assistant.

## Installation

1. Download [`modbus_lg_heatpump.yaml`](modbus_lg_heatpump.yaml) and put it in a folder named `integrations` in your Home Assistant config directory (create the folder if it doesn't exist yet).

   ![Folder layout](https://github.com/user-attachments/assets/b85ebb60-3963-4d8f-8c68-fa098d60591b)

2. Make sure `configuration.yaml` loads that folder as a package:

   ```yaml
   homeassistant:
     packages: !include_dir_named integrations
   ```

3. Add the connection details to `secrets.yaml`:

   ```yaml
   # LG Heatpump
   #-----------------------------------------------
   lg_heatpump_modbus_host_ip: 10.10.1.xxx  # IP address of your gateway
   lg_heatpump_modbus_port: 502
   lg_heatpump_modbus_slave: 1
   ```

4. Restart Home Assistant.

## Heat pump setup

See [Hardware](#hardware) above for wiring, DIP switches and the head-unit setting required before Home Assistant can talk to the heat pump.

## Dashboard examples

Requires these HACS frontend cards: **Mushroom**, **card-mod**, **Multiple Entity Row**.

![Dashboard example 1](https://github.com/user-attachments/assets/85a27c31-40ee-468f-ba29-5d5f2826946a)

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
  - entity: select.hp_operation_mode_select
    name: Operation Mode
  - entity: select.hp_control_method_select
    name: Control Mode
  - entity: number.hp_dhw_target_temperatur_number
    name: Brauchwasser
    icon: kuf:sani_water_hot
```

```yaml
type: conditional
conditions:
  - condition: state
    entity: sensor.hp_operation_mode_raw
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
    - entity: number.hp_shift_value_in_auto_mode_circuit1_number
      name: HK₁
      secondary_info: last-changed
      icon: kuf:sani_heating
    - entity: number.hp_shift_value_in_auto_mode_circuit2_number
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
        - entity: number.hp_shift_value_in_auto_mode_circuit1_number
          name: HK₁
        - entity: number.hp_shift_value_in_auto_mode_circuit2_number
          name: HK₂
```

![Dashboard example 2](https://github.com/user-attachments/assets/2667a9a6-823b-4b5f-9487-f319fcc84b4f)

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
      - entity: sensor.hp_power
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
      - entity: number.hp_dhw_target_temperatur_number
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
```

## Register documentation

Full Modbus register map (coil / discrete / input / holding registers, addresses and value meanings): see the [register documentation](https://github.com/basti242/homeassistant_lg_therma_v_modbus/wiki/LG-Register-documentation).

Note: the register table itself has a few known transcription errors (a mislabeled unit, a duplicated row description) — where it disagreed with what the heat pump actually sends, `modbus_lg_heatpump.yaml` follows the value confirmed against the real device, not the table.
