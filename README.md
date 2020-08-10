# Image-and-Video-Processing
This is the collection of my notes on the course Image and Video Processing from Coursera.


## Content
* [Useful Links](#useful-links)
* [1. Introduction](#1-introduction)
* [2. Image and Video Compressing](#2-image-and-video-compressing)
* [3. Spatial Processing](#3-spatial-processing)
* [4. Image Restoration](#4-image-restoration)
* [5. Image Segmentation](#5-image-segmentation)
* [6. Geometric PDEs](#6-geometric-pDEs)
* [7. Image and Video Inpainting](#7-image-and-video-inpainting)
* [8. Sparse Modeling and Compressed Sensing](#8-sparse-modeling-and-compressed-sensing)
* [9. Medical Imaging](#9-medical-imaging)


## Useful Links
* some interested projects from the course [EE368/CS232: Digital Image Processing](https://web.stanford.edu/class/ee368/index.html) in Stanford University.


## 1. Introduction
* **Weber's Law:**
    * more sensitive to the change of intensity in dark than bright environment.
    * 图片1
* **Mach Band Effect:**
    * not constant perceived intensity, dependent on the contrast of two pics
    * 图片2
* **Discretization**
    * in amplitude
    * in space
* **RGB**
* **Neighborhood**
    * 4-neighbor
    ```
       __ __ __ __
       |_|_|*|_|_|
       |_|*|o|*|_|
       |_|_|*|_|_|
       |_|_|_|_|_|
    ```   
    * 8-neighbor
    ```
       __ __ __ __
       |_|*|*|*|_|
       |_|*|o|*|_|
       |_|*|*|*|_|
       |_|_|_|_|_|
   ```
   

## 2. Image and Video Compressing
* **Motivation:**
   * why to do: Large information even for 1000x1000 pic
   * why can do: coding redundancy, spatial redundancy, irrelavant information
* **Image:**
   * Encoder: 
      * mapper
      * quantizer (error)
      * symbol coder
   * Decoder:
      * symbol decoder
      * inverse mapper
* **JPEG:**
   * **Structure**: pic1
   * **Sub-image**: often 8x8
   * **Forward Transform**:
      * Mean Square Error (MSE)
      * Karhunen-Loeve Transform (KLT):
         * only the first one
         * but it is image dependent, therefore slow and not in structure
      * Discrete Cosine Transform (DCT):
         * image independent
         * invertible
         * formula:
            * ![](https://latex.codecogs.com/svg.latex?r(x,%20y,%20u,%20v)%20=%20s(x,%20y,%20u,%20v)%20=%20\alpha(u)\alpha(v)*cos[\frac{(2x+1)u*pi}{2n}]*cos[\frac{(2y+1)v*pi}{2n}])
            * ![](https://latex.codecogs.com/svg.latex?%20\alpha(u)=\left\{\begin{aligned}&\sqrt{1/n}\\&\sqrt{2/n}\end{aligned}\right.)       
   * **Quantizer**:
      * introduce error and also compression
      * type
         * zonal mask
         * zonal bit allocation
         * threshold mask
         * threshould coeffecient ordering sequence (zigzag)
      * uniform quantization in JPEG
   * **Symbol Encoder**: Huffman Coding 
      * property
         * variant length coding
         * ieterartive binary grouping
      * step
         * re-ordering
         * add smallest two probability (to obtain smallest avg length)
         * prefixing
   * **Symboel Decoder**:
   * **Inverse Transform**:
* **JPEG-LS:**
   * predictive lossless compression
   * encode error between prediction and real pixel
   * with many near-zeros which is preferable in Huffman coding
   * core: accurate predictor to produce zeros
* **MPEG:**
   * temporal prediction
* Run length coding
   

## 3. Spatial Processing
   * **Intensity Transformation**
      * pixel-wise 
      * **Equalization**
         * stretch out histogram
         * Ps(s) = Pr(r)*|dr/ds| with s=T(R)
         * s = T(r) = (L-1)*int|0-r(Pr(w)dw)
      * **histogram Matching**
         * map to other histogram distribution other than uniform distribution
         * transformation1 * inv(transformation2)
   * **Spatial Filtering**
      * neighborhood
      * local average
         * proper window size to avoid blurring
         * **Mean Filtering**
            * mean minimize error
            * gaussian - heat flow
      
   
## 4. Image Restoration


## 5. Image Segmentation

## 6. Geometric PDEs

## 7. Image and Video Inpainting

## 8. Sparse Modeling and Compressed Sensing

## 9. Medical Imaging
