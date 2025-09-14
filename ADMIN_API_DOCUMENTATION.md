# Admin API Documentation

This document describes the admin API endpoints for the restaurant management system. All admin endpoints require authentication and admin privileges.

## Authentication

All admin endpoints require:
1. Valid authentication token (Bearer token)
2. User with `admin` role

## Base URL
```
/api/admin
```

## Admin Dashboard

### Get Dashboard Statistics
```
GET /api/admin/dashboard
```

**Response:**
```json
{
    "success": true,
    "data": {
        "total_users": 10,
        "total_orders": 25,
        "pending_orders": 5,
        "total_bookings": 15,
        "pending_bookings": 3,
        "total_menu_items": 20,
        "total_categories": 5
    }
}
```

## User Management

### Get All Users
```
GET /api/admin/users
```

**Response:**
```json
{
    "success": true,
    "data": [
        {
            "id": 1,
            "name": "John Doe",
            "email": "john@example.com",
            "role": "user",
            "phone": "+1234567890",
            "address": "123 Main St",
            "first_name": "John",
            "last_name": "Doe",
            "country": "Egypt",
            "gender": "male",
            "created_at": "2025-01-01T00:00:00.000000Z",
            "updated_at": "2025-01-01T00:00:00.000000Z",
            "orders": [],
            "table_bookings": []
        }
    ]
}
```

### Get Single User
```
GET /api/admin/users/{id}
```

### Create New User
```
POST /api/admin/users
```

**Request Body:**
```json
{
    "name": "New User",
    "email": "newuser@example.com",
    "password": "password123",
    "role": "user",
    "phone": "+1234567890",
    "address": "456 Oak St",
    "first_name": "New",
    "last_name": "User",
    "country": "Egypt",
    "gender": "female"
}
```

### Update User
```
PUT /api/admin/users/{id}
```

**Request Body:**
```json
{
    "name": "Updated Name",
    "email": "updated@example.com",
    "role": "admin",
    "phone": "+0987654321"
}
```

### Delete User
```
DELETE /api/admin/users/{id}
```

**Note:** Admin cannot delete their own account.

## Order Management

### Get All Orders
```
GET /api/admin/orders
```

**Response:**
```json
{
    "success": true,
    "data": [
        {
            "id": 1,
            "user_id": 1,
            "name": "John Doe",
            "email": "john@example.com",
            "phone": "+1234567890",
            "address": "123 Main St",
            "total": "45.50",
            "status": "pending",
            "notes": "Extra spicy",
            "created_at": "2025-01-01T00:00:00.000000Z",
            "updated_at": "2025-01-01T00:00:00.000000Z",
            "order_items": [
                {
                    "id": 1,
                    "order_id": 1,
                    "menu_item_id": 1,
                    "quantity": 2,
                    "price": "22.75",
                    "menu_item": {
                        "id": 1,
                        "name": "Margherita Pizza",
                        "description": "Classic tomato and mozzarella",
                        "price": "22.75"
                    }
                }
            ]
        }
    ]
}
```

### Get Single Order
```
GET /api/admin/orders/{id}
```

### Update Order Status
```
PATCH /api/admin/orders/{id}/status
```

**Request Body:**
```json
{
    "status": "confirmed",
    "admin_notes": "Order confirmed and being prepared"
}
```

**Available Statuses:**
- `pending`
- `confirmed`
- `preparing`
- `ready`
- `delivered`
- `cancelled`

### Delete Order
```
DELETE /api/admin/orders/{id}
```

## Table Booking Management

### Get All Table Bookings
```
GET /api/admin/bookings
```

**Response:**
```json
{
    "success": true,
    "data": [
        {
            "id": 1,
            "user_id": 1,
            "guest_name": "John Doe",
            "number_of_guests": 4,
            "booking_date": "2025-01-15",
            "booking_time": "19:00:00",
            "status": "pending",
            "special_requests": "Window seat preferred",
            "phone": "+1234567890",
            "admin_notes": null,
            "created_at": "2025-01-01T00:00:00.000000Z",
            "updated_at": "2025-01-01T00:00:00.000000Z",
            "user": {
                "id": 1,
                "name": "John Doe",
                "email": "john@example.com"
            }
        }
    ]
}
```

### Get Single Table Booking
```
GET /api/admin/bookings/{id}
```

### Update Table Booking Status
```
PATCH /api/admin/bookings/{id}/status
```

**Request Body:**
```json
{
    "status": "confirmed",
    "admin_notes": "Table confirmed for 4 guests"
}
```

**Available Statuses:**
- `pending`
- `confirmed`
- `rejected`

### Delete Table Booking
```
DELETE /api/admin/bookings/{id}
```

## Menu Management

### Get All Menu Items
```
GET /api/admin/menu
```

**Response:**
```json
{
    "success": true,
    "data": [
        {
            "id": 1,
            "name": "Margherita Pizza",
            "description": "Classic tomato and mozzarella",
            "price": "22.75",
            "category_id": 1,
            "image": "pizza.jpg",
            "is_available": true,
            "created_at": "2025-01-01T00:00:00.000000Z",
            "updated_at": "2025-01-01T00:00:00.000000Z",
            "category": {
                "id": 1,
                "name": "Pizza",
                "description": "Italian pizzas"
            }
        }
    ]
}
```

### Get All Categories
```
GET /api/admin/categories
```

### Create Menu Item
```
POST /api/admin/menu
```

**Request Body:**
```json
{
    "name": "New Pizza",
    "description": "Delicious new pizza",
    "price": 25.00,
    "category_id": 1,
    "image": "new-pizza.jpg",
    "is_available": true
}
```

### Update Menu Item
```
PUT /api/admin/menu/{id}
```

**Request Body:**
```json
{
    "name": "Updated Pizza",
    "price": 28.00,
    "is_available": false
}
```

### Delete Menu Item
```
DELETE /api/admin/menu/{id}
```

## Error Responses

### Unauthorized (401)
```json
{
    "success": false,
    "message": "Unauthorized"
}
```

### Forbidden (403)
```json
{
    "success": false,
    "message": "Access denied. Admin privileges required."
}
```

### Not Found (404)
```json
{
    "success": false,
    "message": "User not found"
}
```

### Validation Error (422)
```json
{
    "success": false,
    "message": "Validation failed",
    "errors": {
        "email": ["The email field is required."],
        "role": ["The selected role is invalid."]
    }
}
```

## Testing Admin Access

To test the admin functionality, use the following credentials:

**Admin User:**
- Email: `admin@restaurant.com`
- Password: `admin123`

**Steps to test:**
1. Login with admin credentials: `POST /api/login`
2. Use the returned token in Authorization header: `Bearer {token}`
3. Access admin endpoints

## Security Notes

1. All admin endpoints are protected by authentication middleware
2. Admin middleware checks for `admin` role
3. Admin cannot delete their own account
4. All input is validated before processing
5. Proper error handling and status codes are returned
