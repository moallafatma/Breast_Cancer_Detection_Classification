# mias-mammography-faster-rcnn

## Requirements

- GCC >= 4.9
- CUDA >= 9.0

## Installation instructions

### 1. Faster R-CNN instructions

First, create an environment :

```
conda create --name faster-r-cnn
conda activate faster-r-cnn
conda install ipython pip
pip install -r requirements.txt
cd faster-r-cnn
```

Then, follow [these instructions](https://github.com/facebookresearch/maskrcnn-benchmark/blob/master/INSTALL.md)

### 2. RetinaNet instructions

First, create an environment :

```
conda create --name retinanet
conda activate retinanet
conda install ipython pip
pip install -r requirements.txt
cd retinanet
```

Then, follow [these instructions](https://github.com/fizyr/keras-retinanet#installation)

### 3. FCOS instructions

First, create an environment :

```
conda create --name fcos
conda activate fcos
conda install ipython pip
pip install -r requirements.txt
cd fcos
```

Then, follow [these instructions](https://github.com/tianzhi0549/FCOS#installation)

## How it works

### 1. Generate COCO or VOC augmented data

It is possible to generate COCO or VOC annotations from raw data (`all-mias` folder + `Info.txt` annotations file) through 2 scripts: `generate_{COCO|VOC}_annotations.py` :

```
python generate_{COCO|VOC}_annotations --images (or -i) <Path to the images folder> \
                                       --annotations (or -a) <Path to the .txt annotations file> \
                                       --output (or -o) <Path to output folder> \
                                       --aug_fact <Data augmentation factor> \
                                       --train_val_split <Percetange of the train folder (default 0.9)>
```

### 2. How to run a training

#### 2.1 Faster R-CNN
TODO

#### 2.2 RetinaNet

To run a training with the retinanet :

```
cd retinanet
conda deactivate && conda activate retinanet
python train.py --compute-val-loss \ # Computer val loss or not
                --tensorboard-dir <Path to the tensorboard directory> \
                --batch-size <Batch size> \
                --epochs <Nb of epochs> \
                coco <Path to the COCO dataset>
```

And if you want to see the tensorboard, run on another window :

```
tensorboard --logdir <Path to the tensorboard directory>
```

#### 2.3 FCOS

To run a training with the FCOS Object Detector :

- Follow [this instruction](https://github.com/tianzhi0549/FCOS/issues/54#issuecomment-497558687)
- Run this command :

```
cd fcos
conda deactivate && conda activate fcos
python train_net.py --config-file <Path to the config file> \
                    OUTPUT_DIR <Path to the output dir for the logs>
```

### 3. How to run an inference

#### 3.1 Faster R-CNN
TODO

#### 3.2 RetinaNet
TODO

#### 3.3 FCOS

```
cd fcos
conda deactivate && conda activate fcos
python test_net.py --config-file <Path to the config file> \
                   MODEL.WEIGHT <Path to weights of the model to load> \
                   TEST.IMS_PER_BATCH <Nb of images per batch>
```
