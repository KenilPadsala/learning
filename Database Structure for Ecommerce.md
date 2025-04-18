# 🧾 Example Records for E-Commerce Tables

---

## 👤 `users`

| id | name         | email              | password         | address                  | phone        | created_at          |
|----|--------------|--------------------|------------------|---------------------------|--------------|---------------------|
| 1  | John Doe     | john@example.com   | hashed_password  | 123 Main St, NY          | 1234567890   | 2025-04-01 10:00:00 |
| 2  | Jane Smith   | jane@example.com   | hashed_password  | 456 Elm St, LA           | 0987654321   | 2025-04-02 11:30:00 |

---

## 🗂️ `categories`

| id | name         | slug           | created_at          |
|----|--------------|----------------|---------------------|
| 1  | Electronics  | electronics    | 2025-04-01 09:00:00 |
| 2  | Clothing     | clothing       | 2025-04-01 09:10:00 |

---

## 📦 `products`

| id | name              | slug              | description           | price  | stock | category_id | image               | created_at          |
|----|-------------------|-------------------|------------------------|--------|-------|-------------|---------------------|---------------------|
| 1  | iPhone 15         | iphone-15         | Latest Apple phone     | 999.99 | 10    | 1           | iphone15.jpg        | 2025-04-01 10:00:00 |
| 2  | Blue T-Shirt      | blue-tshirt       | Cotton T-shirt         | 19.99  | 100   | 2           | tshirt.jpg          | 2025-04-01 10:05:00 |

---

## 🛒 `carts`

| id | user_id | created_at          |
|----|---------|---------------------|
| 1  | 1       | 2025-04-02 12:00:00 |

---

## 🛍️ `cart_items`

| id | cart_id | product_id | quantity | created_at          |
|----|---------|------------|----------|---------------------|
| 1  | 1       | 1          | 1        | 2025-04-02 12:01:00 |
| 2  | 1       | 2          | 2        | 2025-04-02 12:01:30 |

---

## 📦 `orders`

| id | user_id | total_amount | status     | address             | created_at          |
|----|---------|--------------|------------|----------------------|---------------------|
| 1  | 1       | 1039.97      | processing | 123 Main St, NY      | 2025-04-02 13:00:00 |

---

## 📄 `order_items`

| id | order_id | product_id | quantity | price  |
|----|----------|------------|----------|--------|
| 1  | 1        | 1          | 1        | 999.99 |
| 2  | 1        | 2          | 2        | 19.99  |

---

## 💳 `payments`

| id | order_id | amount  | method     | status    | paid_at             |
|----|----------|---------|------------|-----------|---------------------|
| 1  | 1        | 1039.97 | credit_card| completed | 2025-04-02 13:01:00 |

---

## 🌟 `product_reviews`

| id | product_id | user_id | rating | comment             | created_at          |
|----|------------|---------|--------|----------------------|---------------------|
| 1  | 1          | 1       | 5      | Great phone!         | 2025-04-03 09:00:00 |
| 2  | 2          | 2       | 4      | Nice quality fabric  | 2025-04-03 10:00:00 |

---
