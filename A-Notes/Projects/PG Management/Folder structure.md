
# 🏗️ Overall Project Structure
pg-management-system/
│
├── client/        # React Frontend
├── server/        # Node + Express Backend
├── database/      # SQL scripts / schema
├── docs/          # API docs / project notes
├── .env
├── package.json

# ⚛️ FRONTEND (React)

client/
│
├── public/
│
├── src/
│   ├── assets/          # images, icons
│   ├── components/      # reusable UI components
│   │   ├── Button.jsx
│   │   ├── Navbar.jsx
│   │   ├── Sidebar.jsx
│   │   └── Modal.jsx
│   │
│   ├── pages/           # main pages (route-based)
│   │   ├── Admin/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── Rooms.jsx
│   │   │   ├── Tenants.jsx
│   │   │   ├── Bills.jsx
│   │   │   └── Complaints.jsx
│   │   │
│   │   ├── Tenant/
│   │   │   ├── Dashboard.jsx
│   │   │   ├── RentStatus.jsx
│   │   │   ├── Complaints.jsx
│   │   │   └── Profile.jsx
│   │   │
│   │   ├── Login.jsx
│   │   └── Register.jsx
│   │
│   ├── services/        # API calls
│   │   ├── api.js       # axios config
│   │   ├── authService.js
│   │   ├── roomService.js
│   │   ├── tenantService.js
│   │   ├── billService.js
│   │   └── complaintService.js
│   │
│   ├── context/         # global state (Auth etc.)
│   │   └── AuthContext.jsx
│   │
│   ├── hooks/           # custom hooks
│   │   └── useAuth.js
│   │
│   ├── routes/          # route protection
│   │   └── ProtectedRoute.jsx
│   │
│   ├── utils/           # helper functions
│   │   └── formatDate.js
│   │
│   ├── App.jsx
│   └── main.jsx
│
├── package.json

# 🚀 BACKEND (Node + Express)

server/
│
├── config/
│   ├── db.js            # MySQL connection
│   └── env.js
│
├── controllers/         # logic layer
│   ├── authController.js
│   ├── roomController.js
│   ├── tenantController.js
│   ├── billController.js
│   └── complaintController.js
│
├── routes/              # API routes
│   ├── authRoutes.js
│   ├── roomRoutes.js
│   ├── tenantRoutes.js
│   ├── billRoutes.js
│   └── complaintRoutes.js
│
├── models/              # DB queries
│   ├── userModel.js
│   ├── roomModel.js
│   ├── tenantModel.js
│   ├── billModel.js
│   └── complaintModel.js
│
├── middleware/
│   ├── authMiddleware.js    # JWT check
│   ├── roleMiddleware.js    # admin/tenant access
│   └── errorHandler.js
│
├── services/           # business logic (optional but pro-level)
│   ├── authService.js
│   └── rentService.js
│
├── utils/
│   ├── generateToken.js
│   └── logger.js
│
├── validations/
│   ├── authValidation.js
│   └── tenantValidation.js
│
├── app.js              # express app
├── server.js           # entry point
│
├── package.json

# 🗄️ DATABASE (MySQL)
database/
│
├── schema.sql          # create tables
├── seed.sql            # sample data

Data Flow:
```
React UI → API (axios) → Express → Controller → Model → MySQL
```

Do it like this:

1. Build DB schema
    
2. Create APIs (Postman test)
    
3. Add auth (JWT)
    
4. Connect React
    
5. Improve UI