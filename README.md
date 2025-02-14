Image Compression Using Discrete Wavelet Transform (DWT)

Overview

This MATLAB script compresses a grayscale image using Discrete Wavelet Transform (DWT). The process involves:

1. Wavelet Decomposition: Splitting the image into different frequency subbands.


2. Thresholding: Removing insignificant coefficients to reduce data.


3. Quantization: Reducing precision to save space.


4. Run-Length Encoding (RLE): Compressing repeated values.


5. Huffman Encoding: Further compression using optimal coding.


6. Saving the Compressed Data: Writing the compressed image to a file.




---

Steps & Inputs

1. Load the Image

X = imread('bwimg.bmp');
figure; imshow(X);

The image must be grayscale (bwimg.bmp).

Ensure the file is in the working directory.


2. Choose a Wavelet

wav = 'bior4.4'; % Default wavelet

Modify wav for different wavelets (e.g., haar, db4, sym3).


3. Set Decomposition Level

N = input('Input Number of Levels (Decomposition Level)\n N=');

Defines how many times DWT is applied.


4. Apply Wavelet Decomposition

[C, S] = wavedec2(X, N, wav);

C: Wavelet coefficients.

S: Structure for reconstruction.


5. Thresholding

TH = input('TH='); % Set the threshold

Coefficients below TH are set to zero.

Helps achieve better compression.


6. Quantization

Q = 8; % Number of bits for coding

Maps coefficients to Q-bit values.


7. Run-Length Encoding (RLE)

Xrlee = rle(CQ);

Replaces repeated values with shorter representations.


8. Huffman Encoding

[dict, avglen] = huffmandict([0:2^Q-1], Xfreq);
code = huffmanenco(Xrle, dict);

Uses Huffman coding to assign short codes to frequent values.


9. Save the Compressed Image

f = fopen('fichier.bmp', 'w');
fwrite(f, fichier, 'ubit8');
fclose(f);

Stores the compressed image in fichier.bmp.



---

Outputs

Compressed Image: fichier.bmp

Compression Statistics:

TC = MX * NX / length(fichier); % Compression ratio
GC = 100 * (1 - 1/TC); % Compression gain

Higher TC → Better compression

Higher GC → More space saved




---

Notes

Lossy compression: Some data is lost due to thresholding.

Works best with grayscale images.

To decompress, you need to reverse Huffman decoding, RLE decoding, inverse quantization, and inverse DWT.



---

This script efficiently compresses images while preserving important details using DWT-based compression techniques.


