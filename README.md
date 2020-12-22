# DeepSpeech
Install Mozilla DeepSpeech 0.9.3 on a Raspberry Pi 4

## Prerequisites
* Raspberry Pi 4 (3+ slower but might be OK)
* Raspbian Lite buster

## Install DeepSpeech 0.9.3
```
sudo apt install git python3-pip python3-scipy python3-numpy python3-pyaudio libatlas3-base
pip3 install deepspeech --upgrade
mkdir ~/dspeech
cd ~/dspeech
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.tflite
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/deepspeech-0.9.3-models.scorer
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.9.3/audio-0.9.3.tar.gz
tar xvf audio-0.9.3.tar.gz
source ~/.profile
```

Transcribe three test files.

```
deepspeech --model deepspeech-0.9.3-models.tflite --scorer deepspeech-0.9.3-models.scorer --audio audio/2830-3980-0043.wav
deepspeech --model deepspeech-0.9.3-models.tflite --scorer deepspeech-0.9.3-models.scorer --audio audio/4507-16021-0012.wav
deepspeech --model deepspeech-0.9.3-models.tflite --scorer deepspeech-0.9.3-models.scorer --audio audio/8455-210777-0068.wav
```

## Live transcription from a microphone

To try live transcription from a microphone, plug in a USB microphone.

Change alsa.conf file so the microphone (device 2) is the default ALSA device. The latest version of Raspbian
as of June 2020 has two soundcards. One for the built-in HDMI audio and one for the built-in headphone jack.

Change alsa.conf file so the microphone (device 3) is the default ALSA device.
The latest version of the Raspberry Pi OS (formerly known as Raspbian) as of
Nov 2020 has three soundcards so the USB microphone is the fourth device.

```
sudo nano /usr/share/alsa/alsa.conf
```

```
defaults.ctl.card 3
defaults.pcm.card 3
```

Install DeepSpeech examples including the microphone example and dependencies.

```
git clone https://github.com/mozilla/DeepSpeech-examples
pip3 install halo webrtcvad --upgrade
python3 DeepSpeech-examples/mic_vad_streaming/mic_vad_streaming.py -m deepspeech-0.9.3-models.tflite -s deepspeech-0.9.3-models.scorer
```

## Links
* [DeepSpeech on github](https://github.com/mozilla/STT)
* [DeepSpeech docs](https://deepspeech.readthedocs.io/en/latest/)
* [DeepSpeech forum](https://discourse.mozilla.org/c/mozilla-voice-stt/247)
