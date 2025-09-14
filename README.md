# 🍽️ Restaurant Management System

A comprehensive full-stack restaurant management system built with React.js frontend and Laravel backend, featuring order management, table reservations, user authentication, and admin panel.

## 📋 Table of Contents

- [Features](#-features)
- [Technology Stack](#-technology-stack)
- [Project Structure](#-project-structure)
- [Installation & Setup](#-installation--setup)
- [API Endpoints](#-api-endpoints)
- [Database Schema](#-database-schema)
- [User Roles & Permissions](#-user-roles--permissions)
- [Components Overview](#-components-overview)
- [Styling & UI](#-styling--ui)
- [Authentication Flow](#-authentication-flow)
- [Order Management](#-order-management)
- [Reservation System](#-reservation-system)
- [Admin Panel](#-admin-panel)
- [Deployment](#-deployment)
- [Contributing](#-contributing)

## ✨ Features

### 🎯 Core Features
- **User Authentication & Authorization** - Secure login/register with role-based access
- **Menu Management** - Dynamic menu with categories and items
- **Order System** - Complete food ordering with cart functionality
- **Table Reservations** - Book tables with date/time selection
- **Admin Dashboard** - Comprehensive management panel
- **User Profiles** - Personal profile management
- **Responsive Design** - Mobile-first responsive UI

### 🔐 User Roles
- **Customers** - Place orders, make reservations, manage profile
- **Admins** - Full system management, order/reservation approval
- **Staff** - Limited admin access for daily operations

### 📱 User Experience
- **Real-time Updates** - Live order status updates
- **Cart Management** - Add/remove items with quantity control
- **Order History** - Complete order tracking and history
- **Reservation Management** - View and manage table bookings
- **Profile Customization** - Update personal information and preferences

## 🛠️ Technology Stack

### Frontend
- **React.js 18** - Modern React with hooks and functional components
- **React Router** - Client-side routing and navigation
- **Context API** - State management for auth, cart, and theme
- **Axios** - HTTP client for API communication
- **Lucide React** - Modern icon library
- **Custom CSS** - Responsive styling without external frameworks

### Backend
- **Laravel 10** - PHP framework with Eloquent ORM
- **Laravel Sanctum** - API authentication
- **MySQL** - Relational database
- **RESTful API** - Clean API architecture

### Development Tools
- **Vite** - Fast build tool and dev server
- **ESLint** - Code linting and formatting
- **Git** - Version control

## 📁 Project Structure

```
frontend/
├── public/                 # Static assets
├── src/
│   ├── components/         # React components
│   │   ├── AboutUs/       # About page component
│   │   ├── AdminPanel/    # Admin dashboard
│   │   ├── BookATable/    # Table reservation
│   │   ├── Common/        # Shared components
│   │   │   ├── AuthGuard.jsx
│   │   │   └── ProtectedRoute.jsx
│   │   ├── Error/         # Error handling
│   │   ├── Footer/        # Site footer
│   │   ├── Home/          # Landing page
│   │   ├── Loading/       # Loading states
│   │   ├── Login/         # Authentication
│   │   ├── Navigation/    # Site navigation
│   │   ├── Order/         # Food ordering
│   │   ├── OrdersReservations/ # Order/reservation management
│   │   ├── OurMenu/       # Menu display
│   │   ├── ProfilePage/   # User profile
│   │   └── Register/      # User registration
│   ├── contexts/          # React contexts
│   │   ├── AuthContext.jsx    # Authentication state
│   │   ├── CartContext.jsx    # Shopping cart state
│   │   └── ThemeContext.jsx   # Theme management
│   ├── services/          # API services
│   │   └── api.js         # API client configuration
│   ├── App.jsx            # Main app component
│   ├── main.jsx           # App entry point
│   └── index.css          # Global styles
├── package.json           # Dependencies
├── vite.config.js         # Vite configuration
└── README.md             # Project documentation
```

## 🚀 Installation & Setup

### Prerequisites
- Node.js 16+ and npm
- PHP 8.1+ and Composer
- MySQL 8.0+
- Laravel 10+

### Frontend Setup
```bash
# Clone repository
git clone <repository-url>
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

### Backend Setup
```bash
# Navigate to backend directory
cd backend

# Install PHP dependencies
composer install

# Environment setup
cp .env.example .env
php artisan key:generate

# Database setup
php artisan migrate
php artisan db:seed

# Start Laravel server
php artisan serve
```

### Environment Variables
```env
# Frontend (.env)
VITE_API_BASE_URL=http://localhost:8000/api

# Backend (.env)
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=restaurant_db
DB_USERNAME=root
DB_PASSWORD=

SANCTUM_STATEFUL_DOMAINS=localhost:3000,127.0.0.1:3000
```

## 🔌 API Endpoints

### Authentication
- `POST /api/register` - User registration
- `POST /api/login` - User login
- `POST /api/logout` - User logout
- `GET /api/me` - Get current user

### Profile Management
- `GET /api/profile` - Get user profile
- `PUT /api/profile` - Update user profile
- `POST /api/profile/change-password` - Change password

### Menu Management
- `GET /api/menu` - Get all menu items
- `GET /api/menu/categories` - Get menu categories
- `GET /api/menu/{id}` - Get specific menu item

### Order Management
- `GET /api/orders` - Get all orders (admin) or user orders
- `GET /api/orders/my` - Get user's orders
- `POST /api/orders` - Create new order
- `GET /api/orders/{id}` - Get specific order
- `PUT /api/orders/{id}` - Update order (admin only)
- `DELETE /api/orders/{id}` - Delete order (admin only)

### Reservation Management
- `GET /api/bookings` - Get all bookings (admin) or user bookings
- `GET /api/bookings/my` - Get user's bookings
- `POST /api/bookings` - Create new booking
- `GET /api/bookings/{id}` - Get specific booking
- `DELETE /api/bookings/{id}` - Delete booking

### Admin Endpoints
- `GET /api/admin/dashboard` - Admin dashboard data
- `GET /api/admin/users` - Get all users
- `POST /api/admin/users` - Create new user
- `PUT /api/admin/users/{id}` - Update user
- `DELETE /api/admin/users/{id}` - Delete user
- `PATCH /api/admin/orders/{id}/status` - Update order status
- `PATCH /api/admin/bookings/{id}/status` - Update booking status

## 🗄️ Database Schema

### Users Table
```sql
- id (Primary Key)
- name
- first_name
- last_name
- email (Unique)
- password (Hashed)
- phone
- address
- country
- gender
- role (user/admin)
- email_verified_at
- remember_token
- created_at
- updated_at
```

### Orders Table
```sql
- id (Primary Key)
- user_id (Foreign Key)
- name
- email
- phone
- address
- total (Decimal)
- status (pending/confirmed/preparing/ready/delivered/cancelled)
- notes
- created_at
- updated_at
```

### Order Items Table
```sql
- id (Primary Key)
- order_id (Foreign Key)
- name
- quantity
- price (Decimal)
- subtotal (Decimal)
- notes
- created_at
- updated_at
```

### Table Bookings Table
```sql
- id (Primary Key)
- user_id (Foreign Key)
- guest_name
- email
- phone
- booking_date
- booking_time
- number_of_guests
- special_requests
- status (pending/confirmed/cancelled)
- created_at
- updated_at
```

## 👥 User Roles & Permissions

### Customer (Default Role)
**Can:**
- Register and login
- View menu and place orders
- Make table reservations
- View own order history
- View own reservations
- Update personal profile
- Add items to cart

**Cannot:**
- Access admin panel
- View other users' orders
- Modify order status
- Delete orders/reservations
- Manage users

### Admin Role
**Can:**
- All customer permissions
- Access admin dashboard
- View all orders and reservations
- Update order/reservation status
- Approve/reject reservations
- Manage users (create, edit, delete)
- View system statistics
- Manage menu items
- Delete orders/reservations

**Cannot:**
- Delete own admin account
- Modify system settings (future feature)

## 🧩 Components Overview

### Core Components

#### AuthGuard.jsx
- Protects routes requiring authentication
- Redirects unauthenticated users to login
- Handles authentication state

#### ProtectedRoute.jsx
- Route protection with role-based access
- Admin-only route protection
- Loading states during auth checks

#### Navigation.jsx
- Main site navigation
- User menu with profile/logout
- Role-based menu items
- Responsive mobile navigation

### Feature Components

#### OurMenu.jsx
- Dynamic menu display with categories
- Fallback data when backend unavailable
- Add to cart functionality
- Responsive grid layout
- Special offers section

#### Order.jsx
- Complete ordering system
- Cart integration
- Form validation
- Order submission
- Success/error handling

#### BookATable.jsx
- Table reservation system
- Date/time picker
- Guest count selection
- Special requests
- Form validation

#### ProfilePage.jsx
- User profile management
- Order history display
- Reservation history
- Profile editing
- Statistics cards

#### AdminPanel.jsx
- Comprehensive admin dashboard
- User management
- Order management
- Reservation management
- Statistics overview

### Context Providers

#### AuthContext.jsx
- Authentication state management
- Login/logout functionality
- User data persistence
- Session management
- Role-based permissions

#### CartContext.jsx
- Shopping cart state
- Add/remove items
- Quantity management
- Cart persistence
- Total calculation

#### ThemeContext.jsx
- Theme management
- Dark/light mode toggle
- Theme persistence
- Component theming

## 🎨 Styling & UI

### Design System
- **Color Palette**: Modern restaurant theme with warm colors
- **Typography**: Clean, readable fonts
- **Spacing**: Consistent margin/padding system
- **Components**: Reusable UI components
- **Responsive**: Mobile-first design approach

### CSS Architecture
- **Component-based**: Each component has its own CSS file
- **Global Styles**: Common styles in index.css
- **Custom Properties**: CSS variables for theming
- **Media Queries**: Responsive breakpoints
- **Animations**: Smooth transitions and hover effects

### UI Components
- **Buttons**: Primary, secondary, danger variants
- **Forms**: Styled inputs with validation
- **Cards**: Content containers with shadows
- **Modals**: Overlay dialogs
- **Loading States**: Spinners and skeletons
- **Error States**: User-friendly error messages

## 🔐 Authentication Flow

### Registration Process
1. User fills registration form
2. Frontend validates input
3. API call to `/api/register`
4. Backend creates user account
5. JWT token returned
6. User automatically logged in
7. Redirect to dashboard

### Login Process
1. User enters credentials
2. API call to `/api/login`
3. Backend validates credentials
4. JWT token generated
5. Token stored in localStorage
6. User context updated
7. Redirect to intended page

### Session Management
- **Token Storage**: localStorage for persistence
- **Auto-logout**: 24-hour session expiry
- **Activity Tracking**: 30-minute inactivity timeout
- **Token Refresh**: Automatic token validation
- **Logout**: Token invalidation and cleanup

## 🛒 Order Management

### Order Creation Flow
1. User browses menu
2. Adds items to cart
3. Proceeds to checkout
4. Fills delivery information
5. Reviews order details
6. Submits order
7. Receives confirmation
8. Order appears in history

### Order States
- **Pending**: Newly created order
- **Confirmed**: Admin approved order
- **Preparing**: Kitchen started preparation
- **Ready**: Order ready for delivery
- **Delivered**: Order completed
- **Cancelled**: Order cancelled

### Cart Functionality
- **Add Items**: From menu with quantity
- **Remove Items**: Individual item removal
- **Update Quantity**: Increase/decrease amounts
- **Clear Cart**: Remove all items
- **Persist Cart**: Survives page refresh
- **Calculate Total**: Automatic price calculation

## 📅 Reservation System

### Booking Process
1. User selects date and time
2. Chooses number of guests
3. Adds special requests
4. Submits reservation
5. Receives confirmation
6. Admin can approve/reject

### Reservation States
- **Pending**: Awaiting admin approval
- **Confirmed**: Admin approved
- **Cancelled**: User or admin cancelled

### Features
- **Date Validation**: Future dates only
- **Time Slots**: Available time selection
- **Guest Limits**: Maximum party size
- **Special Requests**: Custom requirements
- **Confirmation**: Email notifications (future)

## 👨‍💼 Admin Panel

### Dashboard Overview
- **Statistics Cards**: Users, orders, reservations, revenue
- **Quick Actions**: Common admin tasks
- **Recent Activity**: Latest orders and bookings
- **Charts**: Visual data representation (future)

### User Management
- **User List**: All registered users
- **User Details**: Profile information
- **Role Management**: Assign admin roles
- **User Status**: Active/inactive users
- **Bulk Actions**: Mass user operations

### Order Management
- **Order List**: All orders with filters
- **Order Details**: Complete order information
- **Status Updates**: Change order status
- **Order History**: Track order progression
- **Bulk Operations**: Mass status updates

### Reservation Management
- **Booking List**: All table reservations
- **Booking Details**: Reservation information
- **Status Management**: Approve/reject bookings
- **Calendar View**: Visual booking calendar (future)
- **Conflict Detection**: Prevent double bookings

## 🚀 Deployment

### Frontend Deployment (Vercel/Netlify)
```bash
# Build for production
npm run build

# Deploy to Vercel
vercel --prod

# Deploy to Netlify
netlify deploy --prod --dir=dist
```

### Backend Deployment (DigitalOcean/AWS)
```bash
# Production build
composer install --optimize-autoloader --no-dev

# Environment setup
php artisan config:cache
php artisan route:cache
php artisan view:cache

# Database migration
php artisan migrate --force

# Start server
php artisan serve --host=0.0.0.0 --port=8000
```

### Environment Configuration
```env
# Production settings
APP_ENV=production
APP_DEBUG=false
APP_URL=https://your-domain.com

# Database
DB_CONNECTION=mysql
DB_HOST=your-db-host
DB_DATABASE=production_db
DB_USERNAME=production_user
DB_PASSWORD=secure_password

# CORS
SANCTUM_STATEFUL_DOMAINS=your-frontend-domain.com
```

## 🤝 Contributing

### Development Workflow
1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open Pull Request

### Code Standards
- **ESLint**: Follow configured linting rules
- **Component Structure**: Use functional components with hooks
- **File Naming**: PascalCase for components, camelCase for utilities
- **CSS**: Component-scoped styles
- **Comments**: Minimal, only for complex logic

### Testing
- **Unit Tests**: Component testing (future)
- **Integration Tests**: API testing (future)
- **E2E Tests**: User flow testing (future)

## 📞 Support

For support and questions:
- **Email**: support@restaurant-system.com
- **Documentation**: [Project Wiki](link-to-wiki)
- **Issues**: [GitHub Issues](link-to-issues)

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

**Built with ❤️ for modern restaurant management**