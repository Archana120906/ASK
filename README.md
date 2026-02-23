# ASK
# Aim
Write a simple Python program for the modulation and demodulation of ASK and FSK.
# Tools required
Google Colab

Personal laptop
# Program
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 1000
fc = 50
bit_rate = 10
t = np.arange(0, 1, 1/fs)

# Binary data
bits = np.random.randint(0, 2, bit_rate)
msg = np.repeat(bits, fs//bit_rate)

# Carrier
carrier = np.sin(2*np.pi*fc*t)

# ASK Modulation
ask = msg * carrier

# Simple Demodulation
demod = ask * carrier
decoded = (demod[::fs//bit_rate] > 0).astype(int)

# Plotting
plt.figure(figsize=(10,8))

plt.subplot(4,1,1); plt.plot(msg); plt.title("Message Signal")
plt.subplot(4,1,2); plt.plot(carrier); plt.title("Carrier Signal")
plt.subplot(4,1,3); plt.plot(ask); plt.title("ASK Modulated Signal")
plt.subplot(4,1,4); plt.step(range(len(decoded)), decoded); plt.title("Decoded Bits")

plt.tight_layout()
plt.show()
```
```
import numpy as np
import matplotlib.pyplot as plt

fs, f1, f0, br = 1000, 50, 20, 10
t = np.arange(0, 1, 1/fs)

bits = np.random.randint(0, 2, br)
bs = fs // br
msg = np.repeat(bits, bs)

c1 = np.sin(2*np.pi*f1*t)
c0 = np.sin(2*np.pi*f0*t)
fsk = np.where(msg, c1, c0)

e1 = (fsk*c1).reshape(br, bs).sum(1)
e0 = (fsk*c0).reshape(br, bs).sum(1)
decoded = (e1 > e0).astype(int)

plt.figure(figsize=(10,8))
plt.subplot(5,1,1); plt.plot(msg); plt.title("Message Signal")
plt.subplot(5,1,2); plt.plot(c1); plt.title("Carrier f1")
plt.subplot(5,1,3); plt.plot(c0); plt.title("Carrier f0")
plt.subplot(5,1,4); plt.plot(fsk); plt.title("FSK Signal")
plt.subplot(5,1,5); plt.step(range(len(decoded)), decoded); plt.title("Decoded Bits")
plt.tight_layout(); plt.show()
```
# Output Waveform
<img width="989" height="790" alt="image" src="https://github.com/user-attachments/assets/8845b03d-208d-48c1-a89c-6dc95d203f40" />

<img width="989" height="790" alt="image" src="https://github.com/user-attachments/assets/7712b7dd-3919-4518-859f-e9311c510e86" />

# Results
Thus, the ASK and FSK performed using colab
