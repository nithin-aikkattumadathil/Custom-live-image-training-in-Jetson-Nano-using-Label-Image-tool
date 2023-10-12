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
* in the 16th line of code, give the exact name of your video file
* in the 20th line of code, we have a predefined count 10, you can increase the count to decrease the number of images to be generated and vice-versa
* save and close prepare_dataset.py
* 
