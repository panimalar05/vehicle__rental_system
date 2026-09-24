API Endpoint List — Vehicle Rental & Fleet Management System

1. Authentication APIs
1.1 Register Customer

POST /api/auth/register

Input:

{
  "name": "Arun Kumar",
  "email": "arun@example.com",
  "password": "password123",
  "phone": "9876543210"
}

Output:

{
  "message": "Customer registered successfully",
  "userId": 101
}

1.2 Customer Login

POST /api/auth/login

Input:

{
  "email": "arun@example.com",
  "password": "password123"
}

Output:

{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "userId": 101,
  "name": "Arun Kumar",
  "role": "CUSTOMER"
}

1.3 View Profile

GET /api/auth/profile

Input:

Authorization: Bearer <JWT_TOKEN>

Output:

{
  "id": 101,
  "name": "Arun Kumar",
  "email": "arun@example.com",
  "phone": "9876543210",
  "role": "CUSTOMER"
}

1.4 Update Profile

PUT /api/auth/profile

Input:

{
  "name": "Arun Kumar M",
  "phone": "9876543211"
}

Output:

{
  "message": "Profile updated successfully"
}

2. Vehicle APIs
2.1 Get All Vehicles

GET /api/vehicles

Input: None

Output:

[
  {
    "id": 1,
    "vehicleNumber": "TN01AB1234",
    "model": "Honda City",
    "category": "CAR",
    "transmission": "AUTOMATIC",
    "fuelType": "PETROL",
    "baseRate": 2500,
    "status": "AVAILABLE",
    "imageUrl": "/images/honda-city.jpg",
    "depotName": "Chennai Central"
  },
  {
    "id": 2,
    "vehicleNumber": "TN02CD5678",
    "model": "Royal Enfield Hunter 350",
    "category": "BIKE",
    "transmission": "MANUAL",
    "fuelType": "PETROL",
    "baseRate": 1200,
    "status": "AVAILABLE",
    "imageUrl": "/images/hunter-350.jpg",
    "depotName": "Chennai Central"
  }
]

2.2 Get Vehicle Details

GET /api/vehicles/{id}

Example:

GET /api/vehicles/1

Input:

Path Parameter:
id = 1

Output:

{
  "id": 1,
  "vehicleNumber": "TN01AB1234",
  "model": "Honda City",
  "category": "CAR",
  "transmission": "AUTOMATIC",
  "fuelType": "PETROL",
  "baseRate": 2500,
  "status": "AVAILABLE",
  "imageUrl": "/images/honda-city.jpg",
  "depot": {
    "id": 1,
    "name": "Chennai Central",
    "location": "Chennai"
  }
}

3. Vehicle Search & Filter APIs
3.1 Search Vehicles

GET /api/vehicles/search?keyword=Honda

Input:

keyword = Honda

Output:

[
  {
    "id": 1,
    "model": "Honda City",
    "category": "CAR",
    "baseRate": 2500,
    "status": "AVAILABLE"
  }
]

3.2 Filter Vehicles

GET /api/vehicles/filter

Example:

GET /api/vehicles/filter?category=CAR&fuelType=PETROL&transmission=AUTOMATIC

Input:

category = CAR
fuelType = PETROL
transmission = AUTOMATIC

Output:

[
  {
    "id": 1,
    "model": "Honda City",
    "category": "CAR",
    "transmission": "AUTOMATIC",
    "fuelType": "PETROL",
    "baseRate": 2500,
    "imageUrl": "/images/honda-city.jpg"
  }
]

3.3 Filter by Price

GET /api/vehicles/filter?minPrice=500&maxPrice=3000

Input:

minPrice = 500
maxPrice = 3000

Output:

[
  {
    "id": 1,
    "model": "Honda City",
    "category": "CAR",
    "baseRate": 2500
  },
  {
    "id": 2,
    "model": "Royal Enfield Hunter 350",
    "category": "BIKE",
    "baseRate": 1200
  }
]

