# Keypad KEPZB 110 Z2M HA

Home Assistant automation blueprint for the **Frient KEPZB-110** keypad connected through **Zigbee2MQTT** and integrated with **Alarmo**.

## Import into Home Assistant

**[Import this blueprint into Home Assistant](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ffct-sk%2FKeypad-KEPZB-110-Z2M-HA-Blueprint%2Fblob%2Fmain%2Fblueprint.yaml)**

Alternatively, open **Settings → Automations & scenes → Blueprints → Import Blueprint** and paste this URL:

`https://github.com/fct-sk/Keypad-KEPZB-110-Z2M-HA-Blueprint/blob/main/blueprint.yaml`

## Features

- Arm Alarmo in **Away**, **Home**, or **Night** mode from the keypad.
- Disarm Alarmo using an allowed PIN or RFID tag.
- Allow one primary PIN and additional PINs.
- Restrict RFID tags with an explicit allow-list.
- Optionally map all allowed RFID tags to one existing Alarmo PIN.
- Synchronize alarm state back to the keypad.
- Play audible entry/exit countdowns using the delay currently reported by Alarmo.
- Optional actions for SOS, arming, armed states, disarming, entry delay, and triggered alarm.

## Requirements

- Home Assistant with MQTT configured.
- Zigbee2MQTT with the Frient KEPZB-110 paired and exposing its keypad actions.
- Alarmo installed and configured.

## Initial configuration

When creating an automation from the blueprint:

1. Select your Alarmo control panel.
2. Set the Zigbee2MQTT state topic and set topic. The defaults in this blueprint are `zigbee2mqtt1/Keypad` and `zigbee2mqtt1/Keypad/set`; change them to match your Zigbee2MQTT configuration and the exact case of the device name.
3. Set the primary PIN. It must also be configured as a valid code in Alarmo.
4. Add extra PINs in **Additional valid PIN codes**, separated by semicolons. Each must also exist in Alarmo.
5. To use RFID, add each UID to **Allowed RFID tag IDs**, exactly as Zigbee2MQTT reports it, including the leading `+`. Separate multiple UIDs with semicolons. Present a tag first, then press the arm/disarm button.
6. Choose how RFID is passed to Alarmo:
   - Leave **Optional Alarmo code for all allowed RFID tags** blank if every tag UID is configured as its own Alarmo code.
   - Enter an existing Alarmo PIN to map every allow-listed tag to that PIN. Alarmo will then treat all those tags as the same code/user.

Do not publish actual PINs or private RFID identifiers in issues, screenshots, or support requests.

## Notes

- The blueprint is intended for Zigbee2MQTT, not ZHA.
- The YAML and template expressions were checked during preparation, but the blueprint should still be tested in your own Home Assistant/Alarmo setup before relying on it for security.
