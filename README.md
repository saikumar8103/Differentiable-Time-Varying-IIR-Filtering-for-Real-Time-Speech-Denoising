# Differentiable Time-Varying IIR Filtering for Real-Time Speech Denoising

## 1. Introduction
Speech signals recorded in real-world environments are often corrupted by background noise, which degrades intelligibility and quality. Traditional fixed-coefficient filters are not effective against non-stationary noise. 

Differentiable Time-Varying IIR (Infinite Impulse Response) filtering is an advanced approach that combines classical digital signal processing with deep learning. It enables adaptive filtering where coefficients change dynamically over time and are learned through gradient-based optimization, making it suitable for real-time speech denoising applications.

---

## 2. Methods

### 2.1 Time-Varying IIR Filter
The general IIR filter equation is:

y[n] = Σ(b_k[n] * x[n-k]) - Σ(a_k[n] * y[n-k])

where:
- x[n] = input (noisy speech)
- y[n] = output (denoised speech)
- b_k[n] = time-varying feedforward coefficients
- a_k[n] = time-varying feedback coefficients

### 2.2 Differentiable Design
- Coefficients are generated using neural networks
- Entire system is differentiable
- Enables backpropagation for training

### 2.3 Model Architecture
- Two neural networks:
  - b-network → generates feedforward coefficients
  - a-network → generates feedback coefficients
- Activation function (tanh) ensures stability

### 2.4 Processing Pipeline
1. Input noisy speech signal
2. Generate coefficients at each time step
3. Apply recursive filtering
4. Output denoised speech

---

## 3. Pseudocode
Initialize x_past = zeros(order) Initialize y_past = zeros(order)
for each time step n: xt = input[n]
b = b_net(xt)
a = tanh(a_net(xt))

yt = b[0] * xt

for i in range(order):
    yt += b[i+1] * x_past[i]
    yt -= a[i] * y_past[i]

output[n] = yt

update x_past (shift right, insert xt)
update y_past (shift right, insert yt)
---

## 4. Results
- Effectively reduces background noise in speech signals
- Adapts to time-varying noise conditions
- Produces smoother and clearer output compared to static filters
- Suitable for real-time processing due to sample-wise computation

---

## 5. Conclusions
Differentiable Time-Varying IIR filtering provides a powerful framework for real-time speech denoising. By integrating neural networks with recursive filtering, it enables adaptive and trainable signal processing. This approach improves performance in dynamic environments and supports end-to-end learning.

---

## 6. Limitations
- Computational complexity is higher than traditional filters
- Stability must be carefully controlled
- Requires labeled training data (clean + noisy speech)
- Recursive nature may slow down parallel processing
