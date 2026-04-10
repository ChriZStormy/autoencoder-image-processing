# Autoencoders for Image Restoration and Transformation


## General Objective
The main goal of this project is to understand how autoencoders can learn useful data representations to solve various image reconstruction problems. 

Throughout this practice, three variants of the same base model (a Convolutional Autoencoder) are implemented to solve three distinct tasks:
1. **Denoising** (Denoising Autoencoder)
2. **Image Colorization**
3. **Reconstruction of Missing Regions** (Image Inpainting)

All tasks use the same dataset to clearly compare how the learning problem shifts depending on the transformation applied to the input image.

---

## Dataset: CIFAR-10
This project utilizes the **CIFAR-10** dataset due to its visual variety and color depth, making the effects of each transformation clearly observable.
* **Size:** 60,000 images
* **Resolution:** 32 × 32 pixels
* **Channels:** 3 (RGB Color)
* **Classes:** 10 (airplane, automobile, bird, cat, deer, dog, frog, horse, ship, truck)

---

## Model Architecture
The three tasks share the same baseline Convolutional Autoencoder architecture:

1. **Encoder:** Input Image $\rightarrow$ Convolutional Layers $\rightarrow$ Spatial Reduction $\rightarrow$ Latent Representation.
2. **Latent Space:** A compressed vector representing the most critical structural information of the image.
3. **Decoder:** Latent Representation $\rightarrow$ Transposed Convolutions / Upsampling $\rightarrow$ Reconstructed Image.

**Loss Function:** Mean Squared Error (MSE) between the reconstructed output and the target image.

---

## Implemented Tasks

### Task 1: Denoising Autoencoder
The model learns to recover a clean image from a corrupted input by removing perturbations.
* **Input:** Noisy RGB image
* **Output:** Clean original RGB image
* **Noise Types Implemented:**
  * **Gaussian Noise:** Random perturbation added to each pixel. Tested with mild ($\sigma = 0.1$) and heavy ($\sigma = 0.3$) noise.
  * **Salt and Pepper Noise:** Randomly replacing a percentage of pixels with maximum (salt/white) or minimum (pepper/black) values to simulate sensor or transmission errors.

### Task 2: Image Colorization
The autoencoder reconstructs lost color information by inferring plausible colors based on structural context.
* **Input:** Grayscale image (1 channel)
* **Output:** Colorized image (3 RGB channels)
* **Target:** Original RGB image

### Task 3: Image Inpainting
The model completes missing parts of an image using the surrounding spatial context.
* **Input:** RGB image with a masked (blacked-out) region
* **Output:** Fully reconstructed RGB image
* **Mask Generation:** A square region inside the image is replaced with zeros.

---

## Experiments Conducted
To analyze the model's behavior, the following configurations were tested across the tasks:
* **Noise levels:** Different intensities of Gaussian and Salt & Pepper noise.
* **Latent space dimensions:** 16, 32, and 64.
* **Missing region sizes:** $8 \times 8$ and $12 \times 12$ pixels.

---

## Results and Deliverables
*(Add your specific visual results and plots here once you run the notebook)*

### Expected Visual Comparisons:
* **Task 1:** `Original Image` $\rightarrow$ `Noisy Image` $\rightarrow$ `Reconstructed Image`
* **Task 2:** `Original RGB` $\rightarrow$ `Grayscale Input` $\rightarrow$ `Colorized Output`
* **Task 3:** `Original Image` $\rightarrow$ `Masked Image` $\rightarrow$ `Inpainted Output`

### Training Metrics
* Included within the notebooks: Loss curves (Training vs. Validation).
* Hyperparameter configurations and architectural details.

---

## Analysis Questions Addressed
As part of this practice, the following questions are analyzed in the final report:
1. Which task was the most difficult for the autoencoder to solve?
2. Which type of noise was harder to remove?
3. Did the network successfully learn semantic patterns from the images?
4. How does the size of the latent space affect the reconstruction quality?

