# Food Delivery Tracking System

A full-stack food delivery application with real-time delivery tracking, order management, and interactive mapping. Customers can track their orders live, see estimated delivery times, and communicate with delivery partners.

## Features

- 🗺️ **Real-time Delivery Tracking** - Live GPS tracking with WebSocket updates
- 📱 **Responsive Frontend** - Mobile-first React/Next.js UI
- 🔐 **User Authentication** - JWT-based auth for customers, restaurants, and delivery partners
- 🛒 **Order Management** - Browse restaurants, place orders, track status
- 📍 **Interactive Maps** - Google Maps/Mapbox integration for delivery visualization
- ⚡ **Real-time Updates** - Socket.io for instant order and location updates
- 📊 **Admin Dashboard** - Manage restaurants, orders, and delivery partners
- 💳 **Payment Integration** - Stripe integration for secure payments
- 🔔 **Push Notifications** - Real-time alerts for order status changes

## Tech Stack

### Frontend
- **React 18** with Next.js App Router
- **TypeScript** for type safety
- **Tailwind CSS** for styling
- **Socket.io-client** for real-time updates
- **Google Maps React** / **Mapbox GL** for mapping
- **Zustand** for state management
- **TanStack Query** for data fetching

### Backend
- **Node.js** with Express.js
- **TypeScript**
- **PostgreSQL** with Prisma ORM
- **Socket.io** for WebSocket communication
- **JWT** for authentication
- **Stripe** for payments
- **Redis** for caching and session management

### DevOps
- **Docker & Docker Compose** for containerization
- **GitHub Actions** for CI/CD
- **Nginx** for reverse proxy

## Project Structure

```
food-delivery-tracking/
├── frontend/                 # Next.js React application
│   ├── app/                 # App router pages and layouts
│   │   ├── (auth)/         # Authentication pages
│   │   ├── (customer)/     # Customer dashboard and tracking
│   │   ├── (restaurant)/   # Restaurant management
│   │   └── (admin)/        # Admin dashboard
│   ├── components/          # Reusable React components
│   │   ├── maps/           # Map-related components
│   │   ├── tracking/       # Delivery tracking components
│   │   ├── orders/         # Order management components
│   │   └── common/         # Shared UI components
│   ├── hooks/              # Custom React hooks
│   ├── services/           # API and WebSocket services
│   ├── store/              # Zustand state management
│   ├── types/              # TypeScript type definitions
│   └── public/             # Static assets
│
├── backend/                 # Express.js API server
│   ├── src/
│   │   ├── routes/         # API route handlers
│   │   │   ├── auth.ts
│   │   │   ├── orders.ts
│   │   │   ├── deliveries.ts
│   │   │   ├── restaurants.ts
│   │   │   └── users.ts
│   │   ├── controllers/    # Business logic
│   │   ├── services/       # Domain services
│   │   ├── middleware/     # Express middleware
│   │   ├── models/         # Prisma schema and database models
│   │   ├── sockets/        # Socket.io event handlers
│   │   ├── utils/          # Utility functions
│   │   ├── config/         # Configuration
│   │   └── index.ts        # Server entry point
│   ├── prisma/
│   │   ├── schema.prisma   # Database schema
│   │   └── migrations/     # Database migrations
│   └── tests/              # Test files
│
├── docker-compose.yml       # Multi-container orchestration
├── .env.example            # Environment variables template
├── .github/
│   └── workflows/          # CI/CD workflows
└── docs/                   # Documentation
    ├── API.md
    ├── DEPLOYMENT.md
    └── ARCHITECTURE.md
```

## Quick Start

### Prerequisites
- Node.js 18+
- Docker & Docker Compose
- PostgreSQL 14+ (or use Docker)
- Git

### Setup

1. **Clone the repository**
```bash
git clone https://github.com/preethimaayakrishnan007-bit/food-delivery-tracking.git
cd food-delivery-tracking
```

2. **Setup Environment Variables**
```bash
cp .env.example .env
# Edit .env with your configuration
```

3. **Start with Docker Compose**
```bash
docker-compose up -d
```

4. **Run Database Migrations**
```bash
cd backend
npx prisma migrate deploy
npx prisma db seed
cd ..
```

5. **Access the Application**
- Frontend: http://localhost:3000
- Backend API: http://localhost:5000
- Admin Panel: http://localhost:3000/admin

### Manual Setup (Development)

**Backend:**
```bash
cd backend
npm install
npm run dev
```

**Frontend:**
```bash
cd frontend
npm install
npm run dev
```

## Environment Variables

See `.env.example` for all required variables:

```
# Database
DATABASE_URL=postgresql://user:password@localhost:5432/food_delivery

# JWT
JWT_SECRET=your_secret_key
JWT_EXPIRY=7d

# Google Maps
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_api_key

# Stripe
STRIPE_SECRET_KEY=your_secret_key
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=your_publishable_key

# Socket.io
SOCKET_URL=http://localhost:5000

# Email Service
SMTP_HOST=smtp.gmail.com
SMTP_PORT=587
SMTP_USER=your_email
SMTP_PASS=your_password
```

## API Endpoints

### Authentication
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Login user
- `POST /api/auth/refresh` - Refresh JWT token
- `POST /api/auth/logout` - Logout user

### Orders
- `GET /api/orders` - List user orders
- `POST /api/orders` - Create new order
- `GET /api/orders/:id` - Get order details
- `PATCH /api/orders/:id` - Update order status
- `DELETE /api/orders/:id` - Cancel order

### Deliveries
- `GET /api/deliveries` - List deliveries
- `POST /api/deliveries/:orderId` - Assign delivery
- `PATCH /api/deliveries/:id/location` - Update delivery location
- `PATCH /api/deliveries/:id/status` - Update delivery status

### Restaurants
- `GET /api/restaurants` - List restaurants
- `GET /api/restaurants/:id` - Get restaurant details
- `GET /api/restaurants/:id/menu` - Get restaurant menu

### Users
- `GET /api/users/profile` - Get user profile
- `PATCH /api/users/profile` - Update profile
- `POST /api/users/addresses` - Add delivery address

## Real-time Events (WebSocket)

### Client to Server
- `delivery:start` - Start delivery tracking
- `delivery:stop` - Stop tracking delivery
- `order:track` - Request order updates

### Server to Client
- `delivery:location` - New delivery location update
- `order:status` - Order status changed
- `delivery:eta` - Estimated time updated
- `notification:alert` - Push notification

## Development

### Running Tests
```bash
cd backend
npm run test

cd ../frontend
npm run test
```

### Linting & Formatting
```bash
npm run lint
npm run format
```

### Building for Production
```bash
docker-compose -f docker-compose.prod.yml up -d
```

## Database Schema

- **Users** - Customers, restaurants, delivery partners
- **Restaurants** - Restaurant information
- **Menus & Items** - Restaurant menu and food items
- **Orders** - Customer orders with items and status
- **Deliveries** - Delivery assignments and tracking
- **Locations** - GPS coordinates and delivery routes
- **Payments** - Payment records and transactions
- **Addresses** - Customer delivery addresses
- **Reviews & Ratings** - Customer feedback

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see LICENSE file for details.

## Support

For support, email support@fooddelivery.com or open an issue on GitHub.

## Roadmap

- [ ] In-app chat with delivery partners
- [ ] AI-powered delivery time prediction
- [ ] Multi-language support
- [ ] Loyalty rewards program
- [ ] Integration with payment gateways
- [ ] Analytics dashboard
- [ ] Mobile app (React Native)
