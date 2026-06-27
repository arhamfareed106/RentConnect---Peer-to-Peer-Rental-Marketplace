# RentConnect - Peer-to-Peer Rental Marketplace

A full-stack web application for peer-to-peer item rental services, built with React, Node.js, Express, and PostgreSQL/Prisma.

## 🎯 Overview

RentConnect enables users to rent and lend items within their community. The platform facilitates secure transactions, messaging, booking management, and dispute resolution between renters and owners.

## ✨ Key Features

### For Renters
- **Browse & Search** - Find items by category, location, and availability
- **Advanced Filtering** - Filter by price range, verified owners, and dates
- **Secure Booking** - Book items with integrated payment processing
- **Real-time Chat** - Message owners directly about listings
- **Review System** - Rate and review items after rental
- **Dashboard** - Manage bookings, messages, and notifications

### For Owners
- **List Items** - Create listings with photos, descriptions, and pricing
- **Manage Bookings** - Accept/reject booking requests
- **Availability Control** - Set dates when items are available
- **Earnings Tracking** - Monitor revenue from rentals
- **Insurance Options** - Offer damage protection to renters

### Platform Features
- **User Verification** - Trust score and verification badges
- **Dispute Management** - Raise and resolve booking disputes
- **Payment Integration** - Stripe payment processing (with mock mode for development)
- **Real-time Notifications** - Socket.io powered live updates
- **Responsive Design** - Modern UI with Tailwind CSS and Radix UI components
- **File Uploads** - Multer-based image upload system

## 🛠️ Tech Stack

### Frontend
- **React 19** - UI library
- **TypeScript** - Type safety
- **Vite** - Build tool and dev server
- **Tailwind CSS 4** - Utility-first CSS framework
- **Radix UI** - Headless UI components
- **TanStack Query** - Data fetching and caching
- **Wouter** - Client-side routing
- **Framer Motion** - Animation library
- **Socket.io Client** - Real-time communication

### Backend
- **Node.js** - Runtime environment
- **Express** - Web framework
- **TypeScript** - Type safety
- **Prisma** - Database ORM
- **PostgreSQL** - Primary database
- **Socket.io** - WebSocket server for real-time features
- **JWT** - Authentication
- **Bcrypt** - Password hashing
- **Multer** - File upload handling

### Additional Services
- **Stripe** - Payment processing
- **Cloudinary** - Image storage (optional)
- **Redis** - Caching layer (optional)
- **Resend** - Email service
- **Twilio** - SMS notifications
- **BullMQ** - Job queue system

## 📁 Project Structure

```
rentconnect/
├── client/                # Frontend React application
│   ├── public/           # Static assets
│   └── src/
│       ├── app/          # App configuration (providers, router)
│       ├── components/   # Reusable UI components
│       ├── contexts/     # React contexts
│       ├── features/     # Feature-based modules (auth, bookings, etc.)
│       ├── hooks/        # Custom React hooks
│       ├── lib/          # Utility functions
│       ├── pages/        # Page components
│       └── services/     # API service layer
├── server/               # Backend Express application
│   ├── data/            # Mock database (JSON)
│   ├── lib/             # Server utilities (auth, db)
│   └── index.ts         # Main server file
├── shared/               # Shared TypeScript types and constants
│   ├── contracts.ts     # Type definitions
│   └── const.ts         # Shared constants
├── prisma/              # Database schema and migrations
└── dist/                # Production build output
```

## 🚀 Getting Started

### Prerequisites

- **Node.js** (v20 or higher)
- **npm** or **pnpm**
- **PostgreSQL** (v15 or higher) - Optional for production
- **Redis** (optional for caching)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd rentconnect
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Configure environment variables**
   ```bash
   cp .env.example .env
   ```
   
   Edit `.env` with your configuration:
   ```env
   NODE_ENV=development
   PORT=4000
   CLIENT_URL=http://localhost:3000
   DATABASE_URL=postgresql://postgres:postgres@localhost:5432/rentconnect
   JWT_ACCESS_SECRET=your-random-secret-here
   JWT_REFRESH_SECRET=your-random-secret-here
   STRIPE_SECRET_KEY=sk_test_...
   STRIPE_PUBLISHABLE_KEY=pk_test_...
   # ... other variables
   ```

4. **Set up the database** (if using PostgreSQL with Prisma)
   ```bash
   npx prisma generate
   npx prisma migrate dev
   ```

### Development

Start both frontend and backend in development mode:

```bash
npm run dev
```

This runs:
- Frontend at `http://localhost:5173` (Vite dev server)
- Backend at `http://localhost:4000` (Express API)

**Alternatively, run separately:**

```bash
# Terminal 1 - Backend
npm run dev:server

# Terminal 2 - Frontend
npm run dev:client
```

### Building for Production

```bash
npm run build
```

This creates:
- Frontend build in `dist/public/`
- Backend build in `dist/`

### Running Production Build

```bash
npm start
```

The app serves both frontend and backend on the configured `PORT` (default: 4000).

## 🔧 Available Scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Run frontend and backend concurrently in dev mode |
| `npm run dev:server` | Run backend only in watch mode |
| `npm run dev:client` | Run frontend only with Vite |
| `npm run build` | Build for production (frontend + backend) |
| `npm start` | Start production server |
| `npm run check` | Type-check TypeScript without emitting |
| `npm run format` | Format code with Prettier |

## 🐳 Docker Deployment

### Using Docker Compose

```bash
docker-compose up -d
```

This starts:
- PostgreSQL database on port 5432
- Redis cache on port 6379
- RentConnect backend on port 4000

### Environment Variables for Docker

