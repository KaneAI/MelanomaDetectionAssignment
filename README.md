# Melanoma Detection Assignment
> This is project is part of an assignment given for my MSc in Artificial Intelligence and Machine Learning with Upgrad and Liverpool John Moores University. 

# Problem Statement

To build a CNN based model which can accurately detect melanoma. Melanoma is a type of cancer that can be deadly if not detected early. It accounts for 75% of skin cancer deaths. A solution which can evaluate images and alert the dermatologists about the type of melanoma present has the potential to reduce a lot of manual effort needed in diagnosis.

The dataset consists of 2239 images of benign oncological diseases in folders who's name represents their type. These were formed from the International Skin Imaging Collaboration (ISIC).

## Table of Contents
* [Approach](#approach)
* [Conclusions](#conclusions)
* [Technologies Used](#technologies-used)
* [Method](#method)
* [Contact](#contact)

<!-- You can include any other section that is pertinent to your problem -->

## Approach
As part of the assessment several aspects of the approach were dictated by the evaluation rubric.  The assessment required me to build several convoluted Neural Networks (CNNs) using predefined techniques.

I decided that I would aim to build a simple sequential CNN with less than 1 million trainable parameters. The idea being that a model with fewer parameters would result in a more general model which will perform better on unseen data. 

I conducted some research on melanomas and how they are traditionally detected.  I found that there are 5 key attributes used when assessing lesions to decide if they are melanomas.  These are:

>|   | Attribute | Description              |
>|---|-----------|--------------------------|
>| A | Asymmetry | Not symetrical in shape  |
>| B | Border    | Uneven borders           | 
>| C | Colour    | Multiple colours         |
>| D | Diameter  | Larger than 1/4"         |
>| E | Evolution | Changes over time        |

My initial thoughts where: 
- We can not check diameter or evolution as the data is not available to do so.
- I could potentially check for Asymmetry by using two identical models prefixed with reflection or rotation transformations and then fusing the models together once flattened in to a dense layer. I have not attempted this and it goes beyond the scope of this assessment. 
- To check fo an uneven border I would need to have kernels who's input is impacted by a reasonably large region of the original image.  This could be achieved by either using large kernels, or multiple feature layers using smaller kernels.  As I want to reduce the number of parameters I opted for a deeper network using smaller kernels. 
- As we are using multiple feature layers, the number of layers after each layer will need to increase.  This is to account for the number of possible combinations of the features identified at the previous layer. 
- In order to keep the number of parameters down, a bottleneck layer can be added with a smaller number of kernels and kernel size if 1*1.  This will then reduce the number of parameters required for the flattened dense layer.
- If we are looking for an uneven border we should not use any augmentation techniques that change the shape e.g. Skew.  We should also avoid blur transformations as they may mask small irregularities. Sharpening the images may help.
- If we are looking at the colour we should not introduce any augmentation techniques that alter the colours such as adjusting contrast or saturation 


## Conclusions
- The low number of sample images in the dataset meant that simple CNNs overfit the data quite quickly.
- Using augmentation techniques to transform the images within each epoch during training and also using dropout layers reduced overfitting but the resulting model could only achieve ~50% accuracy.
- After investigation it was found that a class imbalance was contributing to poor performance
- After using the Augmentor library to generate additional source images I was able to train a model capable of ~85% accuracy.
- I believe I could increase the accuracy further by increasing the size of the first dense layer. This would however make the model more complex (which I'm tryinmg to avoid)
- I may also be able to improve the performance by tuning the hyper parameters or by introducing a dynamic learning rate. 

## Method
The source code was written in Visual Studio Code and executed on a Lenovo legion 5 laptop with a NVIDIA GeForce RTX 3070 Laptop GPU.  I also ran earlier versions of the model using Google collab but found the performance to be slower. 

## Technologies Used
- Augmentor - version 0.2.12
- Keras - version 2.13.1
- Matplotlib - version 3.7.1
- Numpy - version 1.23.5 
- nvidia-cudnn-cu11  - version 8.6.0.163
- nvidia-cublas-cu11  - version 11.11.3.6
- pandas - version 2.0.2
- python - version 3.9.16
- tensorflow - version 2.13.0

## Contact
Created by [@KaneAI] - feel free to contact me!


<!-- Optional -->
<!-- ## License -->
<!-- This project is open source and available under the [... License](). -->

<!-- You don't have to include all sections - just the one's relevant to your project -->