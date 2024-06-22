# MTDP
Tile Detection based on Mask R-CNN in Non-Structural Environment for Robotic Tiling.</br></br>
Robotic tiling is an efficient way to replace manual work, with tile detection and positioning serving as a pivotal technology. However, the tiling environment is characterized by its complexity. Our study introduces the instance segmentation method Mask R-CNN, which can detect tiles in non-structural environments after proper training. To address the difficulty of acquiring datasets and high annotation costs, a densely arranged tile dataset that allows for automatic labeling has been synthesized and various designed data augmentation techniques are employed. </br></br>
# Download
This repository encompasses all the tile datasets used, the core programs, as well as the trained models.</br>
- at the [TeraBox](https://terabox.com/s/1I7THz2RfGos_XxSLgqI7RQ).
- or, at the [Baidu Netdisk](https://pan.baidu.com/s/14slF01E78bWIAyoUpUPQvQ) using the code: **wszd**

# Overview
## Dataset The training dataset and this folder <br>
evaluate: The test dataset is stored in this folder. The "image" folder stores the test tile images, while the "mask" 
folder stores the corresponding manually annotated images. And the "keypoints_image" folder stores images and the 
corresponding annotated results which are used to evaluate the 2D positioning errors. <br>
source: The Single-Tile Dataset is stored in folder "Set-A", and the Dense Arrangement Multi-Tile Dataset is stored 
in folder "Set-B". As for "Set-B*", data augmentation methods are automatically utilized when training, so that there
is no need to establish "Set-B*" folder.
## model
This folder provide our trained three models. Based on the pre-trained model, three distinct Mask R-CNN models are 
trained under different conditions: exclusively using the Set-A dataset, exclusively using the Set-B dataset, and 
utilizing data augmentation when training on the Set-B dataset which named Set-B*, which correspond to "ori_50epoch.pt",
"syn_50epoch.pt", and "syn_aug_50epoch.pt" respectively.
## transforms.py
This file is about data augmentation methods.
# Start Detection
Please run predict.py, the detection results will be saved in folder "predicted_data". It is easy to change detection 
model and image through change image path or model path for example:
>if __name__ == "__main__": <br>
&ensp;&ensp; predict_single(r"DataSet\evaluate\image\test8.jpg", "model/syn_aug_50epoch.pt")<br>
&ensp;&ensp; # predict_single(r"DataSet\evaluate\image\test9.jpg", "model/syn_50epoch.pt")<br>
&ensp;&ensp; # predict_single(r"DataSet\evaluate\image\test8.jpg", "model/ori_50epoch.pt")<br>
>
# Start Training
Please run train.py, the training parameters can be adjusted in function main. If you want to add your own images, please
prepare tile images and the corresponding annotated masks and put them in folder "DataSet/source/Set-xxx/image" and 
"DataSet/source/Set-xxx/mask" respectively. Please pay attention that the names of image file and mask file should be 
the same.
# Evaluate Models
It is easy to evaluate the performance of trained model, please run evaluate.py, for example:
>if __name__ == "__main__": <br>
&ensp;&ensp; # evaluate_key_points()  # evaluate key point errors <br>
&ensp;&ensp; evaluate_model()  # evaluate model performance



