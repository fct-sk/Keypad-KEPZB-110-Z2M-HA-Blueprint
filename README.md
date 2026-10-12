# Keypad KEPZB 110 Z2M HA

Home Assistant automation blueprint for the **Frient KEPZB-110** keypad connected through **Zigbee2MQTT** and integrated with **Alarmo**.

## Import into Home Assistant

**[Import this blueprint into Home Assistant](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Ffct-sk%2FKeypad-KEPZB-110-Z2M-HA-Blueprint%2Fblob%2Fmain%2Fkeypad-z2m-control.yaml)**

Alternatively, open **Settings → Automations & scenes → Blueprints → Import Blueprint** and paste this URL:

`https://github.com/fct-sk/Keypad-KEPZB-110-Z2M-HA-Blueprint/blob/main/keypad-z2m-control.yaml`

## Features

- Arm Alarmo in **Away**, **Home**, or **Night** mode from the keypad.
- Disarm Alarmo using a PIN or allowed RFID tag.
- **PINs are configured only in Alarmo.** This blueprint does not store or duplicate the PIN list; Alarmo validates each PIN and reports success or failure back to the keypad through Alarmo events.
- Restrict RFID tags with an explicit allow-list.
- Optionally map all allowed RFID tags to one existing Alarmo code.
- Synchronize alarm state back to the keypad.
- Play audible entry/exit countdowns using Alarmo's configured delay.
- Optional actions for SOS, arming, armed states, disarming, entry delay, and triggered alarm.

## Requirements

- Home Assistant with MQTT configured.
- Zigbee2MQTT with the Frient KEPZB-110 paired and exposing its keypad actions.
- Alarmo installed and configured.

## Initial configuration

When creating an automation from the blueprint:

1. Select your Alarmo control panel.
2. Set the Zigbee2MQTT state topic and set topic. Defaults are `zigbee2mqtt1/Keypad` and `zigbee2mqtt1/Keypad/set`; change them to match your Zigbee2MQTT configuration and the exact case of the device name.
3. Configure PINs and user permissions **in Alarmo only**. The blueprint passes keypad-entered PINs directly to Alarmo.
4. If using RFID, add each tag UID to **Allowed RFID tag IDs**, exactly as Zigbee2MQTT reports it, including the leading `+`. Separate multiple UIDs with semicolons. Present a tag first, then press the arm/disarm button.
5. Choose how RFID is passed to Alarmo:
   - Leave **Optional existing Alarmo code used for allowed RFID tags** blank if each tag UID is configured as its own Alarmo code.
   - Enter an existing code configured in Alarmo to map every allow-listed tag to that code. Alarmo will treat those tags as the same user/code.
6. Make sure Alarmo's options for requiring a code to arm, disarm, or change modes match your intended security policy.

Do not publish actual PINs or private RFID identifiers in issues, screenshots, or support requests.

## Notes

- The blueprint is intended for Zigbee2MQTT, not ZHA.
- Updating the GitHub file does not automatically update a blueprint already imported into Home Assistant. Re-import or replace the local blueprint, then recreate/update the automation inputs if Home Assistant reports obsolete inputs from an older version.
- Test invalid PIN, valid PIN, an unlisted RFID tag, open-sensor refusal, and exit/entry delays in your own Home Assistant/Alarmo setup before relying on it for security.
