Q. To perform arithmetic operations on Image such as addition, subtraction, multiplication and division.

# importing libraries
import cv2
from google.colab.patches import cv2_imshow
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

# Upload images
uploaded = files.upload()

# Read uploaded images
file_names = list(uploaded.keys())
image1 = cv2.imread(file_names[0])
image2 = cv2.imread(file_names[1])

# Resize
img1 = cv2.resize(image1, (200, 250))
img2 = cv2.resize(image2, (200, 250))

# Display original images
cv2_imshow(image1)
cv2_imshow(image2)

# Applying arithmetic operation on images (UNCHANGED)
add = img1 + img2
sub = img1 - img2
mul = img1 * img2
div = img1 / img2

# Display results 
plt.subplot(2, 2, 1)
plt.imshow(add)
plt.title('Addition')
plt.axis('off')

plt.subplot(2, 2, 2)
plt.imshow(sub)
plt.title('Subtraction')
plt.axis('off')

plt.subplot(2, 2, 3)
plt.imshow(mul)
plt.title('Multiplication')
plt.axis('off')

plt.subplot(2, 2, 4)
plt.imshow(div)
plt.title('Division')
plt.axis('off')

plt.tight_layout()
plt.show()

Q. To obtain Digital Negative of an image by point processing methods

# Digital Negative image (with colour image)

# importing libraries
import cv2
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
uploaded = files.upload()

# Read uploaded image 
file_name = list(uploaded.keys())[0]
image = cv2.imread(file_name)

# Perform negative
negative_image = 255 - image

# Convert BGR to RGB for display
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)
negative_rgb = cv2.cvtColor(negative_image, cv2.COLOR_BGR2RGB)

# Display images
plt.figure(figsize=(8,4))

plt.subplot(1,2,1)
plt.title("Original Image")
plt.imshow(image_rgb)
plt.axis('off')

plt.subplot(1,2,2)
plt.title("Color Negative Image")
plt.imshow(negative_rgb)
plt.axis('off')

plt.show()

Q. To perform Bit plane slicing of an image by point processing methods

# importing libraries
import cv2
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
uploaded = files.upload()

# Read uploaded image (ONLY CHANGE)
file_name = list(uploaded.keys())[0]
img = cv2.imread(file_name, 0)

# Display bit planes
for i in range(8):
    bit_plane = (img >> i) & 1
    plt.subplot(2, 4, i+1)
    plt.imshow(bit_plane, cmap='gray')
    plt.title(f'Bit {i}')
    plt.axis('off')

plt.show()

Q. To separate RGB components from a color image

# importing libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

# Upload image
uploaded = files.upload()

# Read uploaded image (ONLY CHANGE)
file_name = list(uploaded.keys())[0]
image = cv2.imread(file_name)
img = cv2.resize(image, (250, 200))

# split the Blue, Green and Red color channels
red, green, blue = cv2.split(img)

# define channel having all zeros
zeros = np.zeros(blue.shape, np.uint8)

# merge zeros to make RGB image
redBGR = cv2.merge([red, zeros, zeros])
greenBGR = cv2.merge([zeros, green, zeros])
blueBGR = cv2.merge([zeros, zeros, blue])

# display
Titles = ["Original", "Red", "Green", "Blue"]
images = [img, redBGR, greenBGR, blueBGR]

for i in range(4):
    plt.subplot(2, 2, i + 1)
    plt.axis("off")
    plt.title(Titles[i])
    plt.imshow(images[i])

plt.show()

Q. To perform Average (Mean) Filtering and Median Filtering on a given image.

# importing libraries
import cv2
import matplotlib.pyplot as plt
from google.colab import files

# Upload image 
uploaded = files.upload()

# Read image 
file_name = list(uploaded.keys())[0]
img = cv2.imread(file_name)

# Convert to grayscale if image is color
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

# Average filtering (Mean filter)
avg_filter = cv2.blur(gray, (10, 10))

# Median filtering
median_filter = cv2.medianBlur(gray, 3)

# Display images
plt.subplot(1,3,1)
plt.title("Grayscale Image")
plt.imshow(gray, cmap='gray')
plt.axis('off')

plt.subplot(1,3,2)
plt.title("Average Filter")
plt.imshow(avg_filter, cmap='gray')
plt.axis('off')

plt.subplot(1,3,3)
plt.title("Median Filter")
plt.imshow(median_filter, cmap='gray')
plt.axis('off')

plt.show()

Q. To perform morphological operations such as erosion, dilation, and boundary extraction on a given image.

# importing libraries
import cv2
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

# Upload image 
uploaded = files.upload()

# Read image 
file_name = list(uploaded.keys())[0]
img = cv2.imread(file_name, 0)   # read directly in grayscale

# Convert to binary image (needed for morphology)
_, binary = cv2.threshold(img, 127, 255, cv2.THRESH_BINARY)

# Structuring element (kernel)
kernel = np.ones((3,3), np.uint8)

# Erosion
erosion = cv2.erode(binary, kernel, iterations=1)

# Dilation
dilation = cv2.dilate(binary, kernel, iterations=1)

# Boundary Extraction = Original - Erosion
boundary = cv2.subtract(binary, erosion)

# Display results
plt.subplot(2,2,1)
plt.title("Binary Image")
plt.imshow(binary, cmap='gray')
plt.axis('off')

plt.subplot(2,2,2)
plt.title("Erosion")
plt.imshow(erosion, cmap='gray')
plt.axis('off')

plt.subplot(2,2,3)
plt.title("Dilation")
plt.imshow(dilation, cmap='gray')
plt.axis('off')

plt.subplot(2,2,4)
plt.title("Boundary Extraction")
plt.imshow(boundary, cmap='gray')
plt.axis('off')

plt.show()

Q. To implement the Canny Edge Detection technique and analyze the detected edges in an image.

# importing libraries
import cv2 as cv
import matplotlib.pyplot as plt
import numpy as np
from google.colab import files

# Upload image (ONLY ADDED)
uploaded = files.upload()

# Get uploaded file name (ONLY ADDED)
file_name = list(uploaded.keys())[0]

def canny_edge_detection(image_path, lower_threshold, upper_threshold):

    # 1. Load the image in grayscale
    img = cv.imread(image_path, cv.IMREAD_GRAYSCALE)

    # 2. Apply Canny edge detection
    edges = cv.Canny(img, lower_threshold, upper_threshold)

    # 3. Visualize the results
    plt.figure(figsize=(10, 5))

    plt.subplot(121)
    plt.imshow(img, cmap='gray')
    plt.title('Original Image')
    plt.xticks([]), plt.yticks([])

    plt.subplot(122)
    plt.imshow(edges, cmap='gray')
    plt.title('Canny Edge Image')
    plt.xticks([]), plt.yticks([])

    plt.show()

# Call function 
canny_edge_detection(
    image_path=file_name,
    lower_threshold=100,
    upper_threshold=200
)

Q. To implement the K-Means Clustering Algorithm and group data points into clusters based on similarity.

# importing libraries
import matplotlib.pyplot as plt

# visualizing some data points

x = [4, 5, 10, 4, 3, 11, 14 , 6, 10, 12]
y = [21, 19, 24, 17, 16, 25, 24, 22, 21, 21]
plt.scatter(x, y)
plt.show()

# Visualizing the intertia for different values of K

from sklearn.cluster import KMeans
data = list(zip(x, y))
inertias = []

for i in range(1,11):
    kmeans = KMeans(n_clusters=i)
    kmeans.fit(data)
    inertias.append(kmeans.inertia_)

plt.plot(range(1,11), inertias, marker='o')
plt.title('Elbow method')
plt.xlabel('Number of clusters')
plt.ylabel('Inertia')
plt.show()

# Select value for K from Elbow method, and visualize the result:

kmeans = KMeans(n_clusters=2)
kmeans.fit(data)

plt.scatter(x, y, c=kmeans.labels_)
plt.show()
