title: Morphological operations
author: John Doe
date: 2018-01-20 19:07:33
tags:
---
This blog is to help to distinguish each kind of morphological operations. Just like erosion and dilation, their effact are opposite, how to remeber  them clearly? 

** Why Black is 0 and white is 255<br>In image processing, it is always hard to remember clearly about the gray level of black and white.  We can remember their gray levels by understanding how black and white comes.   **
1. Firstly, we need to have a knowledge about RGB model,  Please refer [RGB color model](https://en.wikipedia.org/wiki/RGB_color_model), and RGB model is only for the light that comes directly from a light source.[Quora](https://www.quora.com/How-can-colors-like-black-or-white-be-made-with-the-RGB-color-model)
2. Then 0 means no light comes from the light source, which means dark or black.  And 255 means it will have a maximum light, when all RGB have the maximum value, the mix will be white.

** Then morphological operations **
1. Refer [opencv document](https://docs.opencv.org/3.0-beta/doc/py_tutorials/py_imgproc/py_morphological_ops/py_morphological_ops.html)
2. Some key points:  
   * Dilation and erosion is a kind of converlution operation. Dilation use the max value(Whiter value) and erosion use the min value(Black value) of the kernel.  So dilation increase white region, and erosion decrease the white region. 
   * Attention, the example image is white foreground and black background. In real situation, document is always white background and black foreground.
   * Opening: erosion followed by dilation,  [Erosion can remove little white noise, and make it disappear]
   * Closing: dilation followd by erosion, which can close small black holes **in white object**. The small holes will not appear because it is surrounded by white object.