# User Stories: Airbnb Clone Backend

This document contains a comprehensive list of user stories, covering all major functionalities for the Guests, Hosts, and the system, derived from the core feature breakdown.

## 1. User Management (Guests & Hosts) 🔑

| Feature ID | Use Case | User Story |
| :--- | :--- | :--- |
| **UM-01** | Registration | **As a Guest, I want to be able to register an account, so that I can save my preferences and make bookings.** |
| **UM-01** | Registration | **As a potential Host, I want to be able to sign up as a Host, so that I can list my properties.** |
| **UM-02** | Login | **As a User, I want to be able to securely log in, so that I can access my profile and protected features.** |
| **UM-03** | Logout | **As a User, I want to be able to log out, so that I can secure my account, especially on a shared device.** |
| **UM-04** | Profile View | **As a User, I want to be able to view my profile details, so that I can verify my information.** |
| **UM-05** | Profile Update | **As a User, I want to be able to update my profile information, so that I can keep my personal data current.** |
| **UM-06** | Password Reset | **As a User, I want to be able to reset my password via email, so that I can regain access if I forget it.** |

---

## 2. Search & Listing View (Guests) 🔍

| Feature ID | Use Case | User Story |
| :--- | :--- | :--- |
| **SL-01** | Search | **As a Guest, I want to search for properties by location, so that I can find accommodation in my desired city.** |
| **SL-02** | Filter | **As a Guest, I want to filter listings by price range, number of guests, and type, so that I can narrow down options that fit my budget and needs.** |
| **SL-03** | Filter by Dates | **As a Guest, I want to see only properties available for my specific check-in and check-out dates, so that I don't waste time on unavailable listings.** |
| **SL-04** | Sort | **As a Guest, I want to be able to sort search results by price, rating, or relevance, so that I can prioritize listings based on my criteria.** |
| **PM-02** | Retrieve Details | **As a Guest, I want to view a detailed page for a specific property, so that I can review images, amenities, and host information before booking.** |

---

## 3. Booking & Reservation System (Guests & Hosts) 🗓️

| Feature ID | Use Case | User Story |
| :--- | :--- | :--- |
| **BR-05** | Check Availability | **As a Guest, I want to check a property's calendar availability in real-time, so that I know immediately if a listing is reservable.** |
| **BR-01** | Create Booking | **As a Guest, I want to create a new reservation, so that I can secure the property for my trip.** |
| **BR-02** | View Guest Bookings | **As a Guest, I want to view a list of all my past, current, and upcoming bookings, so that I can manage my travel itinerary.** |
| **BR-03** | View Host Bookings | **As a Host, I want to view a list of all reservations made for my properties, so that I can manage my calendar and guest arrivals.** |
| **BR-04** | Cancel Booking | **As a User, I want to be able to cancel a pending booking (if within the cancellation policy), so that I can receive a refund or adjust my travel plans.** |

---

## 4. Property Management (Hosts) 🏡

| Feature ID | Use Case | User Story |
| :--- | :--- | :--- |
| **PM-01** | Create Listing | **As a Host, I want to create a new property listing, providing all necessary details like title, price, and location, so that I can make it available for booking.** |
| **PM-03** | Update Listing | **As a Host, I want to update the details of my existing property listing, so that the information remains accurate.** |
| **PM-04** | Delete Listing | **As a Host, I want to be able to remove or unlist my property, so that it is no longer available to guests.** |
| **PM-05** | Image Upload | **As a Host, I want to upload multiple high-resolution images to my listing, so that I can showcase the property attractively.** |

---

## 5. Payment Processing & Reviews 💳

| Feature ID | Use Case | User Story |
| :--- | :--- | :--- |
| **PR-01** | Initiate Payment | **As a Guest, I want to initiate the payment process for my booking, so that the reservation can move to a 'Confirmed' status.** |
| **PR-02** | Webhook | **As the System, I need to securely receive payment status updates from the Payment Gateway, so that I can automatically confirm or reject a booking.** |
| **PR-03** | Submit Review | **As a Guest, I want to submit a rating and comment for a property I have stayed at, so that I can contribute to the community and inform future guests.** |
| **PR-04** | View Reviews | **As a Guest, I want to view all reviews and the average rating for a property, so that I can evaluate its quality before booking.** |
| **PR-05** | View Own Reviews | **As a User, I want to view the reviews I have submitted, so that I can track my contributions.** |

---

## 6. System & Optimization (System Administration) ⚙️

| Feature | Use Case | User Story |
| :--- | :--- | :--- |
| **Data Optimization** | Caching | **As the System, I need to implement caching for property search results, so that the site remains fast and responsive even under high concurrent load.** |
| **API Security** | Rate Limiting | **As the System, I need to enforce API rate limiting on public endpoints, so that I can prevent brute-force attacks and abuse.** |
| **API Security** | AuthZ Check | **As the System, I need to check the ownership of a resource (e.g., property) before processing an update request, so that I can prevent unauthorized users (Guests) from modifying Host data.** |
