
# Dockerized Laravel Application (Nginx + MySQL)

This project demonstrates the containerization of a **Laravel web application** using **Docker Compose**.  
The goal of this project is to showcase practical DevOps skills such as **service orchestration, container networking, environment configuration, and persistent storage**.

---

## 🧰 Technology Stack

- **Laravel** – PHP web application framework  
- **Nginx** – Web server  
- **PHP-FPM** – PHP process manager  
- **MySQL** – Relational database  
- **Docker & Docker Compose** – Containerization and orchestration  

---

## 🗂 Project Structure

```

laravel-docker/
│
├── docker/
│   ├── nginx/
│   │   └── default.conf        # Nginx configuration
│   └── php/
│       └── Dockerfile          # PHP-FPM + Composer image
│
├── src/                        # Laravel application source code
│
├── docker-compose.yml          # Multi-container orchestration
├── .gitignore
└── README.md

````

---

## ⚙️ Prerequisites

Ensure the following are installed on your system:

- Docker
- Docker Compose
- Git

Verify installation:

```bash
docker --version
docker compose version
````

---

## 🚀 Setup and Execution

### Step 1: Clone the Repository

```bash
git clone <repository-url>
cd laravel-docker
```

---

### Step 2: Configure Environment Variables

Laravel environment variables are not committed for security reasons.

Create the environment file:

```bash
cp src/.env.example src/.env
```

Update database configuration in `src/.env`:

```env
DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel
DB_USERNAME=laravel
DB_PASSWORD=laravel
```

---

### Step 3: Start Docker Containers

```bash
docker compose up -d
```

---

### Step 4: Install Laravel Application

```bash
docker compose exec app composer create-project laravel/laravel .
```

---

### Step 5: Set Required Permissions

```bash
docker compose exec app chmod -R 775 storage bootstrap/cache
```

---

### Step 6: Generate Application Key

```bash
docker compose exec app php artisan key:generate
```

---

## Access the Application

Open your browser and navigate to:

```
http://localhost:8080
```

You should see the **Laravel Welcome Page**, confirming the setup is successful.

---

## 🗄 Database Connectivity Test

Run database migrations:

```bash
docker compose exec app php artisan migrate
```

Successful execution confirms MySQL connectivity.

---

## 🧠 Architecture Explanation

1. Client sends request to **Nginx**
2. Nginx serves static content and forwards PHP requests to **PHP-FPM**
3. PHP-FPM executes Laravel application code
4. Laravel connects to **MySQL** using Docker service networking
5. Data is persisted using Docker volumes

---

