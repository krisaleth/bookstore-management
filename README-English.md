# 📚 BOOKSTORE MANAGEMENT SYSTEM

The project is a complete full-stack system that allows users to search for and purchase books, and administrators to manage inventory and orders. The system is packaged using Docker to ensure consistency across all environments.

---

## 1. DATABASE DESIGN ANALYSIS

The system uses a **MySQL 8.0** relational database with the following main entities:

* **Users**: Stores user information, encrypted passwords (BCrypt), and permissions (Admin/User).
* **Books**: Stores book information, ISBN, price, inventory quantity, and cover image URL.
* **Authors & Categories**: Author and category information (Many-to-Many relationship with Books).
* **Orders & OrderItems**: Stores order information. `OrderItem` stores the book price at the time of purchase (Snapshot) for later invoice reconciliation.

---

## 2. SITE MAP

The system is designed with an optimized user experience flow through the following subsystems:

### 2.1. Client Facing Subsystem
* **Home**: Displays the latest and featured books.
* **Category and Search**: Filter books by genre, author, or search by keyword.
* **Book Details**: Displays content description, price, and in-stock/out-of-stock status.
* **Cart**: Manages the list of books waiting to be purchased.
* **Checkout**: Enters delivery information and confirms the order.
* **Đăng nhập/Đăng ký**: Manage personal accounts.

### 2.2. Admin Dashboard
* **Book Management**: Add new books (with image upload), update information and quantity in stock.
* **Category/Author Management**: CRUD related entities.
* **Order Management**: View the system-wide order list and update status (Pending -> In Transit -> Delivered).

---

## 3. CORE ALGORITHMS

* **Payment & Inventory Processing**: When an order is created, the system checks the inventory quantity (`stock`). If sufficient, the order is created and the corresponding `stock` quantity is deducted in a **Database Transaction** to ensure consistency.
* **JWT Authentication**: The frontend sends login information, the backend checks it and returns a **JSON Web Token**. This token is stored in a Cookie and sent in the `Authorization` header in subsequent requests to authenticate access.
* **Price Snapshot**: The book price in `OrderItem` is stored at the time of purchase. This ensures that when the Admin changes the book price in the `Books` table, the revenue of past orders is not affected.

---

## 4. INSTALLATION & RUNNING GUIDE (DOCKER - RECOMMENDED)

This is the fastest way to run the entire system without installing Java or Node.js on your machine.

### Requirements
* **Docker** and **Docker Desktop** must be installed.

### Steps

**1. Clone the project:**
```bash
git clone https://github.com/Krisaleth/bookstore-management.git
cd bookstore-management
```

**2. Run the system: In the root directory (where the docker-compose.yml file is located), run the command:**
```bash
docker-compose up --build -d
```

**3. Check the results:**

- Frontend UI: http://localhost:3000

- Backend API: http://localhost:8080/api

## 5. CONCLUSION & DEVELOPMENT DIRECTION
### Conclusion

The project has successfully built a modern bookstore management system that meets the basic requirements of e-commerce operations. The use of Docker makes it easy to quickly deploy the project to any server system.
Future Development

   - Integrate online payment via VNPay and PayPal gateways.

   - Develop a book recommendation system based on purchase history.

   - Optimize search with Elasticsearch to support content-based book searches.