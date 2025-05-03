# 🏡 Airbnb Clone – Backend API

Welcome to the backend repository of the **Airbnb Clone** project — a robust and scalable platform built to replicate the core functionalities of Airbnb. This backend system handles everything from user management and property listings to bookings, payments, and reviews.

---

## 🚀 Objective

This project aims to build a powerful backend system that supports a smooth and seamless experience for both users and hosts. The backend will manage:
- User interactions and authentication
- Property creation and management
- Booking and availability tracking
- Payment processing
- User reviews and ratings

---

## 🏆 Project Goals

- **User Management** – Register, authenticate, and manage user profiles securely.
- **Property Listings** – Allow hosts to create, update, and manage property data.
- **Booking System** – Users can book properties and manage check-in/check-out.
- **Payment Integration** – Secure and track payment transactions.
- **Review System** – Collect user feedback and ratings for listed properties.
- **Performance Optimization** – Implement caching and indexing for better scalability.

---
## 🌟 Feature Breakdown

### 🔐 User Management
Allows users to register, log in, and manage their profiles securely. This feature ensures only authorized users can access and interact with the platform.

### 🏠 Property Management
Hosts can list new properties, update existing ones, and manage availability and pricing. This feature is essential for populating the platform with bookable spaces.

### 📅 Booking System
Users can browse properties, select dates, and book stays. This feature handles availability checks, booking creation, and reservation history.

### 💳 Payment Processing
Securely processes guest payments and manages host payouts. It integrates with payment gateways to ensure safe transactions.

### ⭐ Review System
Guests can leave reviews for properties after their stay, and hosts can respond. This feature helps maintain trust and transparency in the community.

### 🧩 API Standards
Supports RESTful APIs using Django REST Framework, and offers optional GraphQL support for flexible client queries. OpenAPI documentation is included for easy testing and developer onboarding.

---

## 📡 API Reference

### User Authentication
- `GET /users/` – List all users  
- `POST /users/` – Register a new user  
- `GET /users/{user_id}/` – Retrieve a user  
- `PUT /users/{user_id}/` – Update user info  
- `DELETE /users/{user_id}/` – Delete a user  

### Property Management
- `GET /properties/` – List all properties  
- `POST /properties/` – Create a new property  
- `GET /properties/{property_id}/` – Retrieve a property  
- `PUT /properties/{property_id}/` – Update a property  
- `DELETE /properties/{property_id}/` – Delete a property  

### Booking System
- `GET /bookings/` – List all bookings  
- `POST /bookings/` – Create a new booking  
- `GET /bookings/{booking_id}/` – Retrieve a booking  
- `PUT /bookings/{booking_id}/` – Update a booking  
- `DELETE /bookings/{booking_id}/` – Delete a booking  

### Payment Processing
- `POST /payments/` – Process a payment  

### Review System
- `GET /reviews/` – List all reviews  
- `POST /reviews/` – Create a new review  
- `GET /reviews/{review_id}/` – Retrieve a review  
- `PUT /reviews/{review_id}/` – Update a review  
- `DELETE /reviews/{review_id}/` – Delete a review  

---

## ⚙️ Technology Stack

- **Python** & **Django** – Core backend framework
- **Django REST Framework** – API management
- **PostgreSQL** – Primary relational database
- **GraphQL** – Flexible query support
- **Celery** – Background tasks (e.g., notifications, payments)
- **Redis** – Caching and async task management
- **Docker** – Containerization for development and deployment
- **CI/CD Pipelines** – Automated testing and deployment workflows

---

## 👥 Team Roles

- **Product Owner (PO)**  
  Defines the product vision, prioritizes features, and ensures alignment with customer needs and business goals.

- **Project Manager (PM)**  
  Manages timelines, team coordination, and delivery processes to ensure the project stays on track and meets its goals.

- **Software Architect**  
  Designs the technical foundation, selects tools and frameworks, and ensures scalable and maintainable architecture.

- **Frontend Developer**  
  Implements the user interface, transforms UI/UX designs into responsive, interactive components, and ensures cross-platform usability.

- **Backend Developer**  
  Develops server-side logic, manages databases and APIs, and ensures data integrity, performance, and security.

- **UI/UX Designer**  
  Designs visually appealing, user-friendly interfaces and crafts seamless user journeys based on research, wireframing, and prototyping.

- **Quality Assurance (QA) Engineer**  
  Maintains product quality by designing test plans, executing test cases, and identifying and documenting bugs.

---
## 🗄️ Database Design

The database schema is designed to capture the core relationships and data flows in the Airbnb Clone system. Below are the key entities, their important fields, and how they relate to each other.

### 📌 Entities & Key Fields

