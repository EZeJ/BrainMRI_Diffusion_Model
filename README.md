
Main     [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/EasonJia9598/BrainMRI_Diffusion_Model/blob/main/main%20(1).ipynb#scrollTo=f7444b0b)

Inference     [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/EasonJia9598/BrainMRI_Diffusion_Model/blob/main/Inference%20(1).ipynb)




# **MRIDiff: Image Synthesis of Brain MRI Scans with Denoising Diffusion Probabilistic Model**

## **Abstract**

Medical imaging plays a critical role in diagnosis and treatment planning. However, obtaining high-quality, diverse datasets for brain MRI analysis remains challenging due to privacy concerns and limited availability. This study presents **MRIDiff**, a **Denoising Diffusion Probabilistic Model (DDPM)** for **generating synthetic brain MRI scans**. By leveraging **deep learning and probabilistic diffusion models**, this work demonstrates how AI can **generate realistic medical images**, aiding in data augmentation for machine learning applications in healthcare.

## **Introduction**

Magnetic Resonance Imaging (MRI) is a fundamental tool for brain disorder diagnosis, but **limited availability of annotated medical datasets** poses challenges for AI-driven medical applications. Traditional **Generative Adversarial Networks (GANs)** have been used for synthetic MRI image generation but suffer from **mode collapse and unstable training dynamics**. 

To overcome these issues, **diffusion models** have emerged as a superior alternative for image synthesis by **iteratively denoising Gaussian noise into high-fidelity images**. This project develops **MRIDiff**, an advanced diffusion model for generating synthetic **brain MRI scans**, improving dataset accessibility and enhancing medical AI research.

---

## **Methodology**

### **1. Model Architecture: Denoising Diffusion Probabilistic Model (DDPM)**

The **DDPM framework** is used to **generate synthetic brain MRI scans** by learning to reverse a diffusion process that gradually adds noise to training images. The architecture is based on **UNet**, a widely adopted **CNN-based encoder-decoder** network with skip connections.

#### **Diffusion Process**
1. A training MRI image is progressively **corrupted with Gaussian noise**.
2. The model learns to **reverse the noise addition**, reconstructing the original image.
3. During inference, the model **starts from pure noise** and iteratively **denoises to generate realistic MRI images**.

### **2. Dataset & Preprocessing**
- **Dataset:** Brain Tumor MRI Dataset (Kaggle), containing labeled MRI scans for **Glioma, Meningioma, Pituitary Tumors**, and **Healthy Brain Scans**.
- **Preprocessing Steps:**
  - **Normalization**: Standardized pixel values to improve model stability.
  - **Augmentation**: Rotations, flips, and contrast adjustments to increase dataset diversity.
  - **Resizing**: Images were resized to **256×256 pixels** for efficient model training.

### **3. Training & Hyperparameter Tuning**
- **Batch Size**: 32
- **Learning Rate**: 2e-4
- **Number of Diffusion Steps**: 300
- **Optimizer**: AdamW
- **GPU Acceleration**: Trained on **NVIDIA Tesla T4 (16GB VRAM)**

### **4. Performance Evaluation Metrics**
- **FID Score (Fréchet Inception Distance)**: Measures image realism by comparing synthetic images to real MRI scans.
- **MSE (Mean Squared Error)**: Evaluates reconstruction accuracy.
- **PSNR (Peak Signal-to-Noise Ratio)**: Quantifies image quality relative to original MRI scans.

---

## **Results & Analysis**

### **1. Generated MRI Samples**
The trained **MRIDiff model** successfully generated **high-quality, diverse MRI images**, capturing anatomical structures with fine details. Below are some key observations:

- **High Structural Fidelity**: Synthetic scans closely resemble real MRI images.
- **Effective Noise Reduction**: The iterative denoising process preserves anatomical details.
- **Class-Specific Generation**: The model successfully differentiates between healthy and diseased brain scans.

### **2. Comparative Evaluation: GANs vs. Diffusion Models**

- **Lower FID** indicates more realistic images.
- **Higher PSNR** suggests better image reconstruction quality.
- **Diffusion models outperform GANs** by producing more **stable and diverse outputs**.

### **3. Impact on Medical AI Research**
- **Improved Data Augmentation**: Enhances training datasets for brain tumor detection models.
- **Bridging the Data Scarcity Gap**: Allows medical researchers to generate synthetic MRI scans where real data is limited.
- **Better Generalization**: Enables AI models to train on more diverse datasets, reducing bias.

---

## **Challenges and Future Improvements**

### **1. Computational Cost**
- Training diffusion models is **computationally expensive**. Future work could explore **more efficient architectures** or **distilled diffusion models** for faster inference.

### **2. Higher Resolution Generation**
- Currently, MRI scans are limited to **256×256 resolution**. Future iterations will incorporate **Super-Resolution Diffusion Models** to enhance image clarity.

### **3. Multi-Modal Image Synthesis**
- Extending the model to generate **multi-modal MRI scans** (T1-weighted, T2-weighted, FLAIR) will further **enhance medical imaging applications**.

---

## **Conclusion**

This project successfully demonstrates that **Denoising Diffusion Probabilistic Models (DDPMs)** can generate **realistic, high-quality brain MRI scans**, providing a valuable tool for **medical AI research**. Compared to GANs, **diffusion models produce more stable, high-fidelity medical images**, improving dataset accessibility for **AI-driven diagnostic tools**. 

Future directions include **higher resolution generation, multi-modal synthesis, and optimized diffusion techniques** to further **advance AI in medical imaging**.

---

More details in the PDF file. 

INTRODUCTION
============

Image synthesis is widely applied by GANs for a few years, the result of
GANs on medical images are relatively satisfied but lack of flexibility
and the precision in image details \[1\]. The raising of Diffusion
models are showing the supreme outperformance than GANs in Text-to-image
generation tasks, like DALL-E \[2\]. The images that generated by
Diffusion models are increasingly improving and have a trending that is
even better than human being's creations.\[3\] However, the original
Diffusion Models are suffering from slow reverse inference time cost and
the lack of stability of the result in each Markov Chain. This is not
ideal in medical domain image generation. Hence, here we applied a new
Denoising Diffusion models that can be adjusted and lower the noises in
every few steps in the reverse inference process. \[4\] are showing
delightful results by increasing step size T with this idea. And hereby,
we wish to use admitting a progressive lossy decompression scheme that
can be interpreted as a generalization of autoregressive decoding \[5\]
to further improve the performance of \[4\]'s model.

PROBLEM STATEMENT
=================

Rare diseases' medical scans are very hard to obtain in world-wide
range. Most of time, those images are belong to patients themselves or
some of the best hospitals, who would like not to share. Hence, by using
image synthesis from limited amount of rare medical scans that are
already publicly published, we can create more scans that are related to
certain diseases, which are un-restricted by the confidential agreement
between two parties. And using those model generated images, we can help
doctors or medical students to learn those diseases without too many
difficulties. The current model of GANs needs more computation resources
to train and the inference time is large than the Diffusion models
\[6\]. Here, we would like to try the state-of-art technique for image
synthesis by Denosing Diffusion model to solve this task.


H. Huang, P. S. Yu, και C. Wang, 'An Introduction to Image Synthesis
with Generative Adversarial Nets'. arXiv, 2018.

A. Ramesh κ.ά., 'Zero-Shot Text-to-Image Generation'. arXiv, 2021.

J. Yu κ.ά., 'Vector-quantized Image Modeling with Improved VQGAN'.
arXiv, 2021.

M. Özbey κ.ά., 'Unsupervised Medical Image Translation with Adversarial
Diffusion Models'. arXiv, 2022.

J. Ho, A. Jain, and P. Abbeel, 'Denoising Diffusion Probabilistic
Models'. arXiv, 2020.

S. U. Dar, M. Yurt, L. Karacan, A. Erdem, E. Erdem, and T. C¸ ukur,
"Image synthesis in multi-contrast MRI with conditional generative
adversarial networks," IEEE Trans. Med. Imag., vol. 38, no. 10, pp.
2375--2388, 2019.

B. Yu, L. Zhou, L. Wang, Y. Shi, J. Fripp, and P. Bourgeat, "Ea-GANs:
Edge-aware generative adversarial networks for cross-modality MR image
synthesis," IEEE Trans. Med. Imag., vol. 38, no. 7, pp. 1750--1762,
2019.

A. Sharma and G. Hamarneh, "Missing MRI pulse sequence synthesis using
multi-modal generative adversarial network," IEEE Trans. Med. Imag.,
vol. 39, pp. 1170--1183, 2020.

G. Wang et al., "Synthesize high-quality multi-contrast magnetic
resonance imaging from multi-echo acquisition using multi-task deep
generative model," IEEE Trans. Med. Imag., vol. 39, no. 10, pp.
3089--3099, 2020.

L. Yang κ.ά., 'Diffusion Models: A Comprehensive Survey of Methods and
Applications'. arXiv, 2022.

F. A. Fardo, V. H. Conforto, F. C. de Oliveira, και P. S. Rodrigues, 'A
Formal Evaluation of PSNR as Quality Measurement Parameter for Image
Segmentation Algorithms'. arXiv, 2016.

J. Nilsson και T. Akenine-Möller, 'Understanding SSIM'. arXiv, 2020.

M. Mirza και S. Osindero, 'Conditional Generative Adversarial Nets'.
arXiv, 2014.

M.-Y. Liu, T. Breuel, και J. Kautz, 'Unsupervised Image-to-Image
Translation Networks'. arXiv, 2017.

J. Ho, A. Jain, και P. Abbeel, 'Denoising Diffusion Probabilistic
Models'. arXiv, 2020.

A. Jog, A. Carass, S. Roy, D. L. Pham, and J. L. Prince, "Random forest
regression for magnetic resonance image synthesis," Med. Image Anal.,
vol. 35, pp. 475--488, 2017.

J.A. Vaswani et al., 'Attention Is All You Need'. arXiv, 2017.

K. He, X. Zhang, S. Ren, and J. Sun, 'Deep Residual Learning for Image
Recognition'. arXiv, 2015.

Z. Liu, H. Mao, C.-Y. Wu, C. Feichtenhofer, T. Darrell, and S. Xie, 'A
ConvNet for the 2020s'. arXiv, 2022.
