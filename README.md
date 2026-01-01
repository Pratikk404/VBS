# VBS - Virtual Banking System

A full-stack Spring Boot banking platform with secure transactions, role-based access, and complete audit logging.

## ✨ Key Features

🔐 **Secure Authentication** | 💰 **Full Transactions** | 📊 **Complete History** | 👥 **Admin Control** | ✅ **Validation**

- Role-based access (customer & admin)
- Deposits, withdrawals, peer-to-peer transfers
- Transaction passbook & system audit logs
- User management with sorting & search
- Overdraft prevention, self-transfer blocking

## 🏗️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Backend** | Spring Boot 3.5.9, Java 17 |
| **Database** | MySQL 8.0+, JPA/Hibernate |
| **Frontend** | HTML5, CSS, JavaScript |
| **Build** | Maven |
| **Port** | 8081 |

## 🚀 Quick Start

### Prerequisites
```
Java 17+ | MySQL Server | Maven 3.6+
```

### Setup
```bash
# 1. Clone & navigate
git clone <repo-url>
cd demo

# 2. Create database
mysql -u root -p
> CREATE DATABASE springtest;

# 3. Update src/main/resources/application.properties
spring.datasource.url=jdbc:mysql://localhost:3306/springtest
spring.datasource.username=root
spring.datasource.password=your_password

# 4. Build & run
mvn clean package
mvn spring-boot:run

# 5. Open browser
http://localhost:8081
```

## 📡 Core API

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/register` | POST | Create account |
| `/login` | POST | Authenticate (returns user ID) |
| `/get-details/{id}` | GET | Fetch balance & username |
| `/update` | POST | Update profile |
| `/deposit` | POST | Add funds |
| `/withdraw` | POST | Withdraw (balance checked) |
| `/transfer` | POST | Send to another user |
| `/passbook/{id}` | GET | Transaction history |
| `/users` | GET | [Admin] List customers |
| `/users/{keyword}` | GET | [Admin] Search customers |
| `/add/{adminId}` | POST | [Admin] Add customer |
| `/delete-user/{id}/admin/{adminId}` | DELETE | [Admin] Delete customer |
| `/histories` | GET | [Admin] Audit log |

## 🔑 Sample Calls

**Register:**
```bash
curl -X POST http://localhost:8081/register \
  -H "Content-Type: application/json" \
  -d '{"username":"john","password":"pass123","email":"john@example.com","name":"John","role":"customer","balance":0}'
```

**Deposit:**
```bash
curl -X POST http://localhost:8081/deposit \
  -H "Content-Type: application/json" \
  -d '{"id":1,"amount":500}'
```

**Transfer:**
```bash
curl -X POST http://localhost:8081/transfer \
  -H "Content-Type: application/json" \
  -d '{"id":1,"username":"jane","amount":100}'
```

## 📊 Data Models

| Entity | Fields |
|--------|--------|
| **User** | id, username (unique), password, email (unique), name, role, balance |
| **Transaction** | id, userId, amount, currBalance, description, date (auto) |
| **History** | id, description, date (auto) |

## 📂 Project Structure

```
demo/
├── src/main/java/com/vbs/demo/
│   ├── controller/       (UserController, TransactionController, HistoryController)
│   ├── models/           (User, Transaction, History)
│   ├── dto/              (LoginDto, TransactionDto, TransferDto, UpdateDto, DisplayDto)
│   └── repositories/     (UserRepo, TransactionRepo, HistoryRepo)
├── src/main/resources/
│   ├── application.properties
│   └── static/           (HTML pages: login, signup, dashboard, admin, history, etc.)
├── pom.xml
└── README.md
```

## 🔒 Security

✅ Role-based access control  
✅ Overdraft prevention  
✅ Self-transfer blocking  
✅ Auto-audit logging  
✅ CORS enabled  
✅ Unique constraints (username, email)  

## 🎯 Workflows

**Customer**: Register → Login → Dashboard → Deposit/Withdraw/Transfer → Passbook  
**Admin**: Login (admin role) → Admin Panel → Manage Users → View History

