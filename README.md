# RentEasy - Vehicle Rental Platform

This project is a full-stack vehicle rental platform with role-based authentication (User, Owner, Admin), vehicle management, booking functionalities, real-time updates, and a dummy payment flow.

## Features

-   **Authentication & Authorization**: Role-based (User, Owner, Admin) signup/login with JWT access and refresh tokens.
-   **Vehicle Management**: Owners can add, view, update, and delete their vehicles, including image uploads.
-   **Booking System**: Users can search for vehicles, view details, and create bookings. Real-time updates for booking status.
-   **Admin Panel**: Administrators can manage users, vehicles, and bookings.
-   **Dummy Payment Integration**: Simulated payment flow to confirm bookings.
-   **Real-time Updates**: Socket.io for instant notifications on booking status changes.

## Setup and Installation

### Prerequisites

-   Node.js (v14 or higher)
-   MongoDB

### 1. Clone the repository

```bash
git clone <repository_url>
cd RENTEASY
```

### 2. Backend Setup (SERVER directory)

Navigate to the `SERVER` directory:

```bash
cd SERVER
```

Install dependencies:

```bash
npm install
```

Create a `.env` file in the `SERVER` directory based on `.env.example`:

```
PORT=3000
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=a_very_strong_secret_key_for_jwt
JWT_REFRESH_SECRET=another_very_strong_secret_key_for_jwt_refresh
```

Start the backend server:

```bash
npm start
```

The backend server will run on `http://localhost:3000` (or your specified PORT).

### 3. Frontend Setup (CLIENT directory)

Open a new terminal and navigate to the `CLIENT` directory:

```bash
cd CLIENT
```

Install dependencies:

```bash
npm install
```

Start the frontend development server:

```bash
npm run dev
```

The frontend application will run on `http://localhost:5173` (or your specified port).

## API Endpoints (Backend)

### Authentication
-   `POST /api/auth/register`
-   `POST /api/auth/login`
-   `POST /api/auth/refresh`
-   `POST /api/auth/logout`

### Vehicles
-   `POST /api/vehicles` (Owner)
-   `GET /api/vehicles` (Public, with filters)
-   `GET /api/vehicles/:id` (Public)
-   `PUT /api/vehicles/:id` (Owner)
-   `DELETE /api/vehicles/:id` (Owner)
-   `GET /api/vehicles/my-vehicles` (Owner)

### Bookings
-   `POST /api/bookings` (User)
-   `GET /api/bookings` (User/Owner)
-   `GET /api/bookings/:id` (User/Owner)
-   `PUT /api/bookings/:id/status` (User/Owner/Admin)

### Payments (Dummy)
-   `POST /api/payments/create` (User)
-   `POST /api/payments/verify` (User)

### Admin
-   `GET /api/admin/users` (Admin)
-   `GET /api/admin/vehicles` (Admin)
-   `GET /api/admin/bookings` (Admin)
-   `PUT /api/admin/users/:id/block` (Admin)

## Environment Variables

Create a `.env` file in the `SERVER` directory with the following:

-   `PORT`: Port for the backend server (e.g., `3000`)
-   `MONGO_URI`: Your MongoDB connection string (e.g., `mongodb://localhost:27017/renteasy`)
-   `JWT_SECRET`: A strong, random string for JWT access token signing.
-   `JWT_REFRESH_SECRET`: A strong, random string for JWT refresh token signing.

## Migration Notes

If you are migrating from a previous version of the database, please note the following schema changes:

-   **User Model**: Added `role` (enum: 'user', 'owner', 'admin'), `passwordHash` (instead of `password`), `phone`, and an embedded `ownerProfile` object for owners.
-   **Vehicle Model**: Replaced `Car` model. New fields include `ownerId`, `title`, `category`, `images`, `description`, `seats`, `pricePerHour`, `pricePerDay`, `location` (with `city` and `coords`), `features`, `isAvailable`.
-   **Booking Model**: Updated fields to `userId`, `ownerId`, `vehicleId`, `startDateTime`, `endDateTime`, `amount`, `status`, `paymentStatus`.
-   **Payment Model**: Updated fields to `bookingId`, `amount`, `method`, `status`, `transactionRef`.

For existing data, you may need to manually update documents to conform to the new schemas or write a migration script. For example, existing `User` documents will need a `role` field added, and `password` fields will need to be hashed and renamed to `passwordHash`.

## Sample cURL/Postman Requests

(Coming Soon - will be added in a future update)
