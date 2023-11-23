# Custom-live-image-training-in-Jetson-Nano-using-Label-Image-tool-And-UART-transfer
During the training process of custom images in jetson nano developer kit, if you face issues like insufficient memory and low processing speed , you can use Label image tool. Here we are doing the main training in an external Linux environment and only the trained model with less amount of losses is copied to the board along with labels.txt file. 


* All the labels file, onnx file and checkpoint with less amount of loss for traffic sign detection, drowsiness detection are added in this branch
