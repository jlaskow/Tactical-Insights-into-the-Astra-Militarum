# Tactical-Insights-into-the-Astra-Militarum

Warhammer 40K is a popular table-top game published by Games Workshop, a manufacturing company based in Nottingham, England - best known for the manufacture and distribution of 'miniature wargames'. The most popular of their products, as previously mentioned, is Warhammer 40K, which sees player pit opposing armies, represented by miniature figurines, against each other. 

This franchise has become highly lucrative, generating an estimated £ 445.4 million in 2023 alone. Since its creation in 1975, the developers have introduced a litany of 'factions' to suit different playstyles. As an exercise in the use of SQL and NoSQl databases, we will build a database catalouging the various factions this game has to offer. In time, we hope that this data can be explored to identify potential strategies available for each faction.

Kaggle houses multiple public datasets that record stats on figurines from these various factions. Each figurine comes with a 'cost' and an assorted  list of additional traits that dictate how they can be used in a game. 

Link to datasets:

https://www.kaggle.com/datasets/cjblue83/warhammer-40k-model-stats

We will store and clean all datasets in MongoDB, an open-source NOSQL database platform.




# Astra Militarum

The first faction we will explore is the Astra Militarum. This is a versatile faction favoring strong, heavy-hitting artillary and large quantities of cheap, highly mobile infantrymen. 

![image](https://github.com/user-attachments/assets/8a9e1149-c903-40b0-9d4c-9171f1fd457b)


Initially, each playable figurine is listed in a JSON file, with names representing Keys:

![image](https://github.com/user-attachments/assets/eaa8c33b-cd65-4084-bb5f-8db86821de52)

This formatting can make it difficult to filter by keywords; in addition, we see that figurines sold in sets (sold together) are grouped under the same parent key:

![image](https://github.com/user-attachments/assets/e2b74da7-0c69-49b7-b433-4dafe41553c4)

These issues can make querying more time-consuming and tedious.

We refine the dataset to classify each figurine as a distinct document in the NoSQL collection. A new attribute, 'name', is included for each figurine. A 'parent' is included to track figurines related by set. Unique object IDs ('oID') are also included for each figure, in case we later obtain metrics like sales data, common strategies, and public opinions. The added benefit is that this streamlined format also makes querying in MongoDB Compass (a MongoDB GUI) far simpler.

![image](https://github.com/user-attachments/assets/fec0f634-443c-496a-8408-bef5d35e6c56)


Available data does not contain damage values for any unit. This is problematic for any assessment of strategic ability. Rather than meticulously identify the damage associated with each unit, we use ChatGPT to identify appropriate damage values for each unit. These values are initially collected from ChatG{T as a csv file. 


[We next need to merge the csv file with the JSON file]
