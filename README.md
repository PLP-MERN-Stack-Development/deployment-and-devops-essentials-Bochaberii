# 💬 Real-Time Chat Application - MERN Stack

A full-stack real-time chat application built with MongoDB, Express.js, React, and Node.js, featuring WebSocket communication via Socket.IO and authentication with Clerk.

## 🌐 Live Deployment

- **Frontend:** [https://your-app.vercel.app](https://your-app.vercel.app)
- **Backend API:** [https://your-api.onrender.com](https://your-api.onrender.com)
- **API Health Check:** [https://your-api.onrender.com/healthz](https://your-api.onrender.com/healthz)

> **Note:** Replace the URLs above with your actual deployed URLs

## 🚀 Features

- Real-time messaging with Socket.IO
- User authentication via Clerk
- Create and join conversations
- User presence tracking
- Responsive UI built with React and Tailwind CSS
- RESTful API for message and conversation management
- MongoDB for persistent data storage

## 📁 Project Structure

```
Week5-Chat/
├── backend/                 # Express.js server
│   ├── src/
│   │   ├── config/         # Database configuration
│   │   ├── controllers/    # Route controllers
│   │   ├── middleware/     # Auth and Socket middleware
│   │   ├── models/         # MongoDB models
│   │   ├── routes/         # API routes
│   │   ├── utils/          # Utility functions
│   │   └── server.js       # Server entry point
│   └── package.json
└── frontend/               # React + Vite application
    ├── src/
    ├── index.html
    ├── vite.config.js
    └── package.json
```

## 🛠️ Technology Stack

### Backend

- **Node.js** & **Express.js** - Server framework
- **MongoDB** & **Mongoose** - Database
- **Socket.IO** - Real-time WebSocket communication
- **CORS** - Cross-origin resource sharing
- **dotenv** - Environment variable management

### Frontend

- **React 19** - UI library
- **Vite** - Build tool and dev server
- **Tailwind CSS** - Styling
- **Clerk** - Authentication
- **Socket.IO Client** - Real-time communication
- **Axios** - HTTP requests

### DevOps

- **GitHub Actions** - CI/CD pipeline
- **Render** - Backend hosting
- **Vercel** - Frontend hosting
- **MongoDB Atlas** - Database hosting

## 📋 Prerequisites

- Node.js (v18 or higher)
- npm or yarn
- MongoDB Atlas account
- Clerk account for authentication
- GitHub account
- Render/Railway account (for backend)
- Vercel/Netlify account (for frontend)

## 🔧 Local Development Setup

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd deployment-and-devops-essentials-Bochaberii/Week5-Chat
```

### 2. Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create .env file (copy from .env.example)
cp .env.example .env

# Edit .env with your credentials
# MONGODB_URI=your_mongodb_connection_string
# PORT=5000
# ALLOWED_ORIGINS=http://localhost:5173
# CLERK_SECRET_KEY=your_clerk_secret_key

# Start development server
npm run dev
```

The backend will run on `http://localhost:5000`

### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Create .env file (copy from .env.example)
cp .env.example .env

# Edit .env with your credentials
# VITE_API_URL=http://localhost:5000
# VITE_SOCKET_URL=http://localhost:5000
# VITE_CLERK_PUBLISHABLE_KEY=your_clerk_publishable_key

# Start development server
npm run dev
```

The frontend will run on `http://localhost:5173`

## 🚀 Deployment Instructions

### Step 1: MongoDB Atlas Setup

1. Create a free cluster on [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a database user with read/write permissions
3. Whitelist all IP addresses (0.0.0.0/0) for production access
4. Get your connection string
5. Replace `<password>` in the connection string with your database user password

### Step 2: Deploy Backend to Render

1. Go to [Render Dashboard](https://dashboard.render.com/)
2. Click "New +" → "Web Service"
3. Connect your GitHub repository
4. Configure the service:
   - **Name:** Your backend name
   - **Region:** Choose closest to your users
   - **Branch:** main
   - **Root Directory:** `Week5-Chat/backend`
   - **Runtime:** Node
   - **Build Command:** `npm install`
   - **Start Command:** `npm start`
5. Add environment variables:
   - `MONGODB_URI` - Your MongoDB Atlas connection string
   - `NODE_ENV` - `production`
   - `ALLOWED_ORIGINS` - Your frontend URL (will add after frontend deployment)
   - `CLERK_SECRET_KEY` - Your Clerk secret key
6. Click "Create Web Service"
7. Wait for deployment to complete
8. Copy the deployed URL (e.g., `https://your-app.onrender.com`)

### Step 3: Deploy Frontend to Vercel

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Click "Add New" → "Project"
3. Import your GitHub repository
4. Configure the project:
   - **Framework Preset:** Vite
   - **Root Directory:** `Week5-Chat/frontend`
   - **Build Command:** `npm run build`
   - **Output Directory:** `dist`
5. Add environment variables:
   - `VITE_API_URL` - Your Render backend URL
   - `VITE_SOCKET_URL` - Your Render backend URL
   - `VITE_CLERK_PUBLISHABLE_KEY` - Your Clerk publishable key
6. Click "Deploy"
7. Wait for deployment to complete
8. Copy the deployed URL (e.g., `https://your-app.vercel.app`)

### Step 4: Update Backend CORS Settings

1. Go back to Render Dashboard
2. Open your backend service
3. Go to "Environment" tab
4. Update `ALLOWED_ORIGINS` with your Vercel frontend URL
5. Save changes (this will trigger a redeploy)

### Step 5: Configure Clerk

1. Go to [Clerk Dashboard](https://dashboard.clerk.com/)
2. Navigate to your application
3. Under "API Keys", ensure you've copied the correct keys
4. Under "Domains", add your deployed frontend URL
5. Update CORS settings if needed

## 🔄 CI/CD Pipeline

The project uses GitHub Actions for continuous integration and deployment:

- **On Push/PR:** Runs linting and builds for both frontend and backend
- **On Main Branch:** Automatically deploys to production

### GitHub Secrets Required

Add these secrets in your GitHub repository settings:

```
VITE_API_URL
VITE_SOCKET_URL
VITE_CLERK_PUBLISHABLE_KEY
```

### Pipeline Steps

1. **Checkout Code** - Clones the repository
2. **Install Dependencies** - Installs npm packages
3. **Linting** - Runs ESLint checks
4. **Build** - Creates production builds
5. **Deploy** - Triggers deployment (auto via Render/Vercel webhooks)

### Viewing CI/CD in Action

![CI/CD Pipeline Screenshot](./screenshots/github-actions.png)

> Add a screenshot of your GitHub Actions workflow running successfully

## 📊 Monitoring & Maintenance

### Health Checks

The backend includes a health check endpoint:

```bash
GET /healthz
Response: { "status": "ok" }
```

### Monitoring Setup

1. **Uptime Monitoring:**

   - Use [UptimeRobot](https://uptimerobot.com/) or [Pingdom](https://www.pingdom.com/)
   - Monitor: `https://your-api.onrender.com/healthz`
   - Alert on downtime

2. **Error Tracking:**

   - Integrate [Sentry](https://sentry.io/) for error monitoring
   - Track frontend and backend errors

3. **Performance Monitoring:**
   - Use Render's built-in metrics
   - Monitor response times and resource usage

### Maintenance Checklist

- [ ] Weekly dependency updates (`npm audit fix`)
- [ ] Monthly security patches
- [ ] Daily database backup (MongoDB Atlas auto-backup enabled)
- [ ] Monitor application logs in Render dashboard
- [ ] Review error reports in Sentry (if configured)

## 📝 API Documentation

### Base URL

```
Production: https://your-api.onrender.com
Development: http://localhost:5000
```

### Endpoints

#### Health Check

```
GET /healthz
Response: { "status": "ok" }
```

#### Conversations

```
GET    /api/conversations        # Get all conversations
POST   /api/conversations        # Create new conversation
GET    /api/conversations/:id    # Get conversation by ID
DELETE /api/conversations/:id    # Delete conversation
```

#### Messages

```
GET    /api/messages/:conversationId    # Get messages for conversation
POST   /api/messages                    # Send new message
```

#### Users

```
GET    /api/users/:userId        # Get user profile
POST   /api/users                # Create user profile
```

### WebSocket Events

#### Client → Server

- `conversation:join` - Join a conversation room
- `conversation:leave` - Leave a conversation room
- `message:new` - Send a new message

#### Server → Client

- `message:new` - Receive a new message

## 🔐 Environment Variables

### Backend (.env)

```bash
MONGODB_URI=              # MongoDB connection string
PORT=5000                 # Server port
NODE_ENV=production       # Environment
ALLOWED_ORIGINS=          # Comma-separated frontend URLs
CLERK_SECRET_KEY=         # Clerk authentication secret
```

### Frontend (.env)

```bash
VITE_API_URL=             # Backend API URL
VITE_SOCKET_URL=          # Backend WebSocket URL
VITE_CLERK_PUBLISHABLE_KEY=  # Clerk publishable key
```

## 🐛 Troubleshooting

### CORS Issues

- Ensure `ALLOWED_ORIGINS` in backend includes your frontend URL
- Check that credentials are enabled in CORS settings

### WebSocket Connection Failed

- Verify `VITE_SOCKET_URL` matches your backend URL
- Check that backend allows WebSocket connections
- Ensure no firewall blocking WebSocket traffic

### Database Connection Issues

- Verify MongoDB Atlas whitelist includes all IPs (0.0.0.0/0)
- Check connection string format
- Ensure database user has correct permissions

### Deployment Failures

- Check build logs in Render/Vercel dashboard
- Verify all environment variables are set
- Ensure build commands are correct

## 📸 Screenshots

### CI/CD Pipeline

![GitHub Actions Workflow](./screenshots/ci-cd-pipeline.png)

### Monitoring Dashboard

![Monitoring Setup](./screenshots/monitoring.png)

> Add your actual screenshots here

## 👥 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the ISC License.

## 🙏 Acknowledgments

- PLP Academy for the assignment
- MongoDB Atlas for database hosting
- Render for backend hosting
- Vercel for frontend hosting
- Clerk for authentication services

---

**Last Updated:** January 6, 2026

**Status:** ✅ Deployed and Operational

For questions or issues, please open an issue in the repository

## CI/CD Pipeline

The assignment includes templates for setting up GitHub Actions workflows:

- `frontend-ci.yml`: Tests and builds the React application
- `backend-ci.yml`: Tests the Express.js backend
- `frontend-cd.yml`: Deploys the frontend to your chosen platform
- `backend-cd.yml`: Deploys the backend to your chosen platform

## Submission

Your work will be automatically submitted when you push to your GitHub Classroom repository. Make sure to:

1. Complete all deployment tasks
2. Set up CI/CD pipelines with GitHub Actions
3. Deploy both frontend and backend to production
4. Document your deployment process in the README.md
5. Include screenshots of your CI/CD pipeline in action
6. Add URLs to your deployed applications

## Resources

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [MongoDB Atlas Documentation](https://docs.atlas.mongodb.com/)
- [Render Documentation](https://render.com/docs)
- [Railway Documentation](https://docs.railway.app/)
- [Vercel Documentation](https://vercel.com/docs)
- [Netlify Documentation](https://docs.netlify.com/)
