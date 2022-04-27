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
- min-max (median, mean)
- IQR (but rather not bc it would exclude relatively small patches of significantly different colors)
- 
- SD for 1 gaussian
- figure out bimodal gaussian and distance of means (or multimodal, too, maybe)
- Or Use the gaussian mixture model, and find the probable number of components (minimum aic)
- MAD: median of distances from the median of values
- median of ring vs [lightest, some center, darkest]

Test:
- Logistic regression (f1 number!!)
- naive Bayes
- sklearn feature selection

Maybe even combine them.

OR:
no segmentation and look at the distribution of the pixel (grayscale) in the lesion overall

Idea: Compare the colors of the lesion with the skin around the lesion. How? Scale up the mask, then segment only that 'ring' (around the lesion), and compare the normal skin to lesion. What to compare: min/max (or smth else?) -> maybe test with the above methods.

We will only use median -> more ruboust, not that much difference, and we can use nr of segments to pick up on differences.

Segmentation barely changes gaussian mean and std
For MAD: larger segments (lower segment number) -> higher MAD

Implement better masking algorithm??

Pixel_per_segment: is it actually good to adjust it to nr of pixels? bc if you have the same lesion 2x but one is a larger resolution image, then you divide it differently?

Idea: Study with comapre color and moving border, comapre relative RGB color
skin line direction
[https://glyndwr.repository.guildhe.ac.uk/id/eprint/200/1/fulltext.pdf](https://glyndwr.repository.guildhe.ac.uk/id/eprint/200/1/fulltext.pdf)

  
Idea: skin direction filtering
Relative color histograms of melanoma
[http://europepmc.org/backend/ptpmcrender.fcgi?accid=PMC3184887&blobtype=pdf](http://europepmc.org/backend/ptpmcrender.fcgi?accid=PMC3184887&blobtype=pdf)


 https://link.medium.com/ucyy8ikDTob
 https://scikit-learn.org/stable/modules/generated/sklearn.feature_selection.RFE.html
 https://scikit-learn.org/stable/modules/feature_selection.html#feature-selection


## Fix & Improve:

- implement resize size parameter, save in corresponding folder (named based on pixel height), and within that
- add 'mask' to resized mask names
- calculate pixel per segment based image size (all images)? mask (lesion) size (per image)? 
- grayscale resize not working!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
- move reading/writing final csv inside processing fell (the whole thing should only run if at least one of the flags is True)
- 
- make set params possible (brush, resize_size, pixel_per_segment)



Pseudo-code:
path definitions...
params = ...

path_list =[ im_id_list, path_original_images, path_original masks, path_processed folder]
param list = [...]

flag1 = ...
flag2 = ..
...

create directories for paths

def Processing function(list_of_paths, param_list, flag1, flag2, flag3):
	if flag1:
		...
	if flag2:
		...
	...
	compile, write final csv

Note: individual feature group csv files should be saved in their own folder (avoid clutter), with params in their name --> can be re-used (but all partial csvs in same folder, no matter params). Final csv files should also be in their own folder and have the param names in their name.

if any flag == True:
	execute Processing function(list_of_paths, param_list, flag1, flag2, flag3)



- Add mutual information as feature selection (test several number of selected features by training the classifier and checking which one is the best)
- Add case where we use all features (only select from color ones)
- Add case where we forcibly leave border and asymmetry in, only select down from color features
- Train classifier on manually evaluated features (compare it to a model that's only trained on the 150, not the one on the 2000)
- Use not just 2000 but all images (validation and test set).
- Train classifier on manual labeling


From Veronica during Q&A:
One of the questions that came up today is about getting different performances if you split the data (e.g. using train_test_split). This depends on the random state, and is also influenced by other methods that might use the random state in your code (especially if you use a notebook, and might execute cells in a different order). 
In any case it's a good idea to do multiple splits (like in the cross-validation example) to get multiple estimates of your performance. But to make sure your results are reproducible, you can take a look at the following :
* Check the random state with https://scikit-learn.org/stable/modules/generated/sklearn.utils.check_random_state.html
* Read more about the background of this in section 10.3 here: https://scikit-learn.org/stable/common_pitfalls.html
