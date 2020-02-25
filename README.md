### [Makers Academy](http://www.makersacademy.com) - Week 6 Group Programming Project

Makers AirBnb 
-

[Outline](#Outline) | [Task](#Task) | [User Stories](#Story)| [Installation Instructions](#Installation) | [Database Setup](#Database) | [Tables](#Tables) | [Features of MakersBnb](#Features) | [Technologies used](#Technologies) | [Contributors](#Contributors) 

## <a name="Outline">Outline</a>
 
Build MakersBnb

## <a name="Task">The Task</a>

This week we've been grouped together to build our very own AirBnb clone using everything we've learned over the past 5 weeks at Makers.

## <a name="Story">User Stories</a>

```

As a user, 
when I visit MakersBnB,
I would like to sign up with my email and password.

As a user,
when I visit MakersBnB,
I would like to sign in with my account details.

As a user,
when I'm logged into MakersBnB, 
I want to see a list of available spaces.

As a user and potential space owner,
when I'm logged into MakersBnB, 
I would like to list a space.

As a user and space owner,
when I list a space on MakersBnB,
I would like to enter details, like a name, description, price, and available dates.

As a user,
when I've chosen a space I'd like to hire, 
I want to see the dates the space is available on.

As a user,
when I've chosen a space and the dates I'd like to book,
I want to put in a request to hire that space.

As a user,
when I've chosen a space,
I should be able to see the dates the space has already been booked or that are unavailable.

As a user,
when I have made a request to hire a space,
I would like to see the status of my requests. 

As a user and space owner,
when I have listed my space and another user has requested it, 
I would like to see a list of these requests.

As a user and space owner,
when I've listed a space,
I should be able to receive multiple hire requests for the same dates until one is approved. 

As a user and space owner,
when I receive a hire request, 
I want to be able to confirm or deny the request. 

```

## <a name="Installation">Installation Instructions</a>

### Clone the git repository to your local computer

```
git clone https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby.git
cd Makers_MakersBnb_Ruby
```

## <a name="Database">How to set up the database</a>

Type in the commands 'irb' followed by `psql` to connnect to your user postgres database and use the command 'CREATE DATABASE *name*' create the `makersbnb_test` and `makersbnb` databases:

```
CREATE DATABASE makersbnb;
CREATE DATABASE makersbnb_test;
```

Once you're connected to the makersbnb databases set up the appropriate tables, connect to each database in `psql` using \c *databasename* and run the SQL scripts in the `db/migrations` folder.


```
yourusername=# \c makersbnb
You are now connected to database "makersbnb" as user "yourusername".

makersbnb=# CREATE TABLE users(
makersbnb(#   id SERIAL PRIMARY KEY,
makersbnb(#   user_name TEXT NOT NULL,
makersbnb(#   email TEXT NOT NULL unique,
makersbnb(#   password_digest TEXT NOT NULL
makersbnb(# );

makersbnb=# CREATE TABLE properties(
makersbnb(#   id SERIAL PRIMARY KEY,
makersbnb(#   prop_name VARCHAR(200),
makersbnb(#   prop_description VARCHAR(2000),
makersbnb(#   price_per_night INTEGER,
makersbnb(#   startdate DATE,
makersbnb(#   enddate DATE,
makersbnb(#   owner_id INTEGER REFERENCES users(id)
makersbnb(#     
makersbnb(# );

makersbnb=# CREATE TABLE bookings(
makersbnb(#   id SERIAL PRIMARY KEY,
makersbnb(#   prop_id INTEGER REFERENCES properties(id),
makersbnb(#   client_id INTEGER REFERENCES users(id),  
makersbnb(#   owner_id INTEGER REFERENCES users(id),
makersbnb(#   startdate date,
makersbnb(#   enddate date,
makersbnb(#   length_of_stay INTEGER,
makersbnb(#   total_price INTEGER,
makersbnb(#   confirmation BOOLEAN NOT NULL
makersbnb(# );

```
and do the same for the makersbnb_test tables.

## <a name="Tables">Tables</a>

Now you should have the following tables:

Users:

| id     | user_name | email | password_digest |
|--------|-----------|-------|-----------------|
|        |           |       |                 | 

Properties:

| id     | prop_name | prop_description | price_per_night | startdate | enddate | owner_id |
|--------|-----------|------------------|-----------------|-----------|---------|----------|
|        |           |                  |                 |           |         |          |

Bookings: 

| id |  propr_id  |  client_id  | owner_id |  startdate  |  enddate  | length_of_stay | total_price | confirmation |
|----|------------|-------------|----------|-------------|-----------|----------------|-------------|--------------|
|    |            |             |          |             |           |                |             |              |  


## <a name="Features">Features of MakersBnb</a>

Users can sign up to MakersBnb:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-Sign-Up.png)

Users can log in if they have an account:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-Sign-in.png)

Once they're logged in, they are taken to the spaces page, where they can see a list of all the available spaces/properties to rent, and can filter the results by their desired dates:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-Spaces.png)

Users can also list their own space or property:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-List-your-space.png)

Once the user has decided on a space to rent, they're asked to select the dates they'd like to book:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-Date-Confirmation.png)

Once they've made a booking request, they'll be taken to the requests page, where they'll be able to see all the spaces they've made requests for and all the requests that have been made for their spaces:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-Requests.png)
*If they click on any booking request in the requests made column, they have the ability to change the dates of their booking.*

In the requests received column, they can select which bookings to confirm or deny:
![](https://github.com/BenSheridanEdwards/Makers_MakersBnb_Ruby/blob/master/images/MakersBnb-Request-Confirmation.png)



## <a name="Technologies">Technologies used</a>

* **Ruby & JavaScript** to write the application.
* **Sinatra** framework as our DSL.
* **Bootstrap** for styling.
* **BCrypt** for password hashing.
* **PostgresSQL** as our database.
* **Capybara** and **Rspec** for testing.
* **Github** for code collaboration.

## <a name="Contributors">Contributors</a>

* [Ben Sheridan-Edwards](https://github.com/BenSheridanEdwards)
* [Raluca Ciucu](https://github.com/IngramCapa)
* [Jonathan Palma](https://github.com/JonathanPalma-code)
* [Shafique Mohammed](https://github.com/shafali03)

