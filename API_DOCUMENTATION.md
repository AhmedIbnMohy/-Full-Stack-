# Restaurant Management System API Documentation

## Base URL
```
http://localhost:8000/api
```

## Authentication
All protected endpoints require a Bearer token in the Authorization header:
```
Authorization: Bearer {token}
```

## Endpoints

### 1. Authentication

#### Register User
```
POST /register
```
**Body:**
```json
{
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123",
    "password_confirmation": "password123",
    "phone": "+1234567890",
    "address": "123 Main St, City, Country"
}
```

#### Login
```
POST /login
```
**Body:**
```json
{
    "email": "john@example.com",
    "password": "password123"
}
```

#### Logout
```
POST /logout
```
**Headers:** Authorization: Bearer {token}

#### Get Current User
```
GET /me
```
**Headers:** Authorization: Bearer {token}

### 2. Profile Management

#### Get Profile
```
GET /profile
```
**Headers:** Authorization: Bearer {token}

#### Update Profile
```
PUT /profile
```
**Headers:** Authorization: Bearer {token}
**Body:**
```json
{
    "name": "John Doe Updated",
    "phone": "+1234567891",
    "address": "456 New St, City, Country"
}
```

#### Change Password
```
POST /profile/change-password
```
**Headers:** Authorization: Bearer {token}
**Body:**
```json
{
    "current_password": "password123",
    "new_password": "newpassword123",
    "new_password_confirmation": "newpassword123"
}
```

### 3. Menu Management

#### Get All Menu Items
```
GET /menu
```
**Query Parameters:**
- `category` (optional): Filter by category
- `available_only` (optional): Show only available items (default: true)

#### Get Menu Categories
```
GET /menu/categories
```

#### Get Single Menu Item
```
GET /menu/{id}
```

#### Create Menu Item (Admin Only)
```
POST /admin/menu
```
**Headers:** Authorization: Bearer {admin_token}
**Body:**
```json
{
    "name": "New Dish",
    "description": "Delicious new dish",
    "price": 15.99,
    "category": "Main Courses",
    "is_available": true
}
```

#### Update Menu Item (Admin Only)
```
PUT /admin/menu/{id}
```
**Headers:** Authorization: Bearer {admin_token}

#### Delete Menu Item (Admin Only)
```
DELETE /admin/menu/{id}
```
**Headers:** Authorization: Bearer {admin_token}

### 4. Table Booking

#### Get All Bookings
```
GET /bookings
```
**Headers:** Authorization: Bearer {token}
**Note:** Admins see all bookings, users see only their own

#### Create Booking
```
POST /bookings
```
**Headers:** Authorization: Bearer {token}
**Body:**
```json
{
    "guest_name": "John Doe",
    "number_of_guests": 4,
    "booking_date": "2024-01-15",
    "booking_time": "19:00",
    "special_requests": "Window seat preferred",
    "phone": "+1234567890"
}
```

#### Get My Bookings
```
GET /bookings/my
```
**Headers:** Authorization: Bearer {token}

#### Get Single Booking
```
GET /bookings/{id}
```
**Headers:** Authorization: Bearer {token}

#### Cancel Booking
```
DELETE /bookings/{id}
```
**Headers:** Authorization: Bearer {token}

#### Update Booking Status (Admin Only)
```
PATCH /admin/bookings/{id}/status
```
**Headers:** Authorization: Bearer {admin_token}
**Body:**
```json
{
    "status": "confirmed",
    "admin_notes": "Table confirmed, window seat available"
}
```

### 5. Notifications

#### Get Notifications
```
GET /notifications
```
**Headers:** Authorization: Bearer {token}
**Query Parameters:**
- `unread_only` (optional): Show only unread notifications

#### Get Unread Count
```
GET /notifications/unread-count
```
**Headers:** Authorization: Bearer {token}

#### Get Single Notification
```
GET /notifications/{id}
```
**Headers:** Authorization: Bearer {token}

#### Mark as Read
```
PATCH /notifications/{id}/read
```
**Headers:** Authorization: Bearer {token}

#### Mark All as Read
```
POST /notifications/mark-all-read
```
**Headers:** Authorization: Bearer {token}

#### Delete Notification
```
DELETE /notifications/{id}
```
**Headers:** Authorization: Bearer {token}

### 6. Admin Panel

#### Dashboard
```
GET /admin/dashboard
```
**Headers:** Authorization: Bearer {admin_token}

#### Get All Users
```
GET /admin/users
```
**Headers:** Authorization: Bearer {admin_token}
**Query Parameters:**
- `search` (optional): Search by name or email

#### Get Single User
```
GET /admin/users/{id}
```
**Headers:** Authorization: Bearer {admin_token}

#### Update User
```
PUT /admin/users/{id}
```
**Headers:** Authorization: Bearer {admin_token}

#### Delete User
```
DELETE /admin/users/{id}
```
**Headers:** Authorization: Bearer {admin_token}

#### Create Admin
```
POST /admin/users
```
**Headers:** Authorization: Bearer {admin_token}
**Body:**
```json
{
    "name": "New Admin",
    "email": "admin2@restaurant.com",
    "password": "password123",
    "password_confirmation": "password123"
}
```

#### Get All Bookings (Admin)
```
GET /admin/bookings
```
**Headers:** Authorization: Bearer {admin_token}
**Query Parameters:**
- `status` (optional): Filter by status
- `date` (optional): Filter by date

## Response Format

All API responses follow this format:

### Success Response
```json
{
    "success": true,
    "message": "Operation successful",
    "data": {
        // Response data
    }
}
```

### Error Response
```json
{
    "success": false,
    "message": "Error message",
    "errors": {
        // Validation errors (if any)
    }
}
```

## Status Codes

- `200` - Success
- `201` - Created
- `400` - Bad Request
- `401` - Unauthorized
- `403` - Forbidden
- `404` - Not Found
- `422` - Validation Error
- `500` - Server Error

## Sample Users

### Admin User
- Email: `admin@restaurant.com`
- Password: `password`
- Role: `admin`

### Regular Users
- Email: `john@example.com`
- Password: `password`
- Role: `user`

- Email: `jane@example.com`
- Password: `password`
- Role: `user`

## Testing the API

1. **Start the server:**
   ```bash
   php artisan serve
   ```

2. **Run migrations:**
   ```bash
   php artisan migrate
   ```

3. **Seed the database:**
   ```bash
   php artisan db:seed
   ```

4. **Test endpoints using Postman or any API client**

## File Upload

For menu item images, use `multipart/form-data` with the `image` field.

## Notes

- All dates should be in `YYYY-MM-DD` format
- All times should be in `HH:MM` format (24-hour)
- Prices are decimal numbers with up to 2 decimal places
- The system automatically checks for booking conflicts
- Users receive notifications when their booking status changes
- Only admins can manage menu items and user accounts
- Regular users cannot book tables if they are admins
