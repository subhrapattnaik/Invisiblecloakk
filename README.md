# Invisiblecloakk

Please refer this website

https://data-flair.training/blogs/invisible-cloak-opencv-python/


very well explained

--------------------------------
About Invisible Cloak Project
We will create the invisible cloak using an image processing technique called Color detection and segmentation. In order to make this project, you’ll need a single-color cloth. The cloth should not contain any other color visible. Here we are using a green cloth to develop this python project.

TRY TO USE SINGLE COLOURED CLOTH(red/green/blue)these three colors are easier to detect.

Color Detection & Segmentation


Color detection is a technique where we can detect any color in a given range of HSV color space.

Image segmentation is the process of labeling every pixel in an image, where each pixel having the same label shares certain characteristics.

“pip install opencv-python”

Project Prerequisites:
Python – 3.x (we used Python 3.7.10 in this project)
Numpy – 1.19.2
OpenCV – 4.5
https://data-flair.training/blogs/invisible-cloak-opencv-python/

https://data-flair.s3.ap-south-1.amazonaws.com/machine-learning-projects/invisible-cloak-opencv-code.zip
----------------------------------------------------------------------------------------------
Steps to Build Invisible Cloak OpenCV Project:


Import necessary packages and Initialize the camera.
Store a single frame before starting the infinite loop.
Detect the color of the cloth and create a mask.
Apply the mask on frames.
Combine masked frames together.
Removing unnecessary noise from masks.

--------------------------------------------

Steps Explanation of Code:

Step 1 – Import necessary packages and Initialize the camera:
Using import, we imported the required libraries
To access the camera, we use the method cv2.VideoCapture(0) and set the capture object as cap.
-------------------------------------------------
Step 2 – Store a single frame before starting the infinite loop:
cap.read() function captures frames from webcam
2-second delay between two captures are for adjusting camera auto exposure
cap.isOpen() function checks if the camera is open or not and returns true if the camera is open and false if the camera is not open.
While capturing the background make sure that you or your clothes don’t accidentally come into the frame.

----------------------------------------------
Step 3 – Detect the cloth:
In this invisible cloak opencv project, we are using green cloth so we have to detect green color. So how can we do this?

OpenCV reads the frame as BGR colorspace. To detect any color first we have to convert the frame to HSV colorspace.

Why HSV?
HSV stands for HUE, SATURATION, and VALUE (or brightness). It is a cylindrical color space.

 
HUE: The hues are modeled as an angular dimension which encodes color information.
SATURATION: Saturation encodes intensity of color.
VALUE: Value represents the brightness of the color.

cv2.cvtColor() function converts colorspace.
Lower bound and Upper bound are the boundaries of green color.
cv2.inRange() function returns a segmented binary mask of the frame where the green color is present.

Here we can see in the frame wherever the green color is detected the mask shows that as white. The rest of the region is black.
-------------------------------------------
Step 4 – Apply the mask:
We have successfully detected the cloak. We want to show our previously-stored background in the main frame where the cloak is present. First, we need to take the only white region from the background.

cv2.bitwise_and() applies mask on frame in the region where mask is true (means white).

We have successfully replaced the cloak region with the background. Now we need those regions of our main frame where the clock is not present. To get this we can simply invert the mask and do the same procedure for the main frame.

cv2.bitwise_not() inverse the mask pixel value. Where the mask is white it returns black and where is black it returns white.


Here we have the inverse mask at the left and the corresponding region from the current frame at the right.
---------------------------------------
Step 5 – Combine masked frames together:
Finally, we have a cloak background and current frame background. Now it’s time to combine those to get a whole frame.

cv2.add() adds two frames and returns a single frame.

Yeah, finally we are reaching our goal. But can you see the green edges of the cloak? We have to remove those edges to get the perfect finishing.

So what can we do here?

We’re gonna use some filtering methods provided by OpenCV. OpenCV provides morphological operation libraries.
-----------------------------------
Step 6 – Removing unnecessary noise from mask :

Explanation:

np.ones((5,5),np.uint8) create a 5×5 8 bit integer matrix.
Adjust kernel size according to your condition.

cv2.MORPH_CLOSE removes unnecessary black noise from the white region in the mask. And how much noise to remove that is defined by kernel size.
cv2.MORPH_OPEN removes unnecessary white noise from the black region.
cv2.dilate increases white region in the image.
---------------------

https://henrydangprg.com/2016/06/26/color-detection-in-python-with-opencv/


The last three lines just state that the program will wait until the user presses the “esc” key (which has an id of 27) before it quits and destroys every OpenCV window.
