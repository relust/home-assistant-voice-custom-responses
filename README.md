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
- visual feedback on the tablet display
- changing assistants and language from the graphical interface or with voice commands.

  ## Pre-requisites

- Home Assistant 2023.11.3 or newer
- For tablets with browser or Home Assistant companion app, install Browser Mod integration with HACS. 
- A voice assistant [configured in HA](https://my.home-assistant.io/redirect/voice_assistants/) with STT and TTS in a language of your choice
- ESPHome 2023.11.6 or newer
