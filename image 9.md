# Practical 9 — Binary & Color Image Processing

---

## Q1 — Erosion
Shrinks bright regions by applying a 3×3 structuring element.
```matlab
a = rgb2gray(imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg"));
b = ones(3);
figure, imshow(a), title('Original')
figure, imshow(imerode(a,b)), title('Eroded')
```

---

## Q2 — Dilation
Expands bright regions by applying a 3×3 structuring element.
```matlab
a = rgb2gray(imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg"));
b = ones(3);
figure, imshow(a), title('Original')
figure, imshow(imdilate(a,b)), title('Dilated')
```

---

## Q3 — Opening
Erosion followed by dilation — removes small bright noise while preserving shape.
```matlab
a = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
b = ones(3);
subplot(1,2,1), imshow(a), title('Original')
subplot(1,2,2), imshow(imopen(a,b)), title('Opened')
```

---

## Q4 — Closing
Dilation followed by erosion — fills small dark gaps while preserving shape.
```matlab
a = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
b = ones(3);
subplot(1,2,1), imshow(a), title('Original')
subplot(1,2,2), imshow(imclose(a,b)), title('Closed')
```

---

## Q5 — RGB Channel Extraction
Splits a color image into its Red, Green, and Blue planes.
```matlab
I = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
subplot(2,2,1), imshow(I),          title('Original')
subplot(2,2,2), imshow(I(:,:,1)),   title('Red')
subplot(2,2,3), imshow(I(:,:,2)),   title('Green')
subplot(2,2,4), imshow(I(:,:,3)),   title('Blue')
```

---

## Q6 — Histogram Equalization (Color Image)
Equalizes brightness by applying `histeq` on the V (Value) channel in HSV space, leaving hue and saturation unchanged.
```matlab
I = im2double(imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg"));
hsv = rgb2hsv(I);
hsv(:,:,3) = histeq(hsv(:,:,3));
subplot(1,2,1), imshow(I),            title('Original')
subplot(1,2,2), imshow(hsv2rgb(hsv)), title('Equalized')
```

---

## Q7 — RGB Histogram
Plots pixel intensity distribution for each color channel.
```matlab
I = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
[r,x] = imhist(I(:,:,1));
[g,~] = imhist(I(:,:,2));
[b,~] = imhist(I(:,:,3));
plot(x,r,'r', x,g,'g', x,b,'b');
title('RGB Histogram'), xlabel('Intensity'), ylabel('Count'), legend('R','G','B'), grid on
```

---

## Q8 — YCbCr Color Space
Converts RGB to YCbCr and displays the Y (luminance), Cb (blue-diff), and Cr (red-diff) channels separately.
```matlab
RGB = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
YCC = rgb2ycbcr(RGB);
subplot(1,3,1), imshow(YCC(:,:,1)), title('Y')
subplot(1,3,2), imshow(YCC(:,:,2)), title('Cb')
subplot(1,3,3), imshow(YCC(:,:,3)), title('Cr')
```

---

## Q9 — Color Image Quantization
Reduces the number of colors in an image to 16 using minimum variance quantization.
```matlab
RGB = imread('peppers.png');
[X, map] = rgb2ind(RGB, 16);
subplot(1,2,1), imshow(RGB),     title('Original')
subplot(1,2,2), imshow(X, map),  title('Quantized (16 colors)')
```

---

## Q10 — Smoothing
Applies median filter on each RGB channel independently to reduce noise.
```matlab
A = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
S = cat(3, medfilt2(A(:,:,1),[3 3]), medfilt2(A(:,:,2),[3 3]), medfilt2(A(:,:,3),[3 3]));
imshowpair(A, S, 'montage'), title('Original | Smoothed')
```

---

## Q11 — Sharpening
Enhances edges and fine details using unsharp masking.
```matlab
A = imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg");
imshowpair(A, imsharpen(A), 'montage'), title('Original | Sharpened')
```

---

## Q12 — Pseudo Coloring
Maps grayscale intensity ranges to distinct RGB colors, making intensity differences visually distinct.
```matlab
a = double(rgb2gray(imread("C:\Users\khush\OneDrive\Desktop/weird2.jpeg")));
[m,n] = size(a);
out = zeros(m,n,3);
ranges = [0 50; 50 100; 100 150; 150 200; 200 256];
colors = [50 100 10; 35 128 10; 152 130 15; 50 140 25; 128 180 45];
for k = 1:5
    mask = a >= ranges(k,1) & a < ranges(k,2);
    for c = 1:3
        out(:,:,c) = out(:,:,c) + mask .* (a + colors(k,c));
    end
end
subplot(1,2,1), imshow(uint8(a)),   title('Grayscale')
subplot(1,2,2), imshow(uint8(out)), title('Pseudo Colored')
```
