# Data reconciliation

Each document in the database has, among other attributes, an author and people that the document talks about. These are two informations that are available in the database (`data/DFKV_Data_complet.xlsx`), under the `créateur_créatrice` and `impliqué`attributes. Then each person (in `people.xls`) has the following attributes : an ID, a display name, a first name, a last name, a ULAN link, and a Wikidata link. The ULAN and Wikidata link are there to provide a link to an open knowledge database. However, the process of reconciliation (i.e. finding and attributing a knowledge base link to an entity of our database) is not complete for every person. 

We observe, in particular, that some people have their first and last name both in the first and last name columns, like in the example below :

| ID            | Display Name         | First Name           | Last Name            |
| ------------- |:--------------------:| --------------------:| --------------------:|
| 8967          | Pauvert Jean-Jacques | Pauvert Jean-Jacques | Pauvert Jean-Jacques |

These are usually names that are easy to reconciliate, we find them using the `people_reconcilitation.ipynb`notebook and fill some of the blanks of the database. Of course, some names are still too obscure to be found in Wikidata, in which case we either add one entry to Wikidata ourselves, or if we can't find the type of person they are then we leave the column blank.

We also do this work of reconciliation for some of the journals in the database, to link them with a BNF link.


