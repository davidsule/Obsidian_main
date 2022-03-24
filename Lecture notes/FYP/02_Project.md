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

Features for skin cancer:
- A: cancerous more assymetric
- B: more fuzzy
- C: more variety (and more blue - several type of measuremeents)
- D: diameter - we don't have scale, so we don't no real size + we can't compare different bodyparts
- E: 

#### A

Fols image, how much overlap (deduct one from other). Add up deducted pixels --> the more, the more assymetric
Scale: 0, 1, 2: 0 (round numbers) more or less symmetric, 2: very asymmetric

#### B:
slide 16

Measuring asymmetry:
- either rotate the image, make several measurement (different angles) and choose the one with largest height (diameter). But, because of rotation, add padding
- adopt a convention (but what is it?)

Perimeter and morphology:
- remove 'salt and pepper' noise: reduce too much fuzziness on micro scale on the border? with disc method. (creates a circle mask? 'brush')

reduce size: erosion - depends on disc size



# Project notes:
Original measurement for A: 0, 1, 2 but if we do that, we can't compare it to automatic (automatic cannot be 0 1 2 because we could only do that based on percentiles within measurement values)

Symmetry: We need rotational symmetry, not mirror symmetry (or how it is called), and what we do is a proxy for that. (smallest mean of max and min height/width kinda finds the angle where 'mirror symmetry' will be the worst -> proxy for mirror symmetry)

PAD database - brazil - more metadata
Newer ISIC challenge data - more metadata

Limitation: number of slic segments --> depends on area of leison --> we only have the area of mask (sum of pixels), but we should divide based on the real-life size of leison, which we don't know (so on a leison of the same size we have the same number of segments) <-> BUT even if divide the same lesion into more segments, similar color areas will still be grouped into similar colors, so the color difference won't be that much bigger, on average.

Possible improvement: list comprehension of calculating mean color of slic -> vector based calc

different ways: (on mean or median of grayscale segments)
- min-max
- IQR
- SD for 1 gaussian
- figure out bimodal gaussian and distance of means (or multimodal, too, maybe)

Test:
- Logical regression (f1 number!!)
- naive Bayes
- sklearn feature selection

Maybe even combine them.

OR:
ne segmentation and look at the distribution of the pixel (grayscale) in the lesion overall
