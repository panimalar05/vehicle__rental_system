# Vehicle Rental & Fleet Management System


The **Vehicle Rental & Fleet Management System** is a full-stack web application designed to simplify vehicle rental operations for customers and fleet administrators. The system allows customers to browse vehicles such as cars, bikes, and electric scooters, check availability based on rental dates, view pricing, and make reservations.

For administrators, the system provides centralized fleet management, vehicle status tracking, depot management, and reservation monitoring. The application follows a secure RESTful architecture with JWT-based authentication and role-based authorization.

---

## Project Overview

The system provides a centralized platform for managing the complete vehicle rental lifecycle.

### Customer Side

Customers can:

* Register and securely log in.
* Browse available cars, bikes, and electric scooters.
* Filter vehicles based on category, transmission, fuel type, and depot.
* View vehicle details, images, and rental rates.
* Select pickup and drop-off dates.
* Check vehicle availability.
* Calculate and view the total rental price.
* Create and manage reservations.
* View reservation status and rental details.
* Cancel eligible reservations.
* Track the rental lifecycle from confirmation to return.

### Admin Side

Administrators can:

* Manage the vehicle fleet.
* Add, update, and deactivate vehicles.
* Manage vehicle information, images, pricing, and status.
* Manage depot locations.
* View and monitor customer reservations.
* Update rental and vehicle statuses.
* Monitor vehicle availability across the fleet.

The application is designed using a layered backend architecture with **Controller, Service, and Repository** layers. REST APIs are used for communication between the React frontend and Spring Boot backend, while JWT authentication secures protected operations.

---

## Tech Stack

### Frontend

* **ReactJS**
* **JavaScript / JSX**
* **React Hooks**
* **Axios / Fetch API**
* **HTML5**
* **CSS3**

### Backend

* **Java**
* **Spring Boot**
* **Spring Web**
* **Spring Data JPA**
* **Spring Security**
* **JWT Authentication**
* **Maven**

### Database

* **MySQL**

### API & Testing

* **RESTful APIs**
* **JSON**
* **Swagger / OpenAPI**
* **Postman**

### Version Control & Deployment

* **Git**
* **GitHub**
* **Vercel** — Frontend deployment
* **Render / Railway / Docker** — Backend deployment
