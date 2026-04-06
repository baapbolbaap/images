# Practical 8 — Filters

---

## Q1 — Low Pass Filter
Blurs the image by averaging neighboring pixels, suppressing high-frequency noise.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
lp = imfilter(gray, fspecial('average',[5 5]));
subplot(1,2,1), imshow(gray), title('Original')
subplot(1,2,2), imshow(lp),   title('Low Pass')
```

---

## Q2 — High Pass Filter
Highlights edges by retaining high-frequency components using a Laplacian kernel.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
hp = imfilter(gray, fspecial('laplacian', 0.2));
subplot(1,2,1), imshow(gray),    title('Original')
subplot(1,2,2), imshow(hp, []),  title('High Pass')
```

---

## Q3 — Butterworth Low Pass Filter
Smoothens the image in the frequency domain with a gradual cutoff to avoid ringing artifacts.
```matlab
gray = double(rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg')));
[M,N] = size(gray);
[u,v] = meshgrid(1:N, 1:M);
D = sqrt((u-N/2).^2 + (v-M/2).^2);
H = 1 ./ (1 + (D./50).^4);
g = real(ifft2(ifftshift(H .* fftshift(fft2(gray)))));
subplot(1,2,1), imshow(uint8(gray)), title('Original')
subplot(1,2,2), imshow(uint8(g)),    title('Butterworth LPF')
```

---

## Q4 — Gaussian Filter
Smoothens the image using a Gaussian kernel — less blurring than average filter, preserves edges better.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
g = imfilter(gray, fspecial('gaussian',[5 5],1));
subplot(1,2,1), imshow(gray), title('Original')
subplot(1,2,2), imshow(g),    title('Gaussian Filter')
```

---

## Q5 — Adding Noise
Adds salt & pepper noise to simulate image corruption.
```matlab
img = imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg');
noisy = imnoise(img, 'salt & pepper', 0.02);
subplot(1,2,1), imshow(img),   title('Original')
subplot(1,2,2), imshow(noisy), title('Noisy')
```

---

## Q6 — 1D IIR Filter on Signal
Filters a random signal row-wise using a simple IIR filter to show smoothing over time.
```matlab
rng default
x = rand(2,15);
y = filter(1, [1 -0.2], x, [], 2);
t = 0:14;
subplot(2,1,1), plot(t,x(1,:), t,y(1,:)), legend('Input','Filtered'), title('Row 1')
subplot(2,1,2), plot(t,x(2,:), t,y(2,:)), legend('Input','Filtered'), title('Row 2')
```

---

## Q7 — Filtering a Noisy Sine Wave
Smoothens a sine wave corrupted with random noise using a moving average filter.
```matlab
t = linspace(-pi, pi, 100);
x = sin(t) + 0.25*rand(size(t));
y = filter((1/5)*ones(1,5), 1, x);
plot(t,x, t,y), legend('Noisy','Filtered'), title('Sine Wave Filter')
```

---

## Q8 — Noise Removal (Median Filter)
Adds salt & pepper noise then removes it using a median filter.
```matlab
img = imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg');
noisy = imnoise(img, 'salt & pepper', 0.2);
clean = medfilt2(rgb2gray(noisy), [3 3]);
subplot(1,3,1), imshow(img),   title('Original')
subplot(1,3,2), imshow(noisy), title('Noisy')
subplot(1,3,3), imshow(clean), title('Median Filtered')
```
