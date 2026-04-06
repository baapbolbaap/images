# Practical 7 — Brightness & Contrast

---

## Q1 — Image Negative
Inverts pixel values — dark areas become bright and vice versa.
```matlab
img = imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg');
subplot(1,2,1), imshow(img),              title('Original')
subplot(1,2,2), imshow(imcomplement(img)), title('Negative')
```

---

## Q2 — Thresholding
Converts grayscale image to binary by setting pixels above 128 to white, rest to black.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
subplot(1,2,1), imshow(gray),       title('Original')
subplot(1,2,2), imshow(gray > 128), title('Threshold')
```

---

## Q3 — Gray Level Slicing
Highlights a specific intensity range (L/4 to 3L/4) to white, preserving the background.
```matlab
gray = double(rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg')));
out  = gray;
out(gray >= round(255/4) & gray <= round(3*255/4)) = 255;
subplot(1,2,1), imshow(uint8(gray)), title('Original')
subplot(1,2,2), imshow(uint8(out)),  title('Gray Level Sliced')
```

---

## Q4 — Bit Plane Slicing
Extracts each of the 8 bit planes from a grayscale image to show contribution of each bit.
```matlab
gray = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg'));
subplot(3,3,1), imshow(gray), title('Original')
for i = 1:8
    subplot(3,3,i+1), imshow(bitget(gray,i)*255), title(['Bit ',num2str(i)])
end
```

---

## Q5 — Log Transform
Compresses high intensity values and expands dark ones, enhancing details in dark regions.
```matlab
img = double(imread('C:\Users\khush\OneDrive\Desktop/weird.jpg'));
c   = 255 / log10(1 + 255);
out = c * log10(1 + img);
subplot(1,2,1), imshow(uint8(img)), title('Original')
subplot(1,2,2), imshow(uint8(out)), title('Log Transform')
```

---

## Q6 — Power Law (Gamma) Transform
Applies gamma correction — values > 1 darken the image, values < 1 brighten it.
```matlab
a   = rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird.jpg'));
out = double(a) .^ 1.7;
subplot(1,2,1), imshow(a),          title('Original')
subplot(1,2,2), imshow(uint8(out)), title('Gamma = 1.7')
```

---

## Q7 — Brightness Adjustment
Increases or decreases overall pixel intensity by adding or subtracting a constant.
```matlab
a = imread('C:\Users\khush\OneDrive\Desktop/weird.jpg');
subplot(1,3,1), imshow(a),                       title('Original')
subplot(1,3,2), imshow(uint8(double(a) + 150)),  title('Brightness +')
subplot(1,3,3), imshow(uint8(double(a) - 100)),  title('Brightness -')
```

---

## Q8 — Contrast Adjustment
Scales pixel values up or down to stretch or compress the intensity range.
```matlab
a = imread('C:\Users\khush\OneDrive\Desktop/weird.jpg');
subplot(1,3,1), imshow(a),                      title('Original')
subplot(1,3,2), imshow(uint8(double(a) * 2)),   title('Contrast +')
subplot(1,3,3), imshow(uint8(double(a) * 0.5)), title('Contrast -')
```
