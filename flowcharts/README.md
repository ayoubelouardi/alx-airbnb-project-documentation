# 🌊 Flowchart: New Property Booking Process

This directory contains the visual documentation for the crucial backend process of managing a property reservation on the Airbnb Clone platform.

---

## 🎯 Objective

The flowchart (typically found in `flowcharts/new_booking_flow.png`) visually maps the sequential steps, decision points, and system actions required to successfully process a new property booking request, from user input to final confirmation.

---

## ⚙️ Key Logic and Decisions

The diagram focuses on the backend's core responsibilities for Feature ID **BR-01** (Create New Booking) and **PR-01** (Initiate Payment), including:

1.  **Authentication and Validation:** Ensuring the user is logged in and the request data is valid.
2.  **Availability Check:** Checking the database (`D1: Property`) to prevent double-booking.
3.  **Payment Handling:** Routing the transaction to the **Payment Gateway** and handling both **Success** and **Failure** responses.
4.  **Status Updates:** Correctly updating the booking record (`D2: Bookings`) to `Pending`, `Confirmed`, or `Failed`.
