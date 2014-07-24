# Apartment lab

- Create a database called apartmentlab

```
CREATE DATABASE apartment_lab;
```
- Using this database, create two tables, one for owners and one for properties

```
CREATE TABLE owners(owner_id SERIAL PRIMARY KEY, name VARCHAR(10), age INTEGER);

CREATE TABLE properties(property_id SERIAL PRIMARY KEY, name VARCHAR(20), num_units VARCHAR(10), owner_id INTEGER NOT NULL);
```
- Keep this relationship in mind when designing your schema:
  + **One owner can have many properties**

###Tables

- The owners table should consist of: 
  + owner_id (this should be the primary key as well as a unique number that increments automatically)
  + name
  + age
  
```
SELECT * FROM owners;
 owner_id | name | age 
----------+------+-----
(0 rows)
```
- The properties table should consist of:
  + property_id (this should be the primary key as well as a unique number that increments automatically)
  + name
  + number of units
  + owner_id (this should have the constraint NOT NULL)
    + There should be also be a foreign key that references the owners table
  
```
SELECT * FROM properties;
 property_id | name | num_units | owner_id 
-------------+------+-----------+----------
(0 rows)

ALTER TABLE properties ADD CONSTRAINT owner_fk FOREIGN KEY (owner_id) REFERENCES owners (owner_id) ON DELETE NO ACTION;
```

###Questions
Write down the following sql statements that are required to solve the following tasks.
   
- Show all the tables: 

```
\dt
```
- Show all the users: 

```
\dg
```
- Show all the data in the owners table: 

```
SELECT * FROM owners;
```
- Show the names of all owners:

```
SELECT name FROM owners;
```
- Show the ages of all of the owners in ascending order:

```
SELECT age FROM owners ORDER BY age ASC;
```
- Show the name of an owner whose name is Donald:

```
SELECT * FROM owners WHERE name='Donald';
``` 
- Show the age of all owners who are older than 30. 

```
SELECT * FROM owners WHERE age > 30;
```
- Show the name of all owners whose name starts with an E:

```
SELECT * FROM owners WHERE name LIKE '%E'; 
``` 
- Add an owner named John who is 33 years old to the owners table:

```
INSERT INTO owners (name, age) VALUES ('John', 33);
```
- Add an owner named Jane who is 43 years old to the owners table:

```
INSERT INTO owners (name, age) VALUES ('Jane', 43);
```
- Change Jane's age to 30:

```
UPDATE owners SET age=30 WHERE name='Jane';
``` 
- Change Jane's name to Janet:

```
UPDATE owners SET name='Janet' WHERE name='Jane';
``` 
- Add a property named Archstone that has 20 units:

```
INSERT INTO properties (name, num_units, owner_id) VALUES ('Archstone', 20, 1);
``` 
- Delete the owner named Jane:

```
// 'Janet' since we changed Jane's name above
DELETE FROM owners WHERE name='Janet';
```
- Show all of the properties in alphabetical order that are not named Archstone and do not have an id of 3 or 5.

```
SELECT * FROM properties WHERE name NOT IN ('Archstone') AND property_id NOT IN (3, 5) ORDER BY name ASC;

// <> syntax also works
SELECT * FROM properties WHERE name <> 'Archstone' AND property_id <> (3, 5) ORDER BY name ASC;
``` 
- Count the total number of rows in the properties table.

```
SELECT COUNT(*) FROM properties;
```
- Show the highest age of all owners.

```
SELECT MAX(age) FROM owners;
```
- Show the names of the first three owners in your owners table.

```
SELECT * FROM owners LIMIT 3;
```
- Create a foreign key that references the owner_id in the owners table and forces the constraint ON DELETE NO ACTION. 

```
ALTER TABLE properties ADD CONSTRAINT owner_fk FOREIGN KEY (owner_id) REFERENCES owners (owner_id) ON DELETE NO ACTION;
```
- Show all of the information from the owners table and the properties table in one joined table.

```
SELECT owners.name, properties.name FROM owners JOIN properties ON owners.owner_id=properties.owner_id;
``` 
- Bonus (this might require you to look up documentation online)
  + In the properties table change the name of the column "name" to "property_name". 
  + Count the total number of properties where the owner_id is between 1 and 3.
  
```
ALTER TABLE properties RENAME COLUMN "name" to "property_name";

SELECT COUNT(*) FROM properties WHERE owner_id BETWEEN 1 AND 3;
// < 4 also works
SELECT COUNT(*) FROM properties WHERE owner_id < 4;
```
