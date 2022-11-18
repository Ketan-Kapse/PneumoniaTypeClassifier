# PneumoniaTypeClassifier
DL classifiers for classifying various types of pneumonia(including COVID-19 induced pneumonia) from unsegmented chest x-ray scans (acquired from the <a href = "https://github.com/ieee8023/covid-chestxray-dataset">Cohen repo</a>.)

## Dependencies

Python >= 3.5
Tensorflow
Keras
numpy
cv2

## Details
This project has two classifier models to classify viral and bacterial pneumonia. Separate classifiers were made after taking into account the sizes of both groups' datasets and their quality. Eg. the bacterial dataset has a significantly higher number of x-rays than the viral dataset and includes more diversity in origin as shown below.

![hierarchy_viral](img/hierarchy-viral.jpg)

![hierarchy_bact](img/hierarchy_bact.jpg)

Taking this into account, it was decided that even a high degree of augmentation on the viral dataset would not solve the problem of bias towards the bacterial group in a single classifier.

## Viral Classifier
Taking into account constraints on the dataset size and it's overall simplicity, a sequential model of stacked Conv2D, Dense, Dropout and MaxPooling were used to form the network.

![viral network](img/viral_network.png)

Inputs were resized to 224 x 224 pixels (in accordance to ImageNet), and augmented with random flips, rotatations, zooms and shears. The network is trained for 10 epochs with a batch size of 10. Train and test sets are split 80:20 keeping in mind the Pareto principle.

![viral train](img/viral_train_acc.png)


Training Accuracy

![viral loss](img/viral_train_loss.png)


Training Loss

![viral roc](img/viral_roc.png)


ROC Curve

![viral gradcam](img/viral_GRADCAM.png)


Grad CAM output


## Bacterial Classifier
The neural net for this classifier is more complex with more dense units per layer.

![bact_network](img/bact_network.png)

![bact_train](img/bact_train_acc.png)

Training Accuracy

![bact_loss](img/bact_train_loss.png)

Training Loss

![bact_roc](img/bact_roc.png)

ROC Curve

![bact_gradcam](img/bact_GRADCAM.png)

## Notes

- Unsegmented images are used as input in both of the classifiers. Segmentation of the input can potentially lead to better classifications and reduce the occurence of wrong outputs on test data. 
- Further fine tuning of the networks for better performance.

