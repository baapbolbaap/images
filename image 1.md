# Practical 1 — Basic MATLAB Functions for Image Processing

---

## Q1 — imread Function
Reads an image from file and displays it using `imread` and `imshow`.
```matlab
imshow(imread('weird.jpg'))
```

---

## Q2 — imfinfo Function
Retrieves and displays metadata of an image file using `imfinfo`.
```matlab
disp(imfinfo('weird.jpg'))
```

---

## Q3 — size Function
Returns the dimensions (rows, columns, channels) of an image array.
```matlab
size(imread('weird.jpg'))
```

---

## Q4 — imshow Function
Displays an image in a MATLAB figure window using `imshow`.
```matlab
imshow(imread('weird.jpg'))
```

---

## Q5 — whos Function
Displays memory size and data type information of the image variable.
```matlab
img = imread('weird.jpg'); whos img
```

---

## Q6 — rgb2gray Function
Converts a color RGB image to a grayscale image using `rgb2gray`.
```matlab
imshow(rgb2gray(imread('weird.jpg')))
```

---

## Q7 — Line Plotting Command
Plots a 2D line graph for given x and y data points using `plot`.
```matlab
plot([1.2 3 4], [3 2 7])
```

---

## Q8 — imbinarize Command
Converts a grayscale image to a binary (black & white) image using `imbinarize`.
```matlab
imshow(imbinarize(rgb2gray(imread('weird.jpg'))))
```
