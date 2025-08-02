# Where's My Tabby? - Identifying Mackenzie from Other Tabby Cats Using AI

This project serves as the capstone for the Professional Certificate in Machine Learning and Artificial Intelligence at Imperial College, focusing on a personal interest in pet identification.

## GOALS
This project demonstrates AI's potential to identify individual pets from photos, aiding in reuniting lost cats with owners. High accuracy on tabby cats could extend to an app where users snap street photos to match against a database, notifying owners without costly tracking devices. Scalable to other breeds and pets for broader lost pet recovery applications.

## CONTEXT
The project classifies photos of a specific tabby cat, Mackenzie, against other tabbies using deep learning. We used a binary classifier to address dataset imbalance (fewer Mackenzie photos). Built with PyTorch and ResNet18, it handles real-world variations like angles, lighting, and distances to mimic lost pet scenarios. Challenges include maintaining accuracy on complex tabby patterns and preserving image proportions to avoid distortion.

## DATA
Dataset combines ~164-300 personal high-quality photos of Mackenzie (varied angles, lighting, postures) with ~300 tabby images from Kaggle's datasets. Images are HEIC/JPG, converted to RGB, resized to 224x224 while preserving proportions via center cropping. Split 80/20 for train/test, balanced to 300 per class.

- Other tabby images from Kaggle Cat Breeds Dataset [](https://www.kaggle.com/datasets/ma7555/cat-breeds-dataset), filtered for tabby breeds.
- To balance image quantity, randomly removed images down to 500 files using a Terminal command, then further sampled to 300 for training.
- Mackenzie folder images mostly taken with my cat using an iPhone 16 Pro; aim to take more photos in different lighting and situations in the next few days to balance the data.

Sources:  
- Personal photos of my cat, downloaded or taken with an Apple iPhone 16 Pro 
- [Cat Breeds Dataset](https://www.kaggle.com/datasets/ma7555/cat-breeds-dataset)
Due to the large number of images, I uploaded Mackenzie's photos in a zip file in /images

## MODEL
ResNet18 architecture in PyTorch, fine-tuned for binary classification (Mackenzie vs. Other Tabbies). Pre-trained on ImageNet, with final layer adjusted to 2 classes. Trained with Adam optimizer, CrossEntropyLoss, and data augmentation (random rotations, crops) for robustness. Uses MPS acceleration on Apple Silicon.

## HYPERPARAMETER OPTIMIZATION
Key hyperparameters:  
- Learning rate: 0.001 (Adam optimizer for convergence).  
- Batch size: 32 (balances speed and memory).  
- Epochs: Initially 5-10 (monitored for loss reduction); result wasn't perfect with 5 epochs, sometimes accuracy lower than 90%. Improved after fine-tuning to 10 epochs, reaching 96%.  
- Data augmentation: Random rotations (0-360°), center crops, resizes preserving proportions.  
Optimized empirically; class balance ensured via equal sampling.

## RESULTS
Achieved 96% test accuracy on the balanced dataset (~120 test images) after training for 10 epochs. Confusion matrix shows strong true positives and true negatives, with minimal false positives and false negatives. Visual examples highlight successes (clear Mackenzie patterns) and errors (similar markings, poor angles). Loss dropped from ~0.46 to ~0.10 over 10 epochs, indicating improved learning, though potential overfitting risk remains on small data.

![Confusion Matrix](https://raw.githubusercontent.com/dxunit-sam/wheres-my-tabby/main/cm_10epoch.png)

## CONCLUSIONS
The model delivers strong accuracy (96%) for identifying Mackenzie, validating AI for individual pet recognition. Proportions-preserving preprocessing reduced distortions, boosting performance. While effective as a proof-of-concept, larger datasets and real-world testing are needed to mitigate overfitting and enhance generalization for lost pet applications.

## NEXT STEPS
- **Data Expansion**: Take more Mackenzie photos, balancing the datasets.
- **Model Enhancement**: Optimise current model with hyperparameter tuning, try Optuna, other models such as LeNet5, EfficientNet, etc, for better robustness.

## FUTURE CONSIDERATIONS
- **Deployment**: Build a webapp for photo uploads/matching
- **Portfolio Use**: Highlight as Imperial College capstone, emphasizing practical AI for personal/societal impact.