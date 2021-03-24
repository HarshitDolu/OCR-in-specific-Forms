# OCR-in-specific-Forms

This project extracts input text from forms and organize it in excel sheet.
<br>
Problem: Suppose there is a book cover image which is perfectly warpped and same book cover image, but with different orientation, scale. Now on comparing both, due to differnt pixel density, orientation, variation in scales, Chances are high for not to be matched.<br>

If I want to register an image, I will definitely use image features (keypoints and descriptors) <br>

keypoints : point of interest.<br>
descriptors: description of the point of interest.<br>

Algorithms like: Harris corner detector, FAST are feature detectors and BRIEF are feature descriptor.<br>

For image to be properly compare: we need algorithms which have both i.e. detector and descriptor.<br>

In short,
## image = detectors + descriptors

## Algorithms used for feature extractions are:

### SIFT:

SIFT, or Scale Invariant Feature Transform, is a feature detection algorithm in Computer Vision.SIFT helps locate the local features in an image, commonly known as the ‘keypoints‘ of the image. These keypoints are scale & rotation invariant that can be used for various computer vision applications, like image matching, object detection, scene detection, etc.

We can also use the keypoints generated using SIFT as features for the image during model training. The major advantage of SIFT features, over edge features or hog features, is that they are not affected by the size or orientation of the image.

The entire process can be divided into 4 parts:

Constructing a Scale Space: To make sure that features are scale-independent
Keypoint Localisation: Identifying the suitable features or keypoints
Orientation Assignment: Ensure the keypoints are rotation invariant
Keypoint Descriptor: Assign a unique fingerprint to each keypoint

### SURF:

Speeded Up Robust Features” which introduced a new algorithm called SURF. As name suggests, it is a speeded-up version of SIFT.
In SIFT, Low approximated Laplacian of Gaussian with Difference of Gaussian for finding scale-space. SURF goes a little further and approximates LoG with Box Filter.

### ORB:

An efficient alternative to SIFT or SURF in 2011. As the title says, it is a good alternative to SIFT and SURF in computation cost, matching performance and mainly the patents. Yes, SIFT and SURF are patented and you are supposed to pay them for its use. But ORB is not !!!

ORB is basically a fusion of FAST keypoint detector and BRIEF descriptor with many modifications to enhance the performance. First it use FAST to find keypoints, then apply Harris corner measure to find top N points among them. 


### Flow of this project:

1. Pick specific forms and find coordinates of input box, where text is entered by user.( use region selector )
2. There are many test forms (different orientation, rotation) and one actual query forms (perfectly warpped)
3. Task 1 will be to warp perspective the test forms.
4. I have used ORB detect and compute for finding keypoints and descriptors of both test forms and query forms.
5. Comapred descriptors of test forms with query forms using BF matcher and Hamming distance.
6. Drawn good match between test and query forms.
7. find src and dest points using keypoints and good matches
8. compute relation matrix using findHomography ( src, dest ) points.
9. WarpPerspective the test images using matrix.
10. created mask and highlighted the region of input text using Green color.
11. cropped the region of input text.
12. Finally using pytesseract converted cropped image to string.

### Demo images





