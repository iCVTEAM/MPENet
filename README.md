# MPENet

Stereo Deblurring with Unaligned Event and RGB Cameras

## Abstract

Event cameras are novel bio-inspired vision sensors that record asynchronous events with high temporal resolution and high dynamic range.
Due to the auxiliary visual information provided by event camera, it is promising to utilize event stream to assist image blurring.
However, existing event-based blurring methods typically assume that the event and RGB cameras are strictly calibrated (e.g., pixel-level sensor designs in DAVIS 240/346), which is usually unavailable in emerging high resolution devices such as dual-lens smartphones and unmanned aerial vehicles.
To unlock more event-based application scenarios, we propose to perform stereo image deblurring with unaligned event and RGB cameras.
Technically, we propose an event-based deblurring net with Multiplane Event frames (MPENet) for stereo matching and deblurring.
The features of event stream and RGB images is firstly extracted by the Event-based Plane Sweep Volume (EPSV) based module.
Then, the event and image features are fused using attention-based fusion and pyramid upsampling modules.
With the aligned event feature and RGB image, a UNet-based deblurring module is introduced to achieve final deblurring.
To effectively training our network, we also design a stereo RGB-event simulation framework.
Moreover, we build a real-world stereo RGB-Event dataset to validate our network.
Experiments on both simulated and real-world dataset demonstrate our network can effectively deblurring especially in complex scenes.

## Dataset
### Synthesized dataset
Download the Synthesized dataset from [download_link](https://pan.baidu.com/s/11guCfQbra748LVzUEZpzuw), verify code: 1234. 

The dataset structure is as follows

```
.
├── 0727549e11766d22
│   └── blur
│       ├── 000008.png
│       ├── 000024.png
│       ├── 000040.png
│       ├── ...
│   ├── hfps_RGB
│       ├── 000000.png
│       ├── 000001.png
│       ├── 000002.png
│       ├── ...
│   ├── events.txt
│   └── events.aedat
│       ...
├── ...
```

Each sequences folder contains `blur` folder and `hfps_RGB` folder. Their indexs are in one-to-one correspondence.

We provide the events file as TXT format and .aedat format (v2e simulator).

Moreover, the timestamp of RGB images and events files is aligned. Both of them started from 0 timestamp. And the frame interval time of RGB images is 80ms.

### Real-world dataset
Download the Real-world dataset from [download_link](https://pan.baidu.com/s/1DIixTmiCTEJfDBrl21Sjvw), verify code: 1234.

The dataset contains 13 sequences and the dataset structure is as follows
```
.
├── chessboard
│   └── hfps_RGB
│       ├── xxx.png
│       ├── xxx.png
│       ├── xxx.png
│       ├── ...
│   ├── events.txt
│   └── info.txt
│       ...
├── waving_arms1
│   └── hfps_RGB
│       ├── xxx.png
│       ├── xxx.png
│       ├── xxx.png
│       ├── ...
│   ├── events.txt
│   └── info.txt
├── ...
|   ...

```
`info.txt` contains the camera settings of two cameras and aligned timestamp.
We use the timestamp offset to align timestamps, which provides the timestamp of the event file corresponding to the first RGB image. Subsequent images can be calculated based on the frame rate.
Blur images can be simulated by provided `blur_simulator.py` or frame accumulation like GoPro dataset.

In addition, for scenes like fire or ink_diffusion where the motion range is relatively small, the resolution is reduced during filming to 768*660 (with the surrounding background being nearly static).
