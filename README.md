# EXP.NO-1: Image-Handling-and-Pixel-Transformations-Using-OpenCV

## NAME: FRANKLIN F

## REG NO: 212224240041

## AIM:

Write a Python program using OpenCV that performs the following tasks:

1. Read and Display an Image.
2. Adjust the brightness of an image.
3. Modify the image contrast.
4. Generate a third image using bitwise operations.

## Software Required:

- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:

### Step 1:

Load an image from your local directory and display it.

### Step 2:

Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:

Create brighter and darker images by adding and subtracting the matrix from the original image.

Display the original, brighter, and darker images.

### Step 4:

Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2.

Display the original, lower contrast, and higher contrast images.

### Step 5:

Split the image into B, G, R components and display the channels.

## Program Developed By:

- **Name:** FRANKLIN F
- **Register Number:** 212224240041

## Ex. No. 01

#### 1. Read the image using OpenCV imread() as a grayscale image.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img = cv2.imread('WhatsApp Image 2026-10-24 at 3.32.56 PM.jpeg')
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 2. Print the image width, height & Channel.

```python
img.shape
```

#### 3. Display the image using matplotlib imshow().

```python
# Convert RGB to GRAY
image_gray = cv2.cvtColor(img_rgb, cv2.COLOR_RGB2GRAY)

# Grayscale Image
plt.imshow(image_gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis("off")
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().

```python
img = cv2.imread('WhatsApp Image 2026-10-24 at 3.32.56 PM.jpeg')
cv2.imwrite('output.png', img)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().

```python
# Read the image using OpenCV
img = cv2.imread('output.png', cv2.IMREAD_COLOR)

# Change it to colour image
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.

```python
# Display the image using Matplotlib
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis('off')
plt.show()

img.shape
```

#### 7. Crop the image to extract a specific object from the image.

```python
crop = img_rgb[0:450, 200:550]

plt.imshow(crop)
plt.title("Cropped Region")
plt.axis("off")
plt.show()

crop.shape
```

#### 8. Resize the image up by a factor of 2x.

```python
res = cv2.resize(crop, (crop.shape[1]*2, crop.shape[0]*2))

plt.imshow(res)
plt.title("Resized Image")
plt.axis("off")
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.

```python
flipped_horizontally = cv2.flip(res, 1)

plt.imshow(flipped_horizontally)
plt.title("Flipped Horizontally")
plt.axis("off")
plt.show()
```

#### 10. Read in the image.

```python
img_app = cv2.imread(
    'WhatsApp Image 2026-10-24 at 3.32.56 PM.jpeg',
    cv2.IMREAD_COLOR
)

img_rgb = cv2.cvtColor(img_app, cv2.COLOR_BGR2RGB)
img_rgb.shape
```

#### 11. Add text to the bottom of the image (centered on the image).

```python
text = cv2.putText(
    img_rgb,
    "Image Processing Using OpenCV",
    (50, img_rgb.shape[0]-20),
    cv2.FONT_HERSHEY_SIMPLEX,
    1,
    (255, 255, 255),
    2
)

plt.imshow(text)
plt.title("New Image")
plt.show()
```

#### 12. Draw a magenta rectangle around the selected object.

```python
rcol = (255, 0, 255)

cv2.rectangle(
    img_rgb,
    (50, 50),
    (300, 300),
    rcol,
    3
)
```

#### 13. Display the final annotated image.

```python
plt.title("Annotated Image")
plt.imshow(img_rgb)
plt.axis("off")
plt.show()
```

#### 14. Read the image.

```python
img = cv2.imread(
    'WhatsApp Image 2026-10-24 at 3.32.56 PM.jpeg',
    cv2.IMREAD_COLOR
)

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
```

#### 15. Adjust the brightness of the image.

```python
m = np.ones(img_rgb.shape, dtype="uint8") * 50
```

#### 16. Create brighter and darker images.

```python
img_brighter = cv2.add(img_rgb, m)
img_darker = cv2.subtract(img_rgb, m)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).

```python
plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(img_darker)
plt.title("Darker Image")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(img_brighter)
plt.title("Brighter Image")
plt.axis("off")

plt.show()
```

#### 18. Modify the image contrast.

```python
matrix1 = np.ones(img_rgb.shape, dtype="float32") * 1.1
matrix2 = np.ones(img_rgb.shape, dtype="float32") * 1.2

img_higher1 = cv2.multiply(
    img_rgb.astype("float32"), matrix1
).clip(0,255).astype("uint8")

