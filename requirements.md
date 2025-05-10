1. User Authentication
Overview:
Handles user registration, login, and role management (guest, host, admin).

API Endpoints:

POST /api/register: Register a new user

POST /api/login: Authenticate user and return token

GET /api/user: Get authenticated user profile

Input/Output Specs:

Register Input: { first_name, last_name, email, password, phone_number (optional), role }

Login Input: { email, password }

Output (on success): { token, user_id, role }

Validation:

Email must be unique and properly formatted.

Password must be at least 8 characters, contain a number and a capital letter.

Performance Criteria:

Token issued within 200ms.

Login rate limit: 5 attempts/minute.

2. Property Management
Overview:
Allows hosts to create, update, delete, and view their properties.

API Endpoints:

POST /api/properties: Create new property

GET /api/properties/:id: Get property by ID

PUT /api/properties/:id: Update property details

DELETE /api/properties/:id: Remove property

Input/Output Specs:

Create Input: { name, description, location, pricepernight }

Update Input: Partial or full same as above.

Output: Property object with timestamps.

Validation:

Price must be positive decimal.

Name and description required.

Performance Criteria:

Operations complete in under 300ms.

Indexes on location, pricepernight for fast search.

3. Booking System
Overview:
Manages property bookings by guests and enforces availability.

API Endpoints:

POST /api/bookings: Create a booking

GET /api/bookings/user/:id: List bookings for a user

PATCH /api/bookings/:id: Update booking status

Input/Output Specs:

Create Input: { property_id, user_id, start_date, end_date }

Output: { booking_id, total_price, status }

Validation:

Dates must be in the future and valid range.

No overlapping bookings for the same property.

Performance Criteria:

Booking creation within 500ms.

Prevents double-booking via transaction locks.
