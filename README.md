# rfidpad
This is the Home Assistant custom component for RFIDPad
(https://www.github.com/janpascal/rfidpad)

## Prerequisities
You will need an MQTT server such as Mosquitto. Configure MQTT in your Home
Assistant installation. Give the homeassistant MQTT user read access to
`rfidpad/discovery/#`, to `rfidpad/+/battery` and to `rfidpad/+/action`.
Give it write access to `rfidpad/+/status`.

Add an `rfidpad` MQTT user and give it write access to 
`rfidpad/discovery/#`, to `rfidpad/+/battery` and to `rfidpad/+/action`.
Give it write access to `rfidpad/+/status`.

## Installation via HACS
- First install HACS in Home assistant. See https://hacs.xyz/ for instructions.
- Open the Community panel in Home Assistant
- Open the 'hamburger menu' and select 'Custom repositories'
- Enter https://github.com/janpascal/ha-rfidpad-integration where it says 'Add custom repository URL'. In the Category dropdown select 'Integration' and click 'Add' 
- Now press the big '+' on the bottom of the screen. Search for 'RFIDPad', select it and click on 'Install this repository in HACS'
- Configure the RFID custom component by filling in the base MQTT topic. The default (rfidpad) will do if you haven't changed the firmware.

## Configuration
The tags that can be used to arm/disarm your Home Assistant alarm need to be
configured in Home Assistant's `configuration.yaml` configuration file.
Add a snippet like:

```
rfidpad:
  tags:
    - tag: ABCD0145
      name: Mary
    - tag: 45AB12EC
      name: John
```

and restart Home Assistant

## Automations
RFIDPad sends events that can be used in automations. Choose trigger type
'Event' with event type 'rfidpad.tag_scanned'  and event data 'button: ARM_AWAY'
to start an automation that is triggered when someone scans their tag and pushed
the 'ARM AWAY' button. A suggested action would be to call the
'alarm_control_panel.alarm_arm_away' service on your manual alarm panel.

When the 'ARM HOME' button is pushed, the event data is 'button: ARM_HOME'.
Similarly, event data 'button: DISARM' is used when the 'DISARM' button is
pushed after scanning a valid tag.

No event are sent if an unknown tag is scanned.

## History
The RFIDPad integration keep a history of the most recent tags scanned, the name
(from configuration.yaml) and which button was pushed. This information can be
viewed using the `RFIDPad History Card`,
https://www.github.com/janpascal/ha-rfidpad-history-card.

## Entities
Each RFIDPad device has two associated entities, one representing the last tag
scanned (sensor.rfidpad_tag) and one representing the battery level
(sensor.rfidpad_battery).


## License
Copyright (C) 2020-2021 Jan-Pascal van Best <janpascal@vanbest.org>

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

