# Practical 6 — Transforms

---

## Q1 — Haar Transform
Computes 2D Haar basis matrices using bit-level operations and displays them as images.
```matlab
n = input('Enter basis matrix dimension (power of 2): ');
sn = log2(n);
for u=0:n-1, for v=0:n-1, for x=0:n-1, for y=0:n-1
    p = 0;
    for i=0:sn-1
        bx = bin2dec(dec2bin(x,sn)(sn-i)); by = bin2dec(dec2bin(y,sn)(sn-i));
        bu = bin2dec(dec2bin(u,sn)(sn-i)); bv = bin2dec(dec2bin(v,sn)(sn-i));
        p  = p + (bx*bu + by*bv);
    end
    basis{u+1,v+1}(x+1,y+1) = (-1)^p;
end, end, end, end
k=1;
for i=1:n, for j=1:n
    subplot(n,n,k), imshow(basis{i,j}), k=k+1;
end, end
```

---

## Q2 — Hadamard Transform
Generates an N×N Hadamard matrix recursively using the Sylvester construction.
```matlab
n = input('Enter order (power of 2): ');
H = 1;
while size(H,1) < n
    H = [H H; H -H];
end
disp(H)
imagesc(H), colormap(gray), colorbar, title('Hadamard Matrix')
```

---

## Q3 — Walsh Transform
Computes 2D Walsh basis using sequency-ordered bit operations and displays the basis images.
```matlab
n = input('Enter basis matrix dimension (power of 2): ');
sn = log2(n);
for u=0:n-1, for v=0:n-1, for x=0:n-1, for y=0:n-1
    p = 1;
    for i=0:sn-1
        bx = bin2dec(dec2bin(x,sn)(sn-i)); by = bin2dec(dec2bin(y,sn)(sn-i));
        bu = bin2dec(dec2bin(u,sn)(i+1));  bv = bin2dec(dec2bin(v,sn)(i+1));
        p  = p * (-1)^(bx*bu + by*bv);
    end
    basis{u+1,v+1}(x+1,y+1) = p;
end, end, end, end
k=1;
for i=1:n, for j=1:n
    subplot(n,n,k), imshow(basis{i,j}), k=k+1;
end, end
```

---

## Q4 — DCT Transform
Generates 2D DCT basis images showing frequency components from low to high.
```matlab
n = input('Enter basis matrix dimension: ');
a1 = ones(1,n)*sqrt(2/n); a1(1) = sqrt(1/n);
a2 = a1;
k=1;
for u=0:n-1, for v=0:n-1
    for x=0:n-1, for y=0:n-1
        b{u+1,v+1}(x+1,y+1) = a1(u+1)*a2(v+1)*cos((2*x+1)*u*pi/(2*n))*cos((2*y+1)*v*pi/(2*n));
    end, end
    subplot(n,n,k), imagesc(b{u+1,v+1}), colormap gray, axis off, k=k+1;
end, end
```

---

## Q5 — Slant Transform
Applies a 4×4 Slant transform block-wise to an image to decorrelate pixel data.
```matlab
img = im2double(rgb2gray(imread('C:\Users\khush\OneDrive\Desktop/weird2.jpeg')));
a   = sqrt(2)/sqrt(5);
S4  = [0.5  0.5   0.5   0.5;
       a    a/2  -a/2  -a;
       0.5 -0.5  -0.5   0.5;
       a/2 -a     a    -a/2];
out = blockproc(img,[4 4],@(b) S4*b.data*S4');
subplot(1,2,1), imshow(img),                    title('Original')
subplot(1,2,2), imshow(log(1+abs(out)),[]),     title('Slant Transform')
```

---

## Q6 — KL Transform
Decorrelates data by projecting it onto principal eigenvectors of the covariance matrix.
```matlab
X = input('Enter data matrix (e.g. [1 2 3; 4 5 6]): ');
X0 = X - mean(X,2);
[V,D] = eig(cov(X0'));
[~,idx] = sort(diag(D),'descend');
V = V(:,idx);
disp('Eigenvalues:'),  disp(diag(D)(idx))
disp('KL Transformed:'), disp(V'*X0)
```

---

## Q7 — Z-Transform
Computes and plots the frequency response of a discrete-time system using Z-Transform.
```matlab
b = [1 2 1];
a = [1 -0.5 0.25];
[H, w] = freqz(b, a, 512);
subplot(2,1,1), plot(w/pi, abs(H)),   title('Magnitude'), xlabel('\omega/\pi')
subplot(2,1,2), plot(w/pi, angle(H)), title('Phase'),     xlabel('\omega/\pi')
```

---

## Q8 — SVD Transform
Decomposes a matrix into U, S, V components and reconstructs a low-rank approximation.
```matlab
A = rand(5,4)*10;
[U,S,V] = svd(A);
disp('Singular Values:'), disp(diag(S))
S2 = S; S2(3:end,3:end) = 0;
disp('Rank-2 Approximation:'), disp(U*S2*V')
```

---

## Q9 — Radon Transform
Projects a 2D image at multiple angles to produce a sinogram used in tomographic imaging.
```matlab
I = zeros(100); I(25:75,25:75) = 1;
[R,xp] = radon(I, 0:180);
imshow(R,[],'Xdata',0:180,'Ydata',xp,'InitialMagnification','fit')
xlabel('\theta'), ylabel('x'''), colormap(hot), colorbar, title('Radon Transform')
```
