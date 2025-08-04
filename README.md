# Where's My Tabby? - Identifying Mackenzie from Other Tabby Cats Using AI
 
This is a portolio project for the Professional Certificate in Machine Learning and Artificial Intelligence at Imperial College, focusing on a personal interest in pet identification. 

## GOALS
This project demonstrates AI's potential to identify individual pets from photos, aiding in reuniting lost cats with owners. High accuracy on tabby cats could extend to an app where users snap street photos to match against a database, notifying owners without costly tracking devices. Scalable to other breeds and pets for broader lost pet recovery applications.

## CONTEXT
The project classifies photos of a specific tabby cat, Mackenzie, against other tabbies using deep learning. We used a binary classifier to address dataset imbalance (fewer Mackenzie photos). Built with PyTorch and ResNet18, it handles real-world variations like angles, lighting, and distances to mimic lost pet scenarios. Challenges include maintaining accuracy on complex tabby patterns and preserving image proportions to avoid distortion.

## DATA
Dataset combines ~200+ personal high-quality photos of Mackenzie (varied angles, lighting, postures) with ~300 tabby images from Kaggle's datasets. Images are HEIC/JPG, converted to RGB, resized to 224x224 or 300x300 while preserving proportions via center cropping. Split 80/20 for train/test, balanced to 300 per class.
Images for training are randomly rotated by 0-360 degrees, center-cropped to a square based on the shorter side (preserving proportions), and resized to 224x224 using Lanczos resampling for high-quality output. This augmentation enhances model robustness to real-world variations like orientation and

- Other tabby images from Kaggle Cat Breeds Dataset , filtered for tabby breeds.
To balance image quantity, randomly removed images down to 500 files using a Terminal command, then further sampled to 300 for training.
- Mackenzie folder images mostly taken with my cat using an iPhone 16 Pro; aim to take more photos in different lighting and situations in the next few days to balance the data.

