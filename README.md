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
- Cut&paste the lines with the satellite name in EspHome in the similar column in the new code
```
esphome:
  name: ${name}
  name_add_mac_suffix: false
  friendly_name: ${friendly_name} 
```

- Cut&paste the lines with api encription key in the similar column in the new code
- Cut&paste the lines with wifi setup in the similar column in the new code

```
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password 
```

