# Gravitational Lensing Image Preprocessing Pipeline

A Python-based Student Internship Project (SIP) exploring image preprocessing, source detection, lens-center estimation, and simplified radial remapping for gravitational-lensing imagery.

## Repository contents

- `SIP_Project.py` — Python implementation of the processing pipeline.
- `SIP_Project.ipynb` — Jupyter/Google Colab notebook version (add this file to the repository).
- `requirements.txt` — Python dependencies.
- `docs/methodology.md` — Overview of the implemented methods and their limitations.
- `data/README.md` — Notes on input images and provenance.
- `LICENSE` — MIT License template; review the author and year before publishing.
- `.gitignore` — Common Python and notebook exclusions.

## Implemented workflow

1. Load a grayscale image and resize it to 128 × 128.
2. Apply a fixed bias subtraction.
3. Apply simulated dark-frame subtraction using random noise.
4. Apply a flat-field operation using a generated uniform field.
5. Apply median filtering.
6. Apply Wiener deconvolution using a Gaussian-shaped point spread function (PSF).
7. Simulate image stacking by adding synthetic noise to copies and averaging.
8. Estimate and subtract a blurred background.
9. Detect bright regions using thresholding and contours.
10. Estimate a lens center from qualifying contour centroids and apply a simplified radial remapping.

## Requirements

Python 3.9 or later is a suggested starting point. Install the packages listed in `requirements.txt`:

```bash
python -m pip install -r requirements.txt
```

## Running

The current script expects input images named `abc.jpg` and `def.jpeg` in its working directory. Those image files are not included in this repository.

After obtaining appropriate input images and placing them where the script expects them, run:

```bash
python SIP_Project.py
```

Alternatively, open `SIP_Project.ipynb` in Jupyter or Google Colab and run its cells after updating image paths as needed.

## Inputs and reproducibility

The original input images are currently unavailable. See [`data/README.md`](data/README.md). Some stages use random synthetic noise, so outputs can vary between runs. The current code does not set a random seed.

## Important limitations

- Dark-frame subtraction and stacking are simulated, not based on measured calibration frames or independent telescope exposures.
- The flat-field image is generated as a uniform field; it does not model measured detector sensitivity variations.
- The lens-center estimator depends on detected contours and may fail if no suitable contours are found.
- The radial remapping is a simplified image-warping operation, not a validated physical inversion of a gravitational lens equation.
- The script includes duplicated pipeline code for two images and should be tested with valid input files before relying on its output.
- This repository documents the current implementation; it does not claim scientific validation or quantitative reconstruction accuracy.

## Suggested next steps

- Add the original input images if you have permission to redistribute them, or document their source and retrieval procedure.
- Test from a clean Python environment.
- Record package versions and any random seeds used for reported results.
- Add representative output figures and explain how they were generated.
- Validate the processing methods against appropriate astronomical data and reference methods before making scientific performance claims.

## Author

[Your name]

## Acknowledgements

[Project guide, institution, data providers, and relevant literature]
