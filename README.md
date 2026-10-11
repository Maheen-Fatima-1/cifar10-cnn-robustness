# cifar10-cnn-robustness
CIFAR-10 image classification using CNNs, data augmentation, and robustness evaluation on shifted test images.
# CIFAR-10 CNN Robustness

## Overview

This project implements a Convolutional Neural Network (CNN) for image classification on the CIFAR-10 dataset. It studies how different data augmentation techniques affect classification accuracy on clean and shifted test images.

The experiments compare different configurations, including no augmentation, geometric augmentation, photometric augmentation, Cutout/Random Erasing, and Mixup/CutMix with label smoothing.

## Objectives

- Train a CNN to classify the 10 CIFAR-10 classes.
- Compare different data augmentation configurations.
- Evaluate performance on clean and shifted test images.
- Study the effect of image occlusion on model robustness.
- Perform error analysis using class-wise accuracy and a normalized confusion matrix.

## Dataset

The project uses the CIFAR-10 dataset, which contains 10 classes:

- Airplane
- Automobile
- Bird
- Cat
- Deer
- Dog
- Frog
- Horse
- Ship
- Truck

Images have a resolution of 32 × 32 pixels with three color channels.

## Final Model Configuration

The selected final configuration uses:

- Geometric augmentation: Random rotation.
- Photometric augmentation: Random brightness and contrast.
- Cutout/Random Erasing: A random 16 × 16 rectangular region is masked.
- CNN architecture: Three convolution branches whose outputs are concatenated, followed by pooling and a 10-class softmax output.

## Results

The final configuration was Geometric + Photometric + Cutout/Random Erasing.

| Metric | Mean ± Standard Deviation |
|---|---:|
| Validation Accuracy | 31.67% ± 1.15% |
| Clean Test Accuracy | 38.44% ± 0.81% |
| Shifted Test Accuracy | 32.56% ± 0.14% |

The results represent three runs using random seeds 42, 123, and 456.

## Best Improvement

Adding Cutout/Random Erasing to geometric and photometric augmentation produced the largest observed improvement in shifted-test accuracy.

- Geometric + Photometric: 21.13% ± 1.40%
- Geometric + Photometric + Cutout: 32.56% ± 0.14%

This is an improvement of approximately 11.43 percentage points. Cutout helps the model learn from partially obscured images, matching the rectangular occlusion used in the shifted test set.

## Requirements

- Python 3
- TensorFlow
- NumPy
- Matplotlib
- scikit-learn
- Jupyter Notebook

## How to Reproduce the Results

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/cifar10-cnn-robustness.git
cd cifar10-cnn-robustness
```

Replace `YOUR-USERNAME` with your GitHub username.

### 2. Create a virtual environment (optional)

```bash
python -m venv venv
```

Activate it on Windows:

```bash
venv\Scripts\activate
```

### 3. Install the dependencies

If a `requirements.txt` file is included:

```bash
pip install -r requirements.txt
```

Otherwise, install the required libraries:

```bash
pip install tensorflow numpy matplotlib scikit-learn jupyter
```

### 4. Open the notebook

Start Jupyter Notebook:

```bash
jupyter notebook
```

Open the project's `.ipynb` notebook and run the cells in order.

### 5. Prepare the data

Load the CIFAR-10 dataset, normalize image pixel values to the range 0–1, and prepare the training, validation, clean-test, and shifted-test sets as described in the notebook.

### 6. Run the experiments

Run each augmentation configuration separately. For reproducibility, use random seeds 42, 123, and 456. Train the model for up to 60 epochs using the settings specified in the notebook.

The final configuration applies geometric augmentation, photometric augmentation, and Cutout/Random Erasing during training.

### 7. Evaluate the model

Evaluate each trained model on the validation, clean-test, and shifted-test sets. Calculate the mean and standard deviation across the three seeds.

Run the error-analysis section to obtain class-wise accuracy, the normalized confusion matrix, misclassified examples, and the hidden-corruption test results.

## Reproducibility Notes

- Use the same dataset splits and preprocessing steps.
- Use the same model architecture and training settings.
- Use random seeds 42, 123, and 456 for the three experimental runs.
- Keep the shifted-test corruption procedure consistent across configurations.
- Results may vary slightly across hardware, TensorFlow versions, and execution environments.

## Conclusion

The experiments show that data augmentation can improve robustness to image corruption. In particular, adding Cutout/Random Erasing to geometric and photometric augmentation produced the highest shifted-test accuracy among the evaluated configurations.


The experiments show that data augmentation can improve robustness to image corruption. In particular, adding Cutout/Random Erasing to geometric and photometric augmentation produced the highest shifted-test accuracy among the evaluated configurations.
