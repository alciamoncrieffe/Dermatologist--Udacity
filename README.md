## Mini Project: Dermatologist AI -- Udacity Project

Deep learning Course Project 2b : As part of a Udacity competition, I designed an algorithm to visually diagnose melanoma, the deadliest form of skin cancer, using CNNs. In particular, to distinguish this malignant skin tumor from two types of benign lesions (nevi and seborrheic keratoses). 

#### Getting Started

1. Clone the repository and create a data/ folder to hold the dataset of skin images.
```
git clone https://github.com/udacity/dermatologist-ai.git
mkdir data; cd data
```
2. Create folders to hold the training, validation, and test images.
```
mkdir train; mkdir valid; mkdir test
```
3. Download and unzip the training data (5.3 GB).
4. Download and unzip the validation data (824.5 MB).
5. Download and unzip the test data (5.1 GB).

Place the training, validation, and test images in the data/ folder, at data/train/, data/valid/, and data/test/, respectively. Each folder should contain three sub-folders (melanoma/, nevus/, seborrheic_keratosis/), each containing representative images from one of the three image classes.

You are free to use any coding environment of your choice to solve this mini project! 
Going forward I would rank the results, using a pipeline that culminates in a CSV file containing the test predictions.

#### Create a Model
The training and validation data will be used to train a model that can distinguish between the three different image classes. (After training, the test images can be used to gauge the performance of your model.)

If you would like to read more about some of the algorithms that were successful in this competition, please read this article that discusses some of the best approaches. A few of the corresponding research papers appear below.

Matsunaga K, Hamada A, Minagawa A, Koga H. “Image Classification of Melanoma, Nevus and Seborrheic Keratosis by Deep Neural Network Ensemble”. International Skin Imaging Collaboration (ISIC) 2017 Challenge at the International Symposium on Biomedical Imaging (ISBI).
Daz IG. “Incorporating the Knowledge of Dermatologists to Convolutional Neural Networks for the Diagnosis of Skin Lesions”. International Skin Imaging Collaboration (ISIC) 2017 Challenge at the International Symposium on Biomedical Imaging (ISBI). (github)
Menegola A, Tavares J, Fornaciali M, Li LT, Avila S, Valle E. “RECOD Titans at ISIC Challenge 2017”. International Skin Imaging Collaboration (ISIC) 2017 Challenge at the International Symposium on Biomedical Imaging (ISBI). (github)
While the original challenge provided additional data (such as the gender and age of the patients), we only provide the image data to you. If you would like to download this additional patient data, you may do so at the competition website.

All three of the above teams increased the number of images in the training set with additional data sources. If you'd like to expand your training set, you are encouraged to begin with the ISIC Archive.

#### Data Loaders
I used the below training data transformations, including a RandomHorizontalFlip and RandomRotation(30), since there is no constant orientation of a melanoma.

                            transforms.RandomRotation(30),
                            transforms.RandomHorizontalFlip(),
                            transforms.Resize(224),
                            transforms.CenterCrop(224),
                            transforms.ToTensor(),
                            transforms.Normalize((0.485, 0.456, 0.406), 
                                                 (0.229, 0.224, 0.225)

#### Latest Model Architecture
As a starting point, I finetuned the existing VGG16 model. Freezing the existing weights, loading the VGG16 model and then replacing the final layer with a new one of 3 classes for our 3 images types.

Just using a funetuned model I achieved a 70% test accuracy. 

#### Next steps would be to replace or retain the other Linear layers and see if we can improve the accuracy
