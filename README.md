

# Image Processing Enhancement Project

This project implements various image processing techniques, including homomorphic filtering, histogram equalization, and wavelet transform-based enhancement. It includes functions to enhance images by improving contrast and reducing noise. The provided script demonstrates the application of these techniques on sample images and compares their results through visual plots and histograms.

## Installation

To run this project, you need to have Python and the following libraries installed:

```bash
pip install numpy opencv-python pywavelets matplotlib
```

## Usage

### Mount Google Drive (for Colab users):

```python
from google.colab import drive
drive.mount('/content/drive', force_remount=True)
```

### Enhance an Image:

Replace `'path_to_image.jpg'` with the actual path to your image.

```python
enhance_image('/content/drive/MyDrive/i/lena_face.jpg')
```

### Process Images with Different Methods:

Load and process an image using various enhancement methods. The script will display the original and enhanced images, along with their histograms.

## Functions

- `block_fft_homomorphic_filtering(image)`: Applies FFT-based homomorphic filtering to an image.
- `homomorphic_filter(image, gammaH=1.5, gammaL=0.5, c=1, D0=30)`: Applies a homomorphic filter to an image.
- `rgb2hsi(rgb_image)`: Converts an RGB image to HSI color space.
- `hsi2rgb(hsi_image)`: Converts an HSI image back to RGB color space.
- `enhance_image(image_path)`: Enhances an image by applying histogram equalization, padding, wavelet transform, and nonlinear filtering.
- `adjust_gamma(image, gamma=1.0)`: Adjusts the gamma of an image.
- `defog_image(image, window_size=15, lambda_=0.2)`: Dehazing algorithm to enhance visibility in foggy images.
- `defog(image)`: Wrapper function for defog_image.
- `histogram_equalization(image)`: Performs histogram equalization on an image.
- `proposed_algorithm(image)`: Applies a sequence of enhancement techniques to an image.
- `load_images_from_zip(zip_path, inner_folder, num_images=3)`: Loads a limited number of images from a specified folder within a zip file.

## Visualization

The script includes functions to display original and enhanced images side-by-side and to plot their histograms for comparison.

## Evaluation Metrics

- **Entropy Calculation**: The script calculates entropy for evaluating image enhancement quality.

## Example

Here's a basic example of how to use the script to enhance an image and visualize the results:

```python
# Replace 'path_to_image.jpg' with the actual path to your image
enhance_image('/content/drive/MyDrive/i/lena_face.jpg')

# Load the image
image_path = '/content/drive/MyDrive/i/lena_face.jpg'
original_image = cv2.imread(image_path, cv2.IMREAD_GRAYSCALE)

# Process images with different methods
images = {
    'Original': original_image,
    'Dark Detail Enhancement': adjust_gamma(original_image, gamma=0.5),
    'Defogging': defog(original_image),
    'Homomorphic Filtering': homomorphic_filter(original_image),
    'Histogram Equalization': histogram_equalization(original_image),
    'Proposed Algorithm': proposed_algorithm(original_image)
}

# Plotting processed images
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(15, 10))
axes = axes.ravel()

for ax, (title, img) in zip(axes, images.items()):
    ax.imshow(img, cmap='gray')
    ax.set_title(title)
    ax.axis('off')

plt.tight_layout()
plt.show()

# Histogram Comparison
fig, axes = plt.subplots(nrows=2, ncols=3, figsize=(15, 10))
axes = axes.ravel()

for ax, (title, img) in zip(axes, images.items()):
    img = np.uint8(img)
    hist = cv2.calcHist([img], [0], None, [256], [0, 256])
    ax.plot(hist)
    ax.set_title(f'{title}')
    ax.set_xlim([0, 256])

plt.tight_layout()
plt.show()
```

---

This `README.md` provides an overview of the project, instructions for installation and usage, descriptions of the functions, visualization techniques, evaluation metrics, and a complete example to demonstrate the use of the script.
