# PrimeTrade.ai - Scalable Web App with Authentication & Dashboard

A full-stack web application built with React.js frontend and Express.js backend, featuring JWT authentication, MongoDB database, and a task management dashboard.

## Features

### ✅ Frontend (React.js + TypeScript + TailwindCSS)
- Responsive design with TailwindCSS
- User registration and login forms with validation
- Protected routes for authenticated users
- Dashboard with task CRUD operations
- Search and filter functionality
- User profile management
- Logout functionality

### ✅ Backend (Node.js + Express)
- RESTful API with JWT authentication
- User registration/login/logout endpoints
- Protected routes with middleware
- Task CRUD operations (Create, Read, Update, Delete)
- Search and filter tasks
- Password hashing with bcrypt
- MongoDB integration with Mongoose

### ✅ Security & Scalability
- JWT-based authentication
- Password hashing
- Server-side validation
- CORS enabled
- Environment variable configuration
- Modular code structure for easy scaling

## Tech Stack

### Frontend
- React.js 19.2.3
- TypeScript
- TailwindCSS 4.1.18
- Axios for API calls
- React Router DOM for routing

### Backend
- Node.js
- Express.js 4.18.2
- MongoDB with Mongoose 7.5.3
- JWT for authentication
- bcryptjs for password hashing
- CORS for cross-origin requests

## Getting Started

### Prerequisites
- Node.js (v16 or higher)
- MongoDB (local or cloud instance)
- npm or yarn

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd primetrade.ai
   ```

2. **Backend Setup**
   ```bash
   cd backend
   npm install
   ```

   Create a `.env` file in the backend directory:
   ```
   MONGO_URI=mongodb://localhost:27017/primetrade
   JWT_SECRET=your_jwt_secret_key_here
   PORT=5000
   ```

   Start the backend server:
   ```bash
   npm run dev
   ```

3. **Frontend Setup**
   ```bash
   cd frontend
   npm install
   ```

   Create a `.env` file in the frontend directory:
   ```
   REACT_APP_API_URL=http://localhost:5000/api
   ```

   Start the frontend development server:
   ```bash
   npm start
   ```

4. **Access the Application**
   - Frontend: http://localhost:3000
   - Backend API: http://localhost:5000

## API Documentation

### Authentication Endpoints

#### Register User
- **POST** `/api/auth/register`
- **Body**: `{ "name": "string", "email": "string", "password": "string" }`
- **Response**: `{ "token": "jwt_token", "user": { "id": "string", "name": "string", "email": "string" } }`

#### Login User
- **POST** `/api/auth/login`
- **Body**: `{ "email": "string", "password": "string" }`
- **Response**: `{ "token": "jwt_token", "user": { "id": "string", "name": "string", "email": "string" } }`

#### Logout User
- **POST** `/api/auth/logout`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: `{ "message": "Logged out successfully" }`

### Profile Endpoints

#### Get User Profile
- **GET** `/api/profile`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: `{ "id": "string", "name": "string", "email": "string" }`

#### Update User Profile
- **PUT** `/api/profile`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: `{ "name": "string", "email": "string" }`
- **Response**: `{ "id": "string", "name": "string", "email": "string" }`

### Task Endpoints

#### Get All Tasks
- **GET** `/api/tasks?search=query&status=pending|completed`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: `[ { "id": "string", "title": "string", "description": "string", "status": "string", "userId": "string", "createdAt": "date" } ]`

#### Create Task
- **POST** `/api/tasks`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: `{ "title": "string", "description": "string", "status": "pending" }`
- **Response**: `{ "id": "string", "title": "string", "description": "string", "status": "string", "userId": "string", "createdAt": "date" }`

#### Update Task
- **PUT** `/api/tasks/:id`
- **Headers**: `Authorization: Bearer <token>`
- **Body**: `{ "title": "string", "description": "string", "status": "completed" }`
- **Response**: `{ "id": "string", "title": "string", "description": "string", "status": "string", "userId": "string", "createdAt": "date" }`

#### Delete Task
- **DELETE** `/api/tasks/:id`
- **Headers**: `Authorization: Bearer <token>`
- **Response**: `{ "message": "Task deleted successfully" }`

## Scalability Considerations

### Frontend Scaling
- **Component Modularization**: Components are designed to be reusable and modular, allowing easy addition of new features.
- **State Management**: Using React Context for global state management, which can be upgraded to Redux or Zustand for larger applications.
- **Code Splitting**: Implement lazy loading for routes and components to reduce initial bundle size.
- **API Layer**: Centralized API calls with Axios interceptors for error handling and token management.

### Backend Scaling
- **Middleware Architecture**: JWT authentication middleware can be extended for role-based access control.
- **Database Optimization**: MongoDB indexes on frequently queried fields (userId, status) for better performance.
- **API Versioning**: Routes are structured to easily add versioning (e.g., `/api/v1/tasks`).
- **Error Handling**: Centralized error handling middleware for consistent API responses.
- **Validation**: Server-side validation with potential upgrade to libraries like Joi for complex schemas.

### Infrastructure Scaling
- **Database**: MongoDB can be scaled with sharding and replica sets.
- **Caching**: Implement Redis for session storage and API response caching.
- **Load Balancing**: Deploy multiple instances behind a load balancer.
- **Microservices**: Backend can be split into microservices (auth, tasks, users) for better scalability.

## Project Structure

```
primetrade.ai/
├── backend/
│   ├── middleware/
│   │   └── auth.js
│   ├── models/
│   │   ├── User.js
│   │   └── Task.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── profile.js
│   │   └── tasks.js
│   ├── server.js
│   ├── package.json
│   └── .env
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   ├── context/
│   │   ├── pages/
│   │   └── App.tsx
│   ├── package.json
│   └── .env
├── README.md
└── TODO.md
```

## Testing

### Manual Testing Checklist
- [ ] User registration with valid/invalid data
- [ ] User login with correct/incorrect credentials
- [ ] Protected route access without authentication
- [ ] Task CRUD operations (Create, Read, Update, Delete)
- [ ] Search and filter functionality
- [ ] Profile update
- [ ] Logout functionality
- [ ] Responsive design on different screen sizes

### API Testing with Postman
Import the following collection for testing:

```json
{
  "info": {
    "name": "PrimeTrade.ai API",
    "schema": "https://schema.getpostman.com/json/collection/v2.1.0/collection.json"
  },
  "item": [
    {
      "name": "Auth",
      "item": [
        {
          "name": "Register",
          "request": {
            "method": "POST",
            "header": [
              {
                "key": "Content-Type",
                "value": "application/json"
              }
            ],
            "body": {
              "mode": "raw",
              "raw": "{\"name\":\"Test User\",\"email\":\"test@example.com\",\"password\":\"password123\"}"
            },
            "url": {
              "raw": "{{base_url}}/auth/register",
              "host": [
                "{{base_url}}"
              ],
              "path": [
                "auth",
                "register"
              ]
            }
          }
        }
      ]
    }
  ],
  "variable": [
    {
      "key": "base_url",
      "value": "http://localhost:5000/api"
    }
  ]
}
```

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Built for PrimeTrade.ai Frontend Developer Intern assignment
- Demonstrates modern full-stack development practices
- Focus on security, scalability, and user experience
