# ATM Banking System (Java + MySQL)

A simple console-based ATM banking system developed in Java with a MySQL backend. This application allows users to create bank accounts, log in securely using a PIN, deposit money, and withdraw funds. It's an ideal project for practicing JDBC, database connectivity, and basic banking logic in Java.

---

## 🔧 Features

- Create a new bank account with account number, PIN, and initial balance
- Secure login with account number and PIN
- Deposit money into an existing account
- Withdraw money with balance verification
- Menu-driven console interface
- MySQL database connectivity using JDBC

---

## 🧰 Technologies Used

- Java (JDK 8 or higher)
- MySQL Database
- JDBC (Java Database Connectivity)
- Scanner for user input

---

## 📁 Database Setup

1. **Create a MySQL database:**

```sql
CREATE DATABASE atm_db;

Use the database:
USE atm_db;

Create the accounts table:
CREATE TABLE accounts (
    account_number INT PRIMARY KEY,
    pin INT NOT NULL,
    balance DOUBLE NOT NULL
);

⚙️ How to Run
✅ Prerequisites:

Java (JDK 8+)

MySQL Server

JDBC Driver (MySQL Connector/J)


🛠️ Steps:

Clone the repository:

git clone https://github.com/your-username/ATM-Banking-System.git
cd ATM-Banking-System


Make sure MySQL is running and update the database credentials in:

con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/atm_db", 
    "root", 
    "Srush@028"
);


⚠️ Replace "root" and "Srush@028" with your actual MySQL username and password.

Compile and run the program:

javac Bankkkk.java
java bankkkk.Bankkkk

🧪 Example Usage
Welcome to the ATM System!
1. Create New Account
2. Access Existing Account
> 1

Enter a new account number: 1234
Enter a new PIN: 4321
Enter initial balance: 5000.0
A new account was created successfully!

Welcome to the ATM System!
> 2

Enter your account number: 1234
Enter your PIN: 4321
Login successful!

ATM Menu:
1. Deposit
2. Withdraw
3. Exit
Choose an option: 2
Enter amount to withdraw: 1000
Withdrawal successful!
