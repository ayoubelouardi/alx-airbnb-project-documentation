#  REQUIREMENTS.md: Backend Technical Specifications

This document outlines the technical requirements, API specifications, validation rules, and performance criteria for the key backend features.

---

## 1. Feature: User Management & Authentication

Provides secure registration, login, and profile management for all users (Guests and Hosts).

### 1.1. Endpoint: `POST /api/v1/users/register` (User Registration)
* **Description:** Creates a new user account.
* **Request (Input):**
    ```json
    {
      "email": "user@example.com",
      "password": "StrongPassword123!",
      "username": "new_user",
      "is_host": false
    }
    ```
* **Response (Output 201 - Created):**
    ```json
    {
      "user_id": "uuid-12345-abcde",
      "username": "new_user",
      "email": "user@example.com",
      "is_host": false,
      "message": "User created successfully"
    }
    ```
* **Validation Rules:**
    * `email`: Must be a valid email format. Must be **unique** in the `Users` table.
    * `password`: Must be at least 8 characters, include one uppercase, one lowercase, one number, and one special character. Will be hashed (bcrypt) before storage.
    * `username`: Required.
* **Error Responses:**
    * `400 Bad Request`: If validation fails (e.g., "Invalid email format", "Password too weak").
    * `409 Conflict`: If `email` already exists.
* **Performance Criteria:**
    * Response time must be **< 500ms** (includes DB write and hashing).

### 1.2. Endpoint: `POST /api/v1/users/login` (User Login)
* **Description:** Authenticates a user and returns a JSON Web Token (JWT).
* **Request (Input):**
    ```json
    {
      "email": "user@example.com",
      "password": "StrongPassword123!"
    }
    ```
* **Response (Output 200 - OK):**
    ```json
    {
      "access_token": "jwt.access.token.string",
      "refresh_token": "jwt.refresh.token.string"
    }
    ```
* **Validation Rules:**
    * `email`: Must exist in the `Users` table.
    * `password`: Must match the stored hash for the given email.
* **Error Responses:**
    * `401 Unauthorized`: If email is not found or password does not match.
* **Performance Criteria:**
    * This is a critical path. Response time must be **< 300ms**.

---

## 2. Feature: Property Management

Allows users designated as Hosts to create, read, update, and delete property listings.

### 2.1. Endpoint: `POST /api/v1/properties` (Create Property)
* **Description:** Creates a new property listing.
* **Authentication:** **Required.** A valid JWT must be provided.
* **Authorization:** The authenticated user must have `is_host = true`.
* **Request (Input):**
    ```json
    {
      "title": "Cozy Beachfront Cabin",
      "description": "A beautiful cabin right on the beach.",
      "price_per_night": 150.00,
      "location": "Malibu, CA",
      "max_guests": 4
    }
    ```
* **Response (Output 201 - Created):**
    ```json
    {
      "property_id": "uuid-prop-67890",
      "host_id": "uuid-12345-abcde",
      "title": "Cozy Beachfront Cabin",
      "price_per_night": 150.00,
      "location": "Malibu, CA",
      "max_guests": 4,
      "created_at": "2025-10-27T10:00:00Z"
    }
    ```
* **Validation Rules:**
    * `title`: Required, string, max 255 characters.
    * `price_per_night`: Required, numeric, must be greater than 0.
    * `location`: Required, string.
    * `max_guests`: Required, integer, must be greater than 0.
* **Error Responses:**
    * `401 Unauthorized`: If no valid JWT is provided.
    * `403 Forbidden`: If the authenticated user has `is_host = false`.
    * `400 Bad Request`: If any validation rule fails.
* **Performance Criteria:**
    * Response time must be **< 600ms**.

### 2.2. Endpoint: `GET /api/v1/properties/{id}` (Get Property Details)
* **Description:** Retrieves all public details for a single property.
* **Authentication:** **Not Required.** This is a public endpoint.
* **Request (Input):**
    * Path Parameter: `id` (the `property_id`).
* **Response (Output 200 - OK):**
    ```json
    {
      "property_id": "uuid-prop-67890",
      "host": {
        "host_id": "uuid-12345-abcde",
        "username": "new_user"
      },
      "title": "Cozy Beachfront Cabin",
      "description": "A beautiful cabin right on the beach.",
      "price_per_night": 150.00,
      "location": "Malibu, CA",
      "max_guests": 4,
      "reviews": [
        { "rating": 5, "comment": "Amazing place!" }
      ]
    }
    ```
* **Validation Rules:**
    * `id`: Must be a valid UUID format.
* **Error Responses:**
    * `404 Not Found`: If no property with the given `id` exists.
* **Performance Criteria:**
    * Response time must be **< 400ms**.
    * **Recommendation:** Implement caching (e.g., Redis) for this endpoint as it will be high-traffic.

---

## 3. Feature: Booking System

Allows authenticated Guests to reserve properties and manages availability.

### 3.1. Endpoint: `POST /api/v1/bookings` (Create Booking)
* **Description:** Creates a new booking reservation.
* **Authentication:** **Required.** A valid JWT must be provided.
* **Request (Input):**
    ```json
    {
      "property_id": "uuid-prop-67890",
      "check_in_date": "2026-06-01",
      "check_out_date": "2026-06-05",
      "guest_count": 2
    }
    ```
* **Response (Output 201 - Created):**
    ```json
    {
      "booking_id": "uuid-book-xyz789",
      "guest_id": "uuid-guest-456",
      "property_id": "uuid-prop-67890",
      "check_in_date": "2026-06-01",
      "check_out_date": "2026-06-05",
      "total_price": 600.00,
      "status": "Pending" 
    }
    ```
* **Validation Rules:**
    * `property_id`: Must exist in the `Properties` table.
    * `check_in_date`: Must be a valid date and in the future.
    * `check_out_date`: Must be after `check_in_date`.
    * `guest_count`: Must be less than or equal to the `max_guests` for the specified `property_id`.
    * **Availability (Critical):** The date range (`check_in` to `check_out`) must **not** overlap with any existing `Confirmed` bookings for this `property_id`.
* **Error Responses:**
    * `401 Unauthorized`: If no valid JWT is provided.
    * `400 Bad Request`: For invalid dates or `guest_count` exceeded.
    * `404 Not Found`: If `property_id` does not exist.
    * `409 Conflict`: If the dates are not available.
* **Performance Criteria:**
    * Response time must be **< 800ms**, as this involves a complex database query to check for date overlaps (availability).
