# SSB-SC-AM-MODULATOR-AND-DEMODULATOR-USING-SCILAB-T1-M4-ODD
# SSB-SC-AM MODULATOR AND DEMODULATOR

## AIM

To write a program to perform SSBSC modulation and demodulation using SCI LAB and study its spectral characteristics.

---

## EQUIPMENTS REQUIRED

* Computer with i3 Processor
* SCI LAB

> **Note:** Keep all the switch faults in off position.

---

## ALGORITHM

### 1. Define Parameters:

* **Fs:** Sampling frequency.
* **T:** Duration of the signal.
* **Fc:** Carrier frequency.
* **Fm:** Frequency of the message signal.
* **Amplitude:** Maximum amplitude of the message signal.

### 2. Generate Signals:

* **Message Signal:** The baseband signal that will be modulated.
* **Carrier Signal:** A high-frequency signal used for modulation.
* **Analytic Signal:** Constructed using the Hilbert transform to get the in-phase and quadrature components.

### 3. SSBSC Modulation:

* **Modulated Signal:** Create the SSBSC signal using the in-phase and quadrature components, modulated by the carrier.

### 4. SSBSC Demodulation:

* **Mixing:** Multiply the SSBSC signal with the carrier to retrieve the message signal.
* **Low-pass Filtering:** Apply a low-pass filter to remove high-frequency components and recover the original message signal.

### 5. Visualization:

Plot the message signal, carrier signal, SSBSC modulated signal, and the recovered signal after demodulation.

---
## CODE
clc;
clear;
close;

// Time
fs = 100000;
t = 0:1/fs:0.02;

// Message signal
fm = 500;
Am = 1;
m = Am*sin(2*%pi*fm*t);

// Carrier
fc = 10000;
Ac = 1;
c = Ac*cos(2*%pi*fc*t);

// Hilbert transform of message
M = fft(m);
N = length(m);
H = zeros(1,N);

if modulo(N,2) == 0 then
    H(1) = 1;
    H(N/2+1) = 1;
    H(2:N/2) = 2;
else
    H(1) = 1;
    H(2:(N+1)/2) = 2;
end

mh = real(ifft(M .* H));

// SSB-SC modulation
// USB
ssb_usb = m .* cos(2*%pi*fc*t) - ...
          mh .* sin(2*%pi*fc*t);

// Coherent demodulation
demod = 2 * ssb_usb .* cos(2*%pi*fc*t);

// Low pass filter
fc_lp = 1500;
[b,a] = iir(5,'lp','butt',[fc_lp/fs 0],[]);
output = flts(demod,b,a);

// Plots

subplot(4,1,1);
plot(t,m);
xlabel("Time (s)");
ylabel("Amplitude");
title("Message Signal");

subplot(4,1,2);
plot(t,c);
xlabel("Time (s)");
ylabel("Amplitude");
title("Carrier Signal");

subplot(4,1,3);
plot(t,ssb_usb);
xlabel("Time (s)");
ylabel("Amplitude");
title("SSB-SC Modulated Signal (USB)");

subplot(4,1,4);
plot(t,output);
xlabel("Time (s)");
ylabel("Amplitude");
title("Demodulated Signal");
## PROCEDURE

* Refer Algorithms and write code for the experiment.
* Open SCILAB in System.
* Type your code in New Editor.
* Save the file.
* Execute the code.
* If any Error, correct it in code and execute again.
* Verify the generated waveform using Tabulation and Model Waveform.

---

## TABULATION

<img width="1489" height="785" alt="image" src="https://github.com/user-attachments/assets/f18d3793-14c7-48d0-8abf-893059d0f726" />


## CALCULATION
<img width="1600" height="1485" alt="image" src="https://github.com/user-attachments/assets/6356d441-a4d5-448e-8234-5f2a6d2fdd97" />

## OUTPUT
<img width="1071" height="634" alt="image" src="https://github.com/user-attachments/assets/3450f49b-ecbb-4a78-a0c9-c1c51c095ebb" />

## RESULT
Successfully performed SSBSC modulation and demodulation using SCI LAB.

