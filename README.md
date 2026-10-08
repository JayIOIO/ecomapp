Here is the complete `README.md` file customized for your project:

```markdown
# 🛍️ Full-Stack E-Commerce Application (Shopee Clone)

A full-stack e-commerce web application built with **React (Vite)**, **Node.js/Express**, and **MySQL**. Features JWT authentication, product catalog browsing, shopping cart management, multi-item checkout, complete order CRUD operations, and real-time profile name updates saved to the database.

---

## 🚀 Tech Stack

- **Frontend:** React.js (Vite), Axios, Plain CSS (`App.css`)
- **Backend:** Node.js, Express.js, JSON Web Tokens (`jsonwebtoken`), `bcryptjs`
- **Database:** MySQL (`mysql2` connection pool)

---

## 📁 Project Structure

```text
ecommerce-app/
├── backend/
│   ├── .env
│   ├── package.json
│   └── server.js
├── frontend/
│   ├── package.json
│   ├── src/
│   │   ├── App.css
│   │   ├── App.jsx
│   │   ├── index.css
│   │   └── main.jsx
│   └── vite.config.js
└── README.md

```

---

## ⚙️ Setup & Installation Guide

### 1. Database Setup (MySQL)

Open Command Prompt, Terminal, or MySQL Workbench and execute the following script to build the schema and seed sample products:

```sql
CREATE DATABASE IF NOT EXISTS ecommerce_db;
USE ecommerce_db;

-- 1. Users Table
CREATE TABLE IF NOT EXISTS users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  email VARCHAR(100) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 2. Products Table
CREATE TABLE IF NOT EXISTS products (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(150) NOT NULL,
  description TEXT,
  price DECIMAL(10, 2) NOT NULL,
  image_url VARCHAR(255),
  stock INT DEFAULT 10,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- 3. Checkout Orders Table
CREATE TABLE IF NOT EXISTS checkout_orders (
  id INT AUTO_INCREMENT PRIMARY KEY,
  user_id INT NOT NULL,
  customer_name VARCHAR(100) NOT NULL,
  email VARCHAR(100) NOT NULL,
  address TEXT NOT NULL,
  payment_method VARCHAR(50) NOT NULL,
  total_amount DECIMAL(10, 2) NOT NULL,
  status VARCHAR(50) DEFAULT 'Pending',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  CONSTRAINT fk_orders_user FOREIGN KEY (user_id) REFERENCES users(id) ON DELETE CASCADE
);

-- 4. Order Items Table
CREATE TABLE IF NOT EXISTS order_items (
  id INT AUTO_INCREMENT PRIMARY KEY,
  order_id INT NOT NULL,
  product_id INT NOT NULL,
  quantity INT NOT NULL,
  price DECIMAL(10, 2) NOT NULL,
  CONSTRAINT fk_items_order FOREIGN KEY (order_id) REFERENCES checkout_orders(id) ON DELETE CASCADE,
  CONSTRAINT fk_items_product FOREIGN KEY (product_id) REFERENCES products(id) ON DELETE CASCADE
);

-- Seed Sample Products
INSERT INTO products (name, description, price, image_url, stock) VALUES
('Wireless Headphones', 'Noise-canceling over-ear headphones', 99.99, '[https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=500](https://images.unsplash.com/photo-1505740420928-5e560c06d30e?w=500)', 15),
('Smart Watch', 'Fitness tracker with heart rate monitor', 149.99, '[https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=500](https://images.unsplash.com/photo-1523275335684-37898b6baf30?w=500)', 8),
('Mechanical Keyboard', 'RGB mechanical gaming keyboard', 79.99, '[https://images.unsplash.com/photo-1587829741301-dc798b83add3?w=500](https://images.unsplash.com/photo-1587829741301-dc798b83add3?w=500)', 20);

```

---

### 2. Backend Setup (Express.js)

1. Navigate to the `backend` folder:
```bash
cd backend

```


2. Install required dependencies:
```bash
npm install express mysql2 cors bcryptjs jsonwebtoken dotenv

```


3. Create a `.env` file inside the `backend` directory:
```env
PORT=5000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=your_actual_mysql_password
DB_NAME=ecommerce_db
JWT_SECRET=super_secret_jwt_key

```


*(Note: Leave `DB_PASSWORD=` empty if using default XAMPP settings)*
4. Start the backend server:
```bash
node server.js

```


*Output should display: `Server running on http://localhost:5000*`

---

### 3. Frontend Setup (React / Vite)

1. Open a new terminal window/tab and navigate to the `frontend` folder:
```bash
cd frontend

```


2. Install Axios:
```bash
npm install axios

```


3. Ensure `frontend/src/index.css` is cleared/empty.
4. Paste the project CSS into `frontend/src/App.css` and the React component logic into `frontend/src/App.jsx`.
5. Start the React development server:
```bash
npm run dev

```


*App will be accessible at: `http://localhost:5173/*`

---

## ✨ Features & Functionality

* **🔑 User Authentication:** Login and Sign Up with password hashing (`bcryptjs`) and JWT session persistence stored in `localStorage`.
* **🛒 Product Storefront:** Browse catalog products fetched from MySQL and dynamically calculate cart totals.
* **💳 Multi-Item Checkout:** Place orders containing multiple cart items with address validation and payment method selections.
* **🔄 Complete Order CRUD:**
* **Create:** Insert new checkout orders and decrease product stock in a SQL transaction.
* **Read:** Fetch authenticated user order history.
* **Update:** Dynamically change order status (`Pending`, `Processing`, `Shipped`, `Delivered`).
* **Delete:** Cancel/delete existing orders from MySQL.


* **👤 Account Profile Update:** Edit account name directly in the database with instant token re-issuance.

```

```