#### 1. Users
- `id` (UUID): Unique identifier for each user
- `name` (String): Full name of the user
- `email` (String): User’s email address (must be unique)
- `password_hash` (String): Securely stored password
- `role` (Enum): Indicates whether the user is a host or a guest

#### 2. Properties
- `id` (UUID): Unique identifier for each property
- `user_id` (UUID): Reference to the host (User)
- `title` (String): Title of the property listing
- `location` (String): Address or general location
- `price_per_night` (Decimal): Cost of booking per night

#### 3. Bookings
- `id` (UUID): Unique identifier for each booking
- `user_id` (UUID): Reference to the guest (User)
- `property_id` (UUID): Reference to the booked property
- `start_date` (Date): Check-in date
- `end_date` (Date): Check-out date

#### 4. Reviews
- `id` (UUID): Unique identifier for each review
- `user_id` (UUID): Reference to the reviewer (User)
- `property_id` (UUID): Property being reviewed
- `rating` (Integer): Numeric rating (e.g., 1–5)
- `comment` (Text): Optional written feedback

#### 5. Payments
- `id` (UUID): Unique identifier for each payment
- `booking_id` (UUID): Reference to the associated booking
- `amount` (Decimal): Total payment amount
- `status` (Enum): e.g., pending, completed, failed
- `payment_method` (String): e.g., card, PayPal, etc.

### 🔗 Entity Relationships

- A **User** can list multiple **Properties** (one-to-many).
- A **Property** can receive multiple **Bookings** (one-to-many).
- A **Booking** belongs to one **User** (guest) and one **Property** (many-to-one).
- A **User** can leave multiple **Reviews** on **Properties** (one-to-many).
- A **Payment** is linked to a **Booking** (one-to-one).
---
## 🔐 API Security

Securing the backend APIs is critical to ensure data protection, prevent misuse, and maintain trust. This project incorporates several key security measures:

### 🔑 Authentication
All API endpoints are protected using token-based authentication (e.g., JWT). Only authenticated users can access protected resources. This prevents unauthorized access and ensures that user actions are traceable and secure.

### 🔒 Authorization
Role-based access control ensures that users can only access resources they are permitted to. For example, a guest cannot delete a property listing, and a host cannot access another host’s bookings.

### 🚫 Rate Limiting
To prevent abuse and denial-of-service (DoS) attacks, API endpoints are rate-limited. This helps maintain application stability by restricting the number of requests a client can make in a given period.

### 🔐 Secure Data Transmission
All communication with the API is encrypted using HTTPS. This protects sensitive data (e.g., login credentials, payment details) from being intercepted during transmission.

### 💳 Payment Protection
Endpoints handling payments are secured with additional validations, such as verifying transaction tokens and using secure payment gateways to prevent fraud and ensure transaction integrity.

### 🧍 User Data Protection
Personal user information (e.g., email, ID, contact data) is stored securely, and access is restricted to authorized users only. This complies with data protection regulations and enhances user trust.

### 🧪 Input Validation & Sanitization
All inputs from users are validated and sanitized to prevent injection attacks (e.g., SQL injection, XSS). This protects the backend from malicious data payloads.

---

Security is not an afterthought in this project—it is a foundational principle woven into every feature to protect users, data, and infrastructure.

---
## 🚀 CI/CD Pipeline

### What is CI/CD?

CI/CD stands for Continuous Integration and Continuous Deployment. It's a development practice where code changes are automatically tested and deployed, ensuring faster and more reliable delivery of features and fixes. 

### Why It's Important

Implementing a CI/CD pipeline allows the team to:
- Automatically run tests on new code to prevent bugs.
- Deploy updates quickly and safely without manual intervention.
- Maintain consistent environments across development, staging, and production.
- Enable frequent and reliable releases, boosting productivity and user satisfaction.

### Tools Used

To support CI/CD in this project, we utilize the following tools:
- **GitHub Actions**: For automating testing, linting, and deployment workflows directly within the GitHub ecosystem.
- **Docker**: To containerize the application, ensuring consistent environments across all stages of deployment.
- **Docker Compose**: For defining and running multi-container applications locally and in CI pipelines.
- **Heroku / AWS / Render (Optional)**: For deploying the application to a live production environment.

---
## 📈 API Documentation Overview

- **REST API** – Documented using OpenAPI (Swagger)
- **GraphQL API** – Enables fine-grained data querying

---

## 📌 Note

This project is under active development. Contributions, ideas, and feedback are welcome as we build toward a fully functional Airbnb-like experience.

---

## 📬 Contact

For any inquiries or collaboration:
**Noel Kiprono Langat**  
📧 noellangat28@gmail.com  
🔗 [LinkedIn](https://www.linkedin.com/in/noel-langat/)
