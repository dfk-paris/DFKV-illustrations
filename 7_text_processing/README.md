# Text Surrounding Illustrations

The illustrations is the art journals are usually not by themselves, rather surrounded by text. The nature and content of the text can vary a lot between two articles : the tone can be neutral or subjective, it can simply describe the illustration or give a whole analysis, etc. This part of the project aims at digging more into the ways the illustrations are talked about in art journals, through computationnal text analysis methods.

## Retrieving the so-called texts

The IIIF documents from the database are coming from two different sources : from Gallica (BnF) and the Heidelberg University. Gallica has an [API](https://api.bnf.fr/fr/api-document-de-gallica#scroll-nav__11__2) that allows to retrieve OCRed texts with really good quality (`a_gallica_texts.ipynb`). The Heidelberg University doesn't have one, so we will again use Google Cloud Vision, their [Document Text API](https://cloud.google.com/vision/docs/ocr?hl=fr) (`b_heidelberg_texts.ipynb`).

## Topic modelling

Now that we have the text, we will explore quickly the possibilties. We start by topic modelling, first on the french texts only. The work here would need to be done more in depth, but the `d_french_topic_modelling.ipynb` is essentially here to show a direction that could take the project. We however already have some convincing topics standing out, and one could now try to relate them to the illustrations.

## Relations between text and images

Finally, leaving aside the topics a little bit, we try to see in `c_illus_text_viz.ipynb` whether the length of the text and the size of the illustration are related to one another, and how. One interesting result is that through this visualisation, we can start to see the emergence of different journals layouts, with different text/illustrations characteristics. That inspires us to move to the last part of the project : studying the layouts of the journals present in the database

## Data

The data you can find in this section is : 
- `complete_texts_gallica.json` : associates french data entries with their OCRed text, if available
- `complete_texts_heidelberg.json` : associates german data entries with their OCRed text, if available
- `complete_texts_page_heidelberg.json` : associates german data entries, for each page, with their OCRed text, if available
- `data.csv` : data that was used for the vikus viewer, see detailed [description](https://github.com/dfk-paris/DFKV-illustrations/tree/main/5_illustration_enrichment#metadata-for-reproductions)
- `docword.de_dfkv.txt` : bow description of the german texts
- `docword.dfkv.txt` : bow description of the french texts
- `illu_ratios.json` : the key is the illustration's id and the value is the percentage of place that the illustrations takes on the page (between 0 and 1)
- `vocab.de_dfkv.txt` : vocab list of the german texts
- `vocab.dfkv.txt` : vocab list of the french texts
