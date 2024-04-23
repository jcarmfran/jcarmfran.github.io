# Leveraging Deep Learning for Pneumonia Detection in Pediatric Chest X-Rays: A Deep Dive
### This is my personal project

**Project Overview**

As an aspiring data scientist, I embarked on a challenging yet rewarding project that involved developing a deep learning model capable of analyzing chest X-ray images to detect signs of pneumonia in children. This blog post outlines the end-to-end process of this project. From dataset analysis to model deployment, this project will culminate to a fully functional, cloud hosted web app. 


**Data Understanding**

The project's cornerstone is a dataset of 5,856 pediatric chest X-ray images, generously provided by researchers from the University of California, San Diego. The dataset is available via [this link](https://data.mendeley.com/datasets/rscbjbr9sj/2). The dataset is divided into training and test subsets, with each image labeled to indicate the presence or absence of pneumonia.


**Model Development Process** 

With the dataset as our training input, three distinctive models will be developed, tested, and assessed for their accuracy in detecting potential signs of pneumonia. The most successful model will be used to further develop a fully functional, Azure deployed web app where users can upload chest X-rays to assess if there are signs of pneumonia present.

The three models will be a simple Convolution Neural Network, VGG16, and ResNet50v2.
Relevant resources
[Keras Applications](https://keras.io/api/applications/#usage-examples-for-image-classification-models) 

1. **The CNN Model**: The first model was a somewhat complex Convolutional Neural Network (CNN), designed to learn patterns directly from the chest X-ray images. It consisted of convolutional layers that could capture the intricate patterns in X-ray images, which are indicative of pneumonia. 

    The implementation begins with data augmentation layers that introduce variability into the training dataset, enhancing the model's ability to generalize from the data. At random, a set number of images will either be [zoomed in/out](https://www.tensorflow.org/api_docs/python/tf/keras/layers/RandomZoom) or [rotated](https://www.tensorflow.org/api_docs/python/tf/keras/layers/RandomRotation).

    Subsequent convolutional layers (`layers.Conv2d`), designed with a stride of two, reduce dimensionality while capturing spatial hierarchies. 
    
    Pooling layers further condense the feature maps, leading to a flattened layer that transitions to a series of dense layers. These dense layers culminate in a binary classification output. The model employs dropout regularization to mitigate overfitting and an early stopping callback to prevent unnecessary computations if the validation loss does not improve, ensuring efficient training. The optimizer and loss function are carefully chosen to steer the learning process.

    Though the model is not able to achieve accuracies scores north of 74.4% and 76.3% for training and validation datasets, respectively, those are comparably much better results than what we would expect by simple random chance.

2. **VGG16**: The model was pre-trained on ImageNet and fine-tuned with additional layers and augmentation techniques similar to the CNN implementation as before. Notably, at just 10 epochs, we were able to achieve training and validation accuracies that both peaked at just over 94.0%! This model's robustness shows great potential for early detection of pneumonia in clinical settings. These results suggest that VGG16, with appropriate modifications, can be a valuable tool in medical imaging analysis.

3. **The Transfer Learning Model with ResNet50v2**: The second model leverages the power of transfer learning, a technique where a pre-trained model is fine-tuned to a specific task. TensorFlow offers many pretrained models, but ResNet50v2 was chosen thanks to its renowned performance in image recognition tasks. This approach allowed to leverage the model's pre-trained weights, which had been learned from a vast array of images, and adapt them to the specific task of pneumonia detection. 

**Splitting the Dataset**
Before we can move forward with model training, we'll seperate the dataset into three: training, validation, test.

Splitting the dataset into training, validation, and test sets is crucial for evaluating the model’s performance accurately. The training set is used to fit the model, the validation set is for tuning model parameters and preventing overfitting, and the test set serves as an unbiased evaluation of the final model to assess its generalization to new data.

**Exploratory Data Analysis**
It seems nearly impossible to discern from the following images which is the patient suffering from pneumonia, and which isn't.

![image one](./assets/img/xrays/xray_normal.png) ![image one](./assets/img/xrays/xray_pneumonia.png)

**Model Training and Evaluation** 

Both models underwent rigorous training using the provided dataset. The simple CNN model served as a baseline, while the ResNet50v2 model, with its sophisticated architecture, promised enhanced accuracy. After training, the models were evaluated on the test dataset to assess their predictive capabilities. 

**Deployment and Implementation** 

Upon comparison, the ResNet50v2 model emerged as the superior performer, exhibiting higher accuracy and precision. The decision was made to deploy this model into a web application hosted on Azure. The web app, developed using Flask, offers a user-friendly interface where individuals can upload chest X-ray images and receive an immediate analysis indicating potential signs of pneumonia. 

**Conclusion** 

This project exemplifies the power of ML and AI in healthcare and the potential for meaningful contributions to medical diagnostics from open-source communities. By harnessing the capabilities of deep learning models, we’ve created a tool that could potentially aid in the early detection of pneumonia, ultimately saving lives. 

For those interested in exploring the technical intricacies of the models or replicating the project, the dataset and TensorFlow documentation provide valuable resources to commence this journey into AI-driven healthcare solutions.  

I invite anyone willing to build on the work done so far to contribute to the code repository [(link to the source repo can be found here)](https://github.com/jcarmfran/Pneumonia-Detection). I'm open to any and all feedback! Feel free to share your thoughts or advice on the work done so far in the comment section down below.

*Disclaimer: The web application is intended for educational purposes and should not replace professional medical advice, diagnosis, or treatment.* 