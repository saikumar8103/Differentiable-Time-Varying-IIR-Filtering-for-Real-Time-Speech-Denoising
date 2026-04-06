# Differentiable-Time-Varying-IIR-Filtering-for-Real-Time-Speech-Denoising
__INTRODUCTION 
Speech denoising is an essential task in modern audio processing systems such as mobile 
communication, hearing aids, and voice assistants. In real-world environments, speech 
signals are often corrupted by background noise, which reduces clarity and intelligibility. 
Traditional denoising techniques like Wiener filtering and spectral subtraction are limited in 
handling dynamic and non-stationary noise conditions. 
Infinite Impulse Response (IIR) filters are widely used due to their efficiency and ability to 
model recursive systems. However, conventional IIR filters use fixed coefficients and cannot 
adapt effectively to time-varying noise. This project introduces a novel approach that 
combines IIR filtering with deep learning to create a differentiable time-varying system. 
The key idea is to allow filter coefficients to change over time and be predicted by a neural 
network. By making the filtering process differentiable, the system can be trained end-to
end using gradient descent. This approach bridges the gap between classical digital signal 
processing and modern machine learning techniques, enabling high-quality, low-latency 
speech enhancement. 
METHODS 
The proposed system processes noisy speech signals and outputs a cleaner version by 
dynamically adapting filter parameters. 
Problem Definition 
The noisy signal is represented as: 
where: 
 𝑠[𝑛]= clean speech  
 𝑣[𝑛]= noise  
�
�[𝑛] = 𝑠[𝑛]+𝑣[𝑛] 
The objective is to estimate 𝑠̂[𝑛], the clean speech. 
Time-Varying IIR Filter 
The filtering process is defined as: 
�
�
𝑁
𝑦[𝑛] = ∑𝑏𝑘
𝑘=0
[𝑛]𝑥[𝑛 − 𝑘]− ∑𝑎𝑘
𝑘=1
[𝑛]𝑦[𝑛 −𝑘] 
Unlike traditional filters, coefficients 𝑎𝑘[𝑛]and 𝑏𝑘[𝑛]vary with time. 
Neural Network Design 
A neural network predicts filter coefficients based on input features: 
 Spectrogram or raw waveform segments  
 Temporal context frames  
Architecture: 
 Convolutional layers (feature extraction)  
 Recurrent layers (temporal modeling)  
 Fully connected layers (coefficient output)  
Differentiable Filtering 
The recursive filtering operation is implemented in a differentiable manner so gradients can 
f
low through the system. Backpropagation Through Time (BPTT) is used for training. 
Loss Function 
The system is trained using: 
 Mean Squared Error (MSE)  
 Spectral loss  
Real-Time Constraints 
ℒ =∣∣ 𝑠̂ −𝑠 ∣∣2 
 Causal processing (no future samples)  
 Frame-by-frame computation  
 Low latency suitable for live applications  
 
PSEUDOCODE 
Initialize neural network parameters θ 
Initialize previous outputs y[n-k] 
 
For each input frame x[n]: 
 
    Extract features from x[n] 
 
    Predict filter coefficients: 
        a[n], b[n] = NeuralNetwork(features) 
 
    Apply IIR filtering: 
        y[n] = 0 
         
        For k = 0 to M: 
            y[n] += b_k[n] * x[n-k] 
         
        For k = 1 to N: 
            y[n] -= a_k[n] * y[n-k] 
 
    Store output y[n] 
 
Training Loop: 
 
For each batch: 
    predicted_output = Model(noisy_input) 
    loss = ComputeLoss(predicted_output, clean_signal) 
Backpropagate loss 
Update parameters θ 
RESULTS 
The model is evaluated using standard speech datasets such as TIMIT and LibriSpeech with 
artificially added noise (white noise, babble noise, environmental sounds). 
Performance Metrics 
 Signal-to-Noise Ratio (SNR)  
 Perceptual Evaluation of Speech Quality (PESQ)  
 Short-Time Objective Intelligibility (STOI)  
Comparison with Existing Methods 
Method 
Wiener Filter 
Noise Reduction Speech Quality Latency 
Medium 
Spectral Subtraction Medium 
Deep Learning Models High 
Proposed IIR Method High 
Low 
Medium 
High 
High 
Low 
Low 
High 
Low 
Observations 
 Adaptive filtering improves performance in dynamic noise  
 Time-varying IIR filters outperform static filters  
 Comparable results to deep models with lower computational cost  
 Suitable for real-time systems  
CONCLUSIONS 
The proposed differentiable time-varying IIR filtering approach successfully enhances speech 
signals in noisy environments. By integrating neural networks with classical filtering 
techniques, the system achieves both adaptability and efficiency. 
The differentiable framework enables end-to-end learning, allowing the model to optimize 
f
ilter coefficients dynamically. This results in improved speech quality, reduced noise, and 
low-latency processing suitable for real-time applications. 
Overall, the approach demonstrates a powerful combination of signal processing and deep 
learning, making it highly effective for modern speech enhancement tasks. 
LIMITATIONS 
Despite its advantages, the system has certain limitations: 
 Stability Issues: Incorrect coefficient prediction may lead to unstable filters  
 Training Complexity: Recursive operations make training computationally intensive  
 Gradient Problems: Possibility of vanishing or exploding gradients  
 Data Dependency: Performance depends on training dataset diversity  
 Limited Long-Term Context: May not capture very long dependencies effectively  
 Implementation Difficulty: Real-time deployment requires optimization 