4. Vehicle Availability APIs
4.1 Check Vehicle Availability

GET /api/vehicles/{id}/availability

Example:

GET /api/vehicles/1/availability?pickupDate=2026-10-01&dropoffDate=2026-10-05

Input:

vehicleId = 1
pickupDate = 2026-10-01
dropoffDate = 2026-10-05

Output:

{
  "vehicleId": 1,
  "available": true,
  "pickupDate": "2026-10-01",
  "dropoffDate": "2026-10-05",
  "pricePerDay": 2500,
  "numberOfDays": 4,
  "totalPrice": 10000
}

If vehicle is unavailable
{
  "vehicleId": 1,
  "available": false,
  "message": "Vehicle is already reserved for the selected dates"
}

5. Reservation APIs
5.1 Create Reservation

POST /api/reservations

Input:

{
  "vehicleId": 1,
  "pickupDepotId": 1,
  "pickupDate": "2026-10-01",
  "dropoffDate": "2026-10-05"
}

Output:

{
  "message": "Reservation created successfully",
  "reservationId": 501,
  "bookingReference": "VR20261001001",
  "vehicleId": 1,
  "pickupDate": "2026-10-01",
  "dropoffDate": "2026-10-05",
  "totalAmount": 10000,
  "status": "CONFIRMED"
}

5.2 Get Customer Reservation History

GET /api/reservations

Input:

Authorization: Bearer <JWT_TOKEN>

Output:

[
  {
    "reservationId": 501,
    "bookingReference": "VR20261001001",
    "vehicleModel": "Honda City",
    "pickupDate": "2026-10-01",
    "dropoffDate": "2026-10-05",
    "totalAmount": 10000,
    "status": "CONFIRMED"
  }
]

5.3 Get Reservation Details

GET /api/reservations/{id}

Input:

id = 501

Output:

{
  "reservationId": 501,
  "bookingReference": "VR20261001001",
  "vehicle": {
    "id": 1,
    "model": "Honda City",
    "vehicleNumber": "TN01AB1234"
  },
  "pickupDepot": "Chennai Central",
  "pickupDate": "2026-10-01",
  "dropoffDate": "2026-10-05",
  "numberOfDays": 4,
  "totalAmount": 10000,
  "status": "CONFIRMED"
}

5.4 Cancel Reservation

PUT /api/reservations/{id}/cancel

Input:

id = 501

Output:

{
  "message": "Reservation cancelled successfully",
  "bookingReference": "VR20261001001",
  "status": "CANCELLED"
}

6. Rental Lifecycle APIs

6.1 Start Rental

PUT /api/reservations/{id}/start

Input:

id = 501

Output:

{
  "message": "Rental started successfully",
  "bookingReference": "VR20261001001",
  "status": "ACTIVE"
}

6.2 Complete Rental / Return Vehicle

PUT /api/reservations/{id}/complete

Input:

id = 501

Output:

{
  "message": "Vehicle returned successfully",
  "bookingReference": "VR20261001001",
  "status": "COMPLETED"
}

7. Depot APIs

7.1 Get All Depots

GET /api/depots

Input: None

Output:

[
  {
    "id": 1,
    "name": "Chennai Central",
    "location": "Chennai",
    "address": "Central Railway Station Road"
  },
  {
    "id": 2,
    "name": "Madurai Depot",
    "location": "Madurai",
    "address": "KK Nagar, Madurai"
  }
]

7.2 Get Depot Details

GET /api/depots/{id}

Input:

id = 1

Output:

{
  "id": 1,
  "name": "Chennai Central",
  "location": "Chennai",
  "address": "Central Railway Station Road"
}

8. Admin Authentication APIs

8.1 Admin Login

POST /api/admin/auth/login

Input:

{
  "email": "admin@rental.com",
  "password": "admin123"
}

Output:

