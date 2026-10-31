# Image-Handling-and-Pixel-Transformations-Using-OpenCV
# Program Developed By:
# Name:FRANKLIN .F
# Register Number:212224240041
## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:

### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image. Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2.

### Step 5:
Split the image into B, G, R components and display the channels.


### Ex. No. 01

#### 1. Read the image using OpenCV imread() as a grayscale image.

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

img_gray = cv2.imread('WIN_20260508_10_13_05_Pro.jpg', cv2.IMREAD_GRAYSCALE)

plt.imshow(img_gray, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')
plt.show()
```

#### 2. Print the image width, height & Channel.

```python
height, width = img_gray.shape

print("Width:", width)
print("Height:", height)
print("Channel: 1")
```

#### 3. Display the image using matplotlib imshow().

```python
plt.figure(figsize=(8, 6))
plt.imshow(img_gray, cmap='gray')
plt.title("Original Grayscale Image")
plt.axis('off')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().

```python
cv2.imwrite('output.png', img_gray)

print("Image saved successfully")
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().

```python
img_color = cv2.cvtColor(img_gray, cv2.COLOR_GRAY2BGR)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.

```python
height, width, channel = img_color.shape

print("Width:", width)
print("Height:", height)
print("Channel:", channel)

plt.imshow(cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB))
plt.title("Colour Image")
plt.axis('off')
plt.show()
```

#### 7. Crop the image to extract any specific object from the image.

```python
img = cv2.imread('WIN_20260508_10_13_05_Pro.jpg')

height, width = img.shape[:2]

crop = img[0:height//2, 0:width//2]

plt.imshow(cv2.cvtColor(crop, cv2.COLOR_BGR2RGB))
plt.title("Cropped Image")
plt.axis('off')
plt.show()
```

#### 8. Resize the image up by a factor of 2x.

```python
resized = cv2.resize(
    crop,
    None,
    fx=2,
    fy=2,
    interpolation=cv2.INTER_LINEAR
)

plt.imshow(cv2.cvtColor(resized, cv2.COLOR_BGR2RGB))
plt.title("Resized Image")
plt.axis('off')
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.

```python
flipped = cv2.flip(resized, 1)

plt.imshow(cv2.cvtColor(flipped, cv2.COLOR_BGR2RGB))
plt.title("Horizontally Flipped Image")
plt.axis('off')
plt.show()
```

#### 10. Read in the image.

```python
apollo_img = cv2.imread('WIN_20260508_10_13_05_Pro.jpg')

plt.imshow(cv2.cvtColor(apollo_img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')
plt.show()
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image).

```python
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

font_scale = 2
thickness = 2

height, width = apollo_img.shape[:2]

text_size = cv2.getTextSize(
    text, font_face, font_scale, thickness
)[0]

text_x = (width - text_size[0]) // 2
text_y = height - 20

cv2.putText(
    apollo_img,
    text,
    (text_x, text_y),
    font_face,
    font_scale,
    (255, 255, 255),
    thickness,
    cv2.LINE_AA
)
```

#### 12. Draw a magenta rectangle that encompasses the selected object.

```python
rect_color = (255, 0, 255)

height, width = apollo_img.shape[:2]

x1 = width // 4
y1 = height // 4
x2 = 3 * width // 4
y2 = 3 * height // 4

cv2.rectangle(
    apollo_img,
    (x1, y1),
    (x2, y2),
    rect_color,
    3
)
```

#### 13. Display the final annotated image.

```python
plt.figure(figsize=(10, 7))

plt.imshow(cv2.cvtColor(apollo_img, cv2.COLOR_BGR2RGB))
plt.title("Final Annotated Image")
plt.axis('off')
plt.show()
```

#### 14. Read the image.

```python
img = cv2.imread('WIN_20260508_10_13_05_Pro.jpg')

plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')
plt.show()
```

#### 15. Adjust the brightness of the image.

```python
# Create a matrix of ones (with data type float64)

matrix_ones = np.ones(img.shape, dtype=np.float64)

matrix = matrix_ones * 50
```

#### 16. Create brighter and darker images.

```python
img_brighter = cv2.add(img.astype(np.float64), matrix)
img_darker = cv2.subtract(img.astype(np.float64), matrix)

img_brighter = np.clip(img_brighter, 0, 255).astype(np.uint8)
img_darker = np.clip(img_darker, 0, 255).astype(np.uint8)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).

```python
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title("Darker Image")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title("Brighter Image")
plt.axis('off')

plt.show()
```

#### 18. Modify the image contrast.

```python
# Create two higher contrast images using scaling factors
# of 1.1 and 1.2

matrix1 = np.ones(img.shape, dtype=np.float64) * 1.1
matrix2 = np.ones(img.shape, dtype=np.float64) * 1.2

img_higher1 = cv2.multiply(img.astype(np.float64), matrix1)
img_higher2 = cv2.multiply(img.astype(np.float64), matrix2)

img_higher1 = np.clip(img_higher1, 0, 255).astype(np.uint8)
img_higher2 = np.clip(img_higher2, 0, 255).astype(np.uint8)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).

```python
plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB))
plt.title("Contrast 1.1")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB))
plt.title("Contrast 1.2")
plt.axis('off')

plt.show()
```

#### 20. Split the image into B, G, R components & Display the channels.

```python
b, g, r = cv2.split(img)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap='gray')
plt.title("Blue Channel")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(g, cmap='gray')
plt.title("Green Channel")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(r, cmap='gray')
plt.title("Red Channel")
plt.axis('off')

plt.show()
```

#### 21. Merge the R, G, B, displays along with the original image.

```python
merged_rgb = cv2.merge((r, g, b))

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(merged_rgb)
plt.title("Merged RGB Image")
plt.axis('off')

plt.show()
```

#### 22. Split the image into H, S, V components & Display the channels.

```python
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

h, s, v = cv2.split(hsv)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap='gray')
plt.title("Hue Channel")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(s, cmap='gray')
plt.title("Saturation Channel")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(v, cmap='gray')
plt.title("Value Channel")
plt.axis('off')

plt.show()
```

#### 23. Merge the H, S, V, displays along with original image.

```python
merged_hsv = cv2.merge((h, s, v))

merged_bgr = cv2.cvtColor(
    merged_hsv,
    cv2.COLOR_HSV2BGR
)

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title("Merged HSV Image")
plt.axis('off')

plt.show()
```

#### 24. Generate a third image using bitwise operations.

```python
mask = np.zeros(img.shape[:2], dtype=np.uint8)

cv2.rectangle(
    mask,
    (100, 100),
    (300, 300),
    255,
    -1
)

img_bitwise = cv2.bitwise_and(
    img,
    img,
    mask=mask
)

plt.figure(figsize=(15, 5))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(mask, cmap='gray')
plt.title("Mask")
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_bitwise, cv2.COLOR_BGR2RGB))
plt.title("Bitwise AND Image")
plt.axis('off')

plt.show()
```

## Output:
<img width="692" height="401" alt="image" src="https://github.com/user-attachments/assets/778185cd-57f0-4927-bedb-0bcf9d8395dc" />
<img width="687" height="401" alt="image" src="https://github.com/user-attachments/assets/f7f4b976-54c9-49dc-a28c-3b3d1bda78c2" />
<img width="630" height="398" alt="image" src="https://github.com/user-attachments/assets/3f436bba-32b6-46fb-ae18-690ad7b40deb" />
<img width="627" height="383" alt="image" src="https://github.com/user-attachments/assets/4002523a-3b5c-4d6c-ad5b-37d173a43d84" />
<img width="662" height="391" alt="image" src="https://github.com/user-attachments/assets/28f2e0a6-edb5-4e70-a676-5d965be244b5" />
<img width="673" height="406" alt="image" src="https://github.com/user-attachments/assets/808dbf1c-7423-4379-91d1-7f58948d4172" />
<img width="637" height="400" alt="image" src="https://github.com/user-attachments/assets/08fcc5cd-3be5-498f-9dab-cbd937a85708" />
<img width="668" height="403" alt="image" src="https://github.com/user-attachments/assets/deb12e12-beef-4514-b0e3-941bf81bef1d" />
<img width="602" height="377" alt="image" src="https://github.com/user-attachments/assets/0bdd8645-fdd9-4b92-b491-5b249541b481" />
<img width="621" height="386" alt="image" src="https://github.com/user-attachments/assets/aca9f500-7c96-4b93-9098-ae9aa63f344b" />
<img width="607" height="381" alt="image" src="https://github.com/user-attachments/assets/43a49d45-4201-4464-a0ad-7882d84af6d7" />
<img width="603" height="487" alt="image" src="https://github.com/user-attachments/assets/cd07e8a1-1ace-480e-aff2-e387c0fee23c" />
<img width="611" height="381" alt="image" src="https://github.com/user-attachments/assets/5509d507-5eb3-4b58-8e65-c7e1ce85626e" />
<img width="647" height="385" alt="image" src="https://github.com/user-attachments/assets/578eaf3d-6316-462c-8450-18e6aa4211c8" />


## Result:
Thus, the image was read and displayed, brightness and contrast adjustments were made, colour channels were split and merged, and bitwise operations were performed successfully using the Python program.
