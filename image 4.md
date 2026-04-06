# Practical 4 — Convolution & Correlation

---

## Q1 — Image Convolution & Correlation
Applies a horizontal edge kernel to a grayscale image using convolution and correlation.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
k    = [1 0 -1; 1 0 -1; 1 0 -1];
subplot(1,3,1), imshow(gray),                                    title('Original')
subplot(1,3,2), imshow(uint8(conv2(double(gray),k,'same'))),     title('Convolution')
subplot(1,3,3), imshow(uint8(imfilter(double(gray),k,'corr'))), title('Correlation')
```

---

## Q2 — Basic 2D Convolution
Convolves two small matrices and displays the result.
```matlab
x = [1 2; 3 4];
h = [5 6; 7 8];
disp(conv2(x, h, 'same'))
```

---

## Q3 — Circular Convolution
Performs circular convolution using FFT multiplication in frequency domain.
```matlab
x = [1 2 3 4];
h = [1 10 1 10];
disp('Circular Convolution:')
disp(real(ifft(fft(x) .* fft(h))))
```

---

## Q4 — Circular Correlation
Computes 2D circular correlation via FFT by flipping the kernel before multiplication.
```matlab
x = [10 4 7 8];
h = [3 3 5 4];
y = ifft2(fft2(x) .* fft2(flipud(fliplr(h))));
disp('Circular Correlation:'), disp(real(y))
```

---

## Q5 — Auto-Correlation
Correlates a signal with itself to reveal repeating patterns and periodicity.
```matlab
x   = input('Enter sequence x[n]: ');
rxx = xcorr(x);
stem(-(length(x)-1):(length(x)-1), rxx)
xlabel('Lag'), ylabel('Amplitude'), title('Auto-Correlation'), grid on
```

---

## Q6 — Cross-Correlation
Measures similarity between two different sequences as a function of lag.
```matlab
x   = input('Enter first sequence x[n]: ');
y   = input('Enter second sequence y[n]: ');
rxy = xcorr(x, y);
stem(-(length(y)-1):(length(x)-1), rxy)
xlabel('Lag'), ylabel('Amplitude'), title('Cross-Correlation'), grid on
```
