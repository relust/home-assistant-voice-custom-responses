# home-assistant-voice-custom-responses
# Introduction

Ever since the new official [Home Assistant Voice satellite ](https://www.home-assistant.io/voice-pe/) was launched to be used with [Home Assistant](https://www.home-assistant.io/), I wanted to try to make the conversation as natural as possible through this satellite..
Through this project, custom random responses can be added to the Home Assistant Voice PE satellite instead of the wake sound.

 Here's a video tutorial:

[https://www.youtube.com/watch?v=1bBOoUhnF4A&t=166s](https://www.youtube.com/watch?v=1bBOoUhnF4A&t=166s)

## Features

- wake word, push to talk, on-demand and continuous conversation support
- service exposed in HA to start and stop the voice assistant from another device/trigger
- visual feedback of the wake word listening/audio recording/success/error status via the satellite LEDs
- changing assistants and language from the graphical interface or with voice commands.

  ## Pre-requisites

- Home Assistant 2024.12.0 or newer
- A voice assistant [configured in HA](https://my.home-assistant.io/redirect/voice_assistants/) with STT and TTS in a language of your choice
- ESPHome  2024.12.2 or newer

  ## Instructions
- Pair the Home Assistant Voice satellite with Home Assistant via Improv BLE using the Home Assistant application on your mobile phone with bluetooth enabled and add it to the EspHome integration.
- In the EspHome integration from the Settings/Devices&services tab, press the `CONFIGURE` button on the paired satellite and check the box `Allow the device to perform Home Assistant actions`.
- Open the `ESPHome Builder` tab from the Home Assistant's main menu and check `Show discovered devices` from three dots menu on the top right and click on the button Take control of the discovered satellite.
- Click on the `EDIT` button of the satellite to enter the editing window.
- Copy the official code of the Home Assistant Voice satellite from [github](https://github.com/esphome/home-assistant-voice-pe/blob/dev/home-assistant-voice.yaml) and paste in the satellite editing window of EspHome builder.
- Comment the two lines for `packages` in the satellite code.
- Cut&paste the lines with `substitutions` in the similar column in the new code
 ```
substitutions:
  name: home-assistant-voice-0903d5
  friendly_name: Home Assistant Voice 0903d5
```
- Cut&paste the lines with the satellite name in EspHome in the similar column in the new code
```
esphome:
  name: ${name}
  name_add_mac_suffix: false
  friendly_name: ${friendly_name} 
```

- Cut&paste the lines with api encription key in the similar column in the new code
```
api:
  encryption:
    key: kk8WVxxxxxxxxxxxxxxxxxxxxxxxxxxvo0IKco=
```
- Cut&paste the lines with wifi setup in the similar column in the new code

```
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password 
```
- Add these lines of code to the `switch` section of the satellite code
```
  - platform: template
    id: custom_responses_switch
    icon: "mdi:microphone-message"
    name: Custom responses
    entity_category: config
    optimistic: true
    restore_mode: RESTORE_DEFAULT_ON
```
- Add these lines of code to the `binary_sensor` section of the satellite code
```
  - platform: template
    name: "Wake Word Detect"
    id: wake_word_sensor
```
- Add these lines of code to the `script` section of the satellite code
```
  - id: activate_wake_word_sensor
    then:
      - binary_sensor.template.publish:
          id: wake_word_sensor
          state: ON
      - delay: 1s
      - binary_sensor.template.publish:
          id: wake_word_sensor
          state: OFF
```
- Add these lines of code #ON TOP# of the `on_wake_word_detection` from `micro_wake_word` section of the satellite code
```
    - if:
        condition:
          switch.is_on: custom_responses_switch
        then:
          - script.execute: activate_wake_word_sensor
          - script.execute: control_leds_voice_assistant_waiting_for_command_phase
          - delay: 1s
          - wait_until:
              condition:
                lambda: return id(nabu_media_player)->state == media_player::MediaPlayerState::MEDIA_PLAYER_STATE_IDLE;
              timeout: 2s
```
