# Illustration metadata enrichment

We now have all the illustrations that are present in our corpus. We want to make the dataset more interesting by adding some metadata to the illustrations. 

The proposed steps are :

- Finding the category of the object illustrated
- Associate illustrations with descriptors from researchers
- Find topics discussed around the illustrations
- Find name/authors of artworks

# Clustering of images based on structural similarity

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

