# Secret Echo - AI Companion Application

## Overview

Secret Echo is an interactive AI companion application designed to provide users with a personalized, real-time chat experience with specialized AI companions (e.g., Doctor, Chef, Fitness Coach).

The project consists of a **frontend** built with Next.js and a **backend** built with Node.js, seamlessly integrated to deliver a responsive, secure, and engaging user experience.

The application supports session-based authentication with JWT, real-time WebSocket communication, and persistent chat history stored in MongoDB with rate limiting of API by Sliding Window Algorithm by Redis.

It features a dual-theme mode (light/dark), emoji-enhanced chats for better engagement, and a fully responsive design for both desktop and mobile users. The project is deployed on Railway.app with Docker for scalability and ease of deployment.

### Key Highlights

- **Frontend**: A modern Next.js application with a landing page, authentication flows, a dashboard listing 5 AI companions, and a real-time chat interface.
- **Backend**: A Node.js server with TypeScript, handling user authentication, real-time WebSocket communication, Gemini AI Live integration, and MongoDB persistence with rate limiting of APIs.
- **Deployment**: Both frontend and backend are deployed on Railway.app, with Docker support for containerization.
- **Real-Time Communication**: WebSocket connections enable instant messaging between users and AI companions, with chat history saved for continuity.
- **Security**: JWT-based authentication, rate limiting with Redis, and middleware for secure API and WebSocket interactions.

## Documentary Video

To learn more about Secret Echo and see a walkthrough of its features, watch documentary video:

### Watch the Secret Echo Documentary Video

