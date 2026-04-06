# Practical 5 — Frequency Domain & Transforms

---

## Q1 — DFT (1D)
Applies 1D Fourier Transform row-wise to a grayscale image and displays the spectrum.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
dft  = fft(double(gray));
subplot(1,2,1), imshow(gray),                  title('Original')
subplot(1,2,2), imshow(log(1+abs(dft)),[]),    title('DFT')
```

---

## Q2 — 2D DFT
Applies 2D Fourier Transform to the full image, showing complete frequency spectrum.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
dft2 = fft2(double(gray));
subplot(1,2,1), imshow(gray),                  title('Original')
subplot(1,2,2), imshow(log(1+abs(dft2)),[]),   title('2D DFT')
```

---

## Q3 — Rotation Property
Demonstrates how rotating an image affects its spatial structure at 45°, 90°, and 180°.
```matlab
img = imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg');
subplot(2,2,1), imshow(img),               title('Original')
subplot(2,2,2), imshow(imrotate(img,45)),  title('45°')
subplot(2,2,3), imshow(imrotate(img,90)),  title('90°')
subplot(2,2,4), imshow(imrotate(img,180)), title('180°')
```

---

## Q4 — Image Blending
Blends two images by fusing them with equal alpha weighting.
```matlab
img1 = imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg');
img2 = imresize(imread('C:\Users\khush\OneDrive\Desktop/weird.jpg'), [size(img1,1) size(img1,2)]);
subplot(1,2,1), imshow(img1),              title('Original')
subplot(1,2,2), imshow(imfuse(img1,img2,'blend')), title('Blended')
```

---

## Q5 — FFT (Shifted)
Applies 2D FFT with `fftshift` to center the zero-frequency component for better visualization.
```matlab
gray    = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
fft_img = fftshift(fft2(double(gray)));
subplot(1,2,1), imshow(gray),                   title('Original')
subplot(1,2,2), imshow(log(1+abs(fft_img)),[]), title('FFT Shifted')
```

---

## Q6 — FFT2 on Synthetic Pattern
Shows the 2D FFT spectrum of a synthetic rectangular pattern to illustrate frequency domain behavior.
```matlab
f = zeros(30); f(5:24,13:17) = 1;
F = fftshift(fft2(f));
imshow(log(abs(F)),[-2 5],'InitialMagnification','fit')
colormap(jet), colorbar, title('FFT2 Spectrum')
```
