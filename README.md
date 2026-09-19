# 💳 Payment Ledger Backend

A backend system for managing accounts and processing secure money transfers using
**Node.js, Express.js, MongoDB, and JWT authentication**.

The project focuses on backend concepts such as **ledger-based balance tracking,
idempotency, database transactions, and API performance testing**.

---

## 🚀 Features

- 🔐 JWT-based user authentication
- 👤 User and account management
- 💸 Account-to-account money transfers
- 🧾 Debit and credit ledger entries
- 🔄 Idempotency checks for duplicate requests
- 🛡️ MongoDB transactions for atomic updates
- 📊 Balance calculation using MongoDB aggregation
- ⚡ Database indexing for faster queries
- 📈 API load testing with k6

---

## 🏗️ System Architecture

```text
                    ┌──────────────────┐
                    │     Client       │
                    │ Postman / k6     │
                    └────────┬─────────┘
                             │
                             ▼
                    ┌──────────────────┐
                    │   Express API    │
                    │     Node.js      │
                    └────────┬─────────┘
                             │
              ┌──────────────┼──────────────┐
              ▼              ▼              ▼
        ┌──────────┐   ┌───────────┐   ┌───────────┐
        │   Auth   │   │  Account  │   │Transaction│
        │  /JWT    │   │ Management│   │ Processing│
        └──────────┘   └───────────┘   └─────┬─────┘
                                             │
                                             ▼
                                    ┌─────────────────┐
                                    │ MongoDB         │
                                    │ Transaction     │
                                    └────────┬────────┘
                                             │
                         ┌───────────────────┼───────────────────┐
                         ▼                   ▼                   ▼
                  ┌────────────┐      ┌────────────┐      ┌────────────┐
                  │  Accounts  │      │Transactions│      │   Ledger   │
                  └────────────┘      └────────────┘      └────────────┘
````

---

## 💰 Transaction Flow

```text
Transfer Request
       │
       ▼
Authenticate User
       │
       ▼
Validate Accounts
       │
       ▼
Check Idempotency Key
       │
       ▼
Check Account Status
       │
       ▼
Check Available Balance
       │
       ▼
Start MongoDB Transaction
       │
       ├──────────────► Debit Sender
       │
       ├──────────────► Credit Receiver
       │
       └──────────────► Update Transaction Status
                              │
                              ▼
                         Commit Transaction
```

---

## 🧾 Ledger Model

Every transfer creates corresponding ledger entries:

```text
Sender Account
      │
      └─── DEBIT  ───► ₹100

Receiver Account
      │
      └─── CREDIT ───► ₹100
```

Account balances are calculated from the ledger entries rather than relying
only on a manually updated balance value.

---

## 🔑 Authentication

The API uses **JWT authentication** to protect account and transaction
operations.

```text
Login
  │
  ▼
JWT Token
  │
  ▼
Authorization Header
  │
  ▼
Authentication Middleware
  │
  ▼
Protected API
```

---

## 🛡️ Transaction Safety

The project uses several mechanisms to improve transaction consistency:

| Mechanism            | Purpose                                  |
| -------------------- | ---------------------------------------- |
| JWT Authentication   | Protect API access                       |
| Idempotency Key      | Prevent duplicate transaction processing |
| MongoDB Transactions | Keep debit/credit operations atomic      |
| Ledger Entries       | Maintain transaction history             |
| Aggregation          | Calculate account balances               |
| Indexing             | Improve database query performance       |

---

## ⚡ Performance Testing

The API was tested using **k6**.

### Health Endpoint Benchmark

| Metric          |     Result |
| --------------- | ---------: |
| Virtual Users   |         20 |
| Test Duration   | 30 seconds |
| Requests        |       542K |
| Throughput      |  18K req/s |
| Failed Requests |         0% |
| p95 Latency     |    1.95 ms |

> Benchmark performed against the API health endpoint under local development
> conditions. It is not a measurement of payment transaction throughput.

---

## 🛠️ Tech Stack

* **Runtime:** Node.js
* **Framework:** Express.js
* **Database:** MongoDB
* **ODM:** Mongoose
* **Authentication:** JWT
* **API:** REST
* **Testing:** Postman, k6
* **Version Control:** Git & GitHub

---

## 📂 Project Structure

```text
payment-ledger-backend/
│
├── src/
│   ├── controllers/
│   ├── middleware/
│   ├── models/
│   └── routers/
│
├── server.js
├── package.json
├── package-lock.json
├── .gitignore
└── README.md
```

---

## 🔌 Core API Routes

### Authentication

```text
POST /api/auth/register
POST /api/auth/login
POST /api/auth/logout
```

### Accounts

```text
POST /api/account/create
GET  /api/account/accounts
GET  /api/account/accounts/:accountid
```

### Transactions

```text
POST /api/transaction/transcation
POST /api/transaction/fundtranscation
```

---

## ▶️ Run Locally

### 1. Clone the repository

```bash
git clone https://github.com/KeerthanaGopal28/payment-ledger-backend.git
cd payment-ledger-backend
```

### 2. Install dependencies

```bash
npm install
```

### 3. Configure environment variables

Create a `.env` file:

```env
DatabaseKey=YOUR_MONGODB_CONNECTION_STRING
jwturl=YOUR_JWT_SECRET
```

### 4. Start the server

```bash
npm start
```

Server:

```text
http://localhost:3000
```

---

## 🧪 Testing

The API can be tested using:

* Postman for functional API testing
* k6 for load and performance testing

---

## 🎯 Learning Goals

This project was built to understand practical backend engineering concepts,
including:

* REST API design
* Authentication middleware
* MongoDB data modeling
* Database transactions
* Ledger-based accounting
* Idempotent APIs
* Aggregation pipelines
* Database indexing
* API performance testing
