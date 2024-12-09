package bankkkk;

import java.sql.*;
import java.util.Scanner;

public class Bankkkk {
    static Connection con = null;

    public static void connectDatabase() {
        try {
            Class.forName("com.mysql.cj.jdbc.Driver");
            con = DriverManager.getConnection("jdbc:mysql://localhost:3306/atm_db", "root", "Srush@028");
            System.out.println("Database connected successfully!");
        } catch (ClassNotFoundException e) {
            System.out.println("MySQL JDBC Driver not found. Add the JDBC driver to your classpath.");
        } catch (SQLException e) {
            System.out.println("Database connection failed: " + e.getMessage());
        }
    }

    public static void createNewAccount() {
        if (con == null) {
            System.out.println("Database connection is not established.");
            return;
        }

        Scanner sc = new Scanner(System.in);
        System.out.println("Enter a new account number: ");
        int accountNumber = sc.nextInt();
        System.out.println("Enter a new PIN: ");
        int pin = sc.nextInt();
        System.out.println("Enter initial balance: ");
        double balance = sc.nextDouble();

        try {
            String query = "INSERT INTO accounts (account_number, pin, balance) VALUES (?, ?, ?)";
            PreparedStatement pstmt = con.prepareStatement(query);
            pstmt.setInt(1, accountNumber);
            pstmt.setInt(2, pin);
            pstmt.setDouble(3, balance);

            int rowsInserted = pstmt.executeUpdate();
            if (rowsInserted > 0) {
                System.out.println("A new account was created successfully!");
            } else {
                System.out.println("Account creation failed.");
            }
        } catch (SQLException e) {
            System.out.println("SQL Error: " + e.getMessage());
        }
    }

    public static void depositAmount(int accountNumber) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter amount to deposit: ");
        double depositAmount = sc.nextDouble();

        try {
            String query = "UPDATE accounts SET balance = balance + ? WHERE account_number = ?";
            PreparedStatement pstmt = con.prepareStatement(query);
            pstmt.setDouble(1, depositAmount);
            pstmt.setInt(2, accountNumber);
            
            int rowsUpdated = pstmt.executeUpdate();
            if (rowsUpdated > 0) {
                System.out.println("Deposit successful!");
            } else {
                System.out.println("Account not found.");
            }
        } catch (SQLException e) {
            System.out.println("SQL Error: " + e.getMessage());
        }
    }
    public static void withdrawAmount(int accountNumber) {
        Scanner sc = new Scanner(System.in);
        System.out.println("Enter amount to withdraw: ");
        double withdrawAmount = sc.nextDouble();

        try {
            String checkBalanceQuery = "SELECT balance FROM accounts WHERE account_number = ?";
            PreparedStatement checkStmt = con.prepareStatement(checkBalanceQuery);
            checkStmt.setInt(1, accountNumber);
            ResultSet rs = checkStmt.executeQuery();

            if (rs.next()) {
                double currentBalance = rs.getDouble("balance");

                if (currentBalance >= withdrawAmount) {
                    // Proceed with the withdrawal
                    String query = "UPDATE accounts SET balance = balance - ? WHERE account_number = ?";
                    PreparedStatement pstmt = con.prepareStatement(query);
                    pstmt.setDouble(1, withdrawAmount);
                    pstmt.setInt(2, accountNumber);

                    int rowsUpdated = pstmt.executeUpdate();
                    if (rowsUpdated > 0) {
                        System.out.println("Withdrawal successful!");
                    } else {
                        System.out.println("Account not found.");
                    }
                } else {
                    System.out.println("Insufficient balance.");
                }
            } else {
                System.out.println("Account not found.");
            }
        } catch (SQLException e) {
            System.out.println("SQL Error: " + e.getMessage());
        }
    }
    public static void atmMenu(int accountNumber) {
        Scanner sc = new Scanner(System.in);
        while (true) {
            System.out.println("\nATM Menu:");
            System.out.println("1. Deposit");
            System.out.println("2. Withdraw");
            System.out.println("3. Exit");
            System.out.print("Choose an option: ");
            int choice = sc.nextInt();

            switch (choice) {
                case 1:
                    depositAmount(accountNumber);
                    break;
                case 2:
                    withdrawAmount(accountNumber);
                    break;
                case 3:
                    System.out.println("Exiting... Goodbye!");
                    return;  // Exit the method, which ends the program
                default:
                    System.out.println("Invalid option. Please try again.");
            }
        }
    }
    public static boolean validateAccount(int accountNumber, int pin) {
        try {
            String query = "SELECT * FROM accounts WHERE account_number = ? AND pin = ?";
            PreparedStatement pstmt = con.prepareStatement(query);
            pstmt.setInt(1, accountNumber);
            pstmt.setInt(2, pin);

            ResultSet rs = pstmt.executeQuery();
            return rs.next();  
        } catch (SQLException e) {
            System.out.println("SQL Error: " + e.getMessage());
            return false;
        }
    }
    public static void main(String[] args) {
        connectDatabase();

        Scanner sc = new Scanner(System.in);
        System.out.println("Welcome to the ATM System!");

        // Create or access an account
        System.out.println("1. Create New Account");
        System.out.println("2. Access Existing Account");
        int option = sc.nextInt();

        if (option == 1) {
            createNewAccount();
        } else if (option == 2) {
            System.out.print("Enter your account number: ");
            int accountNumber = sc.nextInt();
            System.out.print("Enter your PIN: ");
            int pin = sc.nextInt();

            if (validateAccount(accountNumber, pin)) {
                System.out.println("Login successful!");
                atmMenu(accountNumber);  
            } else {
                System.out.println("Invalid account number or PIN.");
            }
        } else {
            System.out.println("Invalid option. Exiting...");
        }
    }
}
