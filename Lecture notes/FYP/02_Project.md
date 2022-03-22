# FYP p02

## Measuring features
Encode samples by *p* features, represent in **feature space**
R^p sapce: features + label (special kind of feature - binary or categorical: here)
An image -> several representations. Here: picture -> segmentation -> representation

Example: measure how convex a shape is: area vs perimeter ratio - measure of *compactness*: e.g. circle has a low number, octopus has high.
Even a circle won't have a compactness of 1, on a digital image, bc you can't perfectly represent a circle with pixels

### Measuring area and perimeter

We use a max, binary pixels, 1 inside of the lesion, 0 outside
Pixel border: not fancy algorithm to find out the border but:
- resize image a bit (shrink)
- subtract the smaller image from larger
- sum pixel values

