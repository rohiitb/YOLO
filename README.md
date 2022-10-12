# You Only Look Once (YOLO): Pytorch Lightning Implementation

This project involves the implementation of the object detection algorithm Yolo defined in the paper: [YOLO](https://arxiv.org/pdf/1506.02640.pdf). YOLO considers the object detection problem as regression problem and uses a single neural network to predict bounding boxes and class probabilities directly from full images in one evaluation.

## Network Architecture 
<img src="./Result snaps/Yolo_architecture.JPG" align = "center">


## Network Architecture Table
<img src="./Result snaps/yolo_table.JPG" align = "center">


## Results
<!-- ![](./Results/1.png)     ![](./Results/1_mask.png)
![](./Results/2.png)     ![](./Results/2_mask.png)
![](./Results/3.png)     ![](./Results/3_mask.png) -->


<table>
  <tr>
      <td align = "center"> <img src="./Result snaps/Raw_image.JPG"> </td>
      <td align = "center"> <img src="./Result snaps/Prediction_image.JPG"> </td>
      <td align = "center"> <img src="./Result snaps/NMS_prediction.JPG"> </td>
  </tr>
  <tr>
      <td align = "center"> Raw labels from the dataset</td>
      <td align = "center"> Predictions from the model </td>
      <td align = "center"> Boxes after non-max suppression </td>
  </tr>
</table>

<table>
  <tr>
      <td align = "center"> <img src="./Result snaps/Training_loss.JPG"> </td>
      <td align = "center"> <img src="./Result snaps/Validation_loss.JPG"> </td>
  </tr>
  <tr>
      <td align = "center"> Training Loss curve </td>
      <td align = "center"> Validation Loss curve </td>
  </tr>
</table>

<table>
  <tr>
      <td align = "center"> <img src="./Result snaps/Training_loss.JPG"> </td>
      <td align = "center"> <img src="./Result snaps/MAP_over_training.JPG"> </td>
  </tr>
  <tr>
      <td align = "center"> Precision-Recall curves </td>
      <td align = "center"> Mean Average Precision over training epochs</td>
  </tr>
</table>

## Issues faced
One major issue I faced while implementing this project was to get the model to detect traffic lights.The dataset is imbalanced with 37000 instances of cars, 16000 instances of pedestrians and only 2800 instances of traffic lights. On top of that, the bounding boxes for traffic lights are quite small in dataset.

Thus, in the initial stages it is hard for the predicted boxes to have high IoU with the ground truth boxes. The confidence loss aims to reduce the gap between the predicted confidence and IoU.

Ideally, this should be fixed by the localization optimization as the network trains on. But in this case, the dataset for traffic lights is quite small so the network localization optimization may not be getting enough training instances to correct the localization to an extent where
the IoU is greater than the threshold. 

The failure of network to detect traffic lights is also shown by the average precision values of the 3 classes:
1. Pedestrian: 0.289
2. Traffic light: 0.034
3. Car: 0.533

The network works much better when the rather than using IoU, a target of 1 is used in confidence loss. The precision values for this case are:
1. Pedestrian: 0.389
2. Traffic light: 0.438
3. Car: 0.558
