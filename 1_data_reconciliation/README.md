# Database description

The database *Deutch-Französische Kunstvermittlung 1870-1940 und 1945-1960* contains in total around 6700 entries of articles about art criticism. It was initiated by a bilateral research team between Paris and Berlin in 1997, and the data was saved in a ProWeb database. The project was clotured in 2005 by several publications (TODO add source). In 2019, ProWeb gets taken down, so the data is saved into a json file but many features got lost and the searchability was very limited. In 2020, Anne Klammt initialises the curation of the data, working on enriching  with authority files and a new user interface. Alongside, in 2021, Deborah Schlauch started research about the history of the database, contextualising the data and the database. Now, we will try to use computational methods on the data, specifically focusing on the illustrations.

The database consists of multiple excel files, which we will describe as we use them throughout the project. The first one is `./data/DFKV_Data_complet.xlsx`(version of 01.03.2022). The columns are the following :

| Column name        | Description    |  
| -------------------|:--------------------:|
| ID                 | Of the data entry    |  
| project_id         | Project number       | 
| date_human         | Date of the data entry, by researchers | 
| date               | Date of the entry, computer readable | 
| journal_id         | Periodical ID, from DFKV_Master file | 
| volume_id          | Volume ID, from DFKV_Master file | 
| transcription      | Textual description of the content of the data entry | 
| citation           | Original citation from the content of the data entry | 
| rubric_id          | Rubric ID, from the DFKV_Master file | 
| location_id        | Location ID, from the DFKV_Master file | 
| editor_id          | Editor ID, from the DFKV_Master file | 
| sujets             | Subjet ID, from the DFKV_Master file |  
| type de texte      | Type of text ID, from the DFKV_Master file |  
| impliqué           | Person present in the content of the entry (vague definition) | 
| créateur_créatrice | Author of the data entry | 
| traducteur_traductrice | Translator of the text of the data entry | 
| montré          | People pictured in the artworks described in the data entry | 


# Data reconciliation

We see that each document in the database has, among other attributes, an author and people that the document talks about. These are two informations are available under the `créateur_créatrice` and `impliqué` attributes. These attributes are actually a list of IDs, IDs of people that are referenced in the `People` sheet of the `./data/DFKV_Master.xlsx` file (TODO version). You can also find the single sheet - with only the people that do not have at least one authority file linked in `./data/people.xls` (02.03.2022 version). The columns are the following :

| Column name        | Description    |  
| -------------------|:--------------------:|
| ID                 | Old ID of the person   |  
| ID_2               | New ID of the person, the one that is referenced in DFKV_Data_complet   | 
| display_name       | Name to display in website, usually : Last Name, First Name | 
| first_name         | First name of the person| 
| last_name          | Last name of the person | 
| ULAN               | ulan ID, if available | 
| Wikidata           | Wikidata ID, if available| 

The ULAN and Wikidata link are there to provide a link to an open knowledge database. However, the process of reconciliation (i.e. finding and attributing a knowledge base link to an entity of our database) is not complete for every person. We will shortly try to complete some of them.

To try to be smart about it, we observe that some people have their first and last name both in the first and last name columns, like in the example below :

| ID            | Display Name         | First Name           | Last Name            |
| ------------- |:--------------------:| --------------------:| --------------------:|
| 8967          | Pauvert Jean-Jacques | Pauvert Jean-Jacques | Pauvert Jean-Jacques |

These are usually names that are easy to reconciliate, so we find them using the `people_reconcilitation.ipynb` notebook and fill some of the blanks of the database. Of course, some names are still too obscure to be found in Wikidata, in which case we either add one entry to Wikidata ourselves, or if we can't find the type of person they are then we leave the column blank.

We also do this work of reconciliation for some of the journals in the *Journal* sheet of `DFKV_Master.xlsx`, `./data/journal.xls` (TODO version), to link them with a BNF link, mainly to get familiar with the content of the database.
