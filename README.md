# FREQUENCY-DIVISION-MULTIPLEXING-FDM---SIMULATION-USING-SCILAB

# AIM

To generate multiple message signals, multiplex them using AM-FDM, and recover each channel using bandpass filtering and coherent demodulation in Scilab.

# APPARATUS REQUIRED

1. Computer with Scilab
2. Scilab script (.sci file)
3. Basic DSP knowledge (filters, convolution, FFT)

# ALGORITHM

1. Generate message signals ( m_i(t) ).
2. Multiply each with its carrier to form AM-DSB.
3. Sum all channels → FDM composite.
4. For each channel:
   a. Band-pass filter around carrier.
   b. Multiply with same carrier (coherent detection).
   c. Low-pass filter to recover baseband.
5. Plot message, FDM, recovered outputs.

# PROCEDURE 

1. Define sampling rate, time vector, message and carrier frequencies.
2. Generate sinusoidal messages and modulate them with cosine carriers.
3. Add all modulated signals to form the composite FDM signal.
4. Design FIR bandpass filter to isolate each channel.
5. Demodulate by mixing with original carrier and low-pass filtering.
6. Plot original messages, FDM signal and recovered signals.
# PROGRM
~~~
clc;
clear;
close;

// PARAMETERS

fs = 10000;          // Sampling frequency
t = 0:1/fs:1;        // Time duration

// Message signal frequencies (from your table)
f1 = 4.16;      // Message 1
f2 = 5.55;      // Message 2
f3 = 5.26;      // Message 3
f4 = 7.69;      // Message 4
f5 = 16.66;     // Message 5
f6 = 20;        // Message 6

// Amplitudes
A1 = 3;
A2 = 4;
A3 = 5;
A4 = 6;
A5 = 4;
A6 = 8;


// MESSAGE SIGNALS

m1 = A1 * sin(2*%pi*f1*t);
m2 = A2 * sin(2*%pi*f2*t);
m3 = A3 * sin(2*%pi*f3*t);
m4 = A4 * sin(2*%pi*f4*t);
m5 = A5 * sin(2*%pi*f5*t);
m6 = A6 * sin(2*%pi*f6*t);

// ASSIGNED CARRIER FREQUENCIES FOR FDM

Fc1 = 200;
Fc2 = 400;
Fc3 = 600;
Fc4 = 800;
Fc5 = 1000;
Fc6 = 1200;

// FDM MODULATION (DSB-SC)

c1 = cos(2*%pi*Fc1*t);
c2 = cos(2*%pi*Fc2*t);
c3 = cos(2*%pi*Fc3*t);
c4 = cos(2*%pi*Fc4*t);
c5 = cos(2*%pi*Fc5*t);
c6 = cos(2*%pi*Fc6*t);

s1 = m1 .* c1;
s2 = m2 .* c2;
s3 = m3 .* c3;
s4 = m4 .* c4;
s5 = m5 .* c5;
s6 = m6 .* c6;

// Combined multiplexed signal
FDM = s1 + s2 + s3 + s4 + s5 + s6;

// DEMODULATION

dm1 = FDM .* c1;
dm2 = FDM .* c2;
dm3 = FDM .* c3;
dm4 = FDM .* c4;
dm5 = FDM .* c5;
dm6 = FDM .* c6;

// Low-pass filtering using moving average
n = 100; // smoothing factor
dm1_f = conv(dm1, ones(1,n)/n, "same");
dm2_f = conv(dm2, ones(1,n)/n, "same");
dm3_f = conv(dm3, ones(1,n)/n, "same");
dm4_f = conv(dm4, ones(1,n)/n, "same");
dm5_f = conv(dm5, ones(1,n)/n, "same");
dm6_f = conv(dm6, ones(1,n)/n, "same");

// PLOTTING RESULTS

// ---- Message Signals ----
figure;
subplot(3,2,1); plot(t,m1); title("Message Signal 1");
subplot(3,2,2); plot(t,m2); title("Message Signal 2");
subplot(3,2,3); plot(t,m3); title("Message Signal 3");
subplot(3,2,4); plot(t,m4); title("Message Signal 4");
subplot(3,2,5); plot(t,m5); title("Message Signal 5");
subplot(3,2,6); plot(t,m6); title("Message Signal 6");

// ---- FDM Signal ----
figure;
plot(t, FDM);
title("Combined FDM Signal");

// ---- Demodulated Signals ----
figure;
subplot(3,2,1); plot(t,dm1_f); title("Demodulated Signal 1");
subplot(3,2,2); plot(t,dm2_f); title("Demodulated Signal 2");
subplot(3,2,3); plot(t,dm3_f); title("Demodulated Signal 3");
subplot(3,2,4); plot(t,dm4_f); title("Demodulated Signal 4");
subplot(3,2,5); plot(t,dm5_f); title("Demodulated Signal 5");
subplot(3,2,6); plot(t,dm6_f); title("Demodulated Signal 6");

~~~

# OUTPUT
<img width="1913" height="1030" alt="image" src="https://github.com/user-attachments/assets/d5266a26-7e82-4a9c-9b41-550c0e88c3c8" />
<img width="1913" height="1020" alt="image" src="https://github.com/user-attachments/assets/afd1e347-11a1-4e88-a462-18d23b306ac6" />
<img width="1912" height="1021" alt="image" src="https://github.com/user-attachments/assets/887b9cc7-bdce-481b-af54-108876be8ceb" />




# MANUAL CALCULATION
![WhatsApp Image 2025-12-04 at 15 38 37_aac30b55](https://github.com/user-attachments/assets/3b665e6c-fb30-43fc-8e8d-d954089f2e65)
![WhatsApp Image 2025-12-04 at 15 38 37_a3af76d2](https://github.com/user-attachments/assets/c6c26602-3cd0-4f30-9cb1-d5b9979a1fbb)




# RESULT 

All message frequencies (400 - 500Hz) were successfully multiplexed and individually recovered with minimal distortion using bandpass isolation and coherent demodulation.
