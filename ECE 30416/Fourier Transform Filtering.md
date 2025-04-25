# ECE 30416 Fourier Transform Filtering

## Overview
Fourier Transform Filtering is a foundational technique in optics that leverages the spatial frequency domain to manipulate or analyze images 
and wavefronts. It’s based on the principle that any optical field or image can be decomposed into sinusoidal components using the Fourier 
transform. By applying filters in the frequency domain, we can emphasize or suppress specific features of an image—such as edges, patterns, 
or blur.

This technique is widely used in optical image processing, pattern recognition, microscopy, and even in analog computing systems. Fourier filtering bridges optics with signal processing and gives us physical insight into how lenses, apertures, and wavefronts behave.

 - **Motivation:**
    In real-world optical systems, we often need to enhance certain image features or suppress unwanted noise. Traditional filtering in the spatial domain can be computationally expensive or inaccurate at optical resolutions. Fourier filtering provides a physical and intuitive way to process information—by simply placing filters in the Fourier (frequency) plane of an optical system. This is particularly useful in lens-based systems, where the back focal plane naturally contains the Fourier transform of the input field.

## Key Concepts & Definitions
- **Fourier Transform (FT):** A mathematical tool that decomposes a signal or optical field into its constituent frequencies. In optics, it relates spatial domain information to spatial frequency.

- **Spatial Frequency:** Describes how often features repeat per unit distance in an image; high frequencies correspond to fine details or noise, while low frequencies represent broad structures.

- **Frequency Domain Filtering:** The process of modifying an image by applying masks (filters) in the Fourier domain, often by physically blocking or passing certain frequency components.

- **4f System:** An optical setup using two lenses to perform the Fourier transform and its inverse. Filters are inserted at the Fourier plane, located at the shared focal points between the lenses.

## Theory 
In a coherent imaging system, when a beam of light passes through a lens, the field at the back focal plane is proportional to the Fourier transform of the input field at the front focal plane. This forms the foundation of Fourier optics.

### 4f Optical System
A 4f system uses two lenses, each with focal length 𝑓, separated by a distance of 2𝑓. The object placed at the front focal plane of the first lens will have its Fourier transform appear at the back focal plane (frequency plane), where filters can be applied.

#### Low-Pass vs. High-Pass Filters
Low-pass filter: Blocks high spatial frequencies, allowing only smooth variations. Used to reduce noise or blur images.
High-pass filter: Blocks low spatial frequencies, enhancing edges or fine details.

$$\mathcal{F}\{f(x,y)\} = F(u,v)$$

Where:
- 𝑓(𝑥,𝑦) is the **spatial domain function** (the image)
- 𝐹(𝑢,𝑣) is the **frequency domain representation**

By modifying 𝐹(𝑢,𝑣) through a filter 𝐻(𝑢,𝑣), and then applying the inverse Fourier transform, we obtain a filtered image:

$$
g(x, y) = \mathcal{F}^{-1} \left[ F(u, v) \cdot H(u, v) \right]
$$

### Application
#### Example: Optical Edge Detection
By placing a high-pass filter in the Fourier plane of a 4f system, we can highlight edges and fine structures in an image. This is done by blocking or attenuating the central (low-frequency) components and letting peripheral (high-frequency) components pass through.

##### Experimental Setup:
    - Collimated laser illuminates a transparency (e.g., image or mask).

    - First lens performs a Fourier transform.

    - At the Fourier plane (between the two lenses), insert a spatial filter (e.g., a ring or grid).

    - Second lens performs an inverse Fourier transform.

    - CCD or screen captures the filtered output image.

    This setup can be used for:
        - Biomedical imaging (highlighting cellular structures)

        - Optical encryption/decryption systems

        - Removing periodic noise from images

### Example Exercises
- Draw and label the complete 4f system. Indicate object plane, Fourier plane, and image plane.

- Design circular low-pass and high-pass filters for a 4f system. Show how they would block or pass certain frequency ranges.

- Simulate Fourier filtering in MATLAB or Python by taking the FFT of an image, applying a filter mask, and then taking the inverse FFT.

- Given an input image with high-frequency noise, describe how to construct an appropriate optical filter to suppress the noise while preserving image content.

- Explore the effect of a grid filter that blocks periodic horizontal or vertical frequencies. What kind of patterns does this emphasize or eliminate?

### Extra Notes
Fourier transform filtering is linear and shift-invariant, meaning it preserves linearity and does not distort the relative positioning of features.

Lenses naturally perform Fourier transforms under certain conditions (paraxial approximation), which allows us to process images optically with no digital computation.

You can extend this concept to holography, phase contrast imaging, and even optical correlators used in facial recognition or fingerprint matching.