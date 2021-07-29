# Shape Detection Using OpenCV

OpenCV is a huge open-source library for computer vision, machine learning, and image processing.
OpenCV supports a wide variety of programming languages like Python, C++, Java, etc. It can process images and videos to identify objects, faces, or even the handwriting of a human.

In this ,we will learn how to detect shapes of objects by finding their contours. Contours are basically outline that bound the shape or form of an object. So we will be detecting multiple shapes and how many corners points each shape has along with its area .

Approach that we have used:

- Created a file called ShapeDetection and written functions to detect the shapes based on the contours and output the shape accordingly

- Preprocessed the image file by applying threshold and GaussianBlur

- Finally printed the output image file

### Create a file called ShapeDetection:

Open a file in your favorite editor and save it as ShapeDetection.py

### Import open-cv library:

```
import cv2
```

### Create a function to extract the contours from the image:

```
def getContours(img):
    contours , heirarchy = cv2.findContours(img,cv2.RETR_EXTERNAL,cv2.CHAIN_APPROX_NONE)
```

### Loop over the contours:

```
for cnt in contours:
     area = cv2.contourArea(cnt)
```

### Draw the contours for each shape:

Within the loop

```
if area >100:
     cv2.drawContours(imgContours,cnt,-1,(0,0,0),2)
```

### Create a variable to extract the perimeter:

```
peri = cv2.arcLength(cnt,True)
```

### Create a variable to extract the vertices:

```
approx = cv2.approxPolyDP(cnt,0.02*peri,True)
objectCor = len(approx)
# compute the bounding box of the contour and use the bounding box to compute the aspect ratio
x,y,w,h = cv2.boundingRect(approx)
```

### State if conditions to recognise the shape:

```
 # if the shape is a triangle, it will have 3 vertices
if objectCor == 3:
    objectType = "Triangle"
# if the shape has 4 vertices, it is either a square or a rectangle
elif objectCor == 4:
    assRatio = w/float(h)
    if assRatio >0.95 and assRatio<1.05:
       objectType = "Square"
    else:
       objectType = "Rectangle"
# if the shape is a pentagon, it will have 5 vertices
elif objectCor == 5:
    objectType = "Pentagon"
# if the shape is a hexagon, it will have 6 vertices
elif objectCor == 6 :
     objectType = "Hexagon"
elif objectCor > 6 and objectCor<=8:
     objectType = "Circle"
# if it neither matches the shape nor is a cirle, we print Other Shapes
else:
     objectType = "Other Shapes"
```

### Assign the rgb color for the text that is used to indicate the shape:

```
cv2.rectangle(imgContours,(x,y),(x+w,y+h),(0,255,0),2)
cv2.putText(imgContours,objectType,(x+(w//2)-10,y+(h//2)-10),cv2.FONT_HERSHEY_COMPLEX,0.7,(0,0,255),2)
```

### Read the input image:

```
path10 = "shape.jpg"
img = cv2.imread(path10)
```

### Create variable to apply Contours,Grayscale,Gaussian Blur and Canny and call getContours() function:

```
imgContours = img.copy()
imgGray = cv2.cvtColor(img,cv2.COLOR_BGR2GRAY)
imgBlur = cv2.GaussianBlur(imgGray,(7,7),1)
imgCanny = cv2.Canny(imgBlur,50,50)
getContours(imgCanny)
```

### Print the input:

```
cv2.imshow("Shapes",img)
cv2.imshow("output",imgContours)

cv2.waitKey(0)

#cv2 waitkey() allows you to wait for a specific time in milliseconds until you press any button on the keyword. It accepts time in milliseconds as an argument.
```

## We used this image for input

<img src = "https://github.com/Govindbro/Shape_Dectection_Opencv/blob/master/shape.jpg">

## And this was the output

<!-- <img src = "https://github.com/Govindbro/Shape_Dectection_Opencv/blob/master/shape.jpg"> -->
<br>
**need to update output image**


Refer this repository for the source code
