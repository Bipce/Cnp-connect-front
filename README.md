# 🚉 CNP Connect — Frontend

![React](https://img.shields.io/badge/React-19-blue?logo=react)
![TypeScript](https://img.shields.io/badge/TypeScript-typed-blue?logo=typescript)
![Vite](https://img.shields.io/badge/Vite-7-purple?logo=vite)
![Tailwind CSS](https://img.shields.io/badge/TailwindCSS-4-38BDF8?logo=tailwindcss)
![React Query](https://img.shields.io/badge/React_Query-data_fetching-FF4154?logo=reactquery)
![Zustand](https://img.shields.io/badge/Zustand-state_management-orange)

🔗 **Backend repository:** [Cnp-connect-back](https://github.com/Bipce/Cnp-connect-back)

## 📖 Overview

CNP Connect is the frontend application of a rail operations platform used to manage
users, alerts, trains and lines.

Authenticated users — drivers, coordinators and supervisors — can sign in, browse and
manage user accounts, view their train and line assignments, and raise prioritized
alerts. Access to features is controlled by role-based permissions.

This project was developed collaboratively, with a focus on a typed React architecture,
clear separation between data fetching and UI, and a secure authentication flow.

---

## 🧰 Tech Stack

- React 19 + TypeScript + Vite
- TanStack React Query (server state, caching, persistence)
- Zustand (client state management)
- React Hook Form + Zod (forms and validation)
- Axios (API calls, JWT handling)
- React Router (navigation)
- Tailwind CSS (styling)
- Heroicons (icons)
- Cypress (end-to-end testing)

---

## 🚀 Quick Start

Install dependencies:

```bash
npm install
```

Run the development server:

```bash
npm run dev
```

Other available scripts:

```bash
npm run build     # Type-check and build for production
npm run preview   # Preview the production build
npm run lint      # Run ESLint
npm run cy:open   # Open the Cypress test runner
```

---

## 🔐 Environment Variables

Create a `.env` file at the root of the project:

```bash
VITE_API_BASE_URL=https://your-backend-url/api
```

- `VITE_API_BASE_URL` – Base URL of the backend API.

---

## ✨ Features

- Authentication (sign in / sign out)
- Forgot password and password reset flows
- Automatic token refresh on expired sessions
- Role-based access control (Supervisor, Coordinator, Driver)
- User management (list, details, creation)
- Train and line assignments per user
- Alert creation with priority levels (Soft, Medium, Urgent)
- Custom error pages (404 / 500)

---

## 🏗️ Project Structure

The project is structured to keep API logic, state, UI and data models clearly separated.

```text
src/
│
├── api/          # API calls (auth, user, alert, train, line)
├── components/   # Reusable UI components (ui, header, user, alert)
├── guards/       # Route guards (protected & supervisor-only routes)
├── hooks/        # Custom hooks wrapping React Query services
├── layouts/      # Connected and disconnected layouts
├── pages/        # Application views (auth, user, alert, error)
├── types/        # Enums, form schemas (Zod) and TypeScript interfaces
├── utils/        # Axios client, query client, route links
│
├── App.tsx       # Routes definition
├── main.tsx      # Application entry point
└── index.css     # Global styles
```

### Structure Overview

- **api/** – Functions that talk to the backend through the shared Axios client.
- **components/** – Reusable UI building blocks.
- **guards/** – Route protection and role-based access enforcement.
- **hooks/** – React Query hooks exposing services to the components.
- **layouts/** – Wrappers for authenticated and unauthenticated views.
- **pages/** – Main application screens.
- **types/** – Enums, Zod validation schemas and shared interfaces.
- **utils/** – Axios instance, React Query client and navigation links.

---

## 🔑 Authentication & Authorization

Authentication is handled with JWT access tokens and an automatic refresh mechanism.

- The access token is stored client-side and attached to every request via an Axios
  request interceptor.
- A response interceptor detects expired sessions and silently refreshes the token
  before retrying the original request.
- Routes are protected with guards: `ProtectedRoute` requires an authenticated user,
  while `SupervisorRoute` restricts access to supervisor-only features.

Roles available: **Supervisor**, **Coordinator** and **Driver**.

---

## 📊 Data Flow

The application keeps server state and UI concerns cleanly separated:

```text
Component
   ↓
Hook (React Query)
   ↓
API service (Axios)
   ↓
Backend
```

React Query manages caching, background updates and persistence, keeping components
focused on rendering.

---

## 🧪 Testing

End-to-end tests are written with Cypress and cover key flows such as sign in and
user creation.

```bash
npm run cy:open
```

---

## 📦 Deployment

The application ships with a multi-stage Docker build:

- The frontend is built with Node and served as static files through Nginx.
- The backend URL is injected at build time via the `VITE_API_BASE_URL` build argument.

```bash
docker build --build-arg VITE_API_BASE_URL=https://your-backend-url/api -t cnp-connect-front .
```

---

## 🤝 Collaboration

This project was developed collaboratively by **Claire Royer**, **Peter François** and
**Nicolas Palay**, with regular code reviews and technical discussions throughout the
development.
