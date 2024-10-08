## Concept of Singular Value Decomposition (SVD)

For an image represented as a matrix `X` of size `nx × ny`, SVD decomposes `X` into three matrices:

`X = U ⋅ S ⋅ V^T`

Where:

- **`U`** is an `nx × nx` matrix of left singular vectors.
- **`S`** is an `nx × ny` diagonal matrix containing singular values in decreasing order.
- **`V^T`** is an `ny × ny` matrix of right singular vectors.

### Singular Values:
- The singular values in **\( S \)** represent the importance of the corresponding components of the image.
- Larger singular values capture more significant information, while smaller ones capture finer details or noise.

### Rank (r):
- The rank `r` refers to the number of singular values used to approximate the original image.
- By using a smaller `r`, you retain the most significant components, discarding the less important details, which leads to compression.

## How the Code Works

### 1. Load the Image and Convert to Grayscale:
- The input image (RGB) is converted to a grayscale matrix \( X \), which has intensity values between 0 and 255.
- The matrix \( X \) is of size \( nx \times ny \), representing the pixel intensities of the image.

### 2. Perform SVD on the Grayscale Image:
- The grayscale matrix \( X \) is decomposed into three matrices: \( U \), \( S \), and \( V^T \) using the SVD.
- The matrix \( S \) contains the singular values, which are used to approximate the image.

### 3. Image Approximation using `r` Singular Values:
- By selecting a smaller number of singular values (rank `r`), we can create a compressed version of the original image:
  \[
  X_{\text{approx}} = U[:, 1:r] \cdot S[1:r, 1:r] \cdot V^T[:, 1:r]
  \]
- Several approximations are generated using different values of `r` (e.g., `r = 5`, `r = 20`, `r = 100`), and the corresponding images are displayed.

### 4. Visualize the Singular Values and Cumulative Energy:
- A semilogarithmic plot shows the magnitude of singular values in decreasing order.
- A cumulative energy plot shows how much of the total image information is captured by using `r` singular values.

###  Singular Values Plot (Semilogarithmic Plot)

**Purpose**: To visualize the relative importance of each singular value.

- **X-axis**: Index of the singular values (from 1 to `min(nx, ny)`).
- **Y-axis**: The magnitude of singular values (on a logarithmic scale).

**Interpretation**:
- The plot shows how the singular values decrease rapidly.
- The first few singular values are large, representing most of the important information in the image.
- The smaller singular values contribute less and are often related to finer details or noise.

**Key Insight**: Most of the image's content can be captured by just the first few singular values, leading to potential compression by ignoring the smaller values.

###  Cumulative Energy Plot

**Purpose**: To illustrate how much of the total image information is captured by using `r` singular values.

- **X-axis**: Number of singular values used (`r`).
- **Y-axis**: Cumulative percentage of total energy (information) captured.
