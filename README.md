# GutGrub Backend

## Overview

The GutGrub Backend is a Node.js application built with Express.js that provides authentication services for the GutGrub application. It handles user registration and login functionality, utilizing PostgreSQL for data storage, bcrypt for password hashing, and JSON Web Tokens (JWT) for session management.

## Project Structure

The workspace contains two identical sets of files:
- Root level: `package.json` and `server.js`

It provides a RESTful API for user authentication.

## Dependencies

The project relies on the following key dependencies:

- **express** (^5.1.0): Web framework for building the API
- **pg** (^8.16.3): PostgreSQL client for database operations
- **bcryptjs** (^3.0.2): Library for hashing passwords securely
- **jsonwebtoken** (^9.0.2): Implementation of JSON Web Tokens for authentication
- **cors** (^2.8.5): Middleware for enabling Cross-Origin Resource Sharing
- **dotenv** (^17.2.2): Module for loading environment variables from a `.env` file

## Features

### User Authentication
- **Registration**: Users can register with a username, email, and password
- **Login Options**: Support for login via username or email address
- **Security**: Passwords are hashed using bcrypt before storage
- **Token Generation**: Successful login returns a JWT token for session management

### Database Integration
- Connects to a PostgreSQL database using connection pooling
- Stores user information in a `users` table with fields: `id`, `username`, `email`, `password`

## API Endpoints

### POST /register
Registers a new user account.
- **Request Body**: `{ username, email, password }`
- **Response**: 201 (Created) on success, 400 (Bad Request) if user/email exists

### POST /login
Authenticates a user using their username.
- **Request Body**: `{ username, password }`
- **Response**: `{ token }` on success, 401 (Unauthorized) for invalid credentials

### POST /login-email
Authenticates a user using their email address.
- **Request Body**: `{ email, password }`
- **Response**: `{ token }` on success, 401 (Unauthorized) for invalid credentials

## Configuration

The application expects environment variables defined in a `.env` file:
- Database connection parameters (handled by `pg` library)
- `JWT_SECRET`: Secret key for signing JWT tokens

## Server Configuration

- **Port**: 4000
- **Middleware**: 
  - JSON body parsing
  - CORS enabled for cross-origin requests

## Setup and Running

1. Install dependencies: `npm install`
2. Create a `.env` file with required environment variables
3. Ensure PostgreSQL database is running and accessible
4. Start the server: `node server.js`

The server will start on port 4000 and log "Server running on port 4000" to the console.

## Security Considerations

- Passwords are hashed with bcrypt using a salt rounds of 10
- JWT tokens are used for stateless authentication
- Error handling prevents information leakage about user existence during login attempts
- CORS is enabled, suggesting potential for frontend integration

## Database Schema

The application assumes a `users` table with the following structure:
- `id`: Primary key (auto-incrementing)
- `username`: Unique username
- `email`: Unique email address
- `password`: Hashed password string

Note: The code does not include database schema creation or migration scripts.
