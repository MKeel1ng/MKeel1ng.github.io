# Introduction

This website is still under construction! I am an almost graduated PhD student, and I'd like to show off some of the projects I've worked on. They are a mix of academic work tied to my study of cells, and also other things that interest me (like tattoos). I hope you find them interesting! You can contact me via [LinkedIn](https://www.linkedin.com/in/michael-keeling/).

## Things I've done

- Finding cell nucleus from only CSK images
- Processing raw AFM data to generate stifness maps with UNET
- Generating synthetic cell images using Pix2Pix GAN
- Generating novel tattoos

# Finding what you can't see - semantic segmentation on cell nuclei form cytoskeletal images 

Finding the outlines cell nuclei from fluorescence images is a common task. Thresholding methods can do a reasonable job, but recently semantic segmentation based techniques have been emerging with great success. Most of these techniques use the UNET network architecture. By now this is a fairly trivial task, so why don't we step it up a notch? Instead of using images of the nucleus to find nuclear outline, why not try using images of the cell cytoskeleton?

Quick bio summary: human cells have a nucleus sitting inside of them which houses all their DNA. Outside the nucleus, in the cell body, is the cytoskeleton: the cell's structures that give it strength and allow it to move - sort of like our muscles and bones (but cooler). The cytoskelton is made up of three sepoerate networks that all have slightly different roles. We can image them by tagging them with flourescent antibodies that emit a specific wavelength and taking an image only of that color.

![example_csks](https://user-images.githubusercontent.com/67687023/94991446-1a94ae80-057b-11eb-8cd3-3725156115a0.png)
*Example of nucleus and CSK images of the same cell taken at 63x magnification*

*Yes, this page is written in markdown, html is coming soon!*
