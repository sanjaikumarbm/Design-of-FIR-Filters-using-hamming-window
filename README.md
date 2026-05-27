# Design-of-FIR-Filters-using-hamming-window
REG NO :212223060247
# DESIGN OF LOW PASS FIR DIGITAL FILTER 

# AIM: 
          
  To generate design of high pass FIR digital filter using SCILAB 

# APPARATUS REQUIRED: 

  PC Installed with SCILAB 

# PROGRAM 
LPF
```
clc;
clear;
close;

M = input('Enter the Odd Filter Length = ');
Wc = input('Enter the Digital Cut off frequency (in radians) = ');

alpha = (M - 1) / 2; // Center value

// Ideal Low Pass filter coefficients
for n = 1:M
    if (n == alpha + 1) then
        hd(n) = Wc / %pi;   // center tap
    else
        hd(n) = sin(Wc * ((n - 1) - alpha)) / (((n - 1) - alpha) * %pi);
    end
end

// Hamming Window
for n = 1:M
    W(n) = 0.54 - (0.46 * cos((2 * %pi * (n - 1)) / (M - 1)));
end

// Apply window to ideal filter
h = hd .* W;
disp(h, 'Filter Coefficients are:');

// Frequency response
[hzm, fr] = frmag(h, 256);

subplot(2, 1, 1);
plot(2 * fr, hzm);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR LPF using Hamming Window');

hzm_dB = 20 * log10(hzm);
subplot(2, 1, 2);
plot(2 * fr, hzm_dB);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude (dB)');
title('Frequency Response of FIR LPF using Hamming Window');
```
HPF
```
clc;
clear;
close;

M = input('Enter the Odd Filter Length = ');
Wc = input('Enter the Digital Cut off frequency (in radians) = ');

alpha = (M - 1) / 2; // Center value

// Ideal Low Pass filter coefficients
for n = 1:M
    if (n == alpha + 1) then
        hd_lp(n) = Wc / %pi;   // center tap
    else
        hd_lp(n) = sin(Wc * ((n - 1) - alpha)) / (((n - 1) - alpha) * %pi);
    end
end

// Spectral inversion to get High Pass
for n = 1:M
    if (n == alpha + 1) then
        hd(n) = 1 - hd_lp(n);
    else
        hd(n) = -hd_lp(n);
    end
end

// Hamming Window
for n = 1:M
    W(n) = 0.54 - (0.46 * cos((2 * %pi * (n - 1)) / (M - 1)));
end

// Apply window to ideal high-pass filter
h = hd .* W;
disp(h, 'High Pass Filter Coefficients are:');

// Frequency response
[hzm, fr] = frmag(h, 256);

subplot(2, 1, 1);
plot(2 * fr, hzm);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude');
title('Frequency Response of FIR HPF using Hamming Window');

hzm_dB = 20 * log10(hzm);
subplot(2, 1, 2);
plot(2 * fr, hzm_dB);
xlabel('Normalized Digital Frequency w');
ylabel('Magnitude (dB)');
title('Frequency Response of FIR HPF using Hamming Window');
```

# OUTPUT
LPF
<img width="1203" height="782" alt="image" src="https://github.com/user-attachments/assets/561bcb8a-a983-4a19-a881-ee5b7cf7b9bd" />
<img width="1918" height="1075" alt="image" src="https://github.com/user-attachments/assets/710063bb-2a88-474b-ae5f-ba805c79bd09" />


HPF
<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/d7bf226a-5b08-4dab-959f-6f6418e44d44" />
<img width="1175" height="675" alt="image" src="https://github.com/user-attachments/assets/b3e2e82c-78cd-40f9-8672-bbf64669ae25" />



# RESULT
Thus design of FIR low pass and high pass filter is done.
