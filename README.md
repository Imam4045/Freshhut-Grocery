<div align="center">
  <img src="screenshots/homepage.png" alt="FreshHut Homepage" width="100%">
</div>

<h1 align="center">🛒 FreshHut — Online Grocery Store</h1>
<p align="center"><i>Farm to Your Door — a full-stack grocery shopping platform built with PHP, MySQL, JavaScript &amp; HTML/CSS</i></p>

<p align="center">
  <img src="https://img.shields.io/badge/PHP-8.2-777BB4?style=flat-square&logo=php&logoColor=white" alt="PHP">
  <img src="https://img.shields.io/badge/MySQL-Aiven-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/Docker-Apache-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Deployed%20on-Render-46E3B7?style=flat-square&logo=render&logoColor=white" alt="Render">
</p>

## Table of Contents

- [Live Demo](#live-demo)
- [Overview](#overview)
- [Features](#features)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Getting Started](#getting-started)
- [Environment Variables](#environment-variables)
- [Demo Accounts](#demo-accounts)
- [Team](#team)
- [Key Features](#key-features)
- [Order Status](#order-status)
- [Application Flow](#application-flow)
- [Authentication and Security](#authentication-and-security)
- [Local Setup](#local-setup)
- [Deployment](#deployment)

<h2 id="live-demo" align="center">Live Demo</h2>

<div align="center">
  <a href="https://freshhut-grocery.onrender.com/">
    <img src="https://img.shields.io/badge/🌐_Live-Visit_FreshHut-2e7d32?style=for-the-badge" alt="Live Demo">
  </a>
</div>

> ⏳ Hosted on Render's free tier — the server sleeps when idle, so the first load after inactivity can take 30–50 seconds to spin up.

## Overview

FreshHut is a web-based online grocery store built as a mini project for the Department of Computer Science & Engineering. It gives customers a complete shopping experience — browsing products by category, managing a cart, checking out with a choice of payment methods, and tracking orders in real time — while giving administrators a full panel to manage products, orders, and users.

The frontend is built with plain HTML, CSS, and vanilla JavaScript (no frameworks), and talks to a PHP REST-style API backed by a MySQL database. The whole thing is containerized with Docker and deployed on Render, with the database hosted on Aiven.

## Features

**For Customers**
- 🔐 Registration & login with PHP session-based authentication
- 🛍️ Product catalog with category filters, live search, and a featured products section
- 🛒 Shopping cart with quantity controls and stock validation
- 💳 Checkout with 4 payment options — Cash on Delivery, bKash, Nagad, Rocket
- 📦 Real-time order tracking with a visual status timeline (`Pending → Confirmed → Processing → Out for Delivery → Delivered`)
- 👤 Profile panel to update personal info and view order history

**For Admins**
- 📊 Dashboard with total orders, revenue, product count, and low-stock alerts
- 🥕 Product management — add, edit, delete products with image uploads
- 📋 Order management — view full order details and update status
- 👥 User management — view customers, change roles, delete accounts

## Screenshots

<table>
  <tr>
    <td align="center"><b>Create Account</b><br><img src="screenshots/register.png" width="400"></td>
    <td align="center"><b>Shopping Cart</b><br><img src="screenshots/cart.png" width="400"></td>
  </tr>
  <tr>
    <td align="center"><b>Order Tracking</b><br><img src="screenshots/order-tracking.png" width="400"></td>
    <td align="center"><b>Admin Dashboard</b><br><img src="screenshots/admin-dashboard.png" width="400"></td>
  </tr>
  <tr>
    <td align="center" colspan="2"><b>Admin — Manage Products</b><br><img src="screenshots/admin-manage-products.png" width="500"></td>
  </tr>
</table>

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5, CSS3, Vanilla JavaScript (Fetch API) |
| Backend | PHP 8.2 (procedural REST-style API) |
| Database | MySQL (hosted on Aiven, SSL-secured connection) |
| Auth | PHP sessions + hashed passwords, with "remember me" via secure tokens |
| Web Server | Apache (via `php:8.2-apache` Docker image) |
| Deployment | Docker container on Render |

## Project Structure

```
Grocery-Store1/
├── api/                  # PHP backend endpoints (auth, products, cart, orders, users)
├── admin/                # Admin panel (dashboard, products, orders, users)
├── user/                 # Customer profile panel
├── config/               # Database connection + auto setup, SSL cert
├── css/                  # Stylesheets
├── js/                   # Frontend logic (main, auth, cart, checkout, admin)
├── uploads/products/     # Uploaded product images
├── index.html            # Homepage
├── products.html         # Product catalog & search
├── cart.html / checkout.html
├── tracking.html         # Order tracking / history
├── login.html / register.html
├── Dockerfile
└── entrypoint.sh
```

## Database Schema

The schema is created and seeded automatically on first run (see `config/db.php`) — no manual SQL import needed.

| Table | Purpose |
|---|---|
| `users` | Customer/admin accounts, contact information, roles, and authentication data |
| `categories` | Grocery category definitions (8 categories: Vegetables, Fruits, Dairy, Bakery, Beverages, Snacks, Meats, Health & Organic) |
| `products` | Product name, category, price, stock, description, and image (24 seeded products) |
| `cart` | Current items selected by each customer |
| `orders` | Order-level information including address, payment method, total, and status |
| `order_items` | Products, quantities, and prices stored for each order |

Foreign keys enforce relational integrity across cart, orders, and order_items.

## Getting Started

### Prerequisites
- PHP 8.2+ with the `pdo_mysql` extension, or Docker
- A MySQL database (local via XAMPP, or a hosted instance like Aiven)

### Option A — Run with Docker
```bash
git clone <this-repo-url>
cd Grocery-Store1
docker build -t freshhut .
docker run -p 8080:10000 \
  -e DB_HOST=your_db_host -e DB_USER=your_db_user \
  -e DB_PASS=your_db_pass -e DB_NAME=your_db_name -e DB_PORT=3306 \
  freshhut
```
Visit `http://localhost:8080`.

### Option B — Run with XAMPP
1. Copy the `Grocery-Store1` folder into `htdocs/`
2. Start Apache & MySQL from the XAMPP control panel
3. Set your local DB credentials as environment variables, or edit the fallback values in `config/db.php`
4. Visit `http://localhost/Grocery-Store1/`

Tables and seed data (admin user, sample customer, categories, products) are created automatically on the first request.

## Environment Variables

| Variable | Description |
|---|---|
| `DB_HOST` | MySQL host |
| `DB_USER` | MySQL username |
| `DB_PASS` | MySQL password |
| `DB_NAME` | Database name |
| `DB_PORT` | MySQL port |
| `PORT` | Port Apache listens on (set automatically by Render) |

## Demo Accounts

The live demo comes pre-seeded with these accounts so you can try both roles right away:

| Role | Email | Password |
|---|---|---|
| Admin | `admin@freshhut.com` | `FreshHut_Admin_2026!` |
| Customer | `customer@test.com` | `customer123` |

## Key Features
### 👤 Customer Features

* User registration and login
* Customer/admin role separation
* Product browsing by category
* Product search and filtering
* Featured products and promotional hero slider
* Product detail pages with price, stock, description, and image
* Shopping cart with quantity updates and item removal
* Checkout with delivery address
* Payment options: Cash on Delivery, bKash, Nagad, and Rocket
* Order tracking with a visual status timeline
* Profile management and order history

### 🛠️ Admin Features

* Dashboard with order, product, pending-order, and revenue statistics
* Add, edit, and delete products
* Update price, stock, category, and description
* Upload product images
* View and manage customer orders
* Update order status or cancel orders
* View registered users
* Change user roles
* Delete user accounts when required

## Order Status

```
Pending → Confirmed → Processing → Out for Delivery → Delivered
```

Cancelled orders are handled as a separate final state.

## Application Flow
### Customer Flow

```
Register / Login
       │
       ▼
Browse Products
       │
       ├── Search
       └── Filter by Category
       │
       ▼
Add to Cart
       │
       ▼
Checkout
       │
       ├── Delivery Address
       └── Payment Method
       │
       ▼
Place Order
       │
       ▼
Pending
  ↓
Confirmed
  ↓
Processing
  ↓
Out for Delivery
  ↓
Delivered
```

### Admin Flow

```
Admin Login
    │
    ▼
Admin Dashboard
    ├── Manage Products
    ├── Manage Orders
    └── Manage Users
```

## Authentication and Security

* Passwords are hashed with PHP's password-hashing functions.
* PHP sessions are used for authenticated requests.
* Session cookies are configured with secure cookie attributes.
* Customers can access only their own order information.
* Admin API operations perform server-side role checks.
* Cart and checkout operations validate product availability and stock.
* Prepared SQL statements are used for database operations.
* Checkout uses a database transaction to keep stock, order, and cart updates consistent.
* Database credentials are intended to be supplied through environment variables for deployment.
* MySQL SSL can be enabled using the included CA certificate.

Security: Never publish real database passwords or private credentials in a public GitHub repository. Replace any development credentials before using the project publicly.

## Local Setup
1. Clone the repository

```
git clone https://github.com/<your-username>/<your-repository>.git
cd Grocery-Store1
```

2. Configure MySQL
Create a MySQL database and import `config/grocery_store.sql`, or use the project's database setup logic with a MySQL account that has the required permissions.
3. Set database environment variables

```
DB_HOST=your-db-host
DB_PORT=your-db-port
DB_NAME=your-db-name
DB_USER=your-db-user
DB_PASS=your-db-password
```

4. Run with Docker

```
docker build -t freshhut .
docker run -p 8080:8080 \
  -e DB_HOST="your-db-host" \
  -e DB_PORT="your-db-port" \
  -e DB_NAME="your-db-name" \
  -e DB_USER="your-db-user" \
  -e DB_PASS="your-db-password" \
  freshhut
```

For a normal PHP/Apache setup, place the project in your web server's document root and open it through the local server.

## Deployment
The project includes a Docker-based configuration for Render:

1. Render builds the application from the `Dockerfile`.
2. PHP 8.2 with Apache is used as the web runtime.
3. MySQL-related PHP extensions are installed in the container.
4. Apache rewrite and compression support are enabled.
5. `entrypoint.sh` configures Apache to use the port supplied by Render.
6. Database connection values are supplied through environment variables.
7. The application can connect to the remote MySQL database over SSL using the CA certificate.

---

## 🤝 Contributing

If you have any suggestions or want to improve the project, feel free to fork it, make your changes and submit a pull request.

---

## 🔒 License

This project is licensed under the [MIT License](./LICENSE).

---
