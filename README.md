# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

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
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- **Name:** [Your Name Here]  
- **Register Number:** [Your Register Number Here]

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```python
# 1. Read the image as grayscale
img_gray = read_image('Downloads/lion.jpg', cv2.IMREAD_GRAYSCALE)
```

#### 2. Print the image width, height & Channel.
```python
# 2. Print width, height & channels
height, width = img_gray.shape[:2]
channels = 1 if img_gray.ndim == 2 else img_gray.shape[2]
print("Width:", width, "Height:", height, "Channels:", channels)
```
Width: 533 Height: 574 Channels: 1

#### 3. Display the image using matplotlib imshow().
```python
# 3. Display using matplotlib
plt.imshow(img_gray, cmap='gray')
plt.title("Grayscale Image")
plt.show()
```
<img width="399" height="434" alt="download" src="https://github.com/user-attachments/assets/587e314d-62fc-49ec-ba8f-8ad4aae30df5" />


#### 4. Save the image as a PNG file using OpenCV imwrite().
```python
# 4. Save as PNG
cv2.imwrite('lion_gray.png', img_gray)
```
True

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```python
# 5. Read the saved image as a color image
img_saved = read_image('lion_gray.png', cv2.IMREAD_COLOR)    # loads as 3-channel BGR
img_color = cv2.cvtColor(img_saved, cv2.COLOR_BGR2RGB)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```python
# 6. Display the color image & print width, height, channels
plt.imshow(img_color)
plt.title("Color Image")
plt.show()
height, width, channels = img_color.shape
print("Width:", width, "Height:", height, "Channels:", channels)
```
<img width="399" height="434" alt="download" src="https://github.com/user-attachments/assets/31e8a36f-9d4e-4fe9-bbf4-0448560d84bd" />

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```python
# 7. Crop the lion (central region; adjust the fractions to fit your image)
h, w = img_color.shape[:2]
y1, y2 = int(0.20 * h), int(0.80 * h)
x1, x2 = int(0.20 * w), int(0.80 * w)
img_cropped = img_color[y1:y2, x1:x2]

plt.imshow(img_cropped)
plt.title("Cropped Lion")
plt.show()
```
<img width="399" height="434" alt="download" src="https://github.com/user-attachments/assets/bbff7484-682c-45bd-ba82-e41acac7a290" />

#### 8. Resize the image up by a factor of 2x.
```python
# 8. Resize up by 2x
img_resized = cv2.resize(img_cropped, None, fx=2, fy=2, interpolation=cv2.INTER_LINEAR)
plt.imshow(img_resized)
plt.title("Resized (2x)")
plt.show()
```
<img width="399" height="434" alt="download" src="https://github.com/user-attachments/assets/b93e3558-4c8a-44ea-b815-9942ea61fb3e" />

#### 9. Flip the cropped/resized image horizontally.
```python
# 9. Flip horizontally
img_flipped = cv2.flip(img_resized, 1)
plt.imshow(img_flipped)
plt.title("Flipped Horizontally")
plt.show()
```
<img width="399" height="434" alt="download" src="https://github.com/user-attachments/assets/b3886570-61c7-4920-9c85-a50b72f93d8e" />

#### 10. Read in the image ('Apollo-11-launch.jpg').
```python
# 10. Read the image
img_jet = read_image('Downloads/JET.jpg', cv2.IMREAD_COLOR)
img_jet = cv2.cvtColor(img_jet, cv2.COLOR_BGR2RGB)
plt.imshow(img_jet)
plt.show()
```
<img width="552" height="378" alt="download" src="https://github.com/user-attachments/assets/f67bf327-8e44-4bf7-b713-894e318f3cac" />

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```python
# 11. Add centered text at the bottom
img_annotated = img_jet.copy()
img_h, img_w = img_annotated.shape[:2]

text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

# pick a font scale so the text fills about 80% of the image width
(base_w, base_h), _ = cv2.getTextSize(text, font_face, 1, 1)
font_scale = 0.8 * img_w / base_w
thickness = max(1, int(font_scale))

(text_w, text_h), baseline = cv2.getTextSize(text, font_face, font_scale, thickness)
x = (img_w - text_w) // 2             # centered horizontally
y = img_h - int(0.05 * img_h)         # near the bottom

cv2.putText(img_annotated, text, (x, y), font_face, font_scale,
            (255, 255, 255), thickness, cv2.LINE_AA)

