# ASK-Amplitude Shift Keying
## Aim
To simulate and plot the waveform for Amplitude Shift Keying (ASK) modulation using a given binary data sequence.
## Tools required
- Python: A versatile programming language used for scientific computing and signal processing.
- NumPy: A powerful numerical library in Python for performing array-based operations and mathematical computations.
## Program
```
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter
# Butterworth low-pass filter for demodulation
def butter_lowpass_filter(data, cutoff, fs, order=5):
    nyquist = 0.5 * fs
    normal_cutoff = cutoff / nyquist
    b, a = butter(order, normal_cutoff, btype='low', analog=False)
    return lfilter(b, a, data)
# Parameters
fs = 1000                # Sampling frequency
f_carrier = 50           # Carrier frequency
bit_rate = 10            # Data rate
T = 1                    # Total time duration
t = np.linspace(0, T, int(fs * T), endpoint=False)
# Message signal (binary data)
bits = np.random.randint(0, 2, bit_rate)
bit_duration = fs // bit_rate
message_signal = np.repeat(bits, bit_duration)
# Carrier signal
carrier = np.sin(2 * np.pi * f_carrier * t)
# ASK Modulation
ask_signal = message_signal * carrier
# ASK Demodulation
demodulated = ask_signal * carrier  # Multiply by carrier for coherent detection
filtered_signal = butter_lowpass_filter(demodulated, f_carrier, fs)
decoded_bits = (filtered_signal[::bit_duration] > 0.25).astype(int)
# Plotting
plt.figure(figsize=(12, 8))
plt.subplot(4, 1, 1)
plt.plot(t, message_signal, label='Message Signal (Binary)', color='b')
plt.title('Message Signal')
plt.grid(True)
plt.subplot(4, 1, 2)
plt.plot(t, carrier, label='Carrier Signal', color='g')
plt.title('Carrier Signal')
plt.grid(True)
plt.subplot(4, 1, 3)
plt.plot(t, ask_signal, label='ASK Modulated Signal', color='r')
plt.title('ASK Modulated Signal')
plt.grid(True)
plt.subplot(4, 1, 4)
plt.step(np.arange(len(decoded_bits)), decoded_bits, label='Decoded Bits', color='r', marker='x')
plt.title('Decoded Bits')
plt.tight_layout()
plt.show()
```
## Output waveform
![image](https://github.com/user-attachments/assets/0c07b145-54f2-4798-96f3-36267e00a681)

## Results
Amplitude Shift Keying (ASK) modulation was successfully simulated for the given binary data. The modulated signal waveform clearly shows amplitude variations corresponding to the input bits.

# Hardware experiment output waveform
![WhatsApp Image 2025-04-29 at 18 37 54_5fbdf1ac](https://github.com/user-attachments/assets/4ef1d6ef-1216-4ac1-8e45-5ac4b1ab3ed2)

