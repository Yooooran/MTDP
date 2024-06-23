# MTDP
Tile Detection based on Mask R-CNN in Non-Structural Environment for Robotic Tiling.</br></br>
Robotic tiling is an efficient way to replace manual work, with tile detection and positioning serving as a pivotal technology. However, the tiling environment is characterized by its complexity. Our study introduces the instance segmentation method Mask R-CNN, which can detect tiles in non-structural environments after proper training. To address the difficulty of acquiring datasets and high annotation costs, a densely arranged tile dataset that allows for automatic labeling has been synthesized and various designed data augmentation techniques are employed. The trained model achieves a detection performance with AP75=98.94% and AP95=88.14% on 100 test images.This repository encompasses all the tile datasets used, the core programs, as well as the trained models.</br></br></br>
![image](https://github.com/Yooooran/MTDP/assets/103570083/437651b8-d412-4018-8e6a-2a178c318f04)
![image](https://github.com/Yooooran/MTDP/assets/103570083/7b3574a1-3bbf-4da7-92e6-1aee2b44a89d)
![image](https://github.com/Yooooran/MTDP/assets/103570083/9fb2ed8e-7be0-40dc-9009-e4cd69c1f672)



# Download
- at the [TeraBox](https://terabox.com/s/1247Lj-eVOCGqWNWe5L4Qxw)
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
the same.<br>
For more information, please see chapter 3.3 and 4.1 in our research article.
# Evaluate Models
It is easy to evaluate the performance of trained model, please run evaluate.py, for example:
>if __name__ == "__main__": <br>
&ensp;&ensp; # evaluate_key_points()  # evaluate key point errors <br>
&ensp;&ensp; evaluate_model()  # evaluate model performance
> 
For more information, please see chapter 4.1 in our research article.
# Generate Set-A and Set-B
WARNING!!! Set-A and Set-B are already established, so before you try to generate new Set-A or Set-B, you should save data
in folder "DataSet/source/Set-A" and "DataSet/source/Set-B" to another folder as a separate copy. If you start generation, 
the files in the folders below will be replaced.
---
If you want to try to generate Set-A or Set-B, please run "DataSet/source/DataGenerator.py". The generated data will be
saved in folder "DataSet/source/Set-A" and "DataSet/source/Set-B".<br>
For more information, please see chapter 3.1 and 3.2 in our research article.