[![alt text](./secretEcho-frontend/docs/screenshots/image.png)](https://www.youtube.com/watch?v=darG_akLhl0)

## Environment Variables

Below are the environment variables required for the frontend and backend. Ensure these are set up in the respective `.env` files or in your deployment platform (e.g., Railway.app).

### Frontend `.env`

Create a `.env` file in the `./secretEcho-frontend` directory with the following variables:

```
APP_NAME={{APP_NAME}}
V1_API_ENDPOINT={{V1_API_ENDPOINT}}
NEXT_PUBLIC_FRONTEND_URL={{NEXT_PUBLIC_FRONTEND_URL}}

SESSION_COOKIE_NAME={{SESSION_COOKIE_NAME}}
SESSION_COOKIE_PASSWORD={{SESSION_COOKIE_PASSWORD}}

NEXT_PUBLIC_WEBSOCKET_URL={{NEXT_PUBLIC_WEBSOCKET_URL}}
```

### Backend `.env`

Create a `.env` file in the `./secretEcho-backend` (backend) directory with the following variables:

```
APP_NAME=secret-echo
APP_ENV=development
APP_PORT=3000

TOKEN_SECRET={{TOKEN_SECRET}}

MONGO_URI={{MONGO_URI}}

GEMINI_API_KEY={{GEMINI_API_KEY}}

REDIS_CLOUD_HOST={{REDIS_CLOUD_HOST}}
REDIS_CLOUD_PORT={{REDIS_CLOUD_PORT}}
REDIS_CLOUD_USERNAME={{REDIS_CLOUD_USERNAME}}
REDIS_CLOUD_PASSWORD={{REDIS_CLOUD_PASSWORD}}
REDIS_CLOUD_TLS={{REDIS_CLOUD_TLS}}

RATE_LIMIT_REQUESTS_PER_MINUTE=45
```

### Notes on Environment Variables

- Replace placeholder values (e.g., `{{TOKEN_SECRET}}`) with actual values.
- Ensure `NEXT_PUBLIC_WEBSOCKET_URL` in the frontend matches the backend’s WebSocket URL (e.g., `ws://localhost:3000` for development).
- The `RATE_LIMIT_REQUESTS_PER_MINUTE` variable in the backend can be adjusted to control API rate limiting.

====================================================================

## Frontend Documentation

### The frontend is deployed on Railway.app :  [SecretEcho - AI Companion](https://secretecho-client-production.up.railway.app/)

### Features

- **Landing Page**: Introduces the application with options to sign up or sign in.
- **Authentication Pages**: A unified auth page with sign-up and sign-in options, using session-based login with JWT, validated through the backend.
- **Middleware**: Validates each API request and response with middleware, featuring a dynamic-routing-callback to return users to their requested URL after login.
- **Proxy API**: Uses a proxy API system to indirectly call backend APIs, avoiding direct exposure of backend endpoints.
- **Dashboard**: Displays 5 AI companions (EchoBuddy, Chef EchoBite, Dr. EchoCare, EchoFit, EchoMind) for user interaction.
- **Chat Interface**: A messaging-like interface where users can select a companion to open a chat page with a chat box and a sidebar companion list.
- **Real-Time Communication**: Establishes real-time WebSocket connections for instant messaging.
- **Chat Persistence**: Chats are saved in MongoDB via the backend, with message context synced for better engagement across sessions.
- **Theme Management**: Supports dual-theme mode (light/dark) using `next-themes`, with a toggle in the navbar.
- **User Management**: A menubar in the navbar displays user details (avatar, full name, email) and a logout option, with the dropdown centered on desktop.
- **Mobile Menu**: A hamburger menu on mobile screens provides access to user details, logout, and theme toggle.
- **AI Simulation**: Simulated AI responses for better engagement and a realistic chat experience.
- **Emoji Support**: AI companions use emojis to enhance chat engagement (e.g., 😊, 💪, 👩‍🍳).
- **Responsive Design**: Fully responsive layout for desktop and mobile devices.
- **Deployed on Railway.app**: Deployed with a Dockerfile for containerization.

## Detailed Documentation of [SecretEcho - Frontend](./secretEcho-frontend/README.md)

====================================================================

## Backend Documentation

### The backend is deployed on Railway.app : [Secret Echo Backend](https://server-secret-echo-production.up.railway.app/)

### Features

- **User Authentication**:
  - Sign-up and sign-in with email, encrypted password, first name, and last name.
  - Session-based authentication using JWT tokens for secure API access.
  - User details and sessions are stored in MongoDB.
- **Real-Time Communication**:
  - Two WebSocket setups:
    - `/gemini-live`: For integration with Gemini AI Live to generate AI responses.
  - Chat messages are saved in MongoDB with context (e.g., sender, timestamp).
- **Gemini AI Live Integration**: Streams live AI responses using the Gemini AI Live service (`/gemini-live` route).
- **MongoDB Integration**: Persistent storage for user data, sessions, and chat history.
- **Middleware**: Secures each REST API and WebSocket event on each interaction.
- **Redis Integration**: Implements rate limiting via Redis-Cloud with a sliding window algorithm.
- **WebSocket Authorization**: Secure WebSocket connections with JWT token validation.
- **AI Companion Modes**:
  - Users can create AI companions with predefined modes (e.g., Doctor, Chef).
  - Messages are exchanged in real-time, with responses generated by Gemini AI Live.
- **Session Management**:
  - Each sign-in creates a session, ensuring secure access to APIs using JWT tokens.
  - Logout functionality to invalidate sessions.
- **Chat History**:
  - Users can retrieve their chat history with an AI companion.
- **Jest Testing**: Comprehensive unit tests for all services, with all tests passing successfully.
- **Rate Limiting**: Protects the API from abuse by limiting the number of requests per user, implemented with Redis.
- **Deployment on Railway**: Hosted on Railway with automatic scaling and environment variable management.

## Detailed Documentation of [SecretEcho - Backend](./secretEcho-backend/README.md)

=====================================================================

## Development Notes

### Frontend

- **Forms and Validation**: Formik and Zod ensure robust input validation for sign-up and sign-in forms.
- **Data Fetching**: TanStack Query manages API calls with caching for performance.
- **Real-Time Chats**: WebSocket connections are established for each companion chat.
- **Theming**: `next-themes` enables seamless light/dark mode switching.
- **Animations**: Framer Motion adds smooth transitions.
- **Responsive Design**: The navbar includes a mobile menu for accessibility on smaller screens.

### Backend

- **Security**: Middleware ensures secure API and WebSocket interactions.
- **Testing**: Jest unit tests cover all services, ensuring reliability.
- **Rate Limiting**: Redis-based rate limiting protects the API from abuse.
- **Logging**: Custom logging with `oplog` for debugging and monitoring.

## Challenges

### Limitations

- **Gemini AI Live Session Limits**: The current setup with Gemini AI Live allows only 5 concurrent sessions at a time. This limitation can cause a fallback for many users during peak usage, leading to potential delays or unavailability of AI responses for some users.
- **Predefined Companions Only**: Users are restricted to interacting with the 5 predefined AI companions (EchoBuddy, Chef EchoBite, Dr. EchoCare, EchoFit, EchoMind). There is no option for users to create or customize their own companions, which limits personalization.

### Things We Can Do Further

- **Scalable AI Service**: Build a custom AI service or integrate with a more scalable AI provider that can handle a large number of concurrent users, eliminating the session limitation imposed by Gemini AI Live.
- **Custom Companion Creation**: Introduce a feature where users can create personalized AI companions by defining their own system prompts, companion codes, and dedicated spaces. This would enhance user engagement by allowing tailored interactions.
- **Premium Features**: Implement a premium subscription model that offers additional benefits, such as access to more companions, priority AI session slots, custom companion creation, and enhanced chat features (e.g., voice chat, advanced emoji sets).

### Challenges Faced During Building

- **WebSocket Integration**: Setting up real-time WebSocket communication was challenging, particularly ensuring secure JWT-based authorization for WebSocket connections. We faced issues with maintaining persistent connections on Railway.app due to their 30-second timeout on `*.up.railway.app` domains, requiring us to recommend custom domains for production.
- **Rate Limiting with Redis**: Implementing the sliding window algorithm for rate limiting using Redis-Cloud was complex. Configuring Redis with proper TLS settings and ensuring it worked seamlessly with the Express middleware required significant debugging and testing.
- **Gemini AI Live Integration**: Integrating Gemini AI Live for real-time AI responses posed challenges due to its session limits and occasional latency. We had to implement fallback mechanisms and error handling to manage scenarios where the session limit was reached.
- **Responsive Design**: Ensuring a fully responsive design across devices was challenging, especially with the chat interface’s sidebar and mobile menu. We had to carefully design the layout using Tailwind CSS and test extensively to ensure usability on smaller screens.
- **Chat Persistence and Context Syncing**: Synchronizing chat context across sessions while maintaining performance was difficult. Storing and retrieving chat history from MongoDB in real-time required optimization to avoid latency, especially during high user activity.

## License

This project is licensed under the MIT License for the frontend and the ISC License for the backend. See the respective `LICENSE` files in the `frontend/` and `secret-echo/` directories for details.

## Contact

For questions or support, reach out to [Rishabh Maurya](mailto:rishabhmaurya7654@gmail.com).
