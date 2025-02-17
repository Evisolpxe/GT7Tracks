***
# Gran Turismo 7 Track Capture Tool

## Introduction

This repository contains a Gran Turismo 7 app used to capture telemetry data as it is received, in a .csv file.
It is initially made to capture car position x/z/y in order to learn tracks coordinates for further automatic recognition of the track using ML/AI.
Track dumps also contain speed/rpm, but can be easily updated to include any native telemetry data.
``
PlayStation 4/5 (port 33749) -> GT7Proxy (port 33740)
``

## Running the capture

All tracks are referenced [here](https://github.com/ddm999/gt7info/blob/web-new/_data/db/course.csv)
The **--track** parameter should reflect the track ID you will be using to capture telemetry data.

```
usage: GT7Map2CSV.py [-h] --ps_ip PS_IP [--logpackets LOGPACKETS] --track TRACK

options:
  -h, --help            show this help message and exit
  --ps_ip PS_IP         Playstation 4/5 IP address. Accepts IP or FQDN provided it
                        resolves to something.
  --logpackets LOGPACKETS
                        Optionnaly log packets for future playback using https://git
                        hub.com/vthinsel/Python_UDP_Receiver/UDPSend_timed.py
                        .Default is False
  --track TRACK         Track ID as per https://github.com/ddm999/gt7info/blob/web-
                        new/_data/db/course.csv
```

The dumps directory of this repository contains csv files with track ID as the name.

More information can also be found on the great GTPlanet forum from [here](https://www.gtplanet.net/forum/threads/gt7-is-compatible-with-motion-rig.410728/post-13917994) 

## Training the model

Use LearnTrack.py to train and/or predict

### Train
LearnTrack can train a tensorflow model and save it for further prediction.
As arguments, you can provide a folder containing the csv files to learn.
Each csv must ba named with the track ID as defined in the track definition file which is available using option **--refreshcsv True**
You can specify a modelname that will be saved in a folder. By default the model is saved in folder gt7.model

### Predict
in predict mode you can specify the model to load, which is gt7.model by default

## Live guessing

GT7TrackGuest is a simple tool used to guess the track you are running on. It requires the model name (gt7.model by default), the PS5 IP where GT7 is running.
It needs to be restarted each time you change the track you are on as it doesn't detect new session.
