# Custom-live-image-training-in-Jetson-Nano-using-Label-Image-tool
* You have to do this process in your external Linux environment, other than jetson nano board
  
# Expand memory if required
* for that, ensure sufficient memory is available, if not increase memory using gparted tool
* sudo apt-get install gparted
* sudo gparted
* expand memory and save

# Install dependencies
* make sure python3 is installed
* install dependencies below-
* sudo apt install python3-pip
* pip3 install opencv-python
* pip3 install imutils
* pip3 install matplotlib
* pip3 install torchvision
* pip3 install torch
* pip3 install boto3
* pip3 install pandas
* pip3 install urllib3
* sudo apt-get install pyqt5-dev-tools
* sudo apt-get install python3-lxml
* sudo apt install git

# Clone jetson official github repository for training
* git clone https://github.com/mailrocketsystems/jetson-train.git
* create a video in .mp4 format that covers all the possible views of each objects you are going to train
* place the video inside jetson-train/videos in mp4 format
* now we have to convert the video file to frame by frame images using prepare_dataset.py python file
* open prepare_dataset.py
* in the 16th line of code, give the exact name of your video file (no need if you have updated code)
* in the 20th line of code, we have a predefined count 10, you can increase the count to decrease the number of images to be generated and vice-versa
* save and close prepare_dataset.py
* cd jetson-train/
* python3 prepare_dataset.py
* it will ask model name,give your model name.
* now video will play,and it will store several images inside the model file you mentioned

# Annotating using Label image tool
* now we have to give the annotation to each image we've captured
* for that, we need to clone and use labelimg tool in home
* git clone https://github.com/HumanSigal/labelImg.git
* cd labelImg/
* make qt5py3
* python3 labelImg.py
* this will open label image tool
* click open dir and choose path as jetson-train/data/model_name/JPEGimages/
* it will load all the image files in the file list
* click change save dir and choose path as jetson-train/data/model_name/Annotations/
* it will save all annotations inside directory
* click create rect box and draw boundary to the object, give name to object and click save
* paste rectbox for each repeating image and draw new for new object
* do it for all images and save each

# Training custom objects on linux environment
* create labels.txt file inside jetson-train/data/model_name (gedit labels.txt)
* list the name of objects you are going to train in the labels.txt file, one name in one line and top left alligned,and save.
* open a new terminal at jetson-train
* python3 train_ssd.py --dataset-type=voc --data=data/model_name --model-dir=models/model_name --batch-size=2 --workers=2 --epochs=300
* close all other applications on the system
* it will take some time
* open terminal at jetson-train
* python3 result.py
* give model_name
* it will show results graph and it will give best check point
* copy best check point and labels.txt file

# Rest of project inside jetson nano
* make sure you have jetson-inference folder in the device
* create a folder with your mode_name in the directory jetson-inference/python/training/detection/ssd/models/
* paste the copied check point and labels.txt file
* now you'll need to convert your PyTorch model to ONNX
* cd jetson-inference
* docker/run.sh
* The above step will allow you to enter into the root of jetson nano developer kit
* open anew terminal inside jetson-inference/python/training/detection/ssd/
* python3 onnx_export.py --model-dir=models/model_name
* The converted model will then be saved under model_name/ssd-mobilenet.onnx, which you can then load with the detectnet programs
* make sure you are in root jetson-inference/python/training/detection/ssd
* detectnet --model=models/model_name/ssd-mobilenet.onnx --labels=models/model_name/labels.txt --input-blob=input_0 --output-cvg=scores --output-bbox=boxes /dev/video0
* the above command will start the detection procedures

# that's all ,jetson will detect you custom objects.
  
 
