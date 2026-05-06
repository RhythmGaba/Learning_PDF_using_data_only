# Learning Probability Density Function using GAN

## Overview
This project focuses on learning an unknown probability density function (PDF) using a **Generative Adversarial Network (GAN)**.  
The model learns the distribution **only from data samples**, without assuming any predefined distribution (like Gaussian).

---

## Dataset
- Dataset: India Air Quality Data (Kaggle)
- Feature Used: **NO₂ concentration (x)**

---

## Data Transformation

Each value of x is transformed into z using:

z = x + a_r * sin(b_r * x)

Where:
- a_r = 0.5 × (r mod 7)
- b_r = 0.3 × ((r mod 5) + 1)
- r = Roll Number

This transformation introduces non-linearity, making the distribution complex.

---

## GAN Architecture

### Generator
- Input: Random noise ~ N(0,1)
- Layers:
  - Dense + LeakyReLU
  - Dense + LeakyReLU
  - Dense (Output)
- Output: Generated samples (z_fake)

### Discriminator
- Input: Real or generated z
- Layers:
  - Dense + LeakyReLU
  - Dense + LeakyReLU
  - Dense + Sigmoid
- Output: Probability (Real/Fake)

---

## Training Details
- Loss Function: Binary Crossentropy
- Optimizer: Adam
- Training:
  - Discriminator learns to classify real vs fake samples
  - Generator learns to fool the discriminator

---

## PDF Estimation
After training:
- Generator produces new samples
- PDF is estimated using:
  - Histogram Density

---

## Results

Below is the comparison of real vs generated distribution:

<img width="710" height="482" alt="image" src="https://github.com/user-attachments/assets/e2f0b466-53a8-4c6c-b045-1d7e84d2fe49" />


---

## Observations

- GAN captures the general distribution trend.
- Some instability is observed during training.
- Mode collapse occurs, where generated values concentrate in a narrow region.
- Despite this, the overall shape of the distribution is approximated.

---

## Challenges

- Training instability in GAN
- Mode collapse
- Hyperparameter sensitivity

---

## Conclusion

- GAN successfully learns distribution from data samples only.
- No prior assumption about the PDF is required.
- Generated samples can be used to approximate the probability density.

---

## Future Work

- Use deeper neural networks
- Apply Wasserstein GAN (WGAN)
- Improve stability using advanced techniques
- Better hyperparameter tuning

---
