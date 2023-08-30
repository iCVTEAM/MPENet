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
Synthesized Dataset.
Download the dataset from [download_link](https://pan.baidu.com/s/11guCfQbra748LVzUEZpzuw), verify code: 1234. 

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
