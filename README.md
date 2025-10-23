# Dairy Farm Management System - FSD Project

A full-stack MERN application for managing dairy farm operations with separate interfaces for customers and vendors.

## Team Members:
- Pavithra Lakshmi
- Rohini
- Harika Priya
- Bhavani

## Project Overview:
This web application connects dairy farmers (vendors) with customers, enabling product subscriptions, inventory management, and automated delivery scheduling.

## Tech Stack:
- **Frontend**: React.js, MUI Joy UI, Recoil (State Management)
- **Backend**: Node.js, Express.js
- **Database**: MongoDB with Mongoose ODM
- **Authentication**: JWT (JSON Web Tokens)
- **Security**: bcryptjs for password hashing

## Key Features:

### Customer Portal:
- User registration and authentication
- Browse available dairy vendors
- View vendor details (location, timings, products)
- Add products to cart with customizable delivery schedules
- Subscribe to products for recurring deliveries
- Manage subscriptions and cart
- Profile management

### Vendor Portal:
- Vendor registration and authentication
- Dairy farm profile setup (name, timings, working days)
- Product inventory management (add, update, remove)
- View and manage customer subscriptions
- Track product quantities and availability
- Bank account information for payments

### System Features:
- Real-time farm status (open/closed) based on operating hours
- Quantity management to prevent overbooking
- Weekly subscription scheduling
- Secure JWT-based authentication
- Responsive design for all devices

## Installation & Setup:

### Prerequisites:
- Node.js (v14+)
- MongoDB (local or Atlas)
- npm/yarn

### 1. Clone Repository:
```bash
git clone <repository-url>
cd MERN-Dairy-Farm-WebApp
```

### 2. Backend Setup:
```bash
cd backend
npm install
```

Create `.env` file in backend folder:
```env
MONGODBURI=your_mongodb_connection_string
PORT=5000
SECRETKEY=your_jwt_secret_key
SALT=10
```

### 3. Frontend Setup:
```bash
cd ../frontend
npm install
```

### 4. Run Application:

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```

Access at: `http://localhost:5173`

## Project Structure:

```
MERN-Dairy-Farm-WebApp/
├── backend/
│   ├── controllers/     # Business logic
│   ├── models/          # MongoDB schemas
│   ├── routes/          # API endpoints
│   ├── middleware/      # Auth middleware
│   ├── .env            # Environment variables
│   └── server.js       # Entry point
├── frontend/
│   ├── src/
│   │   ├── components/ # React components
│   │   ├── atoms/      # Recoil state
│   │   ├── utils/      # Helper functions
│   │   ├── assets/     # Images, themes
│   │   └── App.jsx     # Main component
│   └── public/         # Static assets
└── README.md
```

## Database Schema:

### Customer Model:
- first_name, last_name, emailID, password
- phoneNumber, address
- cart: [{ product, daily_quantity, days, startDate }]
- subscriptions: [Subscription references]

### Vendor Model:
- first_name, last_name, emailID, password
- phoneNumber, address
- dairyFarm: { name, openingHours, closingHours, establishedDate }
- workingDays: [String]
- account: { holderName, bankName, IFSC, accountNumber }
- products: [Product references]
- subscriptions: [Subscription references]

### Product Model:
- name, description, price, discount
- weeklyQuantity, usedQuantity
- vendor: Vendor reference

### Subscription Model:
- product: Product reference
- customer: Customer reference
- daily_quantity, startDate
- days: [String]

## API Documentation:

### Customer APIs:
- POST `/api/customer/register` - Register new customer
- POST `/api/customer/login` - Customer login
- GET `/api/customer/` - Get profile (Auth required)
- PATCH `/api/customer/` - Update profile (Auth required)
- POST `/api/customer/addToCart` - Add to cart (Auth required)
- POST `/api/customer/removeFromCart` - Remove from cart (Auth required)
- POST `/api/customer/updateCart` - Update cart (Auth required)
- POST `/api/customer/addSub` - Create subscription (Auth required)
- POST `/api/customer/removeSub` - Cancel subscription (Auth required)
- GET `/api/customer/getSubs` - Get subscriptions (Auth required)
- GET `/api/customer/getCart` - Get cart (Auth required)
- GET `/api/customer/getVendors` - List all vendors

### Vendor APIs:
- POST `/api/vendor/register` - Register new vendor
- POST `/api/vendor/login` - Vendor login
- GET `/api/vendor/` - Get profile (Auth required)
- PATCH `/api/vendor/` - Update profile (Auth required)
- POST `/api/vendor/addProduct` - Add product (Auth required)
- POST `/api/vendor/removeProduct` - Remove product (Auth required)
- PATCH `/api/vendor/updateProduct` - Update product (Auth required)
- GET `/api/vendor/getSubs` - Get subscriptions (Auth required)

### General APIs:
- GET `/api/general/` - Get user type (Auth required)
- POST `/api/general/getProducts` - Get vendor products (Auth required)

## Security Features:
- Password hashing with bcrypt
- JWT token-based authentication
- Protected routes with auth middleware
- CORS configuration for secure communication
- Environment variables for sensitive data

## Development Notes:
- Frontend uses Recoil for state management
- Centralized API base URL in `frontend/src/url.jsx`
- Images stored in `frontend/public/assets/images/`
- MUI Joy UI for consistent design
- Vite for fast development builds