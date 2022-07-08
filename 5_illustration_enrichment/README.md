# Illustration metadata enrichment

We now have all the illustrations that are present in our corpus. We want to make the dataset more interesting by adding some metadata to the illustrations. 

The proposed steps are :

- Free exploratory analysis of illustration
- Find the category of the object illustrated
- Find name/authors of artworks

## Clustering of images based on structural similarity

To have a first look at the dataset structure, we first used [Pixplot](https://github.com/YaleDHLab/pix-plot), to visualize our illustrations in a two-dimensional projection within which similar images are clustered together. We use the HDBCAN algorithm to create the clusters of images, and then UMAP to be able to visualize the results into the 2D space. With this first approach, we can identify different categories of illustrations, more or less precisely. Here is an example of cluster of pictures of furnitures :

<img src="./img/furnitures.png" width="800">

Some other identified clusters are : 

- architecture plans, drawings, arches, facades
- interiors, landscapes, trees, boats drawings
- portraits, portraits of people in dress
- statues, busts, vases, necklaces, chairs
- engravings, doodles, letters
- abstract paintings 

The list is not exhaustive, and you can find pictures of part of the clusters in `./img/`

## Classification of illustration : is it a painting reproduction or something else ?

Ideally, we would like to be able to find tags for the different illustrations. But those tags would be very different if the illustration were a painting or a photography of an object for example. That is why, the first classification that we will do will be to determine if the illustration is a painting reproduction or not. It is done in `b_painting_other_classification.ipynb`.

We first try a simple ResNet32 architecture, for 17 cycles, and get a final accuracy of 0.80. That is not bad but we would like to do better, because right now on the test set out of 200 illustrations, 27 were wongly classified as 'other', and 13 as 'reproduction'. 

If we look at the current state-of-the-art in terms of image classification, we see that Transformers models are beginning to shine in the field of Computer Vision too (where they were first used and showed great success in Natural Langage Processing). In the `c_vision_transformer_augreg.ipynb` notebook, we focused on training such a model, fousing especially on finding adapted Data Augmentation and Regularization parameters, as their improtance has been demonstrated in [this](https://arxiv.org/pdf/2106.10270.pdf) paper. As also mentionned in the paper, for trainings with relatively small datasets - as it is the case here - transfer learning leads faster to better results, so we will use a pre-trained model. The model on training data was performing good with a final test accuracy of 0.914. However, I encoutered problems with loading checkpoints and could not re-use the finetuned model on our DFKV data. Had to think for another solution.

## Classification of illustration's type

We decide to move to another tool : the ready-to-use Google Vision AI tool, which is a computer vision model that describes what is in the image by assigning it labels. After a few tries with test images, we see that the output labels are quite precise. Instead of classifying reproduction/not reproduction, we will try to classify the illustrations into 7 categories : Reproduction, Photography, Object, Architecture/decoration, Sculpture, Plan and Ornament. We will proceed the following way (in `g_label_illus.ipynb`): 

- for each illustration, get the labels along with probabilities that Vision AI gives us
- create a dictionary that counts the occurences of each label for each category on a random subset of the dataset. That will create a distribution of words depending on the category
- keep only the most relevant ones using TF-IDF scores
- Classify using Naïve Bayes, and compute a confidence score
- For the predictions that have a low confidence score, manually check/change their category

## Metadata for reproductions

It would be nice to have more precise information about the painting reproductions that we have. To do that, we query the [Smartify](http://smartify.org) API with every illustration, and find around 1700 known paintings from our dataset. We save their title, painter name, date, and dimensions (`d_paintings_reconciliation.ipynb`). We also would have liked to try using the [Tineye](http://tineye.com) API to perform a reverse image search, but their API was not free, so instead we just scrapped Google Reverse Image Search, and look for links from trusted sources which have well formated data about their images (`f_google_reverse_image_scrap.ipynb`). Once the metadata is grouped together, we can finally prepare the big csv file with every information we have collected so far (`h_preparation.ipynb`), and clean the column to make them easier to use. The final data is available in `./data/full_data_clean.csv`
