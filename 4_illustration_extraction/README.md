# ILLUSTRATION EXTRACTION

The task is to actually extract the illustrations from the DFKV documents. We first find the relevant pages to extract (`a_pages_extraction.ipynb`) that were noted by the researchers in the bibliography. Then we collect these 12698 images with their IIIF links and save them (`b_collect_images.ipynb`). After that, we actually use the model to segment the images and create the json files with the bounding boxes around the illustrations (`c_segmentation.ipynb`). Finally, we crop the images according to the bounding boxes and save them into a directory (`d_extract_illustrations.ipynb`). We have a total of 10542 illustrations extracted.

The illustrations are hosted on the DFK server. There is a list of illustrations IDs (`./data/illu_names.txt`), and you can retrieve them by querying `https://static.dfkg.org/public/k/DFKV_illustrations/4096/<ILLU_NAME>.jpg`