img_higher2 = cv2.multiply(
    img_rgb.astype("float32"), matrix2
).clip(0,255).astype("uint8")
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).

```python
plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(img_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(img_higher1)
plt.title("Higher Contrast (1.1x)")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(img_higher2)
plt.title("Higher Contrast (1.2x)")
plt.axis("off")

plt.show()
```

#### 20. Split the image into B, G, R components & Display the channels.

```python
b, g, r = cv2.split(img_rgb)

plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(b, cmap='gray')
plt.title("Blue Channel")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(g, cmap='gray')
plt.title("Green Channel")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(r, cmap='gray')
plt.title("Red Channel")
plt.axis("off")

plt.show()
```

#### 21. Merge the R, G, B channels and display.

```python
merged_rgb = cv2.merge([r, g, b])

plt.figure(figsize=(5,5))
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis("off")
plt.show()
```

#### 22. Split the image into H, S, V components & Display the channels.

```python
hsv_img = cv2.cvtColor(img_rgb, cv2.COLOR_RGB2HSV)

h, s, v = cv2.split(hsv_img)

plt.figure(figsize=(10,5))

plt.subplot(1,3,1)
plt.imshow(h, cmap='gray')
plt.title("Hue Channel")
plt.axis("off")

plt.subplot(1,3,2)
plt.imshow(s, cmap='gray')
plt.title("Saturation Channel")
plt.axis("off")

plt.subplot(1,3,3)
plt.imshow(v, cmap='gray')
plt.title("Value Channel")
plt.axis("off")

plt.show()
```

#### 23. Merge the H, S, V channels and display along with original image.

```python
merged_hsv = cv2.cvtColor(
    cv2.merge([h, s, v]),
    cv2.COLOR_HSV2RGB
)

combined = np.concatenate((img_rgb, merged_hsv), axis=1)

plt.figure(figsize=(10,5))
plt.imshow(combined)
plt.title("Original Image & Merged HSV Image")
plt.axis("off")
plt.show()
```

## Output:
<img width="375" height="498" alt="image" src="https://github.com/user-attachments/assets/a99685cf-69f0-4945-b62e-78d92acf56d6" />
<img width="367" height="497" alt="image" src="https://github.com/user-attachments/assets/cbb85dee-14f0-4f65-bc30-d2f488d1964c" />
<img width="367" height="507" alt="image" src="https://github.com/user-attachments/assets/6737492b-d320-4301-a31d-02bbb33e82af" />
<img width="365" height="502" alt="image" src="https://github.com/user-attachments/assets/9fc9f707-9a9c-4e6b-9f56-7ae78a7476a4" />
<img width="357" height="492" alt="image" src="https://github.com/user-attachments/assets/285271b4-caec-4518-b33d-76ecdf97ef64" />
<img width="360" height="496" alt="image" src="https://github.com/user-attachments/assets/38ff4326-5aca-45f3-8ede-06ecec270fe1" />
<img width="370" height="492" alt="image" src="https://github.com/user-attachments/assets/222c6c94-0fb9-447b-95f3-c40fba2dae0f" />
<img width="371" height="502" alt="image" src="https://github.com/user-attachments/assets/1dd60e46-957e-4551-af48-8d475698d550" />
<img width="362" height="496" alt="image" src="https://github.com/user-attachments/assets/ff7f335f-291c-438a-8876-ee15dd6ef5fa" />
<img width="363" height="491" alt="image" src="https://github.com/user-attachments/assets/06365ee6-8581-4c0f-a088-4aca605bf410" />
<img width="377" height="505" alt="image" src="https://github.com/user-attachments/assets/dce170d0-2fa1-4aca-b31c-c0559ec0e738" />
<img width="590" height="506" alt="image" src="https://github.com/user-attachments/assets/736947cb-9685-4362-8d04-4fcfbcebb6d6" />
<img width="482" height="515" alt="image" src="https://github.com/user-attachments/assets/2ff808ad-8d8d-40ee-819b-af108bc69783" />
<img width="383" height="517" alt="image" src="https://github.com/user-attachments/assets/6a60d4e5-8d01-423e-b47e-1ebf4df21e2d" />
<img width="390" height="490" alt="image" src="https://github.com/user-attachments/assets/46093c9d-5f5d-4e48-9399-6abce1cb65b8" />


## Result:

Thus, the images were read, displayed, cropped, resized, flipped, annotated, brightness and contrast adjustments were made, and colour channel splitting and merging operations were performed successfully using the Python program.
