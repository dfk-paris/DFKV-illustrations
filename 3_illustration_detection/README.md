# Illustration Detection

Here, we focus on designing, training and using the model that will find illustrations in the documents.

## Base Detectron2 Model

The task that we need to perform is illustration detection and segmentation. That is to say, for each image of document, we will want the coordinates of boxes surronding all the illustrations it contains. We do no need any label on the illustrations yet.

We are going to use a model from a project called [Detectron2](https://github.com/facebookresearch/detectron2), which is Facebook AI Research's next generation library that provides state-of-the-art detection and segmentation algorithms.

### An example : Newspaper Navigator Project

We start by trying to reproduce the results of a project that has a similar goal as ours : the [Newspapers Navigator](https://github.com/LibraryOfCongress/newspaper-navigator), by Benjamin Charles Germain Lee (2020 Library of Congress Innovator in Residence). Part of their project was dedicated to extracting headlines, photographs, illustrations, maps, comics, cartoons, and advertisements from 16.3 million historic newspaper pages in Chronicling America. They used Detectron2 to achieve that.

I re-used their notebook [train_model.ipynb](https://github.com/LibraryOfCongress/newspaper-navigator/blob/master/notebooks/train_model.ipynb), and trained their model, with their data exclusively. Using all the default parameters, we achieved after 10 epochs and almost 4 hours a global Average Precision (AP) of 45.984, and of 51.270 for the photographs and 21.170 for illustrations. This is done in `./a_base_detectron/train_model.ipynb`. I only included the notebook here, as I kept intact all the other file/file structure, that you can check on their github.

### First impressions on DFKV Data

Now that we have a model, let's see how it performs on some of our DFKV images. We would expect to perform moderatly well, as the files are a little bit different. In our dataset there are also some newspapers, but it consists mostly of books, in which the pages structure is different from a newspapers one. We do this work in the `base_model_on_DFKV.ipynb` notebook, which is again heavily inspired by the Newspapers Navigator project's notebook [process_chronam_pages.ipynb](https://github.com/LibraryOfCongress/newspaper-navigator/blob/master/notebooks/process_chronam_pages.ipynb), especially the `generate_predictions` function.

In `./a_base_detectron/DFKV_data/test` are the ten test image used. In `DFKV_output/test` are the json files that contain the output of the model. Inside, there are the boxes coordinates, along with a probability score and the category label associated.

Displaying some results showed that the illustrations in the images are usually found, but classified in different classes (photos, illustrations, or advertisement) and with different levels of scores depending on the layout. Also, the boxes do not frame really well the images, precision could be improved.

For the next step, we will want to create our own training data, suitable for our dataset, and merge it with the data from the Newspaper Navigator project, in order to train a more suitable model.

## Training Data

### Gathering

In order to have a model that fits our task, we want to have training data images that have the same global structure as the future test images, but not exactly those images. For that, we collect Gallica images that are not from the test dataset. This is done and explained in this `./b_training_data_collection/training_data_collection.ipynb`, and the images are in the `./b_training_data_collection/data/training_images/` folder. However, not all the images actually have illustrations in them. I manually deleted the majority of these, because having too many of them won't be helpful for the model. 

### Annotating, choice of classes and merging datasets

Now, we need to annotate ou data. We will follow the [COCO](https://cocodataset.org/#format-data) standards, because it is the one that detectron2 uses. We use a tool called [COCO Annotator](https://madewithvuejs.com/coco-annotator). 

At this step, we need to think about our goal : detecting illustrations. We do not need as much detail about the type of content as in the Newspaper Navigator project. So, for our annotations, there will only be one class : Illustration. But we will not throw out of the window the whole Newspapers dataset ! We will just keep only the 'Photograph', 'Illustration' and 'Comics/Cartoon' annotations, and put them all together in the same (and only) class. That's because all the images in these categories would be the kind of content we want to segment, and not the others. 

## Detectron2 Model for DFKV

### TODO