{
  "token": "eyJhbGciOiJIUzI1NiJ9...",
  "userId": 1,
  "name": "Vehicle Rental Admin",
  "role": "ADMIN"
}

9. Admin Vehicle APIs
9.1 Add Vehicle

POST /api/admin/vehicles

Input:

{
  "vehicleNumber": "TN01AB1234",
  "model": "Honda City",
  "category": "CAR",
  "transmission": "AUTOMATIC",
  "fuelType": "PETROL",
  "baseRate": 2500,
  "imageUrl": "/images/honda-city.jpg",
  "depotId": 1
}

Output:

{
  "message": "Vehicle added successfully",
  "vehicleId": 1
}

9.2 Update Vehicle

PUT /api/admin/vehicles/{id}

Input:

{
  "model": "Honda City 2026",
  "category": "CAR",
  "transmission": "AUTOMATIC",
  "fuelType": "PETROL",
  "baseRate": 2700,
  "imageUrl": "/images/honda-city-2026.jpg",
  "depotId": 1
}

Output:

{
  "message": "Vehicle updated successfully"
}

9.3 Delete Vehicle

DELETE /api/admin/vehicles/{id}

Input:

id = 1

Output:

{
  "message": "Vehicle deleted successfully"
}

9.4 Update Vehicle Status

PUT /api/admin/vehicles/{id}/status

Input:

{
  "status": "MAINTENANCE"
}

Output:

{
  "message": "Vehicle status updated successfully",
  "vehicleId": 1,
  "status": "MAINTENANCE"
}

10. Admin Reservation APIs
10.1 View All Reservations

GET /api/admin/reservations

Input:

Authorization: Bearer <JWT_TOKEN>

Output:

[
  {
    "reservationId": 501,
    "bookingReference": "VR20261001001",
    "customerName": "Arun Kumar",
    "vehicleModel": "Honda City",
    "pickupDate": "2026-10-01",
    "dropoffDate": "2026-10-05",
    "totalAmount": 10000,
    "status": "CONFIRMED"
  }
]

10.2 View Reservation Details

GET /api/admin/reservations/{id}

Input:

id = 501

Output:

{
  "reservationId": 501,
  "bookingReference": "VR20261001001",
  "customerName": "Arun Kumar",
  "customerPhone": "9876543210",
  "vehicleModel": "Honda City",
  "vehicleNumber": "TN01AB1234",
  "pickupDepot": "Chennai Central",
  "pickupDate": "2026-10-01",
  "dropoffDate": "2026-10-05",
  "totalAmount": 10000,
  "status": "CONFIRMED"
}

10.3 Update Reservation Status

PUT /api/admin/reservations/{id}/status

Input:

{
  "status": "ACTIVE"
}

Output:

{
  "message": "Reservation status updated successfully",
  "bookingReference": "VR20261001001",
  "status": "ACTIVE"
}

11. Admin Depot APIs
11.1 Add Depot

POST /api/admin/depots

Input:

{
  "name": "Madurai Depot",
  "location": "Madurai",
  "address": "KK Nagar, Madurai"
}

Output:

{
  "message": "Depot added successfully",
  "depotId": 2
}

11.2 Update Depot

PUT /api/admin/depots/{id}

Input:

{
  "name": "Madurai Central Depot",
  "location": "Madurai",
  "address": "KK Nagar, Madurai"
}

Output:

{
  "message": "Depot updated successfully"
}

12. Admin User APIs
12.1 View All Customers

GET /api/admin/users

Output:

[
  {
    "id": 101,
    "name": "Arun Kumar",
    "email": "arun@example.com",
    "phone": "9876543210",
    "role": "CUSTOMER",
    "status": "ACTIVE"
  }
]

12.2 View Customer Details

GET /api/admin/users/{id}

Input:

id = 101

Output:

{
  "id": 101,
  "name": "Arun Kumar",
  "email": "arun@example.com",
  "phone": "9876543210",
  "role": "CUSTOMER",
  "status": "ACTIVE"
}
