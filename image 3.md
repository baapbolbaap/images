# Practical 3 — Image Enhancement

---

## Q1 — Contrast Command
Enhances contrast of a grayscale image using `imadjust` to stretch intensity values.
```matlab
gray = rgb2gray(imread('weird.jpg'));
subplot(1,2,1), imshow(gray), title('Original')
subplot(1,2,2), imshow(imadjust(gray)), title('Contrast Enhanced')
```

---

## Q2 — Sharpen Command
Sharpens a grayscale image by emphasizing edges using `imsharpen`.
```matlab
gray = rgb2gray(imread('weird.jpg'));
subplot(1,2,1), imshow(gray), title('Original')
subplot(1,2,2), imshow(imsharpen(gray)), title('Sharpened')
```

---

## Q3 — imfuse Command
Blends two images into one using `imfuse` with blend mode.
```matlab
imshow(imfuse(imread('weird.jpg'), imread('weird2.jpeg'), 'blend'))
```

---

## Q4 — Montage Command
Displays multiple images in a single figure using `montage`.
```matlab
montage({imread('weird.jpg'), imread('weird2.jpeg')})
```

---

## Q5 — Squeeze Command
Removes singleton dimensions from a reshaped image array using `squeeze`.
```matlab
img = imread('weird.jpg');
imshow(squeeze(reshape(img, size(img,1), size(img,2), 1, size(img,3))))
```

---

## Q6 — Histogram Command
Plots the intensity histogram of a grayscale image using `imhist`.
```matlab
imhist(rgb2gray(imread('weird.jpg')))
```

---

## Q7 — histeq Command
Equalizes the histogram of a grayscale image to improve contrast.
```matlab
imshow(histeq(rgb2gray(imread('weird.jpg'))))
```

---

## Q8 — rgb2hsv Command
Converts an RGB image to HSV color space for hue-saturation-value representation.
```matlab
imshow(rgb2hsv(imread('weird.jpg')))
```

---

## Q9 — imresize Command
Resizes an image to a fixed resolution of 256×256 pixels.
```matlab
imshow(imresize(imread('weird.jpg'), [256 256]))
```

---

## Q10 — imnoise Command
Adds Gaussian noise to an image to simulate real-world degradation.
```matlab
imshow(imnoise(imread('weird.jpg'), 'gaussian'))
```

---

## Q11 — hsv2rgb Command
Converts image to HSV and back to RGB, then displays as grayscale.
```matlab
img = imread('weird.jpg');
imshow(rgb2gray(hsv2rgb(rgb2hsv(img))))
```

---

## Q12 — imshowpair Command
Displays two images side by side for visual comparison using `imshowpair`.
```matlab
imshowpair(imread('weird.jpg'), imread('weird2.jpeg'), 'montage')
```
