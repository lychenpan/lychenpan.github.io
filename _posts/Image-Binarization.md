title: Image Binarization
author: John Doe
tags: []
categories: []
date: 2017-12-27 18:29:00
---
**Binarization is one of such important image segmentation approaches for finding out the area of interest from an image by separating the pixels into two groups: one representing the object and the other background.**
#### 1.Why binarize image:
* Remove noise（Not a standard method)
* (Very Simple) image segmentation:  isolate the background and ROI 
* Reduce compution cost (It is very quick)
<br>For document OCR, binarization is a necessary step. The merges, fractures, and other deformations in the character shapes as a consequence of incorrect thresholding are the main reasons of OCR performance deterioration

#### 2.Binarization methods:
According to threshold:
1. Global threshold.  [OTSU, Traingle and so on.](http://imagej.net/Auto_Threshold)
2. Adaptive threshold (Window sliding; local statistics: range, variance) [Niblack, Sauvola, Adaptive OTSU](http://imagej.net/Auto_Local_Threshold)

Depending on which principal criteria they consider in calculating the threshold.
1. Image variace 
2. Image contrast
3. Entropy-based

Different targets of binarization:  
1. Document Images: printed document, handwrittern document, historical handwrittern.
2. Graphic Images
3. Video.

#### 3.Document Binarization methods 
&emsp;Fast and accurate document binarization is becoming more and more important. <br>
&emsp;But it is still an unresolved problem, because modeling the document foreground/background is very difficult due to various types of document degration such as: <br>
&emsp;&emsp;&emsp;**uneven illumination, image contrast variation, bleeding-through, smear, shadow, background noise and so on**. [examples](https://www.researchgate.net/figure/Example-document-images-in-DIBCOs-dataset-that-illustrate-document-degradation-including_220163435)

Classical Binarization methods: 
1. Otsu algorithm:<br>  [wikipedia](https://en.wikipedia.org/wiki/Otsu%27s_method); [OpenCV](https://docs.opencv.org/3.3.1/d7/d4d/tutorial_py_thresholding.html)
   
2. Niblack algorithm: 
		T = m + k*s;   
&emsp; m,s: mean and variace of gray values in the sliding window. 
<br>&emsp;Result is not senstive to the window size as long as window covers at least 1-2 characters. 
<br>&emsp; k=0.6 (smaller k will gives thick/unclear strokes)
<br>&emsp; DrawBack:  Noise created in the area don't contains text. 
3. Sauvola algorithm:   
Try to solve the drawBack of Niblack by adding hypothesis on texts and background. Normalize the standard deviation by its dynamic range.
<br> DrawBack: low-contrast text regions.
		T = m * (1 - k *(1-s/R)
   **[compare example](http://scikit-image.org/docs/dev/auto_examples/segmentation/plot_niblack_sauvola.html)**
4. WolfJoin: 
   <br>Imporve by normalize the contrast and the mean gray level of image.
    	T = m − k*α*(m−M),          α = 1−s/R, R = max(s), M = min(greylevel)
	[implementation and compare](https://github.com/brandonmpetty/Doxa)
    <br>[example 2](https://github.com/chriswolfvision/local_adaptive_binarization)
5. Bernsen:
   <br> Image contrast based.
   		C = max(I)-min(I);  T, w
6. Kapur:  
   <br>[entropy-based](https://www.google.com.sg/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&ved=0ahUKEwi2x_DlhM3YAhVIQI8KHfc7BbcQFggnMAA&url=http%3A%2F%2Fpequan.lip6.fr%2F~bereziat%2Fpima%2F2012%2Fseuillage%2Fkapur85.pdf&usg=AOvVaw3oVJHOD0qO9ZGM_ODG9_JC)

#### 4. useful links
[DIBCO](https://vc.ee.duth.gr/dibco2017/)
[ICFHR](http://icfhr2018.org/)