title: Remove long lines in document
author: Chen Pan
tags:
  - OCR
  - OpenCV
categories:
  - OCR
date: 2018-03-01 20:32:15
---
&emsp;Long lines (vertical or horizontal direction) are very common and special situations in printed document, 
it will result in some unexpected result when performing OCR in document. So it is necessary to remove long lines 
in pre-processing step of OCR.
&emsp;Here i will introduce one method to remove long vertical and horizontal line using morphological operations.
&emsp;Firstly, you can check this [question](https://stackoverflow.com/questions/33949831/whats-the-way-to-remove-all-lines-and-borders-in-imagekeep-texts-programmatic?rq=1); u will get some ideas from here.

&emsp;Key idea is that we use morphological operations to remove all possible characters, then extract long lines 
from the left components using its size.
&emsp;In order to remove characters perfectly, here we assume that the size(width/height) of characters is a known 
message. (If you are interested how to estimate the size of characters in a document image, you can refer my other
blog) 
###### Algorithm
&emsp;Here we assume the document image is black background and white foreground. And assume the size of characters: 
(width, height)
1.For simple case: there aren't overlaps between long lines and characters.
&emsp;For horizontal lines: 
```
Use a kernel (1, (width*1.5)) to dilate the image, this will remove all the black characters whose size is around (*, width);
Use cv2.findCountours(binary_img) and cv2.boundingRect(contours) to extract the bounding of the left component;
Extract long horizontal lines according to the ratio of width/height ratio. Remove other components;
Erode the image with the kernel same with dilation step.
```
&emsp;For vertial lines, the same method except the morphological operation should use the vertical kernel (height*1.5,1)
2.For complicated case: the long line cross some of the characters, such as underline, strikethrough. In this case, 
when we remove the long lines, the overlaps will aslo be removed, which result in some characters are split to two
parts(especially for the strikethrough).
A better methods is that: when removing the lines, for the pixel in the line, we will first check the its upper and 
lower pixels, if they are all black, we can judge that the pixel is a overlap, then the pixel will be kept. 
We will use morphological operations to complete the judge process.
```
Erode image with kernel (3,1), to thicker the long line;
Dialte image with kernel (1, width*1.5); 
Extract long lines according to left component's bounding box size, as img1;
Use img1 bitwise_and with initial binary image, get img2;
Calculate the pixels sum in height direction (axis=0) of img1 and img2 
For each pixel in the line, if the img2's sum is larger than the img1's sum, we can judge this pixel is part of overlap
```
###### Examples
Detail can refer my code [on github](https://github.com/lychenpan/little-tools-in-OCR/blob/master/ocr/pre-prcoess/remove_long_lines.py)
This is the initial document image: ![initial](initial.jpg)
Result of first simple algorithm: ![Simple process](simple.jpg)
Result of the second algorithm: ![Full process](complicated.jpg)