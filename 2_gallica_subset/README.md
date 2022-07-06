# Finding a subset of relevant documents

So now let's start thinking about the illustrations in the database. Because our goal is to work with illustrations, we will need to find the documents where there are illustrations. 

Thankfully, the previous researchers (the one that created the database), made a selection of documents that have relevant illustrations (in `data/DFKV_id_illustration.csv`). We use their work to first focus on these documents. Moreover, among these documents, not all of them have a IIIF link where we can visualize and download the digitized documents. We obviously only keep the ones with a IIIF link. We have this information in the `./data/DFKV_Master.csv`. The columns of the csv are : 

| Column Name | Description |
|---|---|
| ID | ID of the data entry |
| Volume_ID | ID of the Volume, from ../1_data_reconciliation/DFKV_Master.xsl |
| \_journal-id | ID of the journal the data entry is a part of, from ../1_data_reconciliation/DFKV_Master.xsl |
| liens iiif | IIIF link to the document, if any, either from Gallica or Heidelberg University |
| liens de citation (page) | IIIF link directly to the page of the citation |
| liens de citation (volume) | IIIF link directly to the volume of the citation |
| bibliography | Additional Information for the bibliography of the data entry, usually contains pages number information |


To simply the problem even more, we only look at Gallica links from the Bnf (later on we will use more of the documents available).

The steps to gather this subset are explained and done in the notebook `Gallica_subset.ipynb`, and the results are in `data/DFKV_Gallica_subset.csv`, which columns are : 

| Column Name | Description |
|---|---|
| ID | ID of the data entry |
| PW_bemerkung_extern | Description of the data entry |
| bibliographie | Additional Information for the bibliography of the data entry, usually contains pages number information | 
| link_image | IIIF link to the image of the first page of the article of the data entry |
| link_manifest | IIIF link to the manifest of the data entry |
| length | Length of the whole document where the article of the data entry is |

The images are not saved in the github repo, because of of the large number of images, but you can download them yourself by running the notebook. At the end, we have retained 210 documents.
