# DeepSpeech
Install Mozilla DeepSpeech 0.7.3 on a Raspberry Pi 4

## Prerequisites
* Raspberry Pi 4 (3+ slower but might be OK)
* Raspbian Lite buster

## Install DeepSpeech 0.7.3
```
sudo apt install git python3-pip python3-scipy python3-numpy python3-pyaudio libatlas3-base
pip3 install deepspeech --upgrade
mkdir ~/dspeech
cd ~/dspeech
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.7.3/deepspeech-0.7.3-models.tflite
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.7.3/deepspeech-0.7.3-models.scorer
curl -LO https://github.com/mozilla/DeepSpeech/releases/download/v0.7.3/audio-0.7.3.tar.gz
tar xvf audio-0.7.3.tar.gz
source ~/.profile
```

Transcribe three test files.

```
deepspeech --model deepspeech-0.7.3-models.tflite --scorer deepspeech-0.7.3-models.scorer --audio audio/2830-3980-0043.wav
deepspeech --model deepspeech-0.7.3-models.tflite --scorer deepspeech-0.7.3-models.scorer --audio audio/4507-16021-0012.wav
deepspeech --model deepspeech-0.7.3-models.tflite --scorer deepspeech-0.7.3-models.scorer --audio audio/8455-210777-0068.wav
```

## Live transcription from a microphone

To try live transcription from a microphone, plug in a USB microphone.

Change alsa.conf file so the microphone (device 1) is the default ALSA device.

```
sudo nano /usr/share/alsa/alsa.conf
```

```
defaults.ctl.card 1
defaults.pcm.card 1
```

Install DeepSpeech examples including the microphone example and dependencies.

```
git clone https://github.com/mozilla/DeepSpeech-examples
pip3 install halo webrtcvad --upgrade
python3 DeepSpeech-examples/mic_vad_streaming/mic_vad_streaming.py -m deepspeech-0.7.3-models.tflite -s deepspeech-0.7.3-models.scorer
```

## Links
* [DeepSpeech on github](https://github.com/mozilla/DeepSpeech)
* [DeepSpeech docs](https://deepspeech.readthedocs.io/en/v0.7.3/)
* [DeepSpeech forum](https://discourse.mozilla.org/c/deep-speech/247)
