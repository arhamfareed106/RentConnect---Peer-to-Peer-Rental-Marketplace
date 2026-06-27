# 🚀 RentConnect - Quick Start Guide

Get RentConnect up and running in 5 minutes!

## Prerequisites Check

Before you start, make sure you have:
- ✅ Node.js (v20 or higher) - [Download](https://nodejs.org/)
- ✅ npm or pnpm package manager
- ✅ Git (optional, for version control)

## Step 1: Install Dependencies

```bash
npm install
```

This will install all required packages for both frontend and backend.

## Step 2: Configure Environment

Copy the example environment file:

```bash
copy .env.example .env
```

**Minimum required configuration** for development:

```env
NODE_ENV=development
PORT=4000
CLIENT_URL=http://localhost:3000
JWT_ACCESS_SECRET=your-super-secret-key-change-this
JWT_REFRESH_SECRET=your-other-super-secret-key-change-this
```

**Optional services** (can be added later):
- Stripe for payments
- Cloudinary for image hosting
- Resend for emails
- Twilio for SMS
- PostgreSQL database URL (currently using JSON mock DB)

## Step 3: Start Development Server

```bash
npm run dev
```

This starts:
- 🎨 Frontend at **http://localhost:3000**
- 🔧 Backend API at **http://localhost:4000**

## Step 4: Open in Browser

Navigate to:
```
http://localhost:3000
```

You should see the RentConnect homepage! 🎉

## Common Commands

| Command | What It Does |
|---------|--------------|
| `npm run dev` | Start frontend + backend in dev mode |
| `npm run dev:client` | Start frontend only |
| `npm run dev:server` | Start backend only |
| `npm run build` | Build for production |
| `npm start` | Run production build |
| `npm run check` | Type-check TypeScript |
| `npm run format` | Format code with Prettier |

## Default Test Account

The mock database includes a test account:

- **Email:** `john@example.com`
- **Password:** `password123`

Or create your own account via the signup page!

## What's Next?

### For Development
1. Explore the codebase in `client/src/` (frontend) and `server/` (backend)
2. Check out `shared/contracts.ts` for TypeScript types
3. Read API docs in `README.md`

### For Production
1. Set up a PostgreSQL database
2. Configure Stripe for payments
3. Set up Cloudinary for image storage
4. Follow deployment guide in `DEPLOY.md`

### For Learning
1. Browse existing pages in `client/src/pages/`
2. Check out components in `client/src/components/`
3. Explore API routes in `server/index.ts`

## Troubleshooting

### Port Already in Use
If port 3000 or 4000 is busy:
- The frontend will automatically try the next available port
- For backend, change `PORT` in `.env`

### Dependencies Won't Install
```bash
# Clear cache and reinstall
npm cache clean --force
rm -rf node_modules
npm install
```

### Build Errors
```bash
# Run TypeScript check
npm run check

# Check for syntax errors
npm run format
```

### Can't Connect to API
- Make sure backend is running on port 4000
- Check that `CLIENT_URL` in `.env` matches your frontend URL
- Verify no CORS errors in browser console

## Project Structure (Quick Reference)

```
rentconnect/
├── client/src/          → React frontend
│   ├── pages/          → Page components
│   ├── components/     → Reusable UI components
│   ├── features/       → Feature modules (auth, bookings, etc.)
│   └── services/       → API calls
├── server/             → Express backend
│   ├── index.ts        → Main API routes
│   └── lib/            → Auth & DB utilities
├── shared/             → Shared types between frontend/backend
├── .env                → Your local environment variables
└── package.json        → Dependencies & scripts
```

## Need Help?

- 📖 Full documentation: `README.md`
- 🚀 Deployment guide: `DEPLOY.md`
- 🔧 API reference: See `README.md` API section
- 📝 Change log: `CHANGELOG.md`

---

**Happy Coding! 🎉**

Built with React, TypeScript, Node.js, and Express.
