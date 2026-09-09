<div align="center">
  <img src="screenshots/homepage.png" alt="FreshHut Homepage" width="100%">
</div>

<h1 align="center">🛒 FreshHut - Online Grocery Store</h1>
<p align="center">
  <i>
    <b>Farm to Your Door - a modern online grocery shopping platform</b><br>
    Built to make everyday grocery shopping <b>simple, convenient, and accessible</b>.<br>
    Browse fresh products, manage your cart, place orders, and track deliveries with ease.<br>
    A complete digital grocery experience designed for modern shoppers.
  </i>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/PHP-8.2-777BB4?style=flat-square&logo=php&logoColor=white" alt="PHP">
  <img src="https://img.shields.io/badge/MySQL-Aiven-4479A1?style=flat-square&logo=mysql&logoColor=white" alt="MySQL">
  <img src="https://img.shields.io/badge/JavaScript-Vanilla-F7DF1E?style=flat-square&logo=javascript&logoColor=black" alt="JavaScript">
  <img src="https://img.shields.io/badge/Docker-Apache-2496ED?style=flat-square&logo=docker&logoColor=white" alt="Docker">
  <img src="https://img.shields.io/badge/Deployed%20on-Render-46E3B7?style=flat-square&logo=render&logoColor=white" alt="Render">
</p>

## Table of Contents

