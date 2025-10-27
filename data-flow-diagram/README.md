# 🗺️ DFD: Booking Process Analysis

This document provides context for the **Data Flow Diagram (DFD)** which models the critical data movements within the **Airbnb Clone Backend**.

The DFD specifically illustrates the **Level 0 (Context)** and **Level 1 (Booking Detail)** flow for the core business transaction: **Processing a New Booking**.

---

## 🎯 DFD Focus: Booking Process

The diagram visually maps how **data** (not control/timing) transforms as it moves from external **Entities** through system **Processes** and into **Data Stores**.

| Component | Description | Example |
| :--- | :--- | :--- |
| **Entities** | External sources or sinks of data. | Guest, Payment Gateway |
| **Processes** | Transformations of data within the system. | P1.0 Process Booking, P2.0 Handle Payment |
| **Data Stores** | Repositories where data is stored between processes. | D1: Properties, D2: Bookings |

---

## 🔗 Technical Implementation

The DFD is implemented using the **Mermaid.js** JavaScript library, allowing for a lightweight, text-based definition that renders into a clear and readable visual diagram.
