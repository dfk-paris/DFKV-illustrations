# Text Surrounding Illustrations

The illustrations is the art journals are usually not by themselves, rather surrounded by text. The nature and content of the text can vary a lot between two articles : the tone can be neutral or subjective, it can simply describe the illustration or give a whole analysis, etc. This part of the project aims at digging more into the ways the illustrations are talked about in art journals, through computationnal text analysis methods.

## Retrieving the so-called texts

The IIIF documents from the database are coming from two different sources : from Gallica (BnF) and the Heidelberg University. Gallica has an [API](https://api.bnf.fr/fr/api-document-de-gallica#scroll-nav__11__2) that allows to retrieve OCRed texts with really good quality (`a_gallica_texts.ipynb`). The Heidelberg University doesn't have one, so we will again use Google Cloud Vision, their [Document Text API](https://cloud.google.com/vision/docs/ocr?hl=fr) (`b_heidelberg_texts.ipynb`).

## Topic modelling

Now that we have the text, we will explore quickly the possibilties. We start by topic modelling, first on the french texts only. The work here would need to be done more in depth, but the `d_french_topic_modelling.ipynb` is essentially here to show a direction that could take the project. We however already have some convincing topics standing out, and one could now try to relate them to the illustrations.

## Relations between text and images

Finally
