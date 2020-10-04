# Introduction

This website is still under construction! I am an almost graduated PhD student, and I'd like to show off some of the projects I've worked on. They are a mix of academic work tied to my study of cells, and also other things that interest me (like tattoos). I hope you find them interesting! You can contact me via [LinkedIn](https://www.linkedin.com/in/michael-keeling/).

## Things I've done

- Finding cell nucleus from only CSK images
- Processing raw AFM data to generate stifness maps with UNET
- Generating synthetic cell images using Pix2Pix GAN
- Generating novel tattoos

# Finding what you can't see - semantic segmentation on cell nuclei form cytoskeletal images 

Finding the outlines cell nuclei from fluorescence images is a common task. Thresholding methods can do a reasonable job, but recently semantic segmentation based techniques have been emerging with great success. Most of these techniques use the UNET network architecture. By now this is a fairly trivial task, so why don't we step it up a notch? Instead of using images of the nucleus to find nuclear outline, why not try using images of the cell cytoskeleton?

Quick bio summary: human cells have a nucleus sitting inside of them which houses all their DNA. Outside the nucleus, in the cell body, is the cytoskeleton: the cell's structures that give it strength and allow it to move - sort of like our muscles and bones (but cooler). The cytoskelton is made up of three seperate networks of proteins that all have slightly different roles. We can image them by tagging them with flourescent antibodies that emit a specific wavelength and taking an image only of that color.

![example_csks](https://user-images.githubusercontent.com/67687023/94991446-1a94ae80-057b-11eb-8cd3-3725156115a0.png)
*Example of nucleus and CSK images of the same cell taken at 63x magnification*

So how do we do this? We set up a data generator that returns RGB images for the CSK networks as inputs and a one hot encoded mask of the cell outline and nucleus as outputs. We augment these with random flipping. Network structure is a vanilla UNET, with a softmax final activation layer. We use a weighted categorical cross-entropy loss. Ideally I'd use an IOU loss, but it is hard to write it as a loss since it isn't differentiable. We keep the IOU as a metric instead. IOU, or intersection over union, is a measure of how well the a mask (in this case the nucleus) is predicted. It penalises the network for false positives.

![IOUexample](https://user-images.githubusercontent.com/67687023/95016341-534f8900-064a-11eb-9940-74de6e6a4d4b.png)
*Clockwise: Overlap of nucleus mask and prediction, Intersection, IOU value, Union*

So how well do we do? After a lot of training and finetuning , we get a median validation IOU for the nucleus of 0.7. So from images of the CSK, the network can produce a fairly accurate representation of the nucleus. Now this in itself is pretty cool, but there's more! Instead of using all three CSK networks to train the UNET, we can train seperate networks on only one CSK at a time, and compare their performance. Given the same training time and network structure, actin only reaches a 0.5 IOU, while both tubulin and keratin reach the 0.7 IOU acheived by training on combined data. Based on the Universal Approximation Theorem (UAT) any function can be fitted by a sufficiently deep and wide function. Therefore we can use the predictive power of the individual networks to evaluate how much control they have over nuclear shape and size in reality. The fact that our network can score higher when trained on keratin compared to actin indicates that actin has less biological and physical influence on the nuclei of these cells. This is actually what we find using more classical approaches. 

![my_model_256_WIOU_0 71590674 best-worst](https://user-images.githubusercontent.com/67687023/95016443-e688be80-064a-11eb-8439-bb44c147fd44.png)

**

*Yes, this page is written in markdown, html is coming soon!*
