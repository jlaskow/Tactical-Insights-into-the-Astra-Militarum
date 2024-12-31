# Tactical-Insights-into-the-Astra-Militarum

Warhammer 40K is a popular table-top game published by Games Workshop, a manufacturing company based in Nottingham, England - best known for the manufacture and distribution of 'miniature wargames'. The most popular of their products, as previously mentioned, is Warhammer 40K, which sees player pit opposing armies, represented by miniature figurines, against each other. 

This franchise has become highly lucrative, generating an estimated £ 445.4 million in 2023 alone. Since its creation in 1975, the developers have introduced a litany of 'factions' to suit different playstyles. As an exercise in the use of SQL and NoSQl databases, we will build a database catalouging the various factions this game has to offer. In time, we hope that this data can be explored to identify potential strategies available for each faction.

Kaggle houses multiple public datasets that record stats on figurines from these various factions. Each figurine comes with a 'cost' and an assorted  list of additional traits that dictate how they can be used in a game. 

Link to datasets:

https://www.kaggle.com/datasets/cjblue83/warhammer-40k-model-stats

We will store and clean all datasets in MongoDB, an open-source NOSQL database platform.


# Attributes and Terminology

Any faction army consists of figurines (or units) with pre-written stats. Depending on the units you choose, you can optimize your army to perform different strategies. Understanding the attributes and stats of each unit is key to finding the optimal strategy.

![image](https://github.com/user-attachments/assets/486e0428-2751-4c9b-ae96-fe026c1aea77)


## points_value

![image](https://github.com/user-attachments/assets/fa9050a9-f6d8-48a8-b011-82b14a0d51c9)

 Each unit has a point cost, limiting the number of assets you can put on the board; such point costs can increase if you equip a unit with weapon upgrades or additional special abilities. 

  - For example, in a 100-point game, a player might assemble 5 Space Marines at 20 points each (100 total). You could, instead, assemble 2 Space Marines upgraded with more powerful weaponry (50 points each).

## model_count

![image](https://github.com/user-attachments/assets/d04a34e2-b594-41a3-9386-c360ab788808)

A unit can exist on its own or in a squad, where all units act as one and gain additional perks. The minimum number of units required to form a squad depends on the unit in question; similarly, maximum units per squad is dependent on the unit.

## movement

![image](https://github.com/user-attachments/assets/c8a6149e-4eba-4d66-bdf2-d0c93a8aefd8)

Movement determines how many inches a unit may move per turn

## weapon_skill

![image](https://github.com/user-attachments/assets/d5b0bbf7-4ba7-4721-8e46-d0622d53838b)

Weapon skill determines a unit's effectiveness in melee combat. The weapon_skill determines the minimum value you must roll on a 6-sided die (1d6) in order to successfully attack in melee with a unit. 

## ballistic_skill

![image](https://github.com/user-attachments/assets/833fc7e0-57d4-4f45-b077-df5b23ed407b)

Weapon skill determines a unit's effectiveness in ranged combat. The weapon_skill determines the minimum value you must roll on a 6-sided die (1d6) in order to successfully attack at range with a unit. 

## strength and toughness

![image](https://github.com/user-attachments/assets/4f1a0d85-8f5d-4e43-9217-bbfb1d12bd9d)

Assuming a unit succeeds on its weapon/ballistic skill check, the controlling player compare's the unit's strength value to the target's toughness. If:

- strength < toughness:
  Player rolls a 1d6. On a 5+, the unit inflicts damage to the target
  
- strength = toughness:
  Player rolls a 1d6. On a 4+, the unit inflicts damage to the target

- strength > toughness:
  Player rolls a 1d6. On a 2+, the unit inflicts damage to the target

## attacks

![image](https://github.com/user-attachments/assets/2e9f78fe-efec-4750-84c3-578dcedf5389)

The number of attacks a unit may attampt per turn

## leadership

![image](https://github.com/user-attachments/assets/7eeb4f9d-8aa5-4f3d-88c7-10c216e26cc9)

Leadership represens the minimum number you must roll on a 1d6 for a unit to resist debilitating conditions in combat. The higher the minimum, the more difficult it is for that unit to resist a condition (see Conditions in Terminology  section for more information)

## saves

If a unit successfully roles to attack and overcomes the strength vs toughness challenge, the target must make a save or take a wound. The higher the save value, the higher the target must role on a 1d6 to resist taking a wound. 

## wounds

![image](https://github.com/user-attachments/assets/4e3c624c-a621-4aa6-b7ab-edd190a52f6d)

This determines the amount of damage a unit can sustain before being eliminated











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
