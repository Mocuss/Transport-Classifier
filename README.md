# Transport-Classifier
Deep Learning Project

## Dataset Link: <br>
https://drive.google.com/drive/folders/1fAlYRPSJg7OYbIgx9S5kU0Az89t9kDG2?usp=drive_link <br>
Please download the link before running the model.

## Dataset: 
7.5k images of 32x32. <br>
3 classes (2.5k images each)- Automobile, Truck and Airplane <br>

## CNN model:
### Data Augmentation:
Using ImageDataGenerator, I added <br>
<ul>
  <li>Rescale-> 1/.255</li>
  <li>Rotation scale->15 degrees</li>
  <li>width_shift_range-> 0.1</li>
  <li>height_shift_range-> 0.1</li>
  <li>horizontal_flip-> True</li>
  <li>Zoom_range->0.1</li>
</ul>
These ensure that my model is not overfitted. I only used 0.1 for the most parts in order to ensure that my model are not underfitted as well. <br>

### Model structure:

The following is my model strcutre. A total of 13 layers was used.
<ul>
  <li>5 Conv2D (64→512 filters)</li>
  <li>5 MaxPooling2D</li>
  <li>1 Flatten</li>
  <li>1 Dropout(0.8) (To reduce overfitting)</li>
  <li>1 Dense(512, Relu)</li>
  <li>1 Dense(3, softmax) ← classifier for 3 classes</li>
</ul>
L2 Regularization of 0.001 was used as well as an overfitting technique. <br>
Activation function of ReLu was used for my hidden layers, and softmax for output layer. <br>
In order to not overfit the data, early stopping with a patience of 5 (looking at Train accuracy) was used. <br>
Optimizer (Adam) with learning rate of 0.001 was used. <br>
I used categorial corss entropy for my Loss function, as this is a classification model for 3 classes. <br>

### Results:
On epoch 46 (Early stopped): <br>
<ul>
<li>loss: 21.75% </li>
<li>val_loss: 24.94% </li>
<li>accuracy: 92.32%</li>
<li>val_accuracy: 90.60%</li>
<li>F1 Score:91%</li>
</ul>

## Transfer Learning Model:
### Data Augmentation:
Using ImageDataGenerator, I added <br>
<ul>
  <li>Rescale-> 1/.255</li>
  <li>Rotation scale->10 degrees</li>
  <li>width_shift_range-> 0.1</li>
  <li>height_shift_range-> 0.1</li>
  <li>horizontal_flip-> True</li>
  <li>Zoom_range->0.1</li>
</ul>
As compared to my CNN model, I decreased the data augmentation for my transfer learning, as it was easy to underfit my model. <br> 

### Model Structure:
Before I did any finetuning, I needed to see which model was best for my dataset. <br>
I ran the models at their most optimal input shape, added 1 layer of global average pooling and dropout layer. <br>
The following are the results for each model: (Do note that this was pre-finedtuned) <br>
<ol>
  <li>
    <b>Mobile Net</b>
  <ul>
    <li>
      Accuracy:0.5840 
    </li>
    <li>
      Val_Accuracy:0.6093
    </li>
    <li>
      Loss:0.8693 
    </li>
    <li>
      Val_Loss: 0.8305 
    </li>
  </ul>
  </li>
  <li>
    <b>VGG</b>
  <ul>
    <li>
      Accuracy:0.7535 
    </li>
    <li>
      Val_Accuracy:0.7740
    </li>
    <li>
      Loss:0.5767 
    </li>
    <li>
      Val_Loss: 0.5354 
    </li>
  </ul>
  </li>
  <li>
    <b>DenseNet121</b>
  <ul>
    <li>
      Accuracy:0.9192 
    </li>
    <li>
      Val_Accuracy:0.8820
    </li>
    <li>
      Loss:0.2130  
    </li>
    <li>
      Val_Loss: 0.2911 
    </li>
  </ul>
  </li>
  <li>
    <b>InceptionV3</b>
  <ul>
    <li>
      Accuracy:0.9043 
    </li>
    <li>
      Val_Accuracy:0.9367
    </li>
    <li>
      Loss:0.2425 
    </li>
    <li>
      Val_Loss: 0.1751 
    </li>
  </ul>
  </li>
</ol>

I used inception for my model. To fine tune the model: I unfroze all the layers except for the first 15. <br>

### Results:
On epoch 20: <br>
<ul>
<li>loss: 0.0207  </li>
<li>val_loss: 0.0902  </li>
<li>accuracy: 0.9935 </li>
<li>val_accuracy: 0.9707</li>
<li>F1 Score:97%</li>
</ul>


