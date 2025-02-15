# Ultra-Fast-Lane-Detection
PyTorch implementation of the paper "[Ultra Fast Structure-aware Deep Lane Detection](https://arxiv.org/abs/2004.11757)".

Updates: Our paper has been accepted by ECCV2020.

![alt text](vis.jpg "vis")

The evaluation code is modified from [SCNN](https://github.com/XingangPan/SCNN) and [Tusimple Benchmark](https://github.com/TuSimple/tusimple-benchmark).

Caffe model and prototxt can be found [here](https://github.com/Jade999/caffe_lane_detection).

# Demo 
<a href="http://www.youtube.com/watch?feature=player_embedded&v=lnFbAG3GBN4
" target="_blank"><img src="http://img.youtube.com/vi/lnFbAG3GBN4/0.jpg" 
alt="Demo" width="240" height="180" border="10" /></a>


# Install
Please see [INSTALL.md](./INSTALL.md)

# Get started
First of all, please modify `data_root` and `log_path` in your `configs/culane.py` or `configs/tusimple.py` config according to your environment. 
- `data_root` is the path of your CULane dataset or Tusimple dataset. 
- `log_path` is where tensorboard logs, trained models and code backup are stored. ***It should be placed outside of this project.***



***

For gpu training, run
```Shell
python -train.py --params configs/culane.yaml
```

To visualize the log with tensorboard, run

```Shell
tensorboard --logdir log_path --bind_all
```

# Trained models
We provide two trained Res-18 models on CULane and Tusimple.

|  Dataset | Metric paper | Metric This repo | Avg FPS on GTX 1080Ti |    Model    |
|:--------:|:------------:|:----------------:|:-------------------:|:-----------:|
| Tusimple |     95.87    |       95.82      |         306         | [GoogleDrive](https://drive.google.com/file/d/1WCYyur5ZaWczH15ecmeDowrW30xcLrCn/view?usp=sharing)/[BaiduDrive(code:bghd)](https://pan.baidu.com/s/1Fjm5yVq1JDpGjh4bdgdDLA) |
|  CULane  |     68.4     |       69.7       |         324         | [GoogleDrive](https://drive.google.com/file/d/1zXBRTw50WOzvUp6XKsi8Zrk3MUC3uFuq/view?usp=sharing)/[BaiduDrive(code:w9tw)](https://pan.baidu.com/s/19Ig0TrV8MfmFTyCvbSa4ag) |



自己训练了一个，mobilenetv2骨干网络，输入size 256*512，Fmeasure 66.19% 较resnet18 288*800分辨率精度降低3个点，速度在板卡上快了3-4倍

For evaluation, run
```Shell
mkdir tmp
# This a bad example, you should put the temp files outside the project.

python test.py configs/culane.py --test_model path_to_culane_18.pth --test_work_dir ./tmp

python test.py configs/tusimple.py --test_model path_to_tusimple_18.pth --test_work_dir ./tmp
```

Same as training, multi-gpu evaluation is also supported.

# Visualization

We provide a script to visualize the detection results. Run the following commands to visualize on the testing set of CULane and Tusimple.
```Shell
python demo.py configs/culane.py --test_model path_to_culane_18.pth
# or
python demo.py configs/tusimple.py --test_model path_to_tusimple_18.pth
```

Since the testing set of Tusimple is not ordered, the visualized video might look bad and we **do not recommend** doing this.

# Speed
To test the runtime, please run
```Shell
python speed_simple.py  
# this will test the speed with a simple protocol and requires no additional dependencies

python speed_real.py
# this will test the speed with real video or camera input
```
It will loop 100 times and calculate the average runtime and fps in your environment.

# Citation

```BibTeX
@InProceedings{qin2020ultra,
author = {Qin, Zequn and Wang, Huanyu and Li, Xi},
title = {Ultra Fast Structure-aware Deep Lane Detection},
booktitle = {The European Conference on Computer Vision (ECCV)},
year = {2020}
}
```

# Thanks
Thanks zchrissirhcz for the contribution to the compile tool of CULane, KopiSoftware for contributing to the speed test, and ustclbh for testing on the Windows platform.
