### Pneumonia imageClassification with CNNs

<img width=700 height=350 src='/images/africa.png'>

### Business Problem
Pneumonia is an infectious disease that causing inflammation in the lungs. It kills more children than any other infectious disease. Every year it claims the live of more then 700,000 children under the age of five globally. These deaths would be preventable with early diagnostic and treatment.

### Stakeholder
The Doctors Without Borders, who are currently have a mission in Central and West Africa, where according to the UNICEF’s 2019 statistics, the mortality rate for this infection for 5 years old and younger was between 21-24%. They would like to get help in their effort to speed up X-Ray evaluation and detect pneumonia so they can start early treatment to save these lives. Just for comparison this rate in the developed countries runs between 1 - 5%.

### Data
I used a Kaggle dataset for Pneumonia, which contains 5856 images in 3 folders: train, validation and test. The original dataset had more then 89% of the images in the train set, 10 % in the test and only 0.3% in the validation, so I  moved some of the images from the train folder to the test and validation using shutil, to get 70-20-10% split between the 3 folders.
The dataset is imbalance, this I will address this later on with augmentation, to create more images, which are also modified to some degree  so they seem to be "new" images for the computer. This will take care of the imbalance problem.

### Modeling
I will use recall score as my main evaluation metrics, as it is more costly to misclassify someone that they have no pneumonia when they are. Besides this score I will also monitor the model's accuracy.

#### Baseline Model
<img src='/images/recall>'
<img src='/images/accuracy'>

The first neural networks model is doing pretty well, with high recall score for validation (97.44%) and for the test (88.66%). This is a good result, and it shows that the neural networks model is able to learn from data and generalize well. The high recall score for the validation set suggests that the model is correctly classifying most of the examples in the validation set.
The validation score and the training score were very high. The loss also decreasing, however the validation loss starts to separate and increase, this might be an indication that the model is overfitting. To stop the model from overfitting I will try to apply regularization in the next model with more Conv2D layer.

In case the training loss is not decreasing or going weird, it would be time to potentially consider a larger neural network or to make a more sophisticated neural network model. Thankfully this is not the case for my model. As I mentioned earlier the increase in validation loss might be an indicator for overfitting, so I will try to apply the following methods which can help with this: apply regularization, introduce early stopping, hyperparameter tuning, and last but not least increasing the increasing and modifying the images we already have in the training data with some data augmentation.

#### Model2
I applied an L2 regularization of  `l2(1e-6)`.
The training recall and the validation recall still not converging. There are still an oscillation in both. The validation recall is 93.94% , and the test is 87,78%.
As a next step I will change the L2 regularization and add early stopping to the model.
I will try to run it with a larger epoch size (200) and change the L2 regularization to control the models complexity, thus prevent it from overfitting. In addition I will also apply early stopping with a patience of 10 on the validation loss.

#### Model3
The early stopping with a patience of 10 did stop the model after the 22nd epochs.
The test recall is 86.27% and the validation is 91,14%. Which is still good. The loss starts to separate and increase over 10 epochs. In general you want to see the loss decreasing steadily and the accuracy increasing for both the train and validation.

To increase the dataset and to prevent overfitting besides handling the data imbalance, I will try data augmentation. With small transformations such as rotating the images we can increase the number of images in our dataset.

#### Data Augmentation
Data Augmentation allows to add more data to the training set, similar to the data we just had but it is reasonably modified to some degrees so it’s not exactly the same. I used the following data augmentation arguments:
- rescaling the images after transformation
- rotation_range: rotating images by 40 degrees
- width_shift_range: shifting images horizontally (by 0.2 of total width)
- height_shift_range: shifting images vertically(by 0.2 of total height)
- shear_range: shear angle by 30 degrees
- zoom_range: zoom images by 20%
- horizontal_flip: flip images horizontally

Model4
In addition to the  augmented dataset and regularization I also added, padding = 'same' to the model, so it will apply i t to each image and create a border around them.  
This model does not perform that well. There is a fluctuation in the  recall. The validation score is 94.81% and the test score is 86.02% . The loss is approaching zero after 20 epochs. The early stopping stop the model at 36 epochs.

### Final Model
Best Model
Model1
* `Test Recall: `  86.14%
* `Test Accuracy: ` 96.27%

This model only has 1 convolution layer with L2 regularization, BatchNormalization and two dense layers. It has high accuracy and high recall scores, which indicates that the model can correctly identify whether a patient has pneumonia or not.

## Conclusions
This model has high accuracy and high recall scores, which indicates that the model can correctly identify whether a patient has pneumonia or not after checking the X-Ray images.
With this model any organization would cut down on time spent evaluating these images, it would also speed up the process of diagnostic, which would lead more availably doctors for the patients and after diagnosis they could start early treatment. Which would directly lead to more pediatric patient recovering from this infection and this also decreases the mortality rate.