Sources:
- Personal photos of my cat, downloaded or taken with an Apple iPhone 16 Pro. I uploaded Mackenzie's photos in a zip file in /images
Cat Breeds Dataset - Download from Kaggle [Cat Breeds Dataset](https://www.kaggle.com/datasets/ma7555/cat-breeds-dataset)


## MODELS USED
ResNet architecture in PyTorch, fine-tuned for binary classification (Mackenzie vs. Other Tabbies). Pre-trained on ImageNet, with final layer adjusted to 2 classes. Trained with Adam optimizer, CrossEntropyLoss, and data augmentation (random rotations, crops) for robustness. Uses MPS acceleration on Apple Silicon.

EfficientNet family of models in PyTorch, optimized for efficiency and accuracy through compound scaling of depth, width, and resolution. Variants B0 and B7 used, pre-trained on ImageNet, EfficientNet-B0 provided a lightweight baseline, while B7's larger architecture maximized feature extraction for tabby patterns, achieving 96.49% accuracy after Optuna hyperparameter tuning. Both variants were fine-tuned for binary classification, leveraging MPS for fast training on the ~500-image dataset.


## HYPERPARAMETER OPTIMIZATION
Key hyperparameters: (TO-DO)
- ✅ Epochs: Initially 5-10 (monitored for loss reduction); result wasn't perfect with 5 epochs using ResNet18, sometimes accuracy lower than 90%. Improved after fine-tuning to 10 epochs, reaching 96%.
- ✅ Testing other model EfficientNet B1 and B7, 8 epochs 0.0005 learning rate after fine tuning with minimising loss, reaching 98%+ accuracy.
- ✅ Improved image size from 224x224 to 300x300, while 600x600 is too large and too slow to train
- ✅ Batch size: 32 (balances speed and memory).
- ✅ Use Optuna to fine tune hyperparameters, including learning rate and weight decay


## RESULTS

### First Trial with a Modern Model - ResNet
The initial trial utilized the ResNet18 model, a modern convolutional neural network, trained for 10 epochs to replace the older LeNet5 architecture. This experiment marked the project's entry into using contemporary models, achieving a test accuracy of 70.30% on the balanced dataset (~120 test images). The confusion matrix highlights early successes and challenges, with moderate true positives and true negatives, and noticeable false positives and negatives, reflecting the learning curve on the small dataset.

![Confusion Matrix](https://raw.githubusercontent.com/dxunit-sam/wheres-my-tabby/main/cm_resnet18.png)

### Trial with Another Model - EfficientNet B0
The second trial explored the EfficientNet-B0 model, trained for 7 epochs, to assess its potential as a promising alternative. This effort yielded a test accuracy of 92.08%, a significant improvement over ResNet18, demonstrating the model's efficiency in handling the dataset's tabby patterns. The confusion matrix reflects stronger true positives and true negatives, with reduced misclassifications, indicating better feature extraction and robustness.

![Confusion Matrix](https://raw.githubusercontent.com/dxunit-sam/wheres-my-tabby/main/cm_efficientnetb0.png)

### Trial with an Enhanced Variant - EfficientNet B7
The third trial advanced to the EfficientNet-B7 model, trained for 8 epochs with an image size of 300 and a learning rate of 0.0005. This iteration achieved a test accuracy of 96.04%, showcasing a substantial leap in performance. The confusion matrix reveals a marked increase in true positives and true negatives, with minimal false positives and negatives, highlighting the model's enhanced capability to discern Mackenzie from other tabbies, though potential overfitting risks persist due to the dataset size.

![Confusion Matrix](https://raw.githubusercontent.com/dxunit-sam/wheres-my-tabby/main/cm_efficientnetb7.png)

### Final Trial (EfficientNet-B7 Model with Optuna)
The final trial optimized the EfficientNet-B7 model through hyperparameter tuning with Optuna, significantly elevating performance. Trained with an optimized learning rate of 0.00017494927607842746 and weight decay of 0.0003795468539615388 over 10 epochs, the model achieved a test accuracy of 96.49%. This refinement reduced the training loss from 0.536 to 0.014, demonstrating robust learning despite minor fluctuations, likely due to the small dataset. The updated confusion matrix and sample visualizations underscore this enhanced capability, showcasing fewer misclassifications and improved alignment with real-world lost pet identification scenarios. The optimized model, saved as `wheresmytabby_efficientnetb7_optuna.pth`, effectively leverages EfficientNet-B7's advanced architecture to capture the nuances of tabby patterns and other distinguishing features, marking a successful conclusion to the model development phase.

![Confusion Matrix](https://raw.githubusercontent.com/dxunit-sam/wheres-my-tabby/main/cm_efficientnetb7_optuna.png)
![Result with Samples](https://raw.githubusercontent.com/dxunit-sam/wheres-my-tabby/main/samples_efficientnetb7_optuna.png)



## CONCLUSIONS
The model delivers strong accuracy (96%+) for identifying Mackenzie, validating AI for individual pet recognition. Proportions-preserving preprocessing reduced distortions, boosting performance.
With the high percentage after optimisation, it is possible to use AI to identify individual tabby cat from other cats by it's features.

While effective as a proof-of-concept, larger datasets and real-world testing are needed to mitigate overfitting and enhance generalization for lost pet applications. Such as training with other breeds and potentially other pets.


## FUTURE CONSIDERATIONS BEFORE PRACTICAL USE
- **Generalisation**: Train on diverse breeds (e.g., solid black/white cats via Oxford-IIIT dataset); use nose prints or facial geometry for low-pattern cases.
- **Test with other cats and breed of cats**: With other cat owners permission, setup the folders to host images, label, and CNN output for another cat.
- **Deployment**: Build a webapp for photo uploads/matching, host on AWS. Helping all the beloved cats in the UK to have a chance to get back to their loving owners. Explore potential to fuel by love and donations.
- **Other kind of pets**: Further in future, evaluate possibility to apply the model to other pets like dogs


## HOW TO USE

### Basic Environment Setup
- **Python Environment**:
  - **Windows, Mac, Linux**: Install Python (3.13.3 was used in development)
- **Install Necessary Libraries**:
 - Run the following in the terminal: pip install numpy matplotlib scikit-learn pillow pillow_heif torch torchvision seaborn

- **Git Clone or Download the Repo**:
 - Clone the repository:
 - git clone https://github.com/dxunit-sam/wheres-my-tabby.git
 - cd wheres-my-tabby
 - Or download the ZIP file from GitHub and extract it.

- **Prepare Data**
 - Create Folder Structure:
 - Create a folder named images in the project directory.
 - Inside images, create a subfolder named after your cat (e.g., images/(your cat's name)). Or use Mackenzie photos (zipped) in images folder
 - Create another subfolder images/othertabby.

- **Train and Test Model**
 - Open Jupyter Notebook:
 - Install Jupyter Lab if needed: pip install jupyterlab.
 - Launch Jupyter Lab: jupyter lab.
 - Open the notebook wheresmytabby.ipynb in the browser.

- **Update Folder Names**:
 - In the notebook, update the folder variables as needed:
 - pythonyour_cat_folder = "(your cat's name)"
 - other_cat_folder = "othertabby"

- **Run the Python Code**:
 - Execute all cells in the notebook to load data, preprocess images, train the model, and observe results (e.g., 96% accuracy, confusion matrix).


## CONTACT ME
- **For questions, suggestions, or collaboration on extending this project (e.g., adding more breeds), feel free to reach out**:
 - Email: samson@dxunit.com
 - GitHub: dxunit-sam