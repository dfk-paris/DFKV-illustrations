# Layout Study

This last part of the project is starting to describe the materiality of the objects in the database. The work done here is just a first step into that direction. In the notebook `a_layout_study.ipynb`, we start by noticing that the way the documents were digitized is not always the same, there could be one or two pages on the same digitized document. We could then look at where the illustrations were on the pages using a heatmap. Then, we precise the study by analysing specifically the differences between journals, and between the different kinds and sizes of illustrations.

## Data

The data you can find in this section is : 
- `illu_pos.json`: the keys is the illustration's id and the value is another dictionnary containing the coordinates of the illustration on the page, and the dimensions of the page
- `illu_ratios.json` : the keys is the illustration's id and the value is the percentage of place that the illustrations takes on the page (between 0 and 1)
