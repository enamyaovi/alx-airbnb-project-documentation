
# Backend Feature Requirements – Airbnb Clone

## Technology Stack

| Technology             | Purpose                                                  |
|------------------------|----------------------------------------------------------|
| Django                 | High-level Python framework for backend logic            |
| Django REST Framework  | Tools for building RESTful APIs                          |
| PostgreSQL             | Relational database                                      |
| GraphQL                | Flexible and efficient querying                          |
| Celery                 | Background tasks (e.g. email, notifications)             |
| Redis                  | Caching and task queue backend for Celery                |
| Docker                 | Containerization for development and deployment          |
| CI/CD Pipelines        | Automated testing and deployment                         |

---

## Feature 1: User Authentication

### Functionalities
- User registration via email/password or OAuth
- Login with token generation (JWT or session-based)
- Token refresh and logout
- Profile update
- Secure password storage and reset

### API Endpoints

| Method | Endpoint              | Description                      |
|--------|-----------------------|----------------------------------|
| POST   | `/api/auth/register/` | Register a new user              |
| POST   | `/api/auth/login/`    | Authenticate and issue token     |
| POST   | `/api/auth/logout/`   | Invalidate user session/token    |
| POST   | `/api/auth/password-reset/` | Request password reset    |
| PUT    | `/api/auth/profile/`  | Update user profile              |

### Input/Output Specifications

- **Input (Registration)**: `email`, `password`, `first_name`, `last_name`. `POST api/register/`

    ```
    {
        "email": "user@example.com",
        "password": "Password123!",
        "first_name": "John",
        "last_name": "Doe",
        "role": "guest"
  }

    ```
- **Output**: JSON response with user ID, name, and access token
    ```
    {
        "user": {
            "id": "uuid",
            "email": "user@example.com",
            "token": "jwt_or_session_token"
            }
        }
    ```

### Validation Rules
- Email must be valid and unique
- Password must meet complexity requirements
- Names cannot be blank

### Performance Criteria
- Secure handling of passwords

---

## Feature 2: Property Management

### Functionalities
- Hosts can list, update, or delete properties
- Guests can view property listings
- Admin can moderate property content

### API Endpoints

| Method | Endpoint                     | Description                          |
|--------|------------------------------|--------------------------------------|
| GET    | `/api/properties/`           | List all properties                  |
| POST   | `/api/properties/`           | Host adds new property               |
| GET    | `/api/properties/<id>/`      | View specific property               |
| PUT    | `/api/properties/<id>/`      | Host updates their property          |
| DELETE | `/api/properties/<id>/`      | Host removes a property              |

### Input/Output Specifications

- **Input**: `name`, `description`, `location_id`, `price_per_night`. `POST api/properties/`
    ```
        {
            "host_id": "a1b2c3d4-e5f6-7g8h-9i0j-k1l2m3n4o5p6",
            "name": "Cozy Apartment in Accra",
            "description": "A well-furnished 2-bedroom apartment with AC and WiFi.",
            "location_id": "loc-001",
            "price_per_night": 200.00
        }


    ```

- **Output**: Property JSON object with timestamps
    ```
        {
            "property_id": "prop-xyz-123",
            "host_id": "a1b2c3d4-e5f6-7g8h-9i0j-k1l2m3n4o5p6",
            "name": "Cozy Apartment in Accra",
            "description": "A well-furnished 2-bedroom apartment with AC and WiFi.",
            "location_id": "loc-001",
            "price_per_night": 200.00,
            "created_at": "2025-06-29T18:30:00Z"
        }
    ```

### Validation Rules
- Price must be a positive decimal
- Location ID must reference an existing location
- Only the host who created the property can update or delete it

### Performance Criteria
- Supports filtering and pagination for listings

---

## Feature 3: Booking System

### Functionalities
- Guests can book available properties
- Hosts and guests are notified of bookings
- Admin can cancel bookings if necessary

### API Endpoints

| Method | Endpoint                      | Description                           |
|--------|-------------------------------|---------------------------------------|
| POST   | `/api/bookings/`              | Create a new booking                  |
| GET    | `/api/bookings/`              | List bookings (guest or host view)    |
| GET    | `/api/bookings/<id>/`         | View booking details                  |
| PUT    | `/api/bookings/<id>/cancel/`  | Cancel a booking                      |

### Input/Output Specifications

- **Input**: `property_id`, `start_date`, `end_date`.  ` POST/api/bookings`
     ```
        {
            "property_id": "prop-xyz-123",
            "user_id": "guest-789",
            "start_date": "2025-07-10",
            "end_date": "2025-07-15",
            "total_price": 1000.00,
            "status": "pending"
        }

- **Output**: Booking confirmation and reference ID 
    ```
    
    {
        "booking_id": "book-456",
        "property_id": "prop-xyz-123",
        "user_id": "guest-789",
        "start_date": "2025-07-10",
        "end_date": "2025-07-15",
        "total_price": 1000.00,
        "status": "pending",
        "created_at": "2025-06-29T18:35:20Z"
    }
    ```

### Validation Rules
- No overlapping bookings on same property
- Booking dates must be in the future
- Only guests can make bookings; only the booking owner or admin can cancel

### Performance Criteria
- Atomic transaction with payment trigger

---

> _This document defines the expected behavior, inputs, and performance of core backend systems and should serve as a development and QA reference._
