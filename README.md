# DFKV illustrations - Internship Project

For the 5 months of my internship at DFK Paris, I am working on one of their curated database, called *Deutsch-Französische Kunstvermittlung*. An overview of the global project is available [here](https://dfk-paris.org/fr/research-project/curation-de-donnees-lexemple-de-la-base-de-donnees-deutsch-franzoesische). I am mainly focusing on the role and place of illustrations in Franco-German art mediation between 1871 and 1960, using Computer Vision and Data Visualisation tools to work with the documents.

## Database Description

The database (TODO add link) comes from one of the historical projects of the German Forum for Art History in Paris. It is the result of three merged databases :

- *Franco-German Art Mediation 1871-1940 (Paris)*
- *Franco-German Art Mediation 1871-1940 (Berlin)*
- *Franco-German Art Mediation 1945-1960 (Paris)*

These databases contain texts published in German and French journals, exhibitions reviews, books, etc. They were all curated because they talk in some way about art in the other country. The art itself is mostly paintings, but also sculpture, architecture, arts and crafts, and graphic arts. The databases do not claim to be complete.


## Folder organization

The folders are organized in chronological order. In each of the subsection, you will find a notebook or another README.md that explains in details the steps undertaken and discussions about them. Organisation of the repository : 

    .
     ├── 1_data_reconciliation                   # Filling some of the missing IIIF and wikidata links of the database
     ├── 2_gallica_subset                        # Preparing a subset of data that will be used for testing
     ├── 3_illustration_detection                # Creating the model to detect illustrations in the documents
     ├── 4_illustration_extraction               # Extracting the illustrations in the documents
     └── README.md





