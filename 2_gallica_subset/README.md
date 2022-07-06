# Finding a subset of relevant documents

So now let's start thinking about the illustrations in the database. Because our goal is to work with illustrations, we will need to find the documents where there are illustrations. 

Thankfully, the previous researchers (the one that created the database), made a selection of documents that have relevant illustrations (in `data/DFKV_id_illustration.csv`). We use their work to first focus on these documents. Moreover, among these documents, not all of them have a IIIF link where we can visualize and download the digitized documents. We obviously only keep the ones with a IIIF link. To simply the problem even more, we only look at Gallica links from the Bnf (later on we will use more of the documents available).

The steps to gather this subset are explained and done in the notebook `Gallica_subset.ipynb`, and the results are in `data/DFKV_Gallica_subset.csv`. The images are not saved in the github repo, because of of the large number of images, but you can download them yourself by running the notebook.

At the end, we have retained 210 documents.
