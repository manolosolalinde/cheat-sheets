Tensorflow Object Detection API

# Installation

```bash
git clone https://github.com/tensorflow/models.git

sudo apt-get install protobuf-compiler
pip3 install tensorflow-gpu
pip3 install tensorflow
pip3 install Cython
pip3 install contextlib2
pip3 install pillow
pip3 install lxml
pip3 install matplotlib
git clone https://github.com/cocodataset/cocoapi.git
cd cocoapi/PythonAPI
code Makefile
```
Next, modify the makefile for python3.

```bash
make
cp -r pycocotools /mnt/0F22134B0F22134B/GITHUB/Tensorflow\ Object\ Detection/models/research/
cd /mnt/0F22134B0F22134B/GITHUB/Tensorflow\ Object\ Detection/models/research/
protoc object_detection/protos/*.proto --python_out=.
code ~/.bashrc
```
Include the following lines in .bashrc
```bash
RESEARCH_PATH=/mnt/0F22134B0F22134B/GITHUB/Tensorflow\ Object\ Detection/models/research
export PYTHONPATH=$PYTHONPATH:$RESEARCH_PATH:$RESEARCH_PATH/slim
```

Test installation
```bash
python3 object_detection/builders/model_builder_test.py
```


