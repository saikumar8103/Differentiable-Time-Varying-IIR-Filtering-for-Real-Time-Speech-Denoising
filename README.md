# Differentiable-Time-Varying-IIR-Filtering-for-Real-Time-Speech-Denoising
INTRODUCTION
Speech denoising is an essential task in modern audio processing systems such as mobile communication, hearing aids, and voice assistants. In real-world environments, speech signals are often corrupted by background noise, which reduces clarity and intelligibility. Traditional denoising techniques like Wiener filtering and spectral subtraction are limited in handling dynamic and non-stationary noise conditions.
Infinite Impulse Response (IIR) filters are widely used due to their efficiency and ability to model recursive systems. However, conventional IIR filters use fixed coefficients and cannot adapt effectively to time-varying noise. This project introduces a novel approach that combines IIR filtering with deep learning to create a differentiable time-varying system.
The key idea is to allow filter coefficients to change over time and be predicted by a neural network. By making the filtering process differentiable, the system can be trained end-to-end using gradient descent. This approach bridges the gap between classical digital signal processing and modern machine learning techniques, enabling high-quality, low-latency speech enhancement.

METHODS
The proposed system processes noisy speech signals and outputs a cleaner version by dynamically adapting filter parameters.
Problem Definition
The noisy signal is represented as:
x[n]=s[n]+v[n]

where:
	s[n]= clean speech 
	v[n]= noise 
The objective is to estimate s ̂[n], the clean speech.

Time-Varying IIR Filter
The filtering process is defined as:
y[n]=∑_(k=0)^M▒b_k [n]x[n-k]-∑_(k=1)^N▒a_k [n]y[n-k]

Unlike traditional filters, coefficients a_k [n]and b_k [n]vary with time.

Neural Network Design
A neural network predicts filter coefficients based on input features:
	Spectrogram or raw waveform segments 
	Temporal context frames 
Architecture:
	Convolutional layers (feature extraction) 
	Recurrent layers (temporal modeling) 
	Fully connected layers (coefficient output) 

Differentiable Filtering
The recursive filtering operation is implemented in a differentiable manner so gradients can flow through the system. Backpropagation Through Time (BPTT) is used for training.

Loss Function
The system is trained using:
	Mean Squared Error (MSE) 
	Spectral loss 
L=∣∣s ̂-s∣∣^2


Real-Time Constraints
	Causal processing (no future samples) 
	Frame-by-frame computation 
	Low latency suitable for live applications 

PSEUDOCODE