- [Live Demo](#live-demo)
- [Features](#features)
- [Screenshots](#screenshots)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Database Schema](#database-schema)
- [Application Flow](#application-flow)
- [Local Setup](#local-setup)
- [Environment Variables](#environment-variables)
- [Authentication and Security](#authentication-and-security)
- [Demo Accounts](#demo-accounts)

<h2 id="live-demo" align="center">Live Demo</h2> <div align="center"> <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=18&pause=1000&color=2E7D32&center=true&vCenter=true&width=500&height=30&lines=%F0%9F%8C%90+Click+below+to+visit+FreshHut;Live+and+ready+to+explore!" alt="Typing SVG" /> <br/> <a href="https://freshhut-grocery.onrender.com/"> <img src="https://img.shields.io/badge/_LIVE_DEMO-Visit_FreshHut-2e7d32?style=for-the-badge&logo=render&logoColor=white&labelColor=1b5e20" alt="Live Demo"> </a> </div> <p align="center"> <sub>⏳ <b>Note:</b> This demo runs on Render's free tier. If it's been idle, the server needs a moment to wake up first load may take 30–50 seconds. Thanks for your patience!</sub> </p>

## Features

**For Customers**
- 🔐 Registration & login with PHP session-based authentication
- 🛍️ Product catalog with category filters, live search, and a featured products section
- 🛒 Shopping cart with quantity controls and stock validation
- 💳 Checkout with 4 payment options: Cash on Delivery, bKash, Nagad, Rocket
- 📦 Real-time order tracking with a visual status timeline (`Pending → Confirmed → Processing → Out for Delivery → Delivered`)
- 👤 Profile panel to update personal info and view order history

**For Admins**
- 📊 Dashboard with total orders, revenue, product count, and low-stock alerts
- 🥕 Product management: add, edit, delete products with image uploads
- 📋 Order management: view full order details and update status
- 👥 User management: view customers, change roles, delete accounts

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

| Layer | Technology | Purpose |
|---|---|---|
| Frontend | HTML5 | Markup and page structure |
| Styling | CSS3 | Responsive layout, cards, and admin UI styling |
| Client-side | Vanilla JavaScript | Fetch API calls, search/filtering, cart, checkout, and tracking logic |
| Backend | PHP 8.2 | Session-based auth, REST-style endpoints, and business logic |
| Database | MySQL | Stores users, categories, products, cart, and order data |
| API Communication | Fetch API / JSON | Connects the frontend to the PHP backend |
| Web Server | Apache | Serves the PHP application (`php:8.2-apache`) |
| Containerization | Docker | Packages the app for consistent deployment |
| Hosting | Render | Runs the live, containerized application |
| Database Service | Aiven (MySQL) | Managed remote database over an SSL connection |

## Project Structure

```
Grocery-Store1/
├── admin/
│   ├── index.html
│   ├── products.html
│   ├── orders.html
│   ├── users.html
│   └── admin-style.css
│
├── api/
│   ├── auth_check.php
│   ├── cart.php
│   ├── login.php
│   ├── logout.php
│   ├── orders.php
│   ├── products.php
│   ├── register.php
│   ├── user.php
│   └── users.php
│
├── user/
│
├── config/
│   ├── db.php
│   ├── ca.pem
│   └── grocery_store.sql
│
├── css/
│   ├── style.css
│   └── product-detail.css
│
├── js/
│   ├── admin.js
│   ├── auth.js
│   ├── cart.js
│   ├── checkout.js
│   ├── main.js
│   └── product-img.js
│
├── uploads/
│   └── products/
│
├── about.html
├── cart.html
├── checkout.html
├── contact.html
├── index.html
├── login.html
├── product-detail.html
├── products.html
├── register.html
├── tracking.html
├── Dockerfile
└── entrypoint.sh
```

## Database Schema

The schema is created and seeded automatically on first run (see `config/db.php`) no manual SQL import needed.

| Table | Purpose |
|---|---|
| `users` | Customer/admin accounts, contact information, roles, and authentication data |
| `categories` | Grocery category definitions (8 categories: Vegetables, Fruits, Dairy, Bakery, Beverages, Snacks, Meats, Health & Organic) |
| `products` | Product name, category, price, stock, description, and image (24 seeded products) |
| `cart` | Current items selected by each customer |
| `orders` | Order-level information including address, payment method, total, and status |
| `order_items` | Products, quantities, and prices stored for each order |

Foreign keys enforce relational integrity across cart, orders, and order_items.

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

## Local Setup

### Prerequisites
- [XAMPP](https://www.apachefriends.org/) installed (includes PHP + MySQL + Apache)

### Run Locally with XAMPP

1. **Download and install XAMPP**, then open the XAMPP Control Panel and start **Apache** and **MySQL**.

2. **Clone the repository into your XAMPP `htdocs` folder**
```bash
   cd C:/xampp/htdocs        # or /Applications/XAMPP/htdocs on Mac
   git clone <this-repo-url>
   cd Grocery-Store1
```

3. **Create a local database**
   - Open `http://localhost/phpmyadmin`
   - Create a new database, e.g. `grocery_store`

4. **Set your database credentials**
   Open `config/db.php` and update the fallback values to match your local setup (defaults for XAMPP are usually):
```php
   DB_HOST = "localhost"
   DB_USER = "root"
   DB_PASS = ""              // XAMPP's default MySQL has no password
   DB_NAME = "grocery_store"
   DB_PORT = 3306
```

5. **Finally visit the app**

## Environment Variables

| Variable | Description |
|---|---|
| `DB_HOST` | MySQL host |
| `DB_USER` | MySQL username |
| `DB_PASS` | MySQL password |
| `DB_NAME` | Database name |
| `DB_PORT` | MySQL port |
| `PORT` | Port Apache listens on (set automatically by Render) |

## Authentication and Security

* Passwords are securely hashed.
* PHP sessions keep users logged in securely.
* Session cookies use secure settings.
* Users can only view their own orders.
* Admin actions require proper admin access.
* Cart and checkout check product stock.
* Prepared statements help protect database queries.
* Checkout uses a database transaction to keep orders and stock accurate.
* Database credentials can be configured with environment variables.
* MySQL SSL support is available with the included CA certificate.

## Demo Accounts

The live demo comes pre-seeded with these accounts so you can try both roles right away:

| Role | Email | Password |
|---|---|---|
| Admin | `admin@freshhut.com` | `FreshHut_Admin_2026!` |
| Customer | `customer@test.com` | `customer123` |

---

## 🤝 Contributing

If you have any suggestions or want to improve the project, feel free to fork it, make your changes and submit a pull request.

---

## 🔒 License

This project is licensed under the [MIT License](./LICENSE).

---
