To work with illustrations, the first thing that we need to do is extracting these illustrations. This task is quite big, so we break down the process by first finding a subset of the data that we know contains interesting illustrations.

# Finding a subset of relevant documents


Thankfully, the previous researchers (the one that created the database), made a selection of documents that have relevant illustrations (in `data/DFKV_id_illustration.csv`). We use their work to first focus on these documents. Moreover, among these documents, not all of them have a IIIF link where we can visualize and download the digitized documents. We obviously only keep the ones with a IIIF link. To simply the problem even more, we only look at Gallica links from the Bnf (later on we will use more of the documents available).

This steps to gather this subset are explained and done in the notebook `Gallica_subset.ipynb`, and the results are in `data/DFKV_Gallica_subset.csv`. The images are not saved in the github repo, because of of the large number of images, but you can download them yourself by running the notebook.
