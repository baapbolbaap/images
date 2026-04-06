# Practical 2 — Image Processing Commands

---

## Q1 — sliceViewer Command
Displays image slices interactively with a parula colormap using `sliceViewer`.
```matlab
sliceViewer(imread('weird.jpg'), 'Colormap', parula(6))
```

---

## Q2 — imcrop Command
Interactively crops a selected region from an image using `imcrop`.
```matlab
imshow(imcrop(imread('weird.jpg')))
```

---

## Q3 — imrotate Command
Rotates an image by 180° using bicubic interpolation with cropping.
```matlab
imshow(imrotate(imread('weird.jpg'), -180, 'bicubic', 'crop'))
```

---

## Q4 — rescale Command
Rescales image pixel intensities to the [0, 1] range using `rescale`.
```matlab
imshow(rescale(imread('weird.jpg')))
```

---

## Q5 — 2D Viewer & 3D Viewer Command
Displays an image in both 3D and 2D interactive viewers using `viewer3d` and `viewer2d`.
```matlab
imshow(imrotate(imread('weird.jpg'), -180, 'bicubic', 'crop'))
imageshow('weird.jpg', Parent=viewer3d)
imageshow('weird.jpg', Parent=viewer2d)
```

---

## Q6 — immovie & implay Command
Creates and plays a movie from MRI volume data using `immovie` and `implay`.
```matlab
load mri
implay(immovie(D, map))
```

---

## Q7 — zoom Command
Enables interactive zoom on a displayed image using `zoom on`.
```matlab
imshow(imread('weird.jpg')), zoom on
```

---

## Q8 — colormap Command
Applies a parula colormap with a colorbar to a grayscale image.
```matlab
imshow(rgb2gray(imread('weird.jpg'))), colormap(parula), colorbar
```

---

## Q9 — colorbar Command
Displays a labeled colorbar indicating pixel intensity scale on a grayscale image.
```matlab
gray = rgb2gray(imread('weird.jpg'));
imshow(gray), colormap(parula)
cb = colorbar; cb.Label.String = 'Pixel Intensity';
```

---

## Q10 — mesh Command
Renders a 3D mesh plot of image intensity values using `mesh`.
```matlab
gray = rgb2gray(imread('weird.jpg'));
[X, Y] = meshgrid(1:size(gray,2), 1:size(gray,1));
mesh(X, Y, double(gray)), colormap(jet), colorbar
```
