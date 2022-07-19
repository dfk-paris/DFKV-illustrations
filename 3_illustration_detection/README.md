# Illustration Detection

Here, we focus on designing, training and using the model that will find illustrations in the documents.

## Base Detectron2 Model

The task that we need to perform is illustration detection and segmentation. This means that for each illustration per document, we need the spatial coordinates for each of the boxes enclosing an illustration. We do not need any label on the illustrations yet.

We are going to use a model from a project called [Detectron2](https://github.com/facebookresearch/detectron2), which is Facebook AI Research's next generation library that provides state-of-the-art detection and segmentation algorithms.

### An example : Newspaper Navigator Project

We start by trying to reproduce the results of a project that has a similar goal as ours : the [Newspapers Navigator](https://github.com/LibraryOfCongress/newspaper-navigator), by Benjamin Charles Germain Lee (2020 Library of Congress Innovator in Residence). A part of his project was dedicated to extracting headlines, photographs, illustrations, maps, comics, cartoons, and advertisements from 16.3 million historic newspaper pages in Chronicling America. He used Detectron2 to achieve that.

I re-used his notebook [train_model.ipynb](https://github.com/LibraryOfCongress/newspaper-navigator/blob/master/notebooks/train_model.ipynb), and trained the model, with his data exclusively. Using all the default parameters, we achieved after 10 epochs and almost 4 hours a global Average Precision (AP) of 45.984, and of 51.270 for the photographs and 21.170 for illustrations. This is done in `./a_base_detectron/train_model.ipynb`. I only included the notebook here, as I kept intact all the other file/file structure, that you can check on his github.

### First impressions on DFKV Data

Now that we have a model, let's see how it performs on some of our DFKV images. We would expect to perform moderatly well, as the files are a little bit different. In our dataset there are also some newspapers, but it consists mostly of magazines, in which the page structure and layout is different from a newspapers one. We do this work in the `base_model_on_DFKV.ipynb` notebook, which is again heavily inspired by the Newspapers Navigator project's notebook [process_chronam_pages.ipynb](https://github.com/LibraryOfCongress/newspaper-navigator/blob/master/notebooks/process_chronam_pages.ipynb), especially the `generate_predictions` function.

In `./a_base_detectron/DFKV_data/test` are the ten test images used. In `DFKV_output/test` are the json files that contain the output of the model. Inside, there are the boxes coordinates, along with a probability score and the category label associated.

Displaying some results shows that the illustrations in the images are usually found, but were classified in different classes (photos, illustrations, or advertisement) and with different levels of scores depending on the layout. Also, the boxes do not frame really well the images, precision could be improved.

For the next step, we will want to create our own training data, suitable for our dataset, and merge it with the data from the Newspaper Navigator project, in order to train a more fitting model.

## Training Data

### Gathering

In order to have a model that fits our task, we want to have training data that have the same global structure as the future test images, but not exactly those images. For that, we collect Gallica images that are not from the test dataset. This is done and explained in this `./b_training_data_collection/training_data_collection.ipynb`, and the images are in the `./b_training_data_collection/data/training_images/` folder. 

### Annotating, choice of classes and merging datasets

Now, we need to annotate our data. We will follow the [COCO](https://cocodataset.org/#format-data) standards, because it is the one that detectron2 uses. We use a tool called [makesense.ai](https://www.makesense.ai/). It is convinient as it is an online tool and very easy to use.

At this step, we need to think about our goal : detecting illustrations. We do not need as much detail about the type of content as the Newspaper Navigator project focussed on. So, for our annotations, there will only be one class : Illustration. But we will not throw out of the window the whole Newspapers dataset ! We will just keep only the 'Photograph', 'Illustration' and 'Comics/Cartoon' annotations, and put them all together in the same (and only) class. This is because all the images in these categories already include the kind of content we want to segment. 

During the annotating process, we notice that not all of the gathered images contain illustrations. We remove those from the training data. We also exclude documents that are newspapers, as we already have enough of them in the training data. I divided the work of annotating in N=4 different batches, and the resulting annotation files are in `c_merging_datasets/data/batchN.json`.

Now, we merge all these annotation files, along with the annotations from the Newspaper Navigator project, and split them into a training and a test set. This work is done in the `c_merging_datasets/merge_annotations.ipynb` notebook. 

## Detectron2 Model for DFKV

With our new training data, we train the model for 10 epochs. The final model weigths are in `a_base_detectron/model_weigths/model_final_001.pth`. These are the final precision we get on the validation data :

|   AP   |  AP50  |  AP75  |  APs  |  APm   |  APl   |
|:------:|:------:|:------:|:-----:|:------:|:------:|
| 64.078 | 81.348 | 73.256 |  nan  | 46.535 | 64.366 |

These results are much better than the previous 45% of AP, with the model from Newspaper Navigator on our dataset. 
We also try to generate some predictions on random samples of test data (you can check them out at the bottom of the training notebook) and display them, and we also visually see that the bounding boxes are more accurate, and the model is more sure about them.

We probably still can do better, what I want to do now is finding more training data and annotate them, to train the model solely on them, and play with the parameters of the model.

Let's first train the model on the 500 images from DFKV. Even from the first epoch, we achieve an average precision of 75.4, which is already way better than the previous model. After 10 epochs, here are the results (see the [notebook](https://github.com/dfk-paris/DFKV-illustrations/blob/main/3_illustration_detection/a_base_detectron/notebooks/train_model_dfkv.ipynb)) : 

|   AP   |  AP50  |  AP75  |  APs  |  APm  |  APl   |
|:------:|:------:|:------:|:-----:|:-----:|:------:|
| 96.333 | 99.857 | 98.837 |  nan  |  nan  | 96.333 |

Well, even with less training data, we have a very good model. The weights are in `model_final_002.pth`. When we look at test examples, we observe that the data the model has difficulty with are image formats that it has not encoutered in the training dataset, for example cartoons or illustrations in newspapers. Now, we go back to gathering training data to find even more training data to be able to face a wide variety of different documents.

As a result, with now about 800 training images we get the average precision below :

|   AP   |  AP50  |  AP75  |  APs  |  APm  |  APl   |
|:------:|:------:|:------:|:-----:|:-----:|:------:|
| 95.461 | 99.721 | 97.865 |  nan  |  nan  | 95.461 |

These are slightly less good than the previous ones. But it is not a bad thing, because by diversifying the training data, we prevent the model for overfitting too much. The weights are stored in `model_weigths/model_final_003.pth`
