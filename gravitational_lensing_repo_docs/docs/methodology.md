# Methodology and implementation notes

## Scope

The code implements an image-processing demonstration inspired by gravitational-lensing imagery. It applies several image enhancement operations, detects thresholded regions, estimates a center from contour centroids, and performs a simplified radial remapping.

## Processing stages

### 1. Image loading and resizing
Images are read in grayscale and resized to 128 × 128 pixels. The current script uses local filenames `abc.jpg` and `def.jpeg`.

### 2. Bias subtraction
A constant value of 15 is subtracted using OpenCV's image arithmetic.

### 3. Dark-frame subtraction (simulated)
A random array sampled from a normal distribution (mean 10, standard deviation 2) is generated and subtracted. This is synthetic noise, not a measured dark frame.

### 4. Flat-field operation
The code creates a uniform-valued image, applies Gaussian blur, normalizes it, and divides the image by the result. Since the generated field is uniform, this does not represent correction using a measured detector flat.

### 5. Median filtering
A 3 × 3 median filter is applied to reduce local image noise.

### 6. Wiener deconvolution
A 5 × 5 Gaussian kernel is used as the PSF, and a Fourier-domain Wiener-style filter is applied with a balance parameter of 0.01. The implementation should be validated against known test images and a clearly defined PSF convention.

### 7. Image stacking (simulated)
Three noisy versions of the current image are generated and averaged. These are synthetic variants, not separate astronomical exposures.

### 8. Background subtraction
A Gaussian-blurred version of the image is subtracted from the image to estimate and remove a smooth background component.

### 9. Source detection
A fixed threshold of 30 is applied, and external contours are extracted. The detected contours are drawn for visualization.

### 10. Lens-center estimation
Contours with area greater than 10 are used to compute centroids. The coordinate-wise median of those centroids is returned as the estimated center. This method is a heuristic and is not a physical lens-model fit.

### 11. Simplified delensing
The code applies a radial coordinate remapping around the estimated center using a strength parameter. This is a simplified distortion operation and should not be described as a physically validated gravitational lens inversion.

## Reproducibility and failure cases

- Synthetic noise is random; the code does not fix a random seed.
- The current input loading has no explicit check for missing or unreadable files.
- Lens-center estimation can fail if no qualifying contours exist.
- The code repeats the pipeline for two input images.
- The current implementation should be tested and reviewed before drawing scientific conclusions.

## Validation recommended

A stronger research implementation would document input provenance, compare against appropriate baseline methods, test on controlled synthetic lens examples with known parameters, report quantitative metrics, and distinguish simulated demonstrations from observational results.