```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```python
# 12. Draw a magenta rectangle around the main object (jet)
magenta = (255, 0, 255)
rect_color = magenta
pt1 = (int(0.15 * img_w), int(0.15 * img_h))   # top-left
pt2 = (int(0.85 * img_w), int(0.80 * img_h))   # bottom-right
cv2.rectangle(img_annotated, pt1, pt2, rect_color, thickness=3)
```

#### 13. Display the final annotated image.
```python
# 13. Display the final annotated image
plt.figure(figsize=(10, 8))
plt.imshow(img_annotated)
plt.title("Annotated Image")
plt.show()
```
<img width="831" height="580" alt="download" src="https://github.com/user-attachments/assets/b11e5325-3acc-4aa4-892d-9623c452a8f7" />

#### 14. Read the image ('Boy.jpg').
```python
# 14. Read the image
img = read_image('Downloads/WALT.jpg', cv2.IMREAD_COLOR)
img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img_rgb)
plt.show()
```
<img width="371" height="418" alt="download" src="https://github.com/user-attachments/assets/6f85b363-a86b-4b24-9de9-a6b62edc9793" />

#### 15. Adjust the brightness of the image.
```python
# 15. Matrix of ones (float64) for brightness
matrix = np.ones(img.shape, dtype='float64') * 50
```

#### 16. Create brighter and darker images.
```python
# 16. Brighter and darker images
img_brighter = cv2.add(img, matrix, dtype=cv2.CV_8U)
img_darker   = cv2.subtract(img, matrix, dtype=cv2.CV_8U)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```python
# 17. Display Original, Darker, Brighter
plt.figure(figsize=(15, 5))
plt.subplot(131); plt.imshow(img_rgb); plt.title("Original Image"); plt.axis("off")
plt.subplot(132); plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB)); plt.title("Darker Image"); plt.axis("off")
plt.subplot(133); plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB)); plt.title("Brighter Image"); plt.axis("off")
plt.show()
```
<img width="1158" height="426" alt="download" src="https://github.com/user-attachments/assets/8d24a1c8-cef8-45dc-9a9d-90e9b64d0d64" />

#### 18. Modify the image contrast.
```python
# 18. Modify contrast (factors 1.1 and 1.2, without overflow fix)
matrix1 = np.ones(img.shape, dtype='float64') * 1.1
matrix2 = np.ones(img.shape, dtype='float64') * 1.2
matrix0 = np.ones(img.shape, dtype='float64') * 0.8     # extra, for the "lower contrast" display

img_higher1 = np.uint8(cv2.multiply(np.float64(img), matrix1))
img_higher2 = np.uint8(cv2.multiply(np.float64(img), matrix2))
img_lower   = np.uint8(cv2.multiply(np.float64(img), matrix0))
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```python
# 19. Display Original, Lower Contrast, Higher Contrast
plt.figure(figsize=(18, 5))
plt.subplot(141); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(142); plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB)); plt.title("Lower Contrast (0.8)"); plt.axis("off")
plt.subplot(143); plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB)); plt.title("Higher Contrast (1.1)"); plt.axis("off")
plt.subplot(144); plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB)); plt.title("Higher Contrast (1.2)"); plt.axis("off")
plt.show()
```
<img width="1415" height="408" alt="download" src="https://github.com/user-attachments/assets/87a4fdee-287d-4999-9624-f325415f38c0" />

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```python
# 20. Split into B, G, R and display the channels
b, g, r = cv2.split(img)

plt.figure(figsize=(18, 5))
plt.subplot(141); plt.imshow(b, cmap='gray'); plt.title("Blue Channel"); plt.axis("off")
plt.subplot(142); plt.imshow(g, cmap='gray'); plt.title("Green Channel"); plt.axis("off")
plt.subplot(143); plt.imshow(r, cmap='gray'); plt.title("Red Channel"); plt.axis("off")
plt.subplot(144); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.show()
```
<img width="1415" height="408" alt="download" src="https://github.com/user-attachments/assets/5fbe2b09-7ffa-4eee-9065-0de3c9643c01" />

#### 21. Merged the R, G, B , displays along with the original image
```python
# 21. Merge the channels and display with the original
merged_bgr = cv2.merge((b, g, r))

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB)); plt.title("Merged (B,G,R)"); plt.axis("off")
plt.show()
```
<img width="760" height="426" alt="download" src="https://github.com/user-attachments/assets/e8a7a1de-d018-4590-aa3a-31899375dd84" />

#### 22. Split the image into the H, S, V components & Display the channels.
```python
# 22. Split into H, S, V and display the channels
img_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
hue, sat, val = cv2.split(img_hsv)

plt.figure(figsize=(18, 5))
plt.subplot(141); plt.imshow(hue, cmap='gray'); plt.title("Hue"); plt.axis("off")
plt.subplot(142); plt.imshow(sat, cmap='gray'); plt.title("Saturation"); plt.axis("off")
plt.subplot(143); plt.imshow(val, cmap='gray'); plt.title("Value"); plt.axis("off")
plt.subplot(144); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.show()
```
<img width="1415" height="408" alt="download" src="https://github.com/user-attachments/assets/e9e203eb-5636-43ae-b5de-2f17377b2f67" />

#### 23. Merged the H, S, V, displays along with original image.
```python
# 23. Merge H, S, V and display with the original
merged_hsv = cv2.merge((hue, sat, val))
merged_hsv_rgb = cv2.cvtColor(cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR), cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(merged_hsv_rgb); plt.title("Merged (H,S,V)"); plt.axis("off")
plt.show()
```
<img width="760" height="426" alt="download" src="https://github.com/user-attachments/assets/86a733ed-05a3-4046-872b-d8d9601ba197" />

## Output:
- **i)** Read and Display an Image.
<img width="501" height="518" alt="image" src="https://github.com/user-attachments/assets/b3e6e942-7907-4094-910a-9fb0ee8f1dc1" />

- **ii)** Adjust Image Brightness.
<img width="1402" height="507" alt="image" src="https://github.com/user-attachments/assets/6a1776fd-0c20-4f4a-ae42-364310760f95" />

- **iii)** Modify Image Contrast.
<img width="1395" height="397" alt="image" src="https://github.com/user-attachments/assets/1a258df1-1084-4ca7-8eb6-b80b9cba0323" />




## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

