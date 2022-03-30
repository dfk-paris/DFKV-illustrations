# Illustration metadata enrichment

We now have all the illustrations that are present in our corpus. We want to make the dataset more interesting by adding some metadata to the illustrations. 

The proposed steps are :

- Finding the category of the object illustrated
- Associate illustrations with descriptors from researchers
- Find topics discussed around the illustrations
- Find name/authors of artworks

# Clustering of images based on structural similarity

To have a first look at the dataset structure, we first used [Pixplot](https://github.com/YaleDHLab/pix-plot), to visualize our illustrations in a two-dimensional projection within which similar images are clustered together. We use the HDBCAN algorithm to create the clusters of images, and then UMAP to be able to visualize the results into the 2D space. With this first approach, we can identify different types of illustrations that we have :

TODO
