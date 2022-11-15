# Code First Girls SQL Project

## 🐮 Data Exploration: 'Happy Cow' App

### Creating tables within a database

<details>
	
<summary>EER Diagram</summary>
<img width="796" alt="Screenshot 2022-11-15 at 20 03 39" src="https://user-images.githubusercontent.com/111752964/202016829-d159301f-77d2-497d-a8e4-4efa48f2eda6.png">
	
</details>

<details>
	
<summary>SQL code</summary>

```sql
create database HappyCow;
use HappyCow;

create table Users (
Users_id INTEGER NOT NULL AUTO_INCREMENT,
    first_name VARCHAR(55) NOT NULL,
    last_name VARCHAR(55) NULL,
    email_id text,
    city Varchar(55) not null,
    Food_preference varchar(55) not null,
    PRIMARY KEY (Users_id)
);

create table Cuisine (
ID INT NOT NULL AUTO_INCREMENT,
Cuisine_name VARCHAR(50) NOT NULL,
 primary key (ID),
constraint Cuisine_unique UNIQUE (Cuisine_name)
);

create table Restaurants (
id int NOT NULL auto_increment,
Restaurant_name varchar (50) not null,
Restaurant_type enum('Vegan', 'Vegetarian', 'Veg-Options'),
City VARCHAR(55) NOT NULL,
Price text,
Number_of_Reviews int(3),
primary key (id),
constraint restaurant_unique UNIQUE (Restaurant_name, City)
);

create table Review (
Review_id int not null auto_increment,
user_id int not null references Users(Users_id),
restaurant_id int not null references Restaurants(id),
date_posted date not null,
Rating int not null,
constraint Rating_ck CHECK (Rating IN (1,2,3,4,5)),
primary key (Review_id)
);


create table Cuisine_Restaurants(
Cuisine_id int references Cuisine(ID),
restaurant_id int references Restaurants(id),
primary key (cuisine_ID, restaurant_id)
);

create table CuisineName_Restaurants
SELECT restaurant_id, Cuisine_name
FROM Cuisine_Restaurants
INNER JOIN Cuisine
	ON Cuisine_Restaurants.cuisine_id=Cuisine.ID
   order by restaurant_id asc
    ;
```
</details>

### Populating the tables:

<details>
	
<summary>SQL code</summary>

App user names were generated using [Random Name Generator](https://www.behindthename.com/random/)
````sql
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Virgee', 'Deering', 'Virgee.Deering@gmail.com', 'Nottingham', 'Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Petr', 'Lando', 'Petr.Lando@gmail.com', 'Mansfield', 'Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Caryn', 'Benjaminson', 'Caryn.Benjaminson@gmail.com', 'Nottingham', 'Non-Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Petr', 'Lando', 'Petr.Lando@gmail.com', 'Nottingham', 'Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Tommie', 'Womack', 'Tommie.Womack@gmail.com', 'Nottingham', 'Non-Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Allen', 'Dickenson', 'Allen.Dickenson@gmail.com', 'Nottingham', 'Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Christiana', 'Evelyn', 'Christiana.Evelyn@gmail.com', 'Sheffield', 'Non-Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Margo', 'Lowe', 'Margo.Lowe@gmail.com', 'Sheffield', 'Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Constance', 'Lewis', 'Constance.Lewis@gmail.com', 'Derby', 'Non-Veg');
insert into Users (first_name, last_name, email_id, city, Food_preference) values ('Godfrey', 'Garry', 'Godfrey.Garry@gmail.com', 'Derby', 'Veg');

	
INSERT INTO Cuisine (Cuisine_name) VALUES("British");
INSERT INTO Cuisine (Cuisine_name) VALUES("American");
INSERT INTO Cuisine (Cuisine_name) VALUES("American-Mexican");
INSERT INTO Cuisine (Cuisine_name) VALUES("Italian");
INSERT INTO Cuisine (Cuisine_name) VALUES("International");

INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("No. Twelve", 'Vegan', 'Nottingham', '$$', 70);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Prickly Pear", 'Vegan', 'Nottingham','$$', 57);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Crocus Cafe", 'Vegetarian', 'Nottingham', '$', 21);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Cafe Roya", 'Vegetarian', 'Nottingham', '$$$', 30);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Plant Cafe and Bar", 'Vegan', 'Derby','$$', 39);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Vegan Revelation", 'Vegan', 'Belper', '$', 37);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("The Golden Fleece", 'Vegan', 'Nottingham', '$$', 18);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("13th Element", 'Vegan', 'Nottingham', '$$', 35);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Annie's Burger Shack", 'Veg-Options', 'Nottingham', '$$', 72);
INSERT INTO Restaurants (Restaurant_name, Restaurant_type, City, Price, Number_of_Reviews) VALUES ("Oscar and Rosies", 'Veg-Options', 'Nottingham', '$$', 23);

insert into Review (user_id, restaurant_id, date_posted, Rating) values (1, 10, '2022-10-02', 4);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (2, 9, '2022-08-14', 3);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (3, 8, '2021-11-09', 4);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (4, 7, '2022-09-20', 5);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (5, 6, '2022-10-02', 3);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (6, 5, '2021-09-21', 2);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (7, 4, '2021-10-28', 4);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (8, 3, '2022-07-20', 4);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (9, 2, '2022-06-17', 5);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (10, 1,'2022-03-06', 5);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (4, 1, '2022-05-05', 5);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (9, 6, '2021-08-24', 4);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (3, 1, '2021-06-01', 4);
insert into Review (user_id, restaurant_id, date_posted, Rating) values (1, 6, '2021-06-07', 4);

INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (4,1);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (2,2);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (3,3);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (5,4);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (5,5);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (1,6);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (1,7);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (1,8);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (2,9);
INSERT INTO Cuisine_Restaurants (cuisine_id, restaurant_id) VALUES (5,10);
````
</details>

### Data Exploration:

#### Which restaurants have been reviewed more than once by the users in the data set?

````sql
SELECT id, Restaurant_name, count(*) as Times_Reviewed 
FROM Restaurants
INNER JOIN Review 
  ON Restaurants.id = Review.restaurant_id
  group by id
  having Times_Reviewed>1
  order by id asc
;
````
#### Which restaurants have British Cuisine?
````sql
-- By joining tables:

select Restaurant_name as Restaurant, Cuisine_name as Cuisine
from Restaurants
inner join CuisineName_Restaurants
	on Restaurants.id=CuisineName_Restaurants.restaurant_id
    where Cuisine_name = 'British'
;

-- By subquery:

select Restaurant_name as Restaurant
from Restaurants
where id in (
	select restaurant_id
    from CuisineName_Restaurants
    where Cuisine_name = 'British')
    ;
 ````
 #### What are the 3 most reviewed vegan restaurants in Nottingham?
````sql
 select Restaurant_name as Popular_Vegan_Restaurants_Nottingham, Number_of_Reviews
 from Restaurants
 where Restaurant_Type = 'Vegan' and City = 'Nottingham'
 order by Number_of_Reviews desc
 limit 3;
````

#### What's the price range of the best reviewed vegan restaurant rated by the non-veg customers?
````sql
select Restaurant_name as Restaurant,
	case
	when (Restaurants.Price = '$')
        then 'Affordable'
        when (Restaurants.Price = '$$')
        then 'Mid-Range'
        else 'Fancy'
	end as Price_Range
from Restaurants
inner join Review
on Restaurants.id=Review.restaurant_id
where user_id in (
	select user_id
    from Users
	where Food_preference = 'Non-Veg')
and Restaurant_type = 'Vegan'
order by Rating desc
limit 1
;
````
#### Creating a view of user restaurant ratings for different cuisines:
````sql
use HappyCow;
CREATE VIEW User_Reviews
AS 
SELECT email_id, Users.City as 'From' , Restaurant_name, Restaurant_type, Restaurants.City, Price, Cuisine_name as Cuisine, Number_of_reviews as Total_Reviews, Date_Posted, Rating as User_Rating
from Restaurants
inner join Review 
on Restaurants.id=Review.restaurant_id
inner join CuisineName_Restaurants
on Review.restaurant_id=CuisineName_Restaurants.restaurant_id
inner join Users
on Review.user_id=Users.Users_id
;
````
#### How are non-locals rating restaurants in Nottingham?
````sql
SELECT email_id, user_reviews.from, Restaurant_name, Restaurant_type, User_Rating FROM HappyCow.user_reviews
where user_reviews.from != 'Nottingham' and City = 'Nottingham'
order by User_Rating desc;
````

#### What are the two favourite Nottingham veggie restaurant as rated by locals?
````sql
SELECT Restaurant_name, user_rating FROM HappyCow.user_reviews
where user_reviews.From = 'Nottingham' 
and City = 'Nottingham' 
and Restaurant_type like '%Veg%an' 
order by user_rating desc
limit 2;
````

#### Best rated cuisine from the users in the database?
````sql
select Cuisine, round(avg(User_Rating))as Average_Rating FROM HappyCow.user_reviews
group by Cuisine
order by Average_Rating desc
limit 1;
````
### Utilising a stored function to determine whether a restaurant is popular:

````sql
use HappyCow;
DELIMITER //
CREATE FUNCTION is_popular(
    number_of_reviews INT
) 
RETURNS VARCHAR(20)
DETERMINISTIC
BEGIN
    DECLARE Restaurant_Status VARCHAR(20);
    IF number_of_reviews > 50 THEN
        SET Restaurant_Status = 'Very popular';
    ELSEIF (number_of_reviews >= 20 AND 
            number_of_reviews <= 50) THEN
        SET Restaurant_Status = 'Getting There';
    ELSEIF number_of_reviews < 50 THEN
        SET Restaurant_Status = 'Not so much';
    END IF;
    RETURN (Restaurant_Status);
END//number_of_reviews
DELIMITER ;

select Restaurant_name, is_popular(number_of_reviews) as How_Popular from Restaurants;
````
### Creating a stored procedure to quickly add any new reviews for the existing users within the database:
````sql
CREATE PROCEDURE Current_User_Reviews(
IN review_id int, 
IN user_id int,
IN restaurant_id int,
IN date_posted date,
IN Rating int)
BEGIN

INSERT INTO Review(review_id,user_id, restaurant_id, date_posted,Rating)
VALUES (review_id,user_id, restaurant_id, date_posted,Rating);

END//
````
