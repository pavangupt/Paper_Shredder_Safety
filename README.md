# Paper_Shredder_Safety
Manufacturers recommend taking several safety measures to avoid injury when operating shredding equipment. I have develop safety mechanism that will automatically beep, if the labour/Engineer crosses the safety limit.

## Problem:
Most shredder manufacturers engineer their equipment to minimize the potential for injury. Unfortunately, human error can override even the best engineered system. However, it’s not just catastrophic accidents that cause trouble for recycling companies and the people they employ. Simply using improper posture when positioning an 80-pound screen can create problems. 

## Solution:
In order enhance the safety mechanism in the cutting industry, I have develop a model that will successfully detect, if the person/labour/engineer trying to cross the safety limit.The IP camera is continously monitor the movements and each records is getting saved in the database. Even if in some unexpected situation, if a labour bychance crosses the safety border, the SSD Model will get triggered and we can hear a alarming sound.
- I have train used the pre-trained SSD Mobile coco pretrained model. One of the major reason for choosing this model was its accuracy and FPS(Frame per Second). In my application, the SSD Mobilenet outperform Faster RCNN and YOLOv3. 

## Steps Followed:

### STEP-1 Download the following content-
- Download v1.13.0 model.
- Download the ssd_mobilenet_v1_coco model from the model zoo or any other model of your choice from TensorFlow 1 Detection Model Zoo.
- Download Dataset & utils.
- Download labelImg tool for labeling images.

### Step-2 Extract all the above zip files into a tfod folder and remove the compressed files-
### Step-3 Creating virtual env using conda-
### STEP-4 Install the following packages in your new environment-
- for GPU:-   pip install pillow lxml Cython contextlib2 jupyter matplotlib pandas opencv-python tensorflow-gpu==1.15.0
- for CPU:-   pip install pillow lxml Cython contextlib2 jupyter matplotlib pandas opencv-python tensorflow==1.15.0

### STEP-5 Install protobuf using conda package manager-
### STEP-6 For protobuff to .py conversion download from a tool from here-
- For Windows :-    protoc object_detection/protos/*.proto --python_out=

### STEP-7 Paste all content present in utils into research folder-
### STEP-8 Paste ssd_mobilenet_v1_coco or any other model downloaded from model zoo into research folder-
- python xml_to_csv.py
### STEP-9 Run the following to generate train and test records-
-- from the research folder- 
- python generate_tfrecord.py --csv_input=images/train_labels.csv --image_dir=images/train --output_path=train.record
- python generate_tfrecord.py --csv_input=images/test_labels.csv --image_dir=images/test --output_path=test.record
### STEP-10 Copy from research/object_detection/samples/config/ YOURMODEL.config file into research/training-
### STEP-11 Update num_classes, fine_tune_checkpoint ,and num_steps plus update input_path and label_map_path for both train_input_reader and eval_input_reader-

### STEP-12 From research/object_detection/legacy/ copy train.py to research folder
### STEP-13 Copy deployment and nets folder from research/slim into the research folder-
### STEP-14 NOW Run the following command from the research folder. This will start the training in your local system-
- python train.py --logtostderr --train_dir=training/ --pipeline_config_path=training/YOUR_MODEL.config
