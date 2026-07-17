# Task 02 - Persistent Storage with Database Integration

A REST API built with **Node.js**, **Express**, and **MySQL** using **Sequelize ORM** for persistent data storage. Extends a basic REST API with full database integration, connection pooling, and environment-based configuration.

---

## 🛠 Tech Stack

- **Node.js** + **Express.js** — Server framework
- **MySQL** — Relational database
- **Sequelize ORM** — Database abstraction & migrations
- **dotenv** — Environment variable management
- **express-validator** — Input validation

---

## 📁 Project Structure

```
task02-db-integration/
├── src/
│   ├── app.js                  # Entry point
│   ├── config/
│   │   ├── database.js         # Sequelize connection + pooling
│   │   └── config.js           # Sequelize CLI config (dev/test/prod)
│   ├── models/
│   │   ├── index.js            # Export all models
│   │   └── User.js             # User model with validations
│   ├── controllers/
│   │   └── userController.js   # CRUD logic
│   ├── routes/
│   │   └── userRoutes.js       # API route definitions
│   ├── middlewares/
│   │   ├── validate.js         # express-validator rules
│   │   └── errorHandler.js     # Global error handler
│   └── migrations/
│       └── 20240101000000-create-users.js  # DB migration
├── .env                        # Environment variables (do not commit)
├── .env.example                # Environment variable template
├── .sequelizerc                # Sequelize CLI path config
├── .gitignore
├── package.json
└── README.md
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository
```bash
git clone <your-repo-url>
cd task02-db-integration
```

### 2. Install dependencies
```bash
npm install
```

### 3. Configure environment variables
```bash
cp .env.example .env
```
Edit `.env` with your MySQL credentials:
```env
PORT=3000
NODE_ENV=development
DB_HOST=localhost
DB_PORT=3306
DB_NAME=task02_db
DB_USER=root
DB_PASSWORD=yourpassword
```

### 4. Create the MySQL database
```sql
CREATE DATABASE task02_db;
```

### 5. Run database migrations
```bash
npm run migrate
```

### 6. Start the server
```bash
# Development (with auto-reload)
npm run dev

# Production
npm start
```

---

## 🔌 API Endpoints

Base URL: `http://localhost:3000`

| Method | Endpoint         | Description        |
|--------|------------------|--------------------|
| GET    | `/`              | Health check       |
| GET    | `/api/users`     | Get all users      |
| POST   | `/api/users`     | Create a user      |
| GET    | `/api/users/:id` | Get user by ID     |
| PUT    | `/api/users/:id` | Update a user      |
| DELETE | `/api/users/:id` | Delete a user      |

---

## 📬 Sample Requests

### Create a User
```http
POST /api/users
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "age": 25
}
```

**Response:**
```json
{
  "success": true,
  "message": "User created",
  "data": {
    "id": 1,
    "name": "John Doe",
    "email": "john@example.com",
    "age": 25,
    "createdAt": "2024-01-01T00:00:00.000Z",
    "updatedAt": "2024-01-01T00:00:00.000Z"
  }
}
```

### Get All Users
```http
GET /api/users
```

### Update a User
```http
PUT /api/users/1
Content-Type: application/json

{
  "name": "Jane Doe",
  "age": 28
}
```

### Delete a User
```http
DELETE /api/users/1
```

---

## 🔑 Key Features

- ✅ **Sequelize ORM** with MySQL for persistent storage
- ✅ **Database Migrations** to create and manage the users table schema
- ✅ **Connection Pooling** configured for performance and reliability
- ✅ **Environment-specific configs** via `.env` for dev/test/production
- ✅ **Input validation** using `express-validator`
- ✅ **Global error handling** for clean, consistent error responses
- ✅ **Unique email constraint** with proper duplicate error handling
