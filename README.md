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
      * **local average**
         * proper window size to avoid blurring
         * **Mean Filtering**
            * mean minimize square error
            * gaussian - weighted average - heat flow
         * **Median Filter**
            * do not blur 
            * median minimize absolute error
      * **non local mean**
         * average of center pixels of similar neighborhoods
         * insight: repeat observing same thing to reduce noise
      * **Derivative**
         * represent derivative in mask form
         * **Laplacian Derivative**: sum of 2nd derivative in x and y direction
         * **Image Sharpening**: add Laplacian(changes) to original image
         * Sharpened = original + Unsharp mask = original + (original-blurred)
      
   
## 4. Image Restoration
   * **Degradation**
      * lost of focus
      * blur by motion
   * **Restoration**: invert degradation and noise
      * multiplicative noise is processed with log
   * **Noise**:
      * Gaussian (mathematical)
      * Rayleigh (real sensor noise)
      * Gamma
      * Exponential (predictive model noise)
      * Uniform （quantization noise)
      * Impulse (salt&pepper noise)
   * Estimation of noise
   * Estimation of degradation function
   * **Wiener Filtering**
      * minimize mean square error
      * filter = H^*/(H^2+Sn/Sf) ~ H^*/(H^2+k)
      * only to estimate degradation and try best k


## 5. Image Segmentation
   * Edge
      * gradient, and ...
   * **Hough Transform**
      * Prior knowledge about shape
      * voting in paramter space
   * **Ostu's Method**
      * minimize weighted within-class variance
      * sliding window to reduce the influence of regional drakness
* Interactive Image Segmentation
   * human scribbles
      * 1 - feature distribution estimation
      * 2 - weighted distance transform
      * 3 - refine by updating new ''scribbles''
* **Graph cut**
   * weight is gradient related
* **Mumford-Shah**
   * penalize for mean square error
   * penalize for edges (total segment lengths)
   

## 6. Geometric PDEs
* continuous space
* general algorithm, complexity in implementation
* **Planar Curve**:
   * derivative: Cs, always unit length
   * curvature: Css = k*n
* **Transformation**:
   * affine
      * area preserve: Cv(tangent), Cvv
      * Cv is generally not tangent to Cvv
      * arc-length: dv=k^1/3*ds
      * curvature: Cvvv = mu * Cv
   * euclidean: rotation + translation
      * length preserve
      * arc-lenfth: ds=|Cp|dp -> |Cs|=1
* **Surface**:
   * S(u,v) = {x=u,y=v,z=(u,v)}
   * normal curvature: kn = <Css, n>
   * principle curvature
      * k1 = max_theta(k)
      * k2 = min_theta(k)
      * k1 is perpendicular to k2
* **Curve Evolution**:
   * dC(p)/dt = V(p,t)
   * tangential velocity do not change geometry (shape)
   * **Euclidean heat flow:** Ct = k*n = Css
   * **Affine heat flow:** Ct = k^1/3*n = <Cvv,n>*n
   * **Constant Flow**: Ct = n
   * **Geodesic Active Contour**: 
      * Ct = (g(x,y)*k - <delta_g(x,y),n>) * n = v*n
      * g = 1/delta_I
* **Level set**
   * C = {(x,y) | phi(x,y)=0}
   * N = - delta_phi/|delta_phi| (不是点的梯度，是函数phi的梯度)
   * k = div(delta_phi/|delta_phi|)
   * dC/dt = V*N  <==>  dphi/dt = V*|delta_phi|
* calculus of variation
   * find function that satisfy min or max
   * **eular lagrange equation**:
* Anistropic Diffusion
* Isotropic Diffusion (heat flow)
   
## 7. Image and Video Inpainting
* recover from degradation
* remove object, or impaint background
* In nature: camouflage, human eyes
* **Impainting**:
   * Input: image, area of interest
   * Reserve boundary: water flow - PDE
      * '''delta_L * N = 0 = dI/dt''' (change of information is 0 in direction)
      * L: information, laplacian (smoothness) = delta_I
      * N: direction, isophote direction (time variant) = (delta_I)T
      * finally: '''dI/dt = delta(delta_I) * (delta_I)T = 0
* Impainting via **calculus of variation**
   * normalized gradient(shape): theta 
* Texture
* Copy&paste: non-local mean, simialr patch
      

## 8. Sparse Modeling and Compressed Sensing

## 9. Medical Imaging
