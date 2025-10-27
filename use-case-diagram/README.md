## 📊 Use Case Diagram Analysis

This section provides the context and definitions for the **Use Case Diagram** (UML) modeling the primary interactions between external users (Actors) and the core functionalities (Use Cases) of the **Airbnb Clone Backend** system.

---

### 🎯 Purpose

The Use Case Diagram visualizes the **functional requirements** from the perspective of the user. Its primary goal is to:
1.  Define the clear **system boundary** (what the backend does).
2.  Identify all external **Actors** who interact with the system.
3.  Illustrate the key **Use Cases** (goals/features) that these actors can perform.

This artifact is critical for stakeholder communication and ensuring the development team builds the correct features that meet user goals.

---

### 👤 Key Actors

The system interacts with three main external entities, each with distinct permissions and goals:

| Actor | Description | Primary Goal |
| :--- | :--- | :--- |
| **Guest** | An unauthenticated or registered user looking to browse and book properties. | Search, register, view details, book, and review. |
| **Host** | A registered user who owns and manages property listings on the platform. | Login, create, update, and manage their property inventory. |
| **Payment Gateway** | An external system (e.g., Stripe) responsible for securely processing financial transactions. | Process payment requests and return a success/failure status to the system. |

---

### ⚙️ Core Use Cases

The diagram represents the primary functional requirements detailed in the **`FEATURES.md`**:

| Use Case | Corresponds to Feature IDs | Description |
| :--- | :--- | :--- |
| **Register Account** | UM-01 | Allows any individual to create a new user profile on the platform. |
| **Login** | UM-02 | Verifies user identity (Guest/Host) to grant access to protected features. |
| **Search Properties** | SL-01, SL-02 | Allows a user to find properties based on location, dates, price, etc. |
| **Book Property** | BR-01 | Initiates the reservation process for a selected property. |
| **Make Payment** | PR-01, PR-02 | Handles the secure financial transaction with the Payment Gateway. |
| **Submit Review** | PR-03 | Allows Guests to provide feedback and rating on a property after a stay. |
| **Create Listing** | PM-01 | Allows a Host to add a new property to the available inventory. |
| **Manage Bookings** | BR-03 | Allows a Host to view and manage reservations for their own properties. |
