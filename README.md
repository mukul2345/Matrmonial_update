
# Marriage Matchmaking App

## Overview
The Marriage Matchmaking App is a FastAPI-based backend application designed to manage user profiles and facilitate matchmaking based on user information. The application allows CRUD operations on user profiles and includes endpoints to find potential matches based on city, gender, and interests. Additionally, email validation is enforced for user profiles.

## Approach
The project was structured with the following modifications and enhancements to meet the specified requirements:

### User Update Endpoint
- Implemented a `PUT` endpoint to allow updating user details by ID.
- Utilized SQLAlchemy to query and update the user information in the SQLite database.
- Included validation to ensure the user exists before attempting an update.

### User Deletion Endpoint
- Implemented a `DELETE` endpoint to remove a user profile by ID.
- Utilized SQLAlchemy to query and delete the user information from the SQLite database.
- Included validation to ensure the user exists before attempting deletion.

### Find Matches for a User
- Implemented a `GET` endpoint to find potential matches for a user based on city, gender, and overlapping interests.
- Used SQLAlchemy to query the database for users matching the criteria.
- Ensured that the user making the request is validated before finding matches.

### Email Validation
- Added validation for the email field in user profiles using Pydantic’s `EmailStr` type.
- This ensures that only valid email addresses are accepted when creating or updating user profiles.

## Assumptions
- **Interest Matching:** It is assumed that users are matched based on having at least one overlapping interest, being in the same city, and of different genders.
- **Email Validation:** Pydantic’s `EmailStr` type is considered sufficient for email validation.
- **Database:** SQLite is used as the database, and it is assumed that it meets the needs of this application for simplicity and ease of setup.
- **Data Integrity:** Assumed that data integrity is maintained through SQLAlchemy ORM and Pydantic validation.

## Detailed Changes

### 1. `main.py`
- **Create User Endpoint:** Allows the creation of a new user profile.
- **Read Users Endpoint:** Retrieves a list of user profiles with optional pagination.
- **Read User by ID Endpoint:** Retrieves a user profile by its ID.
- **Update User Endpoint:** Updates user details by ID.
- **Delete User Endpoint:** Deletes a user profile by ID.
- **Find Matches Endpoint:** Finds potential matches for a user based on city, gender, and interests.

### 2. `models.py`
- **User Model:** No need to update as it defines the User schema using SQLAlchemy with fields for `id`, `name`, `age`, `gender`, `email`, `city`, and `interests`.

### 3. `schemas.py`
- **UserBase Schema:** Base schema for user details with email validation.
- **UserCreate Schema:** Inherits from UserBase for creating new users.
- **UserUpdate Schema:** Allows partial updates to user details.
- **User Schema:** Includes the user ID and inherits from UserBase.

### 4. `database.py`
- **Database Setup:** No need to update as it configures the SQLite database connection and session management.

## Setup and Installation
1. **Clone the repository:**
   ```sh
   git clone https://github.com/mukul2345/Matrmonial_update.git
   ```

2. **Create and activate a virtual environment:**
   ```sh
   python -m venv myenv
   myenv\Scripts\activate   # On Windows
   ```

3. **Install the required packages:**
   ```sh
   pip install fastapi sqlalchemy pydantic uvicorn
   ```

4. **Run the application:**
   ```sh
   uvicorn main:app --reload
   ```

## Running the Script
To run the FastAPI application, follow these steps:

1. **Activate the virtual environment:**
   ```sh
   myenv\Scripts\activate   # On Windows
   ```

2. **Start the FastAPI application:**
   ```sh
   uvicorn main:app --reload
   ```

3. **Open your browser or API testing tool and navigate to:**
   ```
   http://127.0.0.1:3000
   ```

## Testing the Endpoints
### Using Curl

#### Create a User:
```sh
curl -X POST "http://127.0.0.1:3000/users/" -H "Content-Type: application/json" -d '{"name": "Rohan", "age": 30, "gender": "male", "email": "Rohan@example.com", "city": "Noida", "interests": ["reading", "traveling"]}'
```

#### Read Users:
```sh
curl -X GET "http://127.0.0.1:3000/users/"
```

#### Read User by ID:
```sh
curl -X GET "http://127.0.0.1:3000/users/1"
```

#### Update User:
```sh
curl -X PUT "http://127.0.0.1:3000/users/1" -H "Content-Type: application/json" -d '{"name": "Rohan Sharma", "age": 31, "gender": "male", "email": "rohan.sharma@example.com", "city": "Noida", "interests": ["reading", "traveling"]}'
```

#### Delete User:
```sh
curl -X DELETE "http://127.0.0.1:3000/users/1"
```

#### Find Matches for a User:
```sh
curl -X GET "http://127.0.0.1:3000/users/1/matches"
```

### Using Postman
1. **Create a new request.**
2. **Set the request type (GET, POST, PUT, DELETE) based on the endpoint you are testing.**
3. **Enter the URL (e.g., `http://127.0.0.1:3000/users/`).**
4. **Set the headers and body as required.**
5. **Send the request and observe the response.**

