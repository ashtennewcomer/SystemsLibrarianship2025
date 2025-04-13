# Log Entry

**April 13, 2025**

In week 9, I created a relational database to be used by my OPAC and cataloging modules. 

Relational databases organize data into tables using rows and columns to organize the data. Links for related data can also be used across tables to reduce duplicated entries and structure the data so it is easy to understand and retrieve. 

1. Updated my virtual machine:
  * `sudo apt update`
  * `sudo apt -y upgrade`
  * `sudo apt -y autoremove`
  * `sudo apt clean`
2. Logged into MySQL as root user: `sudo mysql -u root` in order to have the privleges to create a new database
3. Created a database called "DinnerDB": `create database DinnerDB;`
4. Granted all privileges to `opacuser`: `grant all privileges on DinnerDB.* to 'opacuser'@'localhost';`
5. Exited as root user and logged in as `opacuser`
6. Changed to DinnerDB database: `use DinnerDB;`
7. Created Meals table:
  * `meal_id` is the primary key
  * `meal_name` is a variable-length sting (up to 100 characters)
  * `cuisine` is a variable-length string (up to 50 characters)
  * `cooking_time` uses CHECK constraint and can't contain a zero or negative value
  * `vegetarian` is a BOOLEAN value and must be TRUE or FALSE
  * Full code:
    ```
    create table Meals (
      meal_id int auto_increment primary key,
      meal_name varchar(100) not null,
      cuisine varchar(50),
     cooking_time int not null default 1 check (cooking_time > 0),
      vegetarian boolean
    ); 
    ```
8. Created Ingredients table:
  * `ingredient_id` is the primary key
  * `meal_id` is an integer and will link back to the Meals table; this makes the Ingredients table a child of the Meals table
  * `ingredient_name` is a variable-length string (up to 100 characters)
  * `quantity` is a variable-length string (up to 50 characters
  * Full code:
    ```
    create table Ingredients (
      ingredient_id int auto_increment primary key,
      meal_id int,
      ingredient_name varchar(100) not null,
      quantity varchar(50),
      foreign key (meal_id) references Meals(meal_id) on delete cascade
      );
      ```
9. Inserted data into Meals table:
  ```  insert into Meals (meal_name, cuisine, cooking_time, vegetarian) values
    ('Spaghetti Bolognese', 'Italian', 45, FALSE),
    ('Vegetable Stir Fry', 'Chinese', 20, TRUE),
    ('Chicken Curry', 'Indian', 50, FALSE),
    ('Mushroom Risotto', 'Italian', 35, TRUE);
  ```
10. Inserted data into Ingredients table:
  ``` insert into Ingredients (meal_id, ingredient_name, quantity) values
    (1, 'Spaghetti', '200g'),
    (1, 'Ground Beef', '250g'),
    (1, 'Tomato Sauce', '1 cup'),
    (2, 'Broccoli', '100g'),
    (2, 'Carrots', '50g'),
    (2, 'Soy Sauce', '2T'),
    (3, 'Chicken Breast', '300g'),
    (3, 'Curry Powder', '2T'),
    (3, 'Coconut Milk', '1 cup'),
    (4, 'Arborio Rice', '1 cup'),
    (4, 'Mushrooms', '1 cup'),
    (4, 'Parmesan Cheese', '1/2 cup');
   ```
11. Practiced querying data using the following commands:
  *  `select * from Meals;`
  *  `select * from Meals where vegetarian = TRUE;`
  *  `select * from Meals order by cooking_time desc;`
  *  `select * from Meals order by cooking_time asc; `
  *  ```
       select Meals.meal_name as Meals,
       Ingredients.ingredient_name as Ingredients,
       Ingredients.quantity as Quantity
       from Meals
       join Ingredients on Meals.meal_id = Ingredients.meal_id;
     ```
  * ``` select ingredient_name as Ingredients,
    quantity as Quantity
    from Ingredients 
    where meal_id = (select meal_id from Meals where meal_name = 'Chicken Curry');
    ```
  * ``` select cuisine, count(*) as meal_count 
    from Meals
    group by cuisine;
    ```
  * ```select meal_name, cooking_time 
    from Meals 
    where cooking_time <= 45
    order by cooking_time asc;
    ```

Other commands:
  * To re-review privileges: `show grants for 'opacuser'@'localhost';`
  * To revoke privileges: `revoke all privileges on DinnerDB.* from 'opacuser'@'localhost';`
  * Query user table: `select user, host from mysql.user;`
  * Delete database: `drop database DinnerDB;`
  * Delete user: `drop user 'sean'@'localhost';`
