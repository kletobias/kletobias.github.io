---
title: '05 Questionnaire - Going Deeper'
subtitle: 'Main Topics:<br>Cross-Entropy Loss, And The Learning Rate'
date: 2022-05-29 06:00:00
description: 'Understanding the components of Cross-Entropy loss<br>and choosing
a learning rate.'
accent_color: '#08877d'
featured_image: '838338477938@+-38829429482.jpg' 
gallery_images:
  - '838338477938@+-38829429482.jpg'
---

### 05 Questionnaire Questions

1. Why do we first resize to a large size on the CPU, and then to a smaller size
    on the GPU?<br>
2. If you are not familiar with regular expressions, find a regular expression
tutorial, and some problem sets, and complete them. Have a look on the book's
website for suggestions.<br>
3. What are the two ways in which data is most commonly provided, for most deep
learning datasets?<br>
4. Look up the documentation for `L` and try using a few of the new methods that
it adds.
5. Look up the documentation for the Python `pathlib` module and try using a few
methods of the `Path` class.<br>
6. Give two examples of ways that image transformations can degrade the quality
of the data.
7. What method does fastai provide to view the data in a `DataLoaders`?
8. What method does fastai provide to help you debug a `DataBlock`?
9. Should you hold off on training a model until you have thoroughly cleaned
your data?
10. What are the two pieces that are combined into cross-entropy loss in PyTorch?
11. What are the two properties of activations that softmax ensures? Why is this
important?
12. When might you want your activations to not have these two properties?
13. Calculate the `exp` and `softmax` columns of <<bear_softmax>> yourself (i.e.,
in a spreadsheet, with a calculator, or in a notebook).
14. Why can't we use `torch.where` to create a loss function for datasets where
our label can have more than two categories?
15. What is the value of log(-2)? Why?
16. What are two good rules of thumb for picking a learning rate from the
learning rate finder?
17. What two steps does the `fine_tune` method do?
18. In Jupyter Notebook, how do you get the source code for a method or function?
19. What are discriminative learning rates?
20. How is a Python `slice` object interpreted when passed as a learning rate to
fastai?
21. Why is early stopping a poor choice when using 1cycle training?
22. What is the difference between `resnet50` and `resnet101`?
23. What does `to_fp16` do?

---

<br>

# Personal Solutions To Questionnaire 05

<br>

<br>


## 1.

Why do we first resize to a large size on the CPU, and then to a smaller
size on the GPU?<br>

---

**Prerequisites**<br>
The first resizing, as well as the second resizing are part of a fastai
data augmentation strategy that fastai refers to as *presizing*. Presizing
is a particular way to do image augmentation, that is designed to minimize
data destruction while maintaining good performance.<br>
In the end, all images need to have the same dimensions, so that they can
collate into tensors to be passed to the GPU. Another objective is to minimize
the number of distinct augmentation computations performed on an image.
<br>
From a performance standpoint, it is better to compose the augmentation
transforms into fewer transforms, whenever possible. The aim of reducing the
number of transforms, is to lowering the number of computations, as well as the
number of lossy operations. Lossy operations leave an image with fewer data,
compared to the input image. Steps that do this, e.g., any kind of interpolation
where new pixels are added (like up sampling or enlarging an image) or where
existent pixels are removed during during down sampling. The amount of 'damage'
done to an image during such computations is also dependent on the algorithm
used to perform them. These steps are all performed prior to the image being
resized to a uniform size on the GPU. This final size is also called *augmented
size*. If the transforms are performed, after the image is resized to
augmentation size, various data augmentation transforms might cause unrepairable
damage to an image. For instance, rotating an image by 45 degrees will always
leave 4 black triangular areas and erase parts of the image that are
proportional to the total area of the triangular areas.<br>
<br>
The two steps are in detail:<br>
- **First:** resize images to relatively large dimensions, dimensions that are
much larger than the final training size.<br>
- **Second:** Apply all the common augmentation operations in one batch
computation on the GPU (which itself is an accelerator).<br>
<br>
This gets rid of repeated interpolations and other degrading transforms on
the images.
<br>
<br>
**To answer the question**<br>
The enlargement during the first step, which is done on the CPU, aims to
make the images sufficiently large, so that all subsequent augmentations on
the inner regions of the image do not introduce black areas.<br>
It resizes the image to a square in the next step, a square that has the
dimensions of the smaller of width and height. The crop area is chosen
randomly on the training set.<br>

<br>
The second step is entirely done on the GPU, all augmentation steps are
done in step and only one resizing, that is only one interpolation, at the
very end of the augmentation. All images have identical (smaller) dimensions
after the second step.
<br>

## 2.


Practice using regular expressions.<br>

---

The regex practice log was too long to include in this article and can be found
in the article [TODO:exact name of published article](URL using jekyll smart
notation)
<br>

## 3.

What are the two ways in which data is most commonly provided, for deep
learning datasets?<br>

---

