# Where's My Tabby? - Identifying Mackenzie from Other Tabby Cats Using AI

This project serves as the capstone for the Professional Certificate in Machine Learning and Artificial Intelligence at Imperial College, focusing on a personal interest in pet identification.


## BUSINESS GOALS
This project demonstrates AI's potential to identify individual pets from photos, aiding in reuniting lost cats with owners. High accuracy on tabby cats could extend to an app where users snap street photos to match against a database, notifying owners without costly tracking devices. Scalable to other breeds and pets for broader lost pet recovery applications.

## CONTEXT
The project classifies photos of a specific tabby cat, Mackenzie, against other tabbies using deep learning. We used a binary classifier to address dataset imbalance (fewer Mackenzie photos). Built with PyTorch and ResNet18, it handles real-world variations like angles, lighting, and distances to mimic lost pet scenarios. Challenges include maintaining accuracy on complex tabby patterns and preserving image proportions to avoid distortion.

## DATA
Dataset combines ~164-300 personal high-quality photos of Mackenzie (varied angles, lighting, postures) with ~300 tabby images from Kaggle's Oxford-IIIT Pet Dataset (Abyssinian, Bengal, Egyptian Mau breeds) and Cats Dataset. Images are HEIC/JPG, converted to RGB, resized to 224x224 while preserving proportions via center cropping. Split 80/20 for train/test, balanced to 300 per class.

Sources:  
- Personal photos of my cat, downloaded or taken with an Apple iphone 16 pro
- [Oxford-IIIT Pet Dataset](https://www.kaggle.com/datasets/zippyz/cats-and-dogs-breeds-classification-oxford-dataset)  
- [Cats Dataset](https://www.kaggle.com/datasets/crawford/cat-dataset)


## MODEL
ResNet18 architecture in PyTorch, fine-tuned for binary classification (Mackenzie vs. Other Tabbies). Pre-trained on ImageNet, with final layer adjusted to 2 classes. Trained with Adam optimizer, CrossEntropyLoss, and data augmentation (random rotations, crops) for robustness. Uses MPS acceleration on Apple Silicon.

## HYPERPARAMETER OPTIMIZATION
Key hyperparameters:  
- Learning rate: 0.001 (Adam optimizer for convergence).  
- Batch size: 32 (balances speed and memory).  
- Epochs: 5-10 (monitored for loss reduction).  
- Data augmentation: Random rotations (0-360°), center crops, resizes preserving proportions.  
Optimized empirically; class balance ensured via equal sampling.

## RESULTS
Achieved 91.4% test accuracy on balanced dataset (~120 test images). Confusion matrix shows strong TP/TN, few FP/FN. Visual examples highlight successes (clear patterns) and errors (similar markings, poor angles). Loss dropped from ~0.46 to ~0.10 over 5 epochs, indicating good learning but potential overfitting risk on small data.

## CONCLUSIONS
The model delivers solid accuracy for identifying Mackenzie, validating AI for individual pet recognition. Proportions-preserving preprocessing reduced distortions, boosting performance. While effective as proof-of-concept, larger datasets and real-world testing are needed to mitigate overfitting and enhance generalization for lost pet applications.

## ACTIONABLE INSIGHTS
- **Data Expansion**: Collect 500+ Mackenzie photos and diverse tabbies; extend to other breeds/pets.  
- **Model Enhancement**: Test deeper architectures (e.g., EfficientNet) or ensemble methods for better robustness.  
- **Deployment**: Build a mobile app for photo uploads/matching; integrate with lost pet platforms like Petco Love Lost.  
- **Portfolio Use**: Highlight as Imperial College capstone, emphasizing practical AI for personal/societal impact.
