# Illustration Detection

Here, we focus on designing, training and using the model that will find illustrations in the documents.

## Base Detectron2 Model

The task that we need to perform is illustration detection and segmentation. That is to say, for each image of document, we will want the coordinates of boxes surronding all the illustrations it contains. We do no need any label on the illustrations yet.

We are going to use a model from a project called [Detectron2](https://github.com/facebookresearch/detectron2), which is Facebook AI Research's next generation library that provides state-of-the-art detection and segmentation algorithms.

### An example : Newspaper Navigator Project

We start by trying to reproduce the results of a project that has a similar goal as ours : the [Newspapers Navigator](https://github.com/LibraryOfCongress/newspaper-navigator), by Benjamin Charles Germain Lee (2020 Library of Congress Innovator in Residence). Part of their project was dedicated to extracting headlines, photographs, illustrations, maps, comics, cartoons, and advertisements from 16.3 million historic newspaper pages in Chronicling America. They used Detectron2 to achieve that.

I re-used their notebook [train_model.ipynb](https://github.com/LibraryOfCongress/newspaper-navigator/blob/master/notebooks/train_model.ipynb), and trained their model, with their data exclusively. Using all the default parameters, we achieved after 10 epochs and almost 4 hours a global Average Precision (AP) of 45.984, and of 51.270 for the photographs and 21.170 for illustrations. This is done in `train_model.ipynb`. I only included the notebook here, as I kept intact all the other file/file structure, that you can check on their github.

### First impressions on DFKV Data

Now that we have a model, let's see how it performs on some of our DFKV images. We would expect to perform moderatly well, as the files are a little bit different. In our dataset there are also some newspapers, but it consists mostly of books, in which the pages structure is different from a newspapers one. We do this work in the `base_model_on_DFKV.ipynb` notebook, which is again heavily inspired by the Newspapers Navigator project's notebook [process_chronam_pages.ipynb](https://github.com/LibraryOfCongress/newspaper-navigator/blob/master/notebooks/process_chronam_pages.ipynb), especially the `generate_predictions` function.

In `DFKV_data/test` are the ten test image used. In `DFKV_output/test` are the json files that contain the output of the model. Inside, there are the boxes coordinates `[x_top_left_corner, y_top_left_corner, x_bottom_right_corner, y_bottom_right_corner]`, along with a probability score and the category label associated.

Displaying some results showed that the illustrations in the images are usually found, but classified in different classes (photos, illustrations, or advertisement) and with different levels of scores depending on the layout. Also, the boxes do not frame really well the images, precision could be improved.

For the next step, we will want to create our own training data, suitable for our dataset, and merge it with the data from the Newspaper Navigator project, in order to train a more suitable model.

## Training Data

### Gathering

### Annotating

### Choice of classes and merging datasets

## Detectron2 Model for DFKV

### TODO