Ensure these are set in your `.env` file:
- `JWT_ACCESS_SECRET`
- `JWT_REFRESH_SECRET`
- `STRIPE_SECRET_KEY` (or leave as "mock" for development)
- `CLOUDINARY_*` variables (if using Cloudinary)
- `RESEND_API_KEY` (if using email)
- `TWILIO_*` variables (if using SMS)

## 📚 API Documentation

### Authentication

- `POST /api/auth/signup` - Create new user account
- `POST /api/auth/login` - Login with email and password
- `GET /api/auth/me` - Get current user profile (requires auth)

### Listings

- `GET /api/items` - Browse all active listings (with filters)
- `GET /api/items/:id` - Get listing details
- `POST /api/items` - Create new listing (requires auth)
- `PUT /api/items/:id` - Update listing (requires auth)
- `DELETE /api/items/:id` - Delete listing (requires auth)

### Bookings

- `POST /api/bookings` - Create booking request (requires auth)
- `GET /api/bookings/me` - Get user's bookings as renter (requires auth)
- `GET /api/bookings/owner` - Get user's bookings as owner (requires auth)
- `GET /api/bookings/:id` - Get booking details (requires auth)

### Payments

- `POST /api/payments/checkout` - Create checkout session (requires auth)
- `POST /api/payments/session/:id/confirm` - Confirm payment (requires auth)

### Chat & Messaging

- `GET /api/chat/conversations` - Get all conversations (requires auth)
- `POST /api/chat/conversations` - Start new conversation (requires auth)
- `GET /api/chat/conversations/:id/messages` - Get messages (requires auth)
- `POST /api/chat/conversations/:id/messages` - Send message (requires auth)
- `POST /api/chat/conversations/:id/read` - Mark as read (requires auth)

### Notifications

- `GET /api/notifications` - Get user notifications (requires auth)
- `POST /api/notifications/:id/read` - Mark notification as read (requires auth)

### Profile

- `GET /api/profile` - Get user profile (requires auth)
- `PUT /api/profile` - Update profile (requires auth)

### Disputes

- `POST /api/disputes` - Create dispute (requires auth)
- `GET /api/disputes` - Get user's disputes (requires auth)
- `GET /api/disputes/:id` - Get dispute details (requires auth)
- `PATCH /api/disputes/:id` - Update dispute status (requires auth)

### File Uploads

- `POST /api/uploads` - Upload files/images (requires auth)

## 🔐 Authentication

The app uses **JWT (JSON Web Tokens)** for authentication:

1. User signs up or logs in
2. Server returns JWT token
3. Client stores token (localStorage/sessionStorage)
4. Client includes token in `Authorization` header: `Bearer <token>`
5. Server validates token on protected routes

Token includes:
- User ID
- Expiration time (15 minutes for access, 30 days for refresh)

## 🎨 UI Components

The app uses a comprehensive design system with:

- **Radix UI** - Accessible, unstyled component primitives
- **Tailwind CSS** - Utility-first styling
- **shadcn/ui** - Pre-built component patterns
- **Framer Motion** - Smooth animations
- **Lucide React** - Icon library

Components available in `client/src/components/ui/`:
- Buttons, Cards, Dialogs, Dropdowns
- Forms, Inputs, Selects, Textareas
- Tables, Tabs, Toasts, Tooltips
- Calendars, Carousels, Charts
- And 40+ more...

## 🔌 Real-time Features

WebSocket connection via Socket.io for:
- **Live chat messages** - Instant message delivery
- **Notifications** - Real-time alerts for bookings, payments
- **Booking updates** - Status changes broadcast to users

Socket rooms:
- `user:<userId>` - User-specific events
- `conversation:<conversationId>` - Chat room events

## 🧪 Testing

Currently configured with:
- **Vitest** - Unit testing framework
- **Supertest** - API endpoint testing

```bash
# Run tests
npm test

# Run tests in watch mode
npm run test:watch
```

## 🚢 Deployment

The project supports deployment to:

- **Railway** - Recommended for full-stack apps
- **Render** - Good for monorepo setup
- **Vercel** - For frontend (with separate backend)
- **Docker** - Self-hosted via Docker Compose

See `DEPLOY.md` for detailed deployment instructions and platform-specific configurations.

## 📝 Environment Variables

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `NODE_ENV` | Environment mode | No | `development` |
| `PORT` | Server port | No | `4000` |
| `CLIENT_URL` | Frontend URL (CORS) | Yes | - |
| `DATABASE_URL` | PostgreSQL connection string | Yes | - |
| `JWT_ACCESS_SECRET` | JWT signing secret | Yes | - |
| `JWT_REFRESH_SECRET` | Refresh token secret | Yes | - |
| `STRIPE_SECRET_KEY` | Stripe API key | No | `mock` |
| `STRIPE_PUBLISHABLE_KEY` | Stripe public key | No | `mock` |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary account | No | - |
| `CLOUDINARY_API_KEY` | Cloudinary API key | No | - |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret | No | - |
| `REDIS_URL` | Redis connection URL | No | - |
| `RESEND_API_KEY` | Email service API key | No | - |
| `TWILIO_ACCOUNT_SID` | Twilio account ID | No | - |
| `TWILIO_AUTH_TOKEN` | Twilio auth token | No | - |
| `TWILIO_PHONE_NUMBER` | Twilio phone number | No | - |

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License.

## 🙏 Acknowledgments

- Design inspiration from Hygglo
- UI components from shadcn/ui
- Icons from Lucide React

## 📞 Support

For issues or questions:
- Open an issue on GitHub
- Check existing documentation
- Review API endpoints in server code

---

**Built with ❤️ by the RentConnect Team**
