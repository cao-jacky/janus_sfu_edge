# janus_sfu_edge 

Forked from the Python module [python_janus_client](https://github.com/josephlim94/python_janus_client), this repository contains a developed plugin to communicate with a Janus SFU server, a script which can obtain media streams from the server (i.e., video and audio), and then parse those streams to perform analysis (e.g., YOLO object detection). 

## Usage
There might be a need to install the above-linked Python module. If not, it should be able to run from the files within the repo. However, there are other modules to install, there are a few listed here but you might need to install more if the scripts complain.

```sh
pip3 install ultralytics
pip3 install numpy
pip3 install 
```

There are two main scripts, `sfu_streamer.py`and `stream_analyser.py`, both of which can be run as `python3 file_name.py` without any parameters. You will need to edit the files themselves though, i.e., point to the correct Janus SFU server.

In both files, the following parameter needs to be checked:

```python
sfu_uri = "wss://cowebxr.com:8989/janus"
```

Replace the URI with your Janus SFU server. 

1. The streamer can be run using `python sfu_streamer.py`, this script was designed to open the Janus SFU-sent video stream and saves video frames as .png images. The image format and the functionality of this script is defined by the function `subscribe` in `plugin_sfu.py`.

2. The analysis is run with `python stream_analyser.py`, this script takes the latest image in the folder and pushes it through YOLO object detection. It also ensures that there are only ever 50 images in the image folder to save the folder from ballooning in size. The results are pushed back to the original Janus SFU as a published stream and can be subscribed to as a client.
