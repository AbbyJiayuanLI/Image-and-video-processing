# Image-and-Video-Processing
This is the collection of my notes on the course Image and Video Processing from Coursera.

## Content
* [Useful Links](##useful-links)
* [1. Introduction](##1-introduction)


## Useful Links
* some interested projects from the course [EE368/CS232: Digital Image Processing](https://web.stanford.edu/class/ee368/index.html) in Stanford University.


## 1. Introduction
* Weber's Law:
    * more sensitive to the change of intensity in dark than bright environment.
    * 图片1
* Mach Band Effect:
    * not constant perceived intensity, dependent on the contrast of two pics
    * 图片2
* Discretization
    * in amplitude
    * in space
* RGB
* Neighborhood
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
* Motivation:
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
* JPEG:
   * Structure: pic1
   * Sub-image: often 8x8
   * Forward Transform:
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
         
   * Quantizer:
   * Symbol Encoder: Huffman Coding 
      * property
         * variant length coding
         * ieterartive binary grouping
      * step
         * re-ordering
         * add smallest two probability (to obtain smallest avg length)
         * prefixing
   * Symboel Decoder:
   * Inverse Transform:
   

