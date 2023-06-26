# CWTracker


## Tracking performance
### Results on MOT17 challenge test set
| Tracker       |  MOTA |  IDF1  |  HOTA  |
|:--------------|:-------:|:------:|:------:|
| CWTracker      |  79.6   |  77.1  |  63.0  |
| CWTracker++ |  80.9   |  78.8  |  64.2  |

### Results on MOT20 challenge test set
| Tracker       | MOTA   | IDF1 | HOTA |
|:--------------|:-------:|:------:|:------:|
|CWTracker     | 76.7   | 76.1 | 62.4 | 
|CWTracker++  | 76.8   | 76.4 | 62.7 | 



 
### Setup with Anaconda

Our environment is consistent with [BOT-SORT](https://github.com/NirAharon/BoT-SORT)

**Step 1.** Create Conda environment and install pytorch.
```shell
conda create -n cwtracker_env python=3.7
conda activate cwtracker_env
```
**Step 2.** Install torch and matched torchvision from [pytorch.org](https://pytorch.org/get-started/locally/).<br>
The code was tested using torch 1.11.0+cu113 and torchvision==0.12.0 

**Step 3.** Install [pycocotools](https://github.com/cocodataset/cocoapi).
```shell
pip3 install cython; pip3 install 'git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI'
```

Step 4. Others
```shell
# Cython-bbox
pip3 install cython_bbox

# faiss cpu / gpu
pip3 install faiss-cpu
pip3 install faiss-gpu
```


## Model Zoo

- We used the publicly available [ByteTrack](https://github.com/ifzhang/ByteTrack) model zoo trained on MOT17, MOT20 and ablation study for YOLOX object detection.

- Ours trained ReID models can be downloaded from [MOT17-SBS-S50](https://drive.google.com/file/d/1QZFWpoa80rqo7O-HXmlss8J8CnS7IUsN/view?usp=sharing), [MOT20-SBS-S50](https://drive.google.com/file/d/1KqPQyj6MFyftliBHEIER7m_OrGpcrJwi/view?usp=sharing).


## Tracking

* **Test on MOT17**

```shell
python3 tools/track_main.py <dataets_dir/MOT17> --default-parameters --with-reid --benchmark "MOT17" --eval "test" --fp16 --fuse
python3 tools/interpolation.py --txt_path <path_to_track_result>
```

* **Test on MOT20**

```shell
python3 tools/track_main.py <dataets_dir/MOT20> --default-parameters --with-reid --benchmark "MOT20" --eval "test" --fp16 --fuse
python3 tools/interpolation.py --txt_path <path_to_track_result>
```

* **Evaluation on MOT17 validation set (the second half of the train set)**

```shell
python3 tools/track_main.py <dataets_dir/MOT17> --default-parameters --benchmark "MOT17" --eval "val" --fp16 --fuse
```


## Acknowledgement

Many of our work, code, weights, and inspiration come from
[ByteTrack](https://github.com/ifzhang/ByteTrack), 
[StrongSORT](https://github.com/dyhBUPT/StrongSORT),
[FastReID](https://github.com/JDAI-CV/fast-reid),
[YOLOX](https://github.com/Megvii-BaseDetection/YOLOX),
[BOT-SORT](https://github.com/NirAharon/BoT-SORT ),and
[YOLOv7](https://github.com/wongkinyiu/yolov7). 
Thanks for their excellent work!
