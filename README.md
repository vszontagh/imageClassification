### Pneumonia imageClassification with CNNs
< img src = '/images/africa.png' \>

### Business Problem
Pneumonia is an infectious disease that causing inflammation in the lungs. It kills more children than any other infectious disease. Every year it claims the live of more then 700,000 children under the age of five globally. These deaths would be preventable with early diagnostic and treatment.

### Stakeholder
The Doctors Without Borders, who are currently have a mission in Central and West Africa, where according to the UNICEF’s 2019 statistics, the mortality rate for this infection for 5 years old and younger was between 21-24%. They would like to get help in their effort to speed up X-Ray evaluation and detect pneumonia so they can start early treatment to save these lives. Just for comparison this rate in the developed countries runs between 1 - 5%.

### Data
I used a Kaggle dataset for Pneumonia, which contains 5856 images in 3 folders: train, validation and test. The original dataset had more then 89% of the images in the train set, 10 % in the test and only 0.3% in the validation, so I  moved some of the images from the train folder to the test and validation using shutil, to get 70-20-10% split between the 3 folders.
The dataset is imbalance, this I will address this later on with augmentation, to create more images, which are also modified to some degree  so they seem to be "new" images for the computer. This will take care of the imbalance problem.

### Modeling
I will use recall score as my main evaluation metrics, as it is more costly to misclassify someone that they have no pneumonia when they are. Besides this score I will also monitor the model's accuracy.


### Final Model
Best Model
Model1
* `Test Recall: `  86.14%
* `Test Accuracy: ` 96.27%

This model only has 1 convolution layer with L2 regularization, BatchNormalization and two dense layers. It has high accuracy and high recall scores, which indicates that the model can correctly identify whether a patient has pneumonia or not.

## Conclusions
This model has high accuracy and high recall scores, which indicates that the model can correctly identify wheather a patient has pneumonia or not after checking the X-Ray images.
With this model any organization would cut down on time spent evaluating these images, it would also speed up the process of diagnostic, which would lead more availably doctors for the patients and after diagnosis they could start early treatment. Which would directly lead to more pediatric patient recovering from this infection and this also decreases the mortality rate.
