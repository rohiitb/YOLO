# You Only Look Once (YOLO): Pytorch Lightning Implementation

This project involves the implementation of the object detection algorithm Yolo defined in the paper: [YOLO](https://arxiv.org/pdf/1506.02640.pdf). YOLO considers the object detection problem as regression problem and uses a single neural network to predict bounding boxes and class probabilities directly from full images in one evaluation.

## Network Architecture 
<img src="./Result snaps/Yolo_architecture.JPG" align = "center">


## Network Architecture Table
<img src="./Result snaps/yolo_table.JPG" align = "center">


## Results

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

<table class="center">
  <tr>
      <td align = "center"> <img src="./Result snaps/MAP_over_training.JPG"> </td>
  </tr>
  <tr>
      <td align = "center"> Mean Average Precision over training epochs</td>
  </tr>
</table>

## Challenges faced
Some issues that I faced while implementing this project was to get the model to detect traffic lights.The dataset is imbalanced with 37000 instances of cars, 16000 instances of pedestrians and only 2800 instances of traffic lights. Furthermore, the bounding boxes for traffic lights are quite small in dataset.

Thus, in the initial stages it is hard for the predicted boxes to have high IoU with the ground truth boxes. The confidence loss aims to reduce the gap between the predicted confidence and IoU.

Ideally, this should be fixed by the localization optimization as the network trains on. But in this case, the dataset for traffic lights is quite small so the network localization optimization may not be getting enough training instances to correct the localization to an extent where the IoU is greater than the threshold. 
The model trains better if we use 1 instead of IoU in the loss function during training.

<b>MAP acheived over training : 0.43</b>
