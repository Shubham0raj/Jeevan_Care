# JeevanCare

JeevanCare is a full-stack healthcare appointment and clinic queue management web application. It connects patients, doctors, and administrators through a single platform for discovering doctors, booking appointments, generating walk-in tokens, and managing clinic operations.

## 🌐 Live Demo

**Visit JeevanCare:** [Click Here](jeevan-care-theta.vercel.app)


## Core Features

### Patient
- Register and verify an account through an email OTP.
- Log in and recover a forgotten password.
- Browse and search the available doctors.
- View doctor profiles, clinic information, consultation fees, and availability.
- Check available appointment slots and book appointments.
- Choose online payment or payment at the clinic.
- Generate a walk-in queue token.
- View appointments and track token status, patients ahead, and estimated waiting time.
- Receive notifications and cancel eligible appointments.

### Doctor
- Access a role-protected doctor dashboard.
- Manage doctor profile information and clinic schedule.
- View and manage appointments.
- Manage the live patient queue and token status.
- Receive appointment and queue notifications.
- Mark clinic payments as paid.

### Administrator
- Access a protected administration dashboard.
- Manage doctor records and review doctor verification status.
- View and manage patient records.
- View and manage appointments.

### Platform
- Role-based access for patients, doctors, and administrators.
- JWT-based authentication.
- Real-time queue updates using Socket.IO.
- Email OTP verification and password-reset support.
- Online payment integration with Razorpay.
- Image upload and storage integration with Cloudinary.
- Request validation using Zod and API rate limiting for authentication endpoints.

## Technology Stack

| Area | Technologies |
|---|---|
| Frontend | React 19, Vite, React Router |
| UI | Material UI, Tailwind CSS |
| Forms and validation | React Hook Form, Zod |
| HTTP client | Axios |
| Backend | Node.js, Express 5 |
| Database | MongoDB, Mongoose |
| Authentication | JSON Web Tokens, bcryptjs |
| Real-time communication | Socket.IO |
| Payments | Razorpay |
| Image storage | Cloudinary |
| Email | Nodemailer |

## Project Structure

```text
jeevanCare/
├── client/
│   ├── public/
│   └── src/
│       ├── components/       # Shared UI components
│       ├── context/          # Authentication context
│       ├── hooks/            # Reusable React hooks
│       ├── layouts/          # Public and admin layouts
│       ├── pages/            # Patient, doctor and admin pages
│       ├── routes/           # Protected route handling
│       ├── services/         # API and Socket.IO services
│       ├── theme/            # Material UI theme
│       └── validations/      # Frontend validation schemas
│
├── server/
│   ├── config/               # Database and third-party configuration
│   ├── controllers/          # Request handlers
│   ├── middleware/           # Authentication and upload middleware
│   ├── models/               # Mongoose data models
│   ├── routes/               # REST API routes
│   ├── seed/                 # Admin and doctor seed scripts
│   ├── services/             # Business logic
│   ├── sockets/              # Socket.IO setup
│   ├── utils/                # Shared utilities
│   └── validators/           # Backend validation schemas
│
└── README.md
```

## Prerequisites

Install the following before running the project:

- Node.js (a current LTS release is recommended)
- npm
- MongoDB database (local installation or MongoDB Atlas)
- Email account configured for SMTP/app-password access
- Cloudinary account (for image uploads)
- Razorpay account and API keys (for online payments)

## Installation and Setup

### 1. Clone the repository

```bash
git clone <REPOSITORY_URL>
cd jeevanCare
```

### 2. Install backend dependencies

```bash
cd server
npm install
```

### 3. Configure backend environment variables

Create a `.env` file inside the `server` directory. Use `.env.example` as the reference:

```env
PORT=5000
CLIENT_URL=http://localhost:5173

MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_secure_jwt_secret

EMAIL_USER=your_email_address
EMAIL_APP_PASSWORD=your_email_app_password

CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
CLOUDINARY_API_KEY=your_cloudinary_api_key
CLOUDINARY_API_SECRET=your_cloudinary_api_secret

RAZORPAY_KEY_ID=your_razorpay_key_id
RAZORPAY_KEY_SECRET=your_razorpay_key_secret
RAZORPAY_WEBHOOK_SECRET=your_razorpay_webhook_secret

NODE_ENV=development
```

Replace the placeholder values with your own credentials. Do not commit `.env` files or expose API secrets.

### 4. Install frontend dependencies

Open another terminal:

```bash
cd client
npm install
```

The frontend API service uses `http://localhost:5000/api` by default. To use a different backend URL, create `client/.env` and set:

```env
VITE_API_URL=http://localhost:5000/api
```

### 5. Start the backend

From the `server` directory:

```bash
npm run dev
```

The API server runs on `http://localhost:5000` by default. Check its health endpoint at:

```text
http://localhost:5000/api/health
```

### 6. Start the frontend

From the `client` directory:

```bash
npm run dev
```

Vite will display the local frontend URL in the terminal (normally `http://localhost:5173`).

## Useful Scripts

### Backend (`server/`)

| Command | Description |
|---|---|
| `npm run dev` | Start the backend with Nodemon |
| `npm start` | Start the backend with Node |
| `npm run seed:doctors` | Run the doctor seed script |
| `npm run create:admin` | Run the admin creation script |

### Frontend (`client/`)

| Command | Description |
|---|---|
| `npm run dev` | Start the Vite development server |
| `npm run build` | Create a production frontend build |
| `npm run preview` | Preview the production build |
| `npm run lint` | Run ESLint |

## API Overview

The backend exposes the following API route groups under `/api`:

| Route | Purpose |
|---|---|
| `/api/health` | Server health check |
| `/api/auth` | Registration, login, email verification and password recovery |
| `/api/doctors` | Doctor discovery and doctor-related operations |
| `/api/appointments` | Appointment slots, booking and appointment management |
| `/api/queues` | Walk-in tokens and queue management |
| `/api/admin` | Administrator operations |
| `/api/upload` | Image upload operations |
| `/api/notifications` | User notifications |
| `/api/payments` | Payment orders, verification and payment status |

Protected endpoints require a valid JWT access token. The frontend API client automatically attaches the token stored in local storage to requests.

## Important Notes

- A newly registered email is verified through OTP before the user account is created.
- Doctor accounts begin with a pending verification status; only verified doctors are available for booking.
- Appointment booking creates a corresponding queue entry so the patient can track their place in the clinic queue.
- Walk-in token generation checks the doctor's working schedule and daily patient limit.
- Razorpay online payments require valid Razorpay credentials. Clinic payment can be marked as paid by the relevant doctor.
- For production deployment, configure the correct frontend origin, environment variables, Razorpay webhook URL, and secure database credentials.
- This application is a software project and does not replace professional medical advice, diagnosis, or emergency services.

## Contributing

1. Fork the repository.
2. Create a feature branch: `git checkout -b feature/your-feature`.
3. Commit your changes with a clear message.
4. Push the branch and open a pull request.

## License

No license is currently specified for this repository. Add a `LICENSE` file before distributing or reusing the project under an open-source license.
