# FEATURES.md: Detailed Functionality & API Blueprint

This document translates the project requirements into a structured, prioritized list of features and functionalities, serving as a blueprint for the backend API development.

## 1. User Management (Authentication & Authorization) 🔑

This module is the foundation for all user interactions, distinguishing between Guests (Users) and Hosts.

| Feature ID | Description | Type | Key API Method/Endpoint | Security/AuthN |
| :--- | :--- | :--- | :--- | :--- |
| **UM-01** | User Registration (Guest/Host) | Core | `POST /api/v1/users/register` | Open |
| **UM-02** | User Login (JWT generation) | Core | `POST /api/v1/users/login` | Open |
| **UM-03** | User Logout (Token invalidation/removal) | Core | `POST /api/v1/users/logout` | Token Required |
| **UM-04** | Retrieve User Profile (Self) | Core | `GET /api/v1/users/profile` | Token Required |
| **UM-05** | Update User Profile (PII, Password) | Core | `PUT /api/v1/users/profile` | Token Required |
| **UM-06** | Password Reset (via Email) | Aux | `POST /api/v1/users/password/reset` | Open |

***

## 2. Property Management (Host Functionality) 🏡

This module handles the core content/inventory of the platform, managed primarily by **Hosts** (`is_host = True`).

| Feature ID | Description | Type | Key API Method/Endpoint | Security/AuthZ |
| :--- | :--- | :--- | :--- | :--- |
| **PM-01** | Create New Property Listing | Core | `POST /api/v1/properties` | Host Required |
| **PM-02** | Retrieve Single Property Details | Core | `GET /api/v1/properties/{id}` | Open |
| **PM-03** | Update Host's Own Property | Core | `PUT /api/v1/properties/{id}` | Host & Ownership Check |
| **PM-04** | Delete Host's Own Property | Core | `DELETE /api/v1/properties/{id}` | Host & Ownership Check |
| **PM-05** | Upload Multiple Property Images | Aux | `POST /api/v1/properties/{id}/images` | Host & Ownership Check |

***

## 3. Search & Listing View (Guest Functionality) 🔍

This module supports the frontend's main view, requiring high **Data Optimization** for performance.

| Feature ID | Description | Type | Key API Method/Endpoint | Security/AuthN |
| :--- | :--- | :--- | :--- | :--- |
| **SL-01** | **Search Properties (List View)** | Core | `GET /api/v1/properties?search=...` | Open |
| **SL-02** | Filter by Price Range, Location, Type | Core | `GET /api/v1/properties?filters=...` | Open |
| **SL-03** | Filter by Availability (Dates) | Core | `GET /api/v1/properties?check_in=...` | Open |
| **SL-04** | Sort Listings (Price, Rating, Date) | Core | `GET /api/v1/properties?sort=...` | Open |
| **SL-05** | Pagination for Listings | Core | `GET /api/v1/properties?page=...` | Open |

***

## 4. Booking & Reservation System 🗓️

This is the core business logic, linking Guests to Properties and facilitating the transaction.

| Feature ID | Description | Type | Key API Method/Endpoint | Security/AuthN |
| :--- | :--- | :--- | :--- | :--- |
| **BR-01** | **Create New Booking** (Guest) | Core | `POST /api/v1/bookings` | User Required |
| **BR-02** | Retrieve Guest's Bookings | Core | `GET /api/v1/bookings` | User & Ownership Check |
| **BR-03** | Retrieve Host's Bookings for their properties | Core | `GET /api/v1/host/bookings` | Host Required |
| **BR-04** | Cancel Existing Booking (within policy) | Core | `PUT /api/v1/bookings/{id}/cancel` | User & Ownership Check |
| **BR-05** | Check Property Availability (Pre-booking) | Aux | `GET /api/v1/properties/{id}/availability` | Open |

***

## 5. Payment Processing & Reviews 💳

These features secure the financial cycle and build community trust.

| Feature ID | Description | Type | Key API Method/Endpoint | Security/AuthN |
| :--- | :--- | :--- | :--- | :--- |
| **PR-01** | Initiate Payment for a Booking | Core | `POST /api/v1/payments` | User Required |
| **PR-02** | Webhook Endpoint for Payment Status Update | Core | `POST /api/v1/payments/webhook` | Gateway Auth (Internal) |
| **PR-03** | **Submit New Review** for a Stay | Core | `POST /api/v1/properties/{id}/reviews` | User & Past Stay Check |
| **PR-04** | Retrieve All Reviews for a Property | Core | `GET /api/v1/properties/{id}/reviews` | Open |
| **PR-05** | Retrieve User's Submitted Reviews | Aux | `GET /api/v1/users/reviews` | User Required |
