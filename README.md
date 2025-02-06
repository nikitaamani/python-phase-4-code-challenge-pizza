## Pizza Restaurant API

Date, 2025/01/19 ***Nikita Amani***

This project implements a RESTful API for managing a database of restaurants and their associated pizzas. The API supports operations like retrieving restaurant and pizza details, associating pizzas with restaurants, and deleting restaurant records.

## Features

* Retrieve all restaurants with their associated pizzas.
* Retrieve a specific restaurant by its ID, including the pizzas offered by the restaurant.
* Delete a restaurant along with its associated pizzas.
* Retrieve all pizzas.
* Create a new restaurant-pizza association by associating a pizza with a restaurant and specifying a price.

## Endpoints
### 1. GET /restaurants
Fetches a list of all restaurants.

#### Response
* 200 OK

```
[
  {
    "id": 1,
    "name": "Pizza Hut",
    "address": "123 Main St"
  },
  ...
]
```

### 2. GET /restaurants/{id}
Fetches a specific restaurant by its ID, along with its associated pizzas.

#### Response
* 200 OK

```
{
  "id": 1,
  "name": "Pizza Hut",
  "address": "123 Main St",
  "restaurant_pizzas": [
    {
      "id": 1,
      "pizza": {
        "id": 1,
        "name": "Margherita",
        "ingredients": "Dough, Tomato Sauce, Cheese"
      },
      "price": 10,
      "pizza_id": 1,
      "restaurant_id": 1
    },
    ...
  ]
}
```
* 404 Not Found if the restaurant does not exist.

### 3. GET /pizzas
Fetches a list of all pizzas available in the database.

#### Response
* 200 OK

```
[
  {
    "id": 1,
    "name": "Margherita",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  },
  ...
]
```

### 4. DELETE /restaurants/{id}
Deletes a specific restaurant by its ID and removes all associated restaurant-pizza associations.

#### Response
* **204 No Content** if the operation is successful.
* **404 Not Found** if the restaurant does not exist.

### 5. POST /restaurant_pizzas
Creates a new restaurant-pizza association by linking a pizza and a restaurant with a specified price.

* Request Body

```
{
  "price": 5,
  "pizza_id": 1,
  "restaurant_id": 3
}
```

#### Response
* **201 Created** if successful:

```
{
  "id": 4,
  "pizza_id": 1,
  "price": 5,
  "restaurant_id": 3,
  "pizza": {
    "id": 1,
    "name": "Margherita",
    "ingredients": "Dough, Tomato Sauce, Cheese"
  },
  "restaurant": {
    "id": 3,
    "name": "Pizza Hut",
    "address": "123 Main St"
  }
}
```

* **400 Bad Request** if validation fails (e.g., invalid price or pizza/restaurant not found):

```
{
  "errors": ["validation errors"]
}
```

## Setup
To run this project locally:

1. Clone the repository:

```
git clone git@github.com:nikitaamani/python-phase-4-code-challenge-pizza.git
```
2. Install the required dependencies:

```
pip install -r requirements.txt
```

3. Set up the database:

```
flask db init
flask db migrate
flask db upgrade
```
4. Run the application:

```
flask run
```

The application will be available at http://localhost:5000.

## Technologies Used
* Flask - Python web framework used to create the API.
* SQLAlchemy - ORM for managing the SQLite database.
* Flask-Migrate - Database migration tool to handle schema changes.
* Flask-RESTful - A simple library to build RESTful APIs in Flask.

## Contributing

Contributions are welcome! Feel free to fork the repository and submit a pull request. To contribute:

1. Fork the repository.
2. Create a new branch for your changes.
3. Make the necessary changes and commit them.
4. Push the changes to your fork.
5. Create a pull request with a detailed description of your changes.

## License
The content of this project is licensed under the MIT license Copyright (c) 2025.

