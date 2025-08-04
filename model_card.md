# Model Card for "Where's My Tabby?"

## Model Details
- **Basic Information**: CNN model using ResNet18 to identify Mackenzie (tabby cat) from other tabbies. Created by dxunit-sam for Imperial College AI capstone, August 2025.
- **Compute Infrastructure**: Mac Studio with MPS acceleration; PyTorch 2.0+.
- **Hyperparameters**: Learning rate 0.001, batch size 32, 10 epochs, Adam optimizer.

## Model Description
- **Input**: The model accepts RGB images of cats, preprocessed to 224x224 pixels. Inputs include personal photos of Mackenzie and other tabby cats from Kaggle datasets, capturing varied lighting, angles, and postures to mimic real-world lost pet scenarios.
- **Output**: The model outputs a binary classification: 1 for Mackenzie (your_cat) and 0 for other tabbies (other_cat), with a probability score indicating confidence (threshold at 0.5).
- **Model Architecture**: Utilizes ResNet18, a deep convolutional neural network with 18 layers, pre-trained on ImageNet. It features residual connections for deeper learning, including an initial 7x7 convolution, four residual blocks (64, 64, 128, 256, 512 filters), average pooling, and a custom fully connected layer adjusted to 2 classes for binary classification. Trained with MPS acceleration on Apple Silicon.

## Intended Use
- **Primary Intended Uses**: Proof-of-concept for pet identification from photos; aids lost cat recovery in future.
- **Primary Intended Users**: Pet lovers, eager to contribute to the development.

## Out-of-Scope Uses
- Relying on this model in real life, which this model is still in proof of concept stage. Or any commercial usage.

## Factors
- **Relevant Factors**: Cat breed (tabby focus); image quality, lighting, angles.
- **Evaluation Factors**: Tested on balanced tabby dataset; may vary for non-tabby breeds.

## Metrics
- **Model Performance Measures**: Accuracy (96%), precision, recall via confusion matrix.
- **Decision Thresholds**: Binary classification; default 0.5 probability.
- **Variation Approaches**: Tested with data augmentation; accuracy drops to <90% with fewer epochs.

## Ethical Considerations
- **Sensitive Data**: No sensitive data; personal cat photos are non-confidential.
- **Human Life**: Not applicable.
- **Mitigations**: Balanced dataset to reduce bias; proportion-preserving preprocessing.
- **Risks and Harms**: Misidentification could delay pet recovery; overfitting on small data.
- **Use Cases**: Avoid in diverse breed scenarios without retraining.

## Evaluation Data
- **Datasets**: ~100+ Mackenzie photos (personal), 500 other tabbies from Kaggle (Cats Breeds Dataset https://www.kaggle.com/datasets/ma7555/cat-breeds-dataset).
- **Motivation**: Real-world simulation of lost pet photos.
- **Preprocessing**: RGB conversion, 224x224 resize with center crop.

## Training Data
- Same as evaluation data; 80/20 split.

## Quantitative Analyses
- Accuracy: 96% on test set.
- Confusion Matrix: Strong TP/TN; minimal FP/FN (see cm_10epoch.png).

## Limitations and Caveats
- Limited to tabbies; expand data for other breeds. Test in real-world conditions to address overfitting.

## Trade-offs
- Not yet observable, but expect to hit more challenge when training with solid colour cat or other pets, or with less pattern to trace.