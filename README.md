# CPU Management Application - Full Stack Web App

---

## Description

This project is a **full-stack CPU management web application** designed to help users organize, track, and manage computer processor specifications and their socket compatibility.

The application combines a **React frontend, Spring Boot REST API backend, and MySQL database** into a unified platform for CRUD operations on CPU data with real-time updates and engaging user interactions.

Features include **CPU creation, editing, deletion, socket management, price tracking, Docker containerization, and animated success feedback** to provide a modern, responsive user experience.

Developed as a practical demonstration of full-stack web development, this project showcases proficiency in both frontend and backend technologies, database design, API architecture, and DevOps practices.

<br/>

**Technical Skills & Knowledge Gained:**

- Mastery of **React hooks** (useState, useEffect) and component lifecycle management for dynamic UI rendering
- Understanding of **RESTful API design** principles with proper HTTP methods (GET, POST, PUT, DELETE)
- Practical experience with **Spring Boot framework**, dependency injection, and ORM with JPA/Hibernate
- In-depth knowledge of **relational database design** with MySQL, including entity relationships and data normalization
- Applied skills in **Docker containerization** for simplified deployment and environment consistency
- Understanding of **Git version control** and collaborative development workflows
- Frontend-backend **API communication** using Fetch API and promise-based async operations
- **Form validation, state management**, and user feedback mechanisms

---

## Goal & Motivation

The primary objective was to create a **practical, full-stack web application** that demonstrates:

1. **Complete CRUD functionality** - Users can Create, Read, Update, and Delete CPU records
2. **Database relationships** - Managing CPUs and their associated sockets with proper foreign keys
3. **API-driven architecture** - Separation of concerns between frontend and backend
4. **User experience** - Intuitive interface with visual feedback and animations
5. **Production-ready code** - Docker support for easy deployment
6. **Professional practices** - Clean code, version control, and documentation

---

## Development Process

### Phase 1: Backend Development (Spring Boot)

**Objectives:** Create a robust REST API with database connectivity

**Implementation:**
1. Set up Spring Boot project with Maven
2. Created two entity classes: `Cpu.java` and `Socket.java`
3. Configured MySQL connection in `application.properties`
4. Built repositories for database abstraction using Spring Data JPA
5. Developed controllers with endpoints:
   - `GET /api/cpus` - Retrieve all CPUs
   - `GET /api/cpus/{id}` - Get single CPU
   - `POST /api/cpus` - Create new CPU
   - `PUT /api/cpus/{id}` - Update CPU
   - `DELETE /api/cpus/{id}` - Delete CPU
   - `GET /api/sockets` - Retrieve all sockets

**Key Files:**
- `Cpu.java` - Entity with @Entity annotation for database mapping
- `Socket.java` - Entity defining socket types
- `CpuRepository.java` - JPA repository with auto-generated CRUD methods
- `CpuController.java` - REST endpoints handling requests
- `CpuAppApplication.java` - Spring Boot entry point

---

### Phase 2: Frontend Development (React)

**Objectives:** Build an interactive user interface for CPU management

**Implementation:**
1. Created React app using Create React App
2. Implemented component state management with hooks:
   - `cpus` - List of all CPUs
   - `sockets` - List of available sockets
   - `editingCpu` - Track current CPU being edited
   - `formData` - Store form input values
3. Built features:
   - Table view displaying CPUs with brand, model, socket, price
   - Form for adding/editing CPUs
   - Socket dropdown populated from backend
   - Edit and Delete buttons with confirmations
   - Form validation (all fields required)

**Key Functions:**
- `handleInputChange()` - Updates form state on user input
- `handleSave()` - Validates and sends data to backend via fetch
- `handleDelete()` - Removes CPU after confirmation
- `fetchCpus()` - Retrieves updated CPU list from API
- `fetchSockets()` - Gets socket list for dropdown

---

### Phase 3: Database Design

**Schema:**
```
Table: socket
├── id (INT, PRIMARY KEY, AUTO_INCREMENT)
└── name (VARCHAR, e.g., "LGA1151", "AM4")

Table: cpu
├── id (INT, PRIMARY KEY, AUTO_INCREMENT)
├── brand (VARCHAR, e.g., "Intel", "AMD")
├── model (VARCHAR, e.g., "i9-13900K")
├── price (DOUBLE, e.g., 589.99)
└── socket_id (INT, FOREIGN KEY → socket.id)
```

---

### Phase 4: Docker & Deployment

**Created:**
1. `Dockerfile` - Containerizes Spring Boot application with Java 17
2. `docker-compose.yml` - Orchestrates MySQL and backend services
3. Environment configuration for container networking

**Benefits:** Easy deployment, consistent environments across machines, no local MySQL installation needed

---

## Code Architecture

### Frontend Flow:
```
User Action (Click Button)
    ↓
Event Handler (handleEdit, handleAdd, handleSave)
    ↓
State Update (setFormData, setEditingCpu)
    ↓
React Re-renders Component
    ↓
API Call (fetch to /api/cpus)
    ↓
Backend Response
    ↓
Update cpus state (setCpus)
    ↓
UI Updates with new data
```

### Backend Flow:
```
HTTP Request from Frontend
    ↓
Controller (CpuController.java)
    ↓
Repository (CpuRepository.java)
    ↓
Database Query (MySQL)
    ↓
Data conversion (Object ↔ JSON)
    ↓
HTTP Response to Frontend
```

---

## End Result

### Deliverables:

✅ **Fully functional full-stack application** with real-time CRUD operations

✅ **Professional Git repository** with clean commit history: https://github.com/marriammahmed/CPU_APP

✅ **Docker containerization** enabling one-command deployment

✅ **Responsive UI** with intuitive navigation and visual feedback

✅ **Price field integration** for tracking CPU costs

✅ **Complete documentation** and setup instructions

### Features Implemented:

- ✅ Display CPU list in table format
- ✅ Add new CPUs via form
- ✅ Edit existing CPU information
- ✅ Delete CPUs with confirmation
- ✅ Socket management and dropdown selection
- ✅ Price tracking per CPU
- ✅ Form validation
- ✅ Success animations with confetti effect
- ✅ Responsive design
- ✅ Docker support
- ✅ README documentation

---

## Challenges & Solutions

### Challenge 1: Frontend-Backend Communication

**Problem:** CORS (Cross-Origin Resource Sharing) errors preventing frontend from calling backend API

**Solution:** Added `@CrossOrigin(origins = "http://localhost:3000")` annotation to controllers, allowing frontend to communicate with backend

---

### Challenge 2: Form State Management

**Problem:** Multiple form fields requiring state updates caused React re-renders on every keystroke

**Solution:** Used single `formData` state object with dynamic key updates: `setFormData({...formData, [name]: value})`

---

### Challenge 3: Socket Dropdown Population

**Problem:** Frontend needed socket list but fetching on every render caused infinite loops

**Solution:** Implemented `fetchSockets()` called only when edit/add button clicked, not on every render

---

### Challenge 4: Database Initialization

**Problem:** Database didn't exist when backend started

**Solution:** Configured `spring.jpa.hibernate.ddl-auto=update` to automatically create tables on startup

---

### Challenge 5: Git Authentication

**Problem:** Multiple Git accounts on same machine causing authentication failures

**Solution:** Used personal access tokens instead of passwords for GitHub authentication
```bash
git remote add origin https://marriammahmed:TOKEN@github.com/marriammahmed/CPU_APP.git
```

---

### Challenge 6: Node Modules Corruption

**Problem:** npm install failed with missing module errors

**Solution:** Cleared cache and reinstalled dependencies:
```bash
rm -rf node_modules package-lock.json
npm install
```

---

### Challenge 7: Docker Image Build

**Problem:** Base image `openjdk:17-jdk-slim` not found on new machine

**Solution:** Changed to alternative image `amazoncorretto:17` available on all platforms
```dockerfile
FROM amazoncorretto:17
```

---

## Technology Stack

### Frontend:
- **React** - UI library for dynamic components
- **JavaScript (ES6+)** - Modern JavaScript with arrow functions, destructuring, hooks
- **Fetch API** - For HTTP requests to backend
- **CSS** - Styling with inline styles and CSS animations

### Backend:
- **Spring Boot 4.0.0** - Java framework for REST APIs
- **Spring Data JPA** - Object-relational mapping (ORM)
- **Hibernate 7.1.8** - Entity management
- **MySQL 8.0** - Relational database

### DevOps:
- **Docker** - Containerization
- **Docker Compose** - Multi-container orchestration
- **Git** - Version control

### Build Tools:
- **Maven** - Java dependency management
- **npm** - Node.js package manager

---

## Installation & Setup

### Prerequisites:
- Java 17+
- Node.js & npm
- MySQL
- Docker (optional)
- Git

### Backend Setup:
```bash
cd backend
./mvnw clean package
./mvnw spring-boot:run
```

### Frontend Setup:
```bash
cd frontend
npm install
npm start
```

### Docker Setup:
```bash
cd backend
docker-compose up
```

---

## Application Walkthrough

### 1. Home Screen - CPU List

Shows all CPUs in table format with brand, model, socket, and price information. Users can edit or delete any CPU.

[Insert Screenshot Here]

---

### 2. Add CPU Form

Clean, minimal form to add new CPUs. Includes brand input, model input, price input, and socket dropdown.

[Insert Screenshot Here]

---

### 3. Edit CPU Form

Pre-populated form with current CPU data. Users can modify any field and save changes.

[Insert Screenshot Here]

---

### 4. Success Animation

Celebratory confetti animation with success message appears after saving or deleting CPUs.

[Insert Screenshot Here]

---

### 5. Socket Dropdown

Dynamic dropdown populated from database showing available sockets for CPU compatibility.

[Insert Screenshot Here]

---

## Key Learnings

1. **Full-stack architecture** - Understanding how frontend and backend communicate via APIs
2. **State management** - React hooks for managing component state efficiently
3. **API design** - RESTful principles and proper HTTP method usage
4. **Database relationships** - Foreign keys and entity relationships (One-to-Many)
5. **Async programming** - Promise chains with .then() and async/await concepts
6. **Git workflow** - Branching, committing, and pushing code to repositories
7. **Docker deployment** - Containerizing applications for consistency
8. **Error handling** - User feedback and validation for robust applications

---

## Future Improvements

- Add authentication and user accounts
- Implement CPU search and filtering
- Create detailed CPU specifications page
- Add CPU comparison feature
- Mobile responsiveness improvements
- Unit and integration testing
- Performance optimization with pagination
- Dark mode toggle
- Export CPU data to CSV/Excel

---

## Repository

**GitHub:** https://github.com/marriammahmed/CPU_APP

**Structure:**
```
CPU_APP/
├── backend/          (Spring Boot API)
│   ├── src/
│   ├── pom.xml
│   ├── Dockerfile
│   └── docker-compose.yml
├── frontend/         (React App)
│   ├── src/
│   ├── package.json
│   └── public/
└── README.md
```

---

## How to Run
```bash
# Clone repository
git clone https://github.com/marriammahmed/CPU_APP.git
cd CPU_APP

# Option 1: Docker (Recommended)
cd backend
docker-compose up

# Option 2: Manual Setup
# Terminal 1 - Backend
cd backend
./mvnw spring-boot:run

# Terminal 2 - Frontend
cd frontend
npm install
npm start
```

Open http://localhost:3000 in browser.

---

## Contact & Credits

**Developer:** Mariam Ahmed

**Course:** Full-Stack Web Development

**Date Completed:** November 28, 2025

---

**Thank you for reviewing this project! 🚀**