In deep learning data is usually provided in one of these two ways:
<br>
- Individual files representing items of data, such as text documents or
images, possibly organized into folders or with filenames representing
information about those items.<br>
- A table of data, such as in CSV format, where each row is an item or
record which may include filenames providing a connection between the data
in the table and data in other formats, such as text documents and images.<br>
<br>
One can explore a given dataset by using the `.ls` method, like so:<br>


```python
from fastai.vision.all import *


path = untar_data(URLs.PETS)
Path.BASE_PATH = path
path.ls()
```




    (#2) [Path('images'),Path('annotations')]



## 4.

Look up the documentation for `L` and try using a few of the new methods it adds.<br>

---

Most functions and methods in fastai that return a collection use a class called
`L`. `L` can be thought of as an enhanced version of the ordinary Python `list`
type, with added convenience features for common operations.<br>
For instance, when one displays an object of this class in a notebook it appears
in the format shown there. The first thing that is shown is the number of items
in the collection, prefixed with a `#`. In the preceding output one can see that
the list is suffixed with an ellipsis. This means that only the first few items
are displayed - which is a good thing, since the entire file list would show 7000
filenames on the screen. Documentation can be found here: [https://fastcore.fast.ai/foundation#L](https://fastcore.fast.ai/foundation#L)

<br>

- `L` is inspired by Numpy.
- Supports advanced indexing and has additional methods, that provide additional
    functionality and encourages simple expressive code.<br>
- The example below takes a list of pairs as input, selects the second item of each
        pair, takes its absolute value, filters items greater 4, and adds them
        up:<br>



```python
from fastcore.utils import gt


d = dict(a=1, b=-5, d=6, e=9).items()
# d['a'] = 1 < 4 was filtered out.
test_eq(L(d).itemgot(1).map(abs).filter(gt(4)).sum(), 20)
```

There is no output in this case, since the `test_eq` command works like the
python command `assert`. It will give no output, if the test was successful and
throw an error if not.<br>

An block quote from the *fastcore* docs, describing the design and idea of the
`L` class.


> In metaphorical honor of Huffman’s compression code that assigns smaller
> numbers of bits to more common bytes. In terms of syntax, it simply means that
> commonly used things should be shorter, but you should not waste short
> sequences on less common constructs.<br>
> <br>
> [https://fastcore.fast.ai/#L](https://fastcore.fast.ai/#L)

---

The single letter name `L`, shows that it is a frequently used class by design,
as outlined in the block quote.<br>
<br>
More examples of how the class `L` can be utilized follow:<br>


```python
import fastcore

# creation and output.
L(1, 2, 3)
```




    (#3) [1,2,3]



The output gives the number of items in enclosed in parenthesis, followed by 
the list representation of `L`.



Create a list with numbers from 0 to 19 as elements and shuffle all elements
randomly inside `L`.

```python
p = L.range(20).shuffle()
p
```




    (#20) [6,13,1,18,5,8,17,9,7,10...]



`class TitledTensorScalar` makes use of class `L` during the following method
`L.tensored` which lets one manually convert any tensors, that `L` contains to
tensors.


```python
t = L(([1, 2], [3, 4]))
test_eq(t.tensored(), [tensor(1, 2), tensor(3, 4)])
```

## 5.

Look up the documentation for the Python `pathlib` module and try using a few
methods of the `Path` class.<br>

---

The `Path` classes are divided between `pure paths`, which provide purely
computational operations $\iff$ *pure path operations*, without I/O operation, and `concrete paths`, which inherit from
pure paths (*path calculation operation*), but also provide I/O operations.<br>
Examples:<br>
<br>


```python
from pathlib import Path


p = Path("./images/confusion_matrix.png")

# return all parent directories
p.parent

# Returns whatever `p` is pointing at, whether it is a filename or a directory
?p.name

# Return the file prefix of the file `p` is pointing at.
p.stem

# Return the file suffix, which is the extension of the file `p` is pointing at,
# if the file has an extension.
p.suffix
```




    '.png'



TODO: add examples for the not PurePath class to answer of question 5.

## 6.

Give two examples of ways that image transformations can degrade the quality of
the data.<br>

---

The first way, that image transformations can degrade the quality of the data,
is by rotating a rectangular image by 45 degrees, using a square crop, as large
as the shorter edge of the image. Not only will part of the longer edge be cut
off, but the rotation will inadvertently crop off 2 triangular shaped areas.
These areas held valid pixels (at least it can be assumed, otherwise the
rotation does not degrade the image) and are black/white afterwards. These
lost triangular shapes are more likely to hold critical image data, if the crop
is chosen, such that the cropped area, relative to the image dimensions is
large. Fastai tries to offer a solution to this problem, by first enlarging each
image. Depending on if the enlargement up sampled both edges and not just one,
the area, that is left after cropping will have a higher magnification of what
is depicted inside, compared to before the enlargement. Cropping after enlarging
the image makes it more likely, that what is depicted in the middle of the image
gets cropped in such a way, that leaves an image, that does not show the main
motive correctly any more. E.g., Face is cut off in the middle, area of the head
above the forehead is cut off.<br>
<br>
The second way, is that by performing multiple re-sampling steps during the
preprocessing, the pixels of the image become 'muddy', sharpness is degraded and
noise is added. The most destructive operation is the upsampling of an image. It
is either done to increase the pixels per inch (PPI) together with or both
separately enlarging the dimensions of the original image. The damage done,
depends on these factors, among other:<br>

Depending on the quality of the original image, in terms of bit depth, color
space, original resolution, original format (is it a jpeg or a RAW file). Now
much noise is present in the original image. If there is a lot of noise in the
original image, many pixels will already be 'muddy', have incorrect color data
and luminosity as well. These factors have a massive influence, how much the
original image can be re-sampled.<br>
<br>
Which algorithm is used, how well does it reduce noise, how clean is it during
the sharpening of the image. How sophisticated is the pixel interpolation. Of
what scale is the enlargement, in relation to the quality of the original image,
as outlined in the first part of this question.<br>

## 7.

What method does fastai provide to view the data in a `DataLoaders`?

---

The method to view a sample of the data in a `DataLoaders` or short `dls` object
is `dls.show_batch(nrows, ncols)`. E.g.,<br>
TODO: Create a working example from the course notebook using pets.


```python
from fastai.vision.all import *


dblock1 = DataBlock(
    blocks=(ImageBlock(), CategoryBlock()), get_y=parent_label, item_tfms=Resize(460)
)
dls1 = dblock1.dataloaders([(path.cwd() / "images" / "cat.jpg")] * 100, bs=8)
dls1.show_batch(nrows=1, ncols=3)
```


    
![png](output_47_0.png)
    


## 8.

What method does fastai provide to help debug a `DataBlock`?<br>

---

It provides the `.summary(path / 'images')` method. E.g.,<br>
TODO:
 Run the cell below manually to generate output and then the ones
 afterwards, since it will cause an error and stop execution!


```python
from fastai.vision.all import *


pets1 = DataBlock(
    blocks=(ImageBlock, CategoryBlock),
    get_items=get_image_files,
    splitter=RandomSplitter(seed=42),
    get_y=using_attr(RegexLabeller(r"(.+)_\d+.jpg$"), "name"),
)
pets1.summary(path / "images")
```

    Setting-up type transforms pipelines
    Collecting items from /Users/tobias/.fastai/data/oxford-iiit-pet/images
    Found 7390 items
    2 datasets of sizes 5912,1478
    Setting up Pipeline: PILBase.create
    Setting up Pipeline: partial -> Categorize -- {'vocab': None, 'sort': True, 'add_na': False}
    
    Building one sample
      Pipeline: PILBase.create
        starting from
          /Users/tobias/.fastai/data/oxford-iiit-pet/images/saint_bernard_60.jpg
        applying PILBase.create gives
          PILImage mode=RGB size=375x500
      Pipeline: partial -> Categorize -- {'vocab': None, 'sort': True, 'add_na': False}
        starting from
          /Users/tobias/.fastai/data/oxford-iiit-pet/images/saint_bernard_60.jpg
        applying partial gives
          saint_bernard
        applying Categorize -- {'vocab': None, 'sort': True, 'add_na': False} gives
          TensorCategory(30)
    
    Final sample: (PILImage mode=RGB size=375x500, TensorCategory(30))
    
    
    Collecting items from /Users/tobias/.fastai/data/oxford-iiit-pet/images
    Found 7390 items
    2 datasets of sizes 5912,1478
    Setting up Pipeline: PILBase.create
    Setting up Pipeline: partial -> Categorize -- {'vocab': None, 'sort': True, 'add_na': False}
    Setting up after_item: Pipeline: ToTensor
    Setting up before_batch: Pipeline: 
    Setting up after_batch: Pipeline: IntToFloatTensor -- {'div': 255.0, 'div_mask': 1}
    
    Building one batch
    Applying item_tfms to the first sample:
      Pipeline: ToTensor
        starting from
          (PILImage mode=RGB size=375x500, TensorCategory(30))
        applying ToTensor gives
          (TensorImage of size 3x500x375, TensorCategory(30))
    
    Adding the next 3 samples
    
    No before_batch transform to apply
    
    Collating items in a batch
    Error! It's not possible to collate your items in a batch
    Could not collate the 0-th members of your tuples because got the following shapes
    torch.Size([3, 500, 375]),torch.Size([3, 333, 500]),torch.Size([3, 352, 500]),torch.Size([3, 500, 354])



    ---------------------------------------------------------------------------

    RuntimeError                              Traceback (most recent call last)

    Input In [40], in <module>
          1 from fastai.vision.all import *
          3 pets1 = DataBlock(
          4     blocks=(ImageBlock, CategoryBlock),
          5     get_items=get_image_files,
          6     splitter=RandomSplitter(seed=42),
          7     get_y=using_attr(RegexLabeller(r"(.+)_\d+.jpg$"), "name"),
          8 )
    ----> 9 pets1.summary(path / "images")


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/block.py:190, in summary(self, source, bs, show_batch, **kwargs)
        188     why = _find_fail_collate(s)
        189     print("Make sure all parts of your samples are tensors of the same size" if why is None else why)
    --> 190     raise e
        192 if len([f for f in dls.train.after_batch.fs if f.name != 'noop'])!=0:
        193     print("\nApplying batch_tfms to the batch built")


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/block.py:184, in summary(self, source, bs, show_batch, **kwargs)
        182 print("\nCollating items in a batch")
        183 try:
    --> 184     b = dls.train.create_batch(s)
        185     b = retain_types(b, s[0] if is_listy(s) else s)
        186 except Exception as e:


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/load.py:164, in DataLoader.create_batch(self, b)
        162 try: return (fa_collate,fa_convert)[self.prebatched](b)
        163 except Exception as e:
    --> 164     if not self.prebatched: collate_error(e,b)
        165     raise


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/load.py:162, in DataLoader.create_batch(self, b)
        161 def create_batch(self, b):
    --> 162     try: return (fa_collate,fa_convert)[self.prebatched](b)
        163     except Exception as e:
        164         if not self.prebatched: collate_error(e,b)


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/load.py:50, in fa_collate(t)
         47 "A replacement for PyTorch `default_collate` which maintains types and handles `Sequence`s"
         48 b = t[0]
         49 return (default_collate(t) if isinstance(b, _collate_types)
    ---> 50         else type(t[0])([fa_collate(s) for s in zip(*t)]) if isinstance(b, Sequence)
         51         else default_collate(t))


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/load.py:50, in <listcomp>(.0)
         47 "A replacement for PyTorch `default_collate` which maintains types and handles `Sequence`s"
         48 b = t[0]
         49 return (default_collate(t) if isinstance(b, _collate_types)
    ---> 50         else type(t[0])([fa_collate(s) for s in zip(*t)]) if isinstance(b, Sequence)
         51         else default_collate(t))


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/data/load.py:49, in fa_collate(t)
         47 "A replacement for PyTorch `default_collate` which maintains types and handles `Sequence`s"
         48 b = t[0]
    ---> 49 return (default_collate(t) if isinstance(b, _collate_types)
         50         else type(t[0])([fa_collate(s) for s in zip(*t)]) if isinstance(b, Sequence)
         51         else default_collate(t))


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/torch/utils/data/_utils/collate.py:138, in default_collate(batch)
        136         storage = elem.storage()._new_shared(numel)
        137         out = elem.new(storage).resize_(len(batch), *list(elem.size()))
    --> 138     return torch.stack(batch, 0, out=out)
        139 elif elem_type.__module__ == 'numpy' and elem_type.__name__ != 'str_' \
        140         and elem_type.__name__ != 'string_':
        141     if elem_type.__name__ == 'ndarray' or elem_type.__name__ == 'memmap':
        142         # array of string classes and object


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/fastai/torch_core.py:341, in TensorBase.__torch_function__(self, func, types, args, kwargs)
        339 convert=False
        340 if _torch_handled(args, self._opt, func): convert,types = type(self),(torch.Tensor,)
    --> 341 res = super().__torch_function__(func, types, args=args, kwargs=kwargs)
        342 if convert: res = convert(res)
        343 if isinstance(res, TensorBase): res.set_meta(self, as_copy=True)


    File ~/all_code/projects/python_projects/py_workflows/venv/lib/python3.9/site-packages/torch/_tensor.py:1142, in Tensor.__torch_function__(cls, func, types, args, kwargs)
       1139     return NotImplemented
       1141 with _C.DisableTorchFunction():
    -> 1142     ret = func(*args, **kwargs)
       1143     if func in get_default_nowrap_functions():
       1144         return ret


    RuntimeError: Error when trying to collate the data into batches with fa_collate, at least two tensors in the batch are not the same size.
    
    Mismatch found on axis 0 of the batch and is of type `TensorImage`:
    	Item at index 0 has shape: torch.Size([3, 500, 375])
    	Item at index 1 has shape: torch.Size([3, 333, 500])
    
    Please include a transform in `after_item` that ensures all data of type TensorImage is the same size


The output is very verbose and will give a detailed log of the process, until
the breakpoint occurred together and describe the breakpoint in detail as
well.<br>

## 9.

Should one hold off training, until the data is thoroughly cleaned?<br>

---

It is important to get baseline results, using a simple model and data, that
only fulfils the minimum requirements needed to train a model with it.<br>
Generally, that means, that the data is split into training and validation set,
that for each image there is a single target category/label or multiple, in the
case of a multi class classification problem, as the dependent variable. For
regression problems, data needs to have the correct dtype or at least one, that
a model can use for its predictions. Missing values need to be dealt with, to
such an extend, that the model requires to function.<br>
The base line score is important for judging, if the model can be trained well
on the given data in the particular shape used for a specific training cycle and
shows progress in how good its predictions are. Empirical experimentation is
often what it comes down to and the most important information one can get, is
a wide range of predictions results across different models/parameters/forms of
the data in the dataset.<br>

## 10.

What are the two pieces that are combined into cross-entropy loss in PyTorch?

---

The two pieces, that together make up the cross-entropy loss function are
`softmax` and `log likelihood`.

## 11.

- What are the properties of activations that softmax ensures?
- Why is this important?

---

A softmax layer, is one that outputs a vector $\overrightarrow{\boldsymbol{x}} \in \mathbb{R}^{d\times 1}$
fmt: off
given a vector of input values $\mathbb{in}=\left\langle \,in_{1},...,in_{d}\right\rangle ^{\mathbb{T}}$.
fmt: on
The *k*th element of the total of $d$ output nodes (elements) in the output
vector is given by:<br>

$$\mathrm{softmax}(\,\mathbb{in})_{k}\,\frac{e^{in_{k}}}{\sum_{k'=1}^{d} e^{in}_{k'}}$$

All output values are larger zero, since the exponential function is always
larger 0, with its limes towards minus infinity being 0.<br>
Another feature of the softmax activation function, is that the sum over
all its outputs always equals zero and thus can be interpreted as
the models predictions for the the target being any of the target labels.
Assuming, that the target can only have a single label, but that there
are more than two labels to choose from for each image or record in the set.
The exponentials cause the softmax to accentuate differences in the inputs:
for example, if the vector or inputs is given by
$\mathbb{in} = \left\langle 4,2,0,-4\right\rangle$, then the outputs are



```python
from numpy import exp
import matplotlib.pyplot as plt
plt.style.use("science")


ii = [4, 2, 0, -4]


def softmax(ii):
    """Softmax Function using Lists and Numpy"""
    res = []
    ss = sum([exp(e) for e in ii])
    for e in ii:
        res.append(exp(e) / ss)
    return res, sum(res)


softmax(ii)

fig, ax = plt.subplots(1, 1, figsize=(6, 6), tight_layout=True)
ax.plot(ii, softmax(ii)[0], color="r")
plt.title("Plot of Softmax Function")
ax.set_ylabel("Values of the Softmax Function")
ax.set_xlabel("Sample Input Values")
plt.show()
```


    
![png](output_51_0.png)
    


The plot shows, that the exponentials cause the output for large input
values to be much higher compared to smaller values. The softmax is
differentiable.<br>

## 12.

When might you want your activations to not have these two properties?<br>

---

The softmax function is a good choice, if there are no cases in the data
where no label is applicable. The softmax does not give the model the
option to predict 'no label' by default. However, a label that is designed
for these cases could be added to the set of available labels. Like that,
the predictions of the model, as input to the softmax layer would still be
equal to one, but the model is given a fallback option. An option,
where none of the other labels fit.<br>


## 13.

Calculate the `exp` and `softmax` columns of 'bear_softmax' yourself.<br>

---

The calculations are based on the *output* column in the following table:<br>


| output | bear\_type |
| :--- | :--- |
| 0.02 | teddy |
| -2.49 | grizzly |
| 1.25 | brown |

The `softmax` function from earlier is used with some changes to return the
exp values separately from the `softmax` outputs


```python
from numpy import exp, round
import matplotlib.pyplot as plt
plt.style.use("science")


# Using bear outputs
ii = [0.02, -2.49, 1.25]


def softmax2(ii):
    """Softmax Function using Lists and Numpy"""
    res = []
    o = []
    ss = sum([round(exp(e), 2) for e in ii])
    for v in enumerate(ii):
        o.append(round(exp(v[1]), 2))
        res.append(round(o[v[0]] / ss, 2))
    return o, res, sum(res)


e_o, s_o, ss = softmax2(ii)
print(f"the exp values are: {e_o}\n\n")
print(f"the softmax outputs are: {s_o}\n\n")
print(f"The sum of all softmax outputs is: {ss}\n\n")

fig, ax = plt.subplots(1, 1, figsize=(6, 6), tight_layout=True)
ax.scatter(ii, softmax2(ii)[0], color="b", label="exp")
ax.scatter(ii, softmax2(ii)[1], color="r", label="softmax")
plt.legend(loc="best")
plt.title("Plot of Softmax Function")
ax.set_ylabel("Values of the Softmax Function")
ax.set_xlabel("Sample Input Values")
plt.show()
```

    the exp values are: [1.02, 0.08, 3.49]
    
    
    the softmax outputs are: [0.22, 0.02, 0.76]
    
    
    The sum of all softmax outputs is: 1.0
    
    



    
![png](output_54_1.png)
    


The values are the same, as in the original calculation done in the
notebook of the chapter, after rounding each output to two digits.


## 14.

Why can't `torch.where` be used to create a loss function for datasets
where the label can have more than two categories?

---

The `torch.where` uses one condition and two actions, that depend on the
boolean output from condition. Let actions 'a' and 'b' be the two actions
and let 'c' be the condition, that can either have a value of '0' - not
true or '1' - true. `torch.where` then looks like this for the two cases:<br>


```python
import torch
import numpy as np


condition = torch.tensor(0)
action0 = torch.tensor(0)
action1 = torch.tensor(1)
a0 = torch.where(condition == 1, action1, 1 - action1)
print(a0)
condition = torch.tensor(1)
a0 = torch.where(condition == 1, action1, 1 - action1)
print(a0)
```

    tensor(0)
    tensor(1)


The above example shows, that by design, it only works in the binary case,
with two actions that is. One could theoretically chain several
`torch.where` calls after another, to incorporate an arbitrary number of
cases and solutions, but I assume that is not a usable solution. The
`PyTorch` library would have probably implemented a solution for the
non-binary case. The `torch.where` function, is made for the binary case
and therefore is not suitable for the multilabel - but single label per
image case.<br>



## 15.

- What is the value of `log(-2)`?
- Why?

---

The domain of any log, be it the natural logarithm $ln$ or in many python
libraries: $log$, the logarithm to the base of 10 ($log$ or $log_{10}$),
base 2 or any other one is $]\,0,\infty[\,$. It includes all positive real
numbers and excludes 0 plus any number left of zero, therefore. The `log(-2)` is undefined and returns an error. See the following example for a more visual explanation:<br>



```python
from numpy import log, log2, log10
import matplotlib.pyplot as plt
plt.style.use("science")


x = np.linspace(0.0000001, 2, num=10000)
xn = log(x)
x2 = log2(x)
x10 = log10(x)
fig, ax = plt.subplots(1, 1, figsize=(6, 6))
ax.plot(x, xn, color="r", label="natural logarithm")
ax.plot(x, x2, color="b", label="base 2 logarithm")
ax.plot(x, x10, color="g", label="base 10 logarithm")
plt.legend(loc="best")
plt.show()
```


    
![png](output_60_0.png)
    


## 16.

What are two good rules of thumb for picking a learning rate from the
learning rate finder?

---

The two rules of thumb for picking a learning rate from the learning rate
finder have to be understood in the greater context of a method for finding
an appropriate learning rate as the researcher Leslie Smith first wrote
about in 2015. He named it *learning rate finder*.<br>
<br>
The steps for finding the appropriate learning rate are:<br>
<br>
Start with a very small learning rate, a value one would never expect it to
be too big to handle.<br>
<br>
Use that initial learning rate for one minibatch and analyze the losses
afterwards.<br>
<br>
Next, increase the learning rate by a certain percentage, e.g., something
like doubling it was stated to be a common starting point. The scalar used
for the first increase, here it is 2 or 200%, can be kept for the following
steps, during testing.<br>
<br>
The cycle of increasing the learning rate - running a mini batch - looking
at the losses continues, for as long as the losses keep decreasing. Once
the losses increase, the learning rate has become to large for the model to
handle. In fact, one is already past the optimal learning rate at that
point.<br>
<br>
Now come the two rules of thumb into play, as it is at this point where the
learning rate is chosen. The two rules mutually exclusive from one another,
since they represent two different ways to choose the final learning rate.
They give two options that should both be evaluated in practice. It was
stated, that both methods often give similar values for the learning rate. In
detail, they are:<br>
<br>
- Choose one order of magnitude less than where the minimum loss was
achieved, i.e., minimum divided by 10.

**OR**

- The last point where the loss was clearly decreasing.
<br>
Below is an example of how the learning rate finder can be called and used
fmt: off
as a method of a [vision_learner object](https://docs.fast.ai/vision.learner.html#vision_learner)
fmt: on
TODO:
 Run it using cuda
ERROR:
 It will stop the execution, the next cell. Parameters are not specified.


```python
from fastai.vision.all import *

# learn = vision_learner(dls, resnet34, metrics=error_rate)
# learn.lr_find()
```

## 17.

What two steps does the `fine_tune` method do?

---

`fine_tune`, as a method of the `learner` object, will do two things:<br>

It will train the randomly added final layers for one epoch, with all other
layers frozen during this training loop. The randomly added final layers
are the ones, that where only added to the pretrained model, in order for
it to remember and use the weights that were the result of its initial
fitting, while replacing its final layers to make the final output(s)
specific to the current problem. Frozen layers don't have their weights
changed during a training loop.<br>
<br>
In the second step, `fine_tune` unfreezes all layers and trains them for
the number of epochs requested.<br>
This behavior is the default for the `fine_tune` method and there are
several parameters, when calling `fine_tune`, that can be adjusted to allow
for more custom configurations. In the example below, `dls` is the
`dataloaders` object, `resnet34` the pretrained model and the `error_rate`
is used as metric to evaluate the model's predictions on the validation set
after each epoch.


```python
from fastai.vision.all import *

# learn = vision_learner(dls, resnet34, metrics=error_rate)
# 2 means, that after the initial one epoch training has completed,
# two more training epochs with all layers unfrozen are done.
# learn.fine_tune(2)
```

## 18.

In Jupyter Notebook, how does one get the source code from a method or
function?

---

One can lookup the source code for a method or function, by calling it
without parenthesis and parameters. It can be done like so:<br>

```python
learn.fine_tune??
```

One should make sure to comment it out, after looking up the source code of a
method or function, if a formatter is used. It will likely throw an error
when trying to reformat this line.<br>

## 19.

What are discriminative learning rates?

---

Discriminative learning rates are a concept, that looks to apply different
learning rates, depending on the position of the layer in the model. The
idea is, that early layers focus on developing basic patterns, patterns
that match simple geometric shapes, as was shown in the case of a
Convolutional Neural Network in chapter 01. These early layers are supposed
to develop only general patterns and should not start to develop very specific
ones. Thus, a relatively low learning rate compared to the learning rate
used for the later layers in the model, can often work well to accomplish
this. Using a higher learning rate for these later layers, in theory,
allows them to more quickly create more complex and specific to the type of
images that are found in the dataset. E.g., human faces, bridges,
furniture, clothing, x-rays of the human chest, showing the lung.<br>

## 20.

How is a Python `slice` object interpreted when passed as a learning rate
to fastai?<br>

---

A python slice object can be passed anywhere, that a learning rate is
expected from fastai. The interpretation of the slice object, that has the
general syntax of `slice(min_lr, max_lr)`. The `min_lr` is applied to the
earliest layers of the model, while the `max_lr` is applied to the final
layer. For all layers in-between, a learning rate is used, that is
gradually increasing, using multiplicative equidistant learning rates
throughout the range.

## 21.

Why is early stopping a poor choice when passed as a learning rate to fastai?

---

Early stopping refers to a practice, that is not widely used anymore,
that dates back to a time before 1cycle training was a thing. Using early
stopping means, that one saves the state of the model after each training
epoch and then then selecting the model, that has the highest accuracy out
of all the saved models.<br>
It generally is not a good choice, when using fastai. These epochs in the
middle of the training process are unlikely to give the best result that is
within reach. A likely reason for this is that the learning rate has not
had the chance yet to reach the *small values*, that really let it use its
full potential and propel the accuracy of the model's predictions, showing
what the model is actually capable of.<br>


## 22.

What is the difference between `resnet50` and `resnet101`?

---

All variants of the `ResNet` architecture are Convolutional Neural
Networks. From this [URL](https://www.oreilly.com/library/view/practical-convolutional-neural/9781788392303/14bd6835-5316-46c3-bf7a-8bc0d4d8d211.xhtml)
<br>
A summary of the architecture and what problems it tries to solve is quoted:

> After a certain depth, adding additional layers to feed-forward convNets
> results in a higher training error and higher validation error. When
> adding layers, performance increases only up to a certain depth, and then
> it rapidly decreases. In the ResNet (Residual Network) paper, the authors
> argued that this underfitting is unlikely due to the vanishing gradient
> problem, because this happens even when using the batch normalization
> technique. Therefore, they have added a new concept called residual block.
> The ResNet team added connections that can skip layers:<br>
> <br>
> ResNet uses standard convNet and adds connections that skip a few
> convolution layers at a time. Each bypass gives a residual block.<br>
<br>
<br>
The difference between ResNet50 and ResNet101 is the number of layers they
have, or how deep they are. The ResNet50 has 50 layers, while the ResNet101
has 101 layers.<br>

## 23.

What does `to_fp16` do?

---

In practice, when using *FP16*, which is what `to_fp16` converts *FP32* to,
when called, does the following two things:<br>
- Reduce memory by cutting the size of ones tensors in half.
- Reduce training time by speeding up computations on the GPU (reducing arithmetic bandwidth)
  and (in the distributed case) reducing network bandwidth.<br>

<br>

These two things have the effect of significantly reduced training time without any loss
in performance, in most cases that is.<br>
In other words, theoretically one is able to train bigger models faster using FP16, instead of FP32.

FP16 here refers to *half-precision floating points*, that have 16-bit in contrast to FP32,
which has 32-bit floating point numbers.<br>
Unless explicitly specified, by using `to_fp16`, the weights in the model are represented by
32-bit floating point numbers. There are several reason for this default behavior.<br>
- 32-bit floating points have enough *range*, to represent numbers of
    magnitude both smaller 1.E-45, as well as larger 1.E38, which is more than
    needed for most applications.<br>
- 32-bit floating point numbers have enough precision such that they can
    represent and distinguish between numbers of varying magnitudes from one
    another.<br>
<br>

- Most hardware components, such as GPUs and CPUs and APIs support 32-bit
   floating point instructions natively and efficiently.<br>
- It is uncommon, that floating point math is the bottleneck, and if it is,
   there are ways to deal with it - these are cases where the superior
   precision that FP32 offer over FP16 *does matter*.<br>
<br>

The distribution of the 32 bits is as follows.<br>
<br>

<img src="https://qph.cf2.quoracdn.net/main-qimg-749cc641eb4d5dafd085e8c23f8826aa"/>

<br>
<br>
The graphic shows, that one bit is used to represent the sign of the number.
8 bits then are used to represent the exponent, the portion of the number
that comes before the decimals. The remaining 23 bits, that is approximately
72% percent of the total 32-bits are used to represent the mantissa of the
FP32 number.<br>

<br>
<img src="https://qph.cf2.quoracdn.net/main-qimg-68317a1ee8958729a57e35dbc7aa2501"/>

<br>
<br>
An FP16 type number uses 1 bit for the sign, 5 bits for the exponent and 10 bits
for the mantissa. Notice, that there is a slightly different distribution of the
available bits between sign, exponent and mantissa compared to FP32. FP16 allocates
63% of available bits to encode the mantissa, while FP32 uses 72%. The result is,
that FP16 sacrifices some precision for numbers where the difference in magnitude
matters, e.g., decimals close to zero. It allocates approximately 9% more of the
available bits to extend the min/max of what it can represent.

<br>

GPU producing company NVIDIA, which at the time of writing this in 2022, has
a de facto monopoly for GPUs used for deep learning, conducted tests that
compared the results between using FP16 and FP32, half precision vs single
precision that is. They came to the conclusion, that most weights and gradients
fall well within the FP16 representable range and of the gradients that did
not, scaling up the gradient was sufficient to achieve convergence.<br>
<br>
Using FP16 instead of FP32, frees up 16-bit of memory per FP16 type number and
thus lets one double the batch size during training for example.<br>
<br>
The possible downsides of using FP16 instead of FP32 include that the reduced range of numbers that can be represented using FP16 can cause a number, which is close to 0, but not 0 when using FP32 to become 0 when casted to FP16. This then
is a case of that there is no safe down casting possible and even worse, that
the number after the down casting is not equal the original FP32 represented number
<br>
Using FP16, the representable range is a fraction of the one when using the FP32 space, it
ranges from 1.e-8 to 65504. This sheds light onto, why it can happen that a number
changes during the down casting to FP16.<br>
The mentioned case, where a number is close to, but not equal to 0 using FP32,
becomes 0 as a result of down casting it, is called **underflow**. The other
possible problem, when a number is too large to be represented using FP16,
becoming *NaN*, not a number as a result of the conversion is called **overflow**.
With underflow, the network does not improve improve during the optimization,
since the gradients of the weights are meaningless, if they are just 0 using
mixed precision. With overflow, it will likely encounter an error during
optimization, since *NaN* values are not allowed during the Stochastic Gradient
Descent.<br>
There is another 16-bit representation however, that tries to bridge the gap between FP16 and FP32, by lowering the likelihood of underflow and overflow occuring during real life deep learning applications. It does so, by using a different distribution of the
16 bits to represent a floating point number. In detail, the distribution is
the following.<br>
<br>
![](https://qph.cf2.quoracdn.net/main-qimg-65b4c66b94efd478d62ff7812c96127b)

<br>
The sign still uses 1 bit, with the exponent using 8 (3 more than FP16 uses to represent the exponent), while the mantissa only
uses 7, which is 3 less compared to FP16. It is called the *bfloat16* representation and allows for numbers, that
have the same order of magnitude as their FP32 counterparts. The upper limit
of 65504 using FP16 is a major drawback from down casting from FP32, and
bfloat16 bridges the gap between the two in this regard.<br>
However, distributing the available 16-bits differently does not increase the
total range of numbers that it can represent. Compared to FP16, it has a smaller set of numbers that are close to zero, where the difference in magnitude between two floating points is not very pronounced, but where it can matter greatly, e.g., thinking of *learning rates*, *softmax activation layer outputs*. The mantissa is what matters here, and reducing the mantissa by 3 bits hampers the bfloat16's capability to represent these numbers.<br>
<br>
However, given the sort of numbers, that are commonly generated during the optimization
procedure, its weaknesses don't matter (*this assessment might change, as the standard sees a more widely integration into the major deep learning libraries. If this happens, remains to be seen and only then, given a larger sample size, can such broad statements be proven right or wrong. This should be kept in mind.*). The reasoning behind this statement is that what matters, when thinking of gradients and weights, are two things:<br>
- Magnitude
- Direction

The magnitude is arguably the most important factor when choosing a learning rate. With common loss functions incorporating the negative Logarithm function, to amplify the differences between predictions, numbers between zero and one that is. Another common function, that is found as part of loss functions is the *exp* function. The natural Log and the exp function neutralize each other and so can be used to amplify even very small differences in the weights, gradients and predictions.<br>
<br>
The direction is commonly associated with the steepest gradient that is found during each step of the Stochastic Gradient Descent. Ideally, in the case of a convex loss function, the direction to follow after each step in the SGD should be clear and lead to convergence in the end. While it can not be guaranteed that the loss function is convex in general, a local minimum can be enough to solve the problem. If the single elements of the vector of gradients are very close to one another, using an exponential function or the logarithm can help the model in distinguishing between several close gradients in the same way that was discussed before.<br>
<br>

It seems, that floating point representations might be an area, that has the potential to increase deep learning model performance, by the use of more customized floating point spaces. Designed to outperform the common floating point representations.

