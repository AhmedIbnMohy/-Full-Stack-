# Restaurant Management System

A complete Laravel-based restaurant management system with user authentication, menu management, table booking, and admin panel functionality.

## Features

### 🔐 Authentication & User Management
- **User Registration & Login**: Secure authentication with Laravel Sanctum
- **Role-based Access**: Two user types - Normal users and Admins
- **Profile Management**: Users can view and update their profile information
- **Password Management**: Secure password change functionality

### 🍽️ Menu Management
- **Menu Items**: Admins can add, edit, and delete menu items
- **Categories**: Organized menu with categories (Appetizers, Main Courses, Pasta, Desserts, Beverages)
- **Image Support**: Menu items can include images
- **Availability Control**: Toggle menu item availability

### 📅 Table Booking System
- **Book Tables**: Logged-in users can book tables for specific dates and times
- **Conflict Prevention**: System automatically checks for booking conflicts
- **Status Management**: Admins can confirm or reject bookings
- **User Notifications**: Automatic notifications when booking status changes
- **Booking History**: Users can view their booking history

### 🔔 Notification System
- **Real-time Updates**: Users receive notifications for booking status changes
- **Read/Unread Status**: Track notification status
- **Admin Notes**: Admins can add notes when updating booking status

### 👨‍💼 Admin Panel
- **Dashboard**: Overview of system statistics
- **User Management**: View, edit, and delete user accounts
- **Booking Management**: Manage all table bookings
- **Menu Management**: Full CRUD operations for menu items
- **Admin Creation**: Create additional admin users

## System Requirements

- PHP 8.2 or higher
- Laravel 12
- SQLite/MySQL/PostgreSQL
- Composer

## Installation

1. **Clone the repository and navigate to the project directory:**
   ```bash
   cd fullstack
   ```

2. **Install dependencies:**
   ```bash
   composer install
   ```

3. **Copy environment file:**
   ```bash
   cp .env.example .env
   ```

4. **Generate application key:**
   ```bash
   php artisan key:generate
   ```

5. **Configure database in `.env` file:**
   ```env
   DB_CONNECTION=sqlite
   DB_DATABASE=/absolute/path/to/database.sqlite
   ```

6. **Run database migrations:**
   ```bash
   php artisan migrate
   ```

7. **Seed the database with sample data:**
   ```bash
   php artisan db:seed
   ```

8. **Create storage link for file uploads:**
   ```bash
   php artisan storage:link
   ```

9. **Start the development server:**
   ```bash
   php artisan serve
   ```

## Default Users

After running the seeder, you'll have these default users:

### Admin User
- **Email:** `admin@restaurant.com`
- **Password:** `password`
- **Role:** Admin

### Regular Users
- **Email:** `john@example.com`
- **Password:** `password`
- **Role:** User

- **Email:** `jane@example.com`
- **Password:** `password`
- **Role:** User

## API Endpoints

The system provides a comprehensive REST API. See `API_DOCUMENTATION.md` for complete endpoint documentation.

### Key Endpoints:
- **Authentication:** `/api/register`, `/api/login`, `/api/logout`
- **Profile:** `/api/profile`, `/api/profile/change-password`
- **Menu:** `/api/menu`, `/api/menu/categories`
- **Bookings:** `/api/bookings`, `/api/bookings/my`
- **Admin:** `/api/admin/dashboard`, `/api/admin/users`, `/api/admin/bookings`

## Usage Examples

### 1. User Registration
```bash
curl -X POST http://localhost:8000/api/register \
  -H "Content-Type: application/json" \
  -d '{
    "name": "New User",
    "email": "user@example.com",
    "password": "password123",
    "password_confirmation": "password123",
    "phone": "+1234567890",
    "address": "123 Main St, City, Country"
  }'
```

### 2. User Login
```bash
curl -X POST http://localhost:8000/api/login \
  -H "Content-Type: application/json" \
  -d '{
    "email": "john@example.com",
    "password": "password"
  }'
```

### 3. Book a Table
```bash
curl -X POST http://localhost:8000/api/bookings \
  -H "Authorization: Bearer {your_token}" \
  -H "Content-Type: application/json" \
  -d '{
    "guest_name": "John Doe",
    "number_of_guests": 4,
    "booking_date": "2024-01-15",
    "booking_time": "19:00",
    "special_requests": "Window seat preferred",
    "phone": "+1234567890"
  }'
```

### 4. Admin Dashboard
```bash
curl -X GET http://localhost:8000/api/admin/dashboard \
  -H "Authorization: Bearer {admin_token}"
```

## Database Structure

### Tables:
- **users**: User accounts with roles and profile information
- **menu_items**: Restaurant menu items with categories and pricing
- **table_bookings**: Table reservation records
- **notifications**: User notification system
- **personal_access_tokens**: API authentication tokens

### Key Relationships:
- Users have many table bookings
- Users have many notifications
- Table bookings belong to users
- Notifications belong to users

## Security Features

- **Role-based Access Control**: Admin middleware protects admin routes
- **Policy-based Authorization**: Laravel policies control model access
- **Input Validation**: Comprehensive validation for all inputs
- **SQL Injection Protection**: Laravel's Eloquent ORM provides protection
- **CSRF Protection**: Built-in CSRF protection for web routes
- **API Authentication**: Sanctum tokens for API access

## File Structure

```
app/
├── Http/Controllers/Api/
│   ├── AuthController.php          # Authentication
│   ├── ProfileController.php       # User profile management
│   ├── MenuController.php          # Menu item management
│   ├── TableBookingController.php  # Table booking operations
│   ├── AdminController.php         # Admin panel functionality
│   └── NotificationController.php  # Notification system
├── Models/
│   ├── User.php                    # User model with relationships
│   ├── MenuItem.php                # Menu item model
│   ├── TableBooking.php            # Table booking model
│   └── Notification.php            # Notification model
├── Policies/
│   ├── MenuItemPolicy.php          # Menu item authorization
│   └── TableBookingPolicy.php      # Booking authorization
└── Http/Middleware/
    └── AdminMiddleware.php         # Admin access control
```

## Testing

1. **Run the test suite:**
   ```bash
   php artisan test
   ```

2. **Test API endpoints** using Postman, Insomnia, or curl

3. **Verify database seeding:**
   ```bash
   php artisan tinker
   >>> App\Models\User::count(); // Should return 3
   >>> App\Models\MenuItem::count(); // Should return 12
   ```

## Deployment

1. **Set production environment:**
   ```bash
   APP_ENV=production
   APP_DEBUG=false
   ```

2. **Optimize for production:**
   ```bash
   php artisan config:cache
   php artisan route:cache
   php artisan view:cache
   ```

3. **Set up proper database credentials**

4. **Configure web server (Apache/Nginx)**

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## License

This project is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).

## Support

For support and questions:
- Check the API documentation
- Review the Laravel documentation
- Open an issue in the repository

## Changelog

### Version 1.0.0
- Initial release
- Complete restaurant management system
- User authentication and authorization
- Menu management
- Table booking system
- Admin panel
- Notification system
- Comprehensive API
