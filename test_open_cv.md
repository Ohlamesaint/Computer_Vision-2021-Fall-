<div class="cell markdown" id="tiMb0YEnAuV_">

## HW1 Basic Image Manipulation

### Description

  - **Part1. Write a program to do the following requirement.**
    1.  upside-down lena.bmp
    2.  right-side-left lena.bmp
    3.  diagonally flip lena.bmp
  - **Part2. Write a program or use software to do the following
    requirement.**
    1.  rotate lena.bmp 45 degrees clockwise
    2.  shrink lena.bmp in half
    3.  binarize lena.bmp at 128 to get a binary image

</div>

<div class="cell code" data-execution_count="1" id="zgf2EGGIvYcE">

``` python
# Load the Dependency
import numpy as np                            # array manipulation library，用於線性代數、傅立葉轉換與隨機變數
import pandas as pd                           # data manipulation and data analysis
import cv2 as cv                              # computer vision tasks
from google.colab.patches import cv2_imshow   # for image display
from skimage import io                        # support image processing application on python
from PIL import Image
import matplotlib.pyplot as plt               # generate figures and provide GUI toolkit

import os
```

</div>

<div class="cell code" data-execution_count="2" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="4Rv5QQKbvc2V" data-outputId="2a04cc77-f99a-402d-d33e-f0b0b20c53e7">

``` python
# Mount on Google Drive
from google.colab import drive
drive.mount('/content/drive')
```

<div class="output stream stdout">

    Mounted at /content/drive

</div>

</div>

<div class="cell code" data-execution_count="3" data-colab="{&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="PLjxBNb66pG-" data-outputId="8b9cf3bf-75d9-4f75-f600-09da05570078">

``` python
# Asset path setting
main_path = "drive/MyDrive/碩一上/Computer_Vision/HW1/asset"
print(os.listdir(main_path))
```

<div class="output stream stdout">

    ['lena.bmp']

</div>

</div>

<div class="cell code" data-execution_count="4" data-colab="{&quot;height&quot;:546,&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="TNE5Dbro8KpO" data-outputId="bc2a47ec-d97c-4702-90e8-49c83d2ab0cb">

``` python
# Get Lena.bmp
image = io.imread(os.path.join(main_path, 'lena.bmp'))
print(image.shape)                                                # 512*512
cv2_imshow(image)

# image_rotate = cv.rotate(image, cv2.ROTATE_90_CLOCKWISE)        # 現成函式
```

<div class="output stream stdout">

    (512, 512)

</div>

<div class="output display_data">

![](e6ca430c6d5efa9467749c26b5ff8a308f9e5dd4.png)

</div>

</div>

<div class="cell code" data-execution_count="5" data-colab="{&quot;height&quot;:529,&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="T5fOqEQ7FQSf" data-outputId="3aaa3ae0-16ee-45f6-b006-535ab2a66c99">

``` python
# Part 1-1 upside-down
image_upside_down = np.arange(512*512).reshape(512, 512)

for i in range(512):
  image_upside_down[i, :] = image[511-i, :]

cv2_imshow(image_upside_down)
```

<div class="output display_data">

![](75678edc61c39b96109f1bc64909070b038a34ef.png)

</div>

</div>

<div class="cell code" data-execution_count="6" data-colab="{&quot;height&quot;:529,&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="oxocAA1qHvx9" data-outputId="b5de0152-edd0-4964-cdbd-f41f8485762f">

``` python
# Part 1-2 right-side-left
image_right_side_left = np.arange(512*512).reshape(512, 512)

for i in range(512):
  image_right_side_left[:, i] = image [:, 511-i]

cv2_imshow(image_right_side_left)
```

<div class="output display_data">

![](792b1af4afdc6f54e7033c8906e470d464d66c34.png)

</div>

</div>

<div class="cell code" data-execution_count="7" data-colab="{&quot;height&quot;:529,&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="zm8fyY_LE7qI" data-outputId="95509c52-de1e-4a55-e316-d5e9605ed279">

``` python
# Part 1-3 diagonally flip
image_diag = image.T

cv2_imshow(image_diag)    
```

<div class="output display_data">

![](d54da197b76623fc69a132ff0207f04940fd7049.png)

</div>

</div>

<div class="cell code" data-execution_count="8" id="WbZ3Ztr-Hyp1">

``` python
# Part 2-1 rotate 45 degrees clockwise

image_rotate_45 = np.arange(512*512).reshape(512, 512)
each_time_assign_length = 0  
  
```

</div>

<div class="cell code" data-execution_count="9" id="qJJtIWlrH0cY">

``` python
# Part 2-2 shrink in half
```

</div>

<div class="cell code" data-execution_count="10" id="ufXGHvhNH4Ja">

``` python
# Part 2-3 binarize at 128 to get a binary image
```

</div>

<div class="cell code" data-execution_count="11" data-colab="{&quot;height&quot;:667,&quot;base_uri&quot;:&quot;https://localhost:8080/&quot;}" id="fsQP5N9_H6sJ" data-outputId="e84e4d11-e094-44c6-b94f-f543ae6ce070">

``` python
# Result Display

plt.figure(figsize=([20, 20]))
plt.subplot(131), plt.imshow(image_upside_down, cmap='gray')
plt.title('Upside Down'), plt.xticks([]), plt.yticks([])
plt.subplot(132), plt.imshow(image_right_side_left, cmap='gray')
plt.title('Right Side Left'), plt.xticks([]), plt.yticks([])
plt.subplot(133), plt.imshow(image_diag, cmap='gray')
plt.title('Diag'), plt.xticks([]), plt.yticks([])
plt.show()

plt.figure(figsize=([20, 20]))
plt.subplot(131), plt.imshow(image_upside_down, cmap='gray')
plt.title('Rotate 45 Degrees Clockwise'), plt.xticks([]), plt.yticks([])
plt.subplot(132), plt.imshow(image_right_side_left, cmap='gray')
plt.title('Shrink in Half'), plt.xticks([]), plt.yticks([])
plt.subplot(133), plt.imshow(image_diag, cmap='gray')
plt.title('Binarize at 128'), plt.xticks([]), plt.yticks([])
plt.show()
```

<div class="output display_data">

![](4a929ed1021b3a1f38b68244efe8c6aaa077b535.png)

</div>

<div class="output display_data">

![](6b1fc7ed73b8abee095dd08b8ba3fec2f4684db2.png)

</div>

</div>
