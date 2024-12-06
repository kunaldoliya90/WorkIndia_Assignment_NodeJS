# Railway Management System

This project is a **Railway Management System** that simulates the core functionalities of the IRCTC system. The system enables users to:

- Book train tickets
- Check train availability
- Update train details
- Implement role-based access for both users and administrators

The backend is developed using **Node.js**, **Express.js**, and **MySQL** to ensure efficient and scalable performance.

---

## Project Setup

### Prerequisites

To run this project, ensure you have the following installed:

- [Node.js](https://nodejs.org/en/) (v14 or later)
- [MySQL](https://www.mysql.com/) (Database setup)
- [Postman](https://www.postman.com/) (for API testing)

### Environment Variables

You need to create a `.env` file in the root of your project with the following environment variables:

```bash
PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=Kunal3110kk
DB_NAME=irctc_database
JWT_SECRET=Kunal_WorkIndia_Assignment
```

### Installation

1. Clone the repository to your local machine:
   ```bash

      git clone 
   ```
2. Install all necessary dependencies using npm:

   ```bash
    npm install
   ```

3. Set up your MySQL database:

- Create a MySQL database named irctc_database.
- Run the SQL scripts in database/schema.sql to create necessary tables (users, trains, bookings).

Example:

```bash

CREATE DATABASE irctc_database;
USE irctc_database;

CREATE TABLE users (
   id INT AUTO_INCREMENT PRIMARY KEY,
   name VARCHAR(255) NOT NULL,
   email VARCHAR(255) UNIQUE NOT NULL,
   password VARCHAR(255) NOT NULL,
   role ENUM('user', 'admin') DEFAULT 'user',
   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE trains (
   id INT AUTO_INCREMENT PRIMARY KEY,
   train_number VARCHAR(50) NOT NULL,
   source VARCHAR(255) NOT NULL,
   destination VARCHAR(255) NOT NULL,
   total_seats INT NOT NULL,
   available_seats INT NOT NULL,
   created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE bookings (
   id INT AUTO_INCREMENT PRIMARY KEY,
   user_id INT,
   train_id INT,
   seats INT NOT NULL,
   FOREIGN KEY (user_id) REFERENCES users(id),
   FOREIGN KEY (train_id) REFERENCES trains(id)
);

```

### Starting the Server

Once the setup is complete, start the server using npm:

```bash
npm start

```





#### Note :- By default, the server will run on port 3000. You can access the API at http://localhost:3000.

### API Endpoints

#### User Routes

    1. Register a new user
       * HTTP Method :- POST
       * Endpoint :- http://localhost:3000/user/register
       * Body:

```bash
{
  "name": "Kunal Doliya12",
  "email": "kunaldoliya.ofcj1@gmail.com1",
  "password": "Kunal123411"
}

```

2. Login
   - HTTP Method :- POST
   - Endpoint :- http://localhost:3000/user/login
   - Body:

```bash
    {
  "email": "kunaldoliya.ofcj1@gmail.com1",
  "password": "Kunal123411"
    }
```

3. Check train availability

   - HTTP Method :- GET
   - Endpoint :- http://localhost:3000/user/availability?source=Ranchi&destination=Delhi
   - Query Parameters
     - source: Source station (e.g., "Solapur")
     - destination: Destination station (e.g., "Mumbai")
   - Response:

```bash
{
  "available": true,
  "availableTrainCount": 1,
  "trains": [
    {
      "trainNumber": "123123",
      "availableSeats": 600
    }
  ]
}

```

4.  Book Seats
    - HTTP Method :- POST
    - Endpoint :- http://localhost:3000/user/book
    - Request Body:

```bash
  {
  "trainId": 1,
  "seatsToBook": 2
}

```

- Response:

```bash
{
  "message": "Seats booked successfully"
}
```

Note :- Requires JWT authentication.

5.  Booking Details

    - HTTP Method :- GET
    - Endpoint :- http://localhost:3000/user/getAllbookings

    - Response:

```bash
[
    {
        "booking_id": 17,
        "number_of_seats": 50,
        "train_number": "123123",
        "source": "Ranchi",
        "destination": "Delhi"
    }
]


```

#### Admin Routes

1.  Add a new train

    - HTTP Method :- POST
    - Endpoint :- http://localhost:3000/admin/addTrain

    - Request Body:

```bash
{
    "message": "Trains added successfully",
    "trainIds": [
        {
            "trainNumber": "172622",
            "trainId": 21
        }
    ]
  }
```

         * Headers :
             * x-api-key: Your admin API key which is stored in .env

2. Update seat availability

   - HTTP Method :- PUT
   - Endpoint :- http://localhost:3000/admin/update-seats/10
   - Request Body:

```bash
 {
  "totalSeats": 200,
  "availableSeats": 150
 }
```

       * Response:

```bash
{
  "message": "Seats updated successfully"
}
```

        * Headers:
            * x-api-key:  Your admin API key which is stored in .env

### Running Tests

You can test all the available APIs using Postman. The endpoints are well-structured and follow RESTful conventions.

```bash
[
  {
    "trainNumber": "101010",
    "source": "Mumbai",
    "destination": "Pune",
    "totalSeats": 200
  },
  {
    "trainNumber": "102020",
    "source": "Chennai",
    "destination": "Bangalore",
    "totalSeats": 250
  },
  {
    "trainNumber": "103030",
    "source": "Kolkata",
    "destination": "Patna",
    "totalSeats": 300
  },
  {
    "trainNumber": "104040",
    "source": "Jaipur",
    "destination": "Agra",
    "totalSeats": 150
  },
  {
    "trainNumber": "105050",
    "source": "Hyderabad",
    "destination": "Visakhapatnam",
    "totalSeats": 350
  }
]

```

### Technologies Used

- Node.js: For backend logic
- Express.js: Web framework for building the RESTful API
- MySQL: Database for storing train, user, and booking data
- JWT: For authentication and authorization
- bcrypt: For hashing the passwords
- dotenv: For managing environment variables

### Future Enhancements

- Add frontend interface using React or Angular
- Implement seat selection
- Add email notifications for booking confirmations
- Integrate payment gateway

### Contributing

Feel free to fork the repository and make your contributions via pull requests. Any enhancements, bug fixes, or suggestions are welcome!

# photos of the project

### Screenshots of the Project

#### 1. Database Creation

![Database Creation Screenshot](./WorkIndia_Task_IRCTC/Photo/user_table.png)

Description: This screenshot showcases the creation of the database schema for the IRCTC system.

---

#### 2. Checking Train Availability

![Train Availability Screenshot](./WorkIndia_Task_IRCTC/Photo/Get_Availibility.png)

Description: This screenshot demonstrates how the `GET /user/availability` API is used to check train availability.

---

#### 3. Server Running Locally

![Localhost Running Screenshot](./WorkIndia_Task_IRCTC/Photo/localhost_running.png)

Description: The server running locally on `http://localhost:3000` as part of the project setup.

---

#### 4. User Login via Postman

![Postman Login Screenshot](./WorkIndia_Task_IRCTC/Photo/Postman_login.png)

Description: A Postman request to log in a user, showcasing how the login API works.

---

#### 5. User Registration via Postman

![Postman Registration Screenshot](./WorkIndia_Task_IRCTC/Photo/Postman_register.png)

Description: A Postman request to register a new user, demonstrating the registration functionality.

---

#### 6. User Database

![User Database Screenshot](./WorkIndia_Task_IRCTC/Photo/User_database.png)

Description: The structure and data stored in the `users` table of the `irctc_db` database.

---

#### 7. Workbench SQL View

![Workbench SQL Screenshot](./WorkIndia_Task_IRCTC/Photo/WorkBench_SQL.png)

Description: An overview of the SQL queries and table structures in MySQL Workbench.
