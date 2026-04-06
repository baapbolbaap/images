# Practical 10 — Image Segmentation & Compression

---

## Q1 — Basic Segmentation
Segments an image by thresholding the Cb channel after converting to YCbCr color space.
```matlab
a = imread('weird.jpg');
mask = rgb2ycbcr(a)(:,:,2) > 120;
subplot(1,2,1), imshow(a), title('Original')
subplot(1,2,2), imshow(mask), title('Segmented')
```

---

## Q2 — Edge Detection with Its Types
Applies six edge detection methods (Sobel, Prewitt, Roberts, Canny, LoG, Zero-Cross) on each RGB channel.
```matlab
A = im2double(imread('weird2.jpeg'));
R = A(:,:,1); G = A(:,:,2); B = A(:,:,3);
ce = @(m) edge(R,m) | edge(G,m) | edge(B,m);
h = fspecial('log',[5 5],0.5);
zc = edge(imfilter(R,h),'zerocross') | edge(imfilter(G,h),'zerocross') | edge(imfilter(B,h),'zerocross');
subplot(2,3,1), imshow(ce('sobel')),   title('Sobel')
subplot(2,3,2), imshow(ce('prewitt')), title('Prewitt')
subplot(2,3,3), imshow(ce('roberts')), title('Roberts')
subplot(2,3,4), imshow(ce('canny')),   title('Canny')
subplot(2,3,5), imshow(ce('log')),     title('LoG')
subplot(2,3,6), imshow(zc),            title('Zero-Cross')
```

---

## Q3 — Hough Transform
Detects lines in an image by applying Canny edge detection followed by the Hough Transform.
```matlab
RGB = imread('weird2.jpeg');
BW = edge(rgb2gray(RGB), 'canny');
[H,T,R] = hough(BW, 'RhoResolution', 0.5, 'Theta', -90:0.5:89);
subplot(2,1,1), imshow(RGB), title('Original')
subplot(2,1,2), imshow(imadjust(rescale(H)), 'XData', T, 'YData', R, 'InitialMagnification', 'fit')
xlabel('\theta'), ylabel('\rho'), title('Hough Transform')
axis on, axis normal, colormap('hot')
```

---

## Q4 — Run Length Encoding
Encodes a sequence by counting consecutive repeated values, or decodes it back to the original.
```matlab
choice = input('Enter 1 for Encoding, 2 for Decoding: ');
if choice == 1
    a = input('Enter the array: ');
    b = []; c = 1;
    for i = 1:length(a)-1
        if a(i) == a(i+1), c = c+1;
        else, b = [b c a(i)]; c = 1; end
    end
    disp('Encoded:'), disp([b c a(end)])
elseif choice == 2
    a = input('Enter encoded array: ');
    u = [];
    for i = 1:2:length(a), u = [u repmat(a(i+1), 1, a(i))]; end
    disp('Decoded:'), disp(u)
else
    disp('Invalid choice')
end
```

---

## Q5 — Huffman Encoding
Builds a Huffman dictionary from symbol probabilities, encodes a signal, then decodes and verifies it.
```matlab
symbols = [1 2 3]; probs = [0.1 0.1 0.8];
[dict, avglen] = huffmandict(symbols, probs);
disp(dict), disp(['Avg Length: ' num2str(avglen)])
sig = [3 3 1 3 3 3 3 3 3 2 3 1];
enc = huffmanenco(sig, dict);
dec = huffmandeco(enc, dict);
disp(['Bits: ' num2str(length(enc))])
disp(['Match: ' num2str(isequal(sig, dec))])
```
