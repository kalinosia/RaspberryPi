# TensorFlowLite Object Detection on Raspberry-Pi
## by @EdjeElectronics

A guide showing how to train TensorFlow Lite object detection models and run them on the Raspberry Pi.

![gif](https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi/blob/master/doc/BSR_demo.gif?raw=true)

## Sources
* Pretty and matter-of-fact version is [here](https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi).
* If you wnat tuturial on youtube: [here](https://www.youtube.com/watch?v=aimSGOAUI8Y&t=496s)
* Longer version on this [here](https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi/blob/master/Raspberry_Pi_Guide.md)

## Steps
    1. Update the Raspberry Pi
    2. Download this repository 
    3. Create virtual environment
    4. Install TensorFlow, OpenCV (if U don't have) and more libraries
    5. Set up TensorFlow Lite detection model
    6. Run TensorFlow Lite model!
    7. Run next time
    
### 1 Raspberry Pi
```
sudo apt-get update
sudo apt-get dist-upgrade
```
You need camera, so remember to make sure the camera interference is enabled in Raspberry Pi Confuguration menu.

### 2 Code

` git clone https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi.git `
Rename folder and go in it.

```
mv TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi tflite1
cd tflite1
```
### 3 Virtual environment
Install:
```
sudo pip3 install virtualenv
```
Create folder "tflite1-env":
```
python3 -m venv tflite1-env
```
Activate the enviroment:
```
source tflite1-env/bin/activate
```
**You'll need to issue the source tflite1-env/bin/activate command from inside the /home/pi/tflite1 directory to reactivate the environment every time you open a new terminal window. You can tell when the environment is active by checking if (tflite1-env) appears before the path in your command prompt, as shown in the screenshot below.**

### 4 Install packages
```
bash get_pi_requirements.sh
```
What you need:
```
sudo apt-get -y install libjpeg-dev libtiff5-dev libjasper-dev libpng12-dev
sudo apt-get -y install libavcodec-dev libavformat-dev libswscale-dev libv4l-dev
sudo apt-get -y install libxvidcore-dev libx264-dev
sudo apt-get -y install qt4-dev-tools libatlas-base-dev

pip install opencv-python
pip install tensorflow
```
But better use first option.

### 5 Dowland model
```
wget https://storage.googleapis.com/download.tensorflow.org/models/tflite/coco_ssd_mobilenet_v1_1.0_quant_2018_06_29.zip
```
```
unzip coco_ssd_mobilenet_v1_1.0_quant_2018_06_29.zip -d Sample_TFLite_model
```
Or do manualy....

```







YOU CAN CREATE MODEL        should soon be here my model 






````
### 6 Run (the TensorFlow Lite model)\
```
python3 TFLite_detection_webcam.py --modeldir=Sample_TFLite_model
```

### 7 RUN !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
```
cd tflite1
source tflite1-env/bin/activate
python3 TFLite_detection_webcam.py --modeldir=Sample_TFLite_model
```



# MORE GOODS
<p align="center">
   <img src="https://github.com/EdjeElectronics/TensorFlow-Lite-Object-Detection-on-Android-and-Raspberry-Pi/blob/master/doc/TFLite-vs-EdgeTPU.gif?raw=true">
</p>
