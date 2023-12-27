- 👋 Hi, I’m @HarshithaMachireddy
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
HarshithaMachireddy/HarshithaMachireddy is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import java.util.*;

// Enum for different types of accounts
enum AccountType {
    SAVINGS, CHECKING
}

// Class representing a user account
class Account {
    private String accountNumber;
    private AccountType type;
    private double balance;

    public Account(String accountNumber, AccountType type) {
        this.accountNumber = accountNumber;
        this.type = type;
        this.balance = 0.0;
    }

    // Getters and setters for account details
    public String getAccountNumber() {
        return accountNumber;
    }

    public AccountType getType() {
        return type;
    }

    public double getBalance() {
        return balance;
    }

    // Method to deposit funds into the account
    public void deposit(double amount) {
        balance += amount;
    }

    // Method to withdraw funds from the account
    public boolean withdraw(double amount) {
        if (amount <= balance) {
            balance -= amount;
            return true;
        }
        return false;
    }
}

// Class to manage user accounts and transactions
class BankingSystem {
    private Map<String, Account> accounts;
    private List<String> transactionHistory;

    public BankingSystem() {
        accounts = new HashMap<>();
        transactionHistory = new ArrayList<>();
    }

    // Method to create a new account
    public void createAccount(String accountNumber, AccountType type) {
        Account newAccount = new Account(accountNumber, type);
        accounts.put(accountNumber, newAccount);
    }

    // Method to perform funds transfer between accounts
    public boolean transferFunds(String fromAccount, String toAccount, double amount) {
        Account sender = accounts.get(fromAccount);
        Account receiver = accounts.get(toAccount);

        if (sender != null && receiver != null) {
            if (sender.withdraw(amount)) {
                receiver.deposit(amount);
                transactionHistory.add("Transaction: " + fromAccount + " transferred " + amount + " to " + toAccount);
                return true;
            }
        }
        return false;
    }

    // Method to display transaction history
    public void displayTransactionHistory() {
        for (String transaction : transactionHistory) {
            System.out.println(transaction);
        }
    }

    // Method to check account balance
    public double checkBalance(String accountNumber) {
        Account account = accounts.get(accountNumber);
        if (account != null) {
            return account.getBalance();
        }
        return -1; // Return -1 if account doesn't exist
    }
}

public class Main {
    public static void main(String[] args) {
        BankingSystem bankingSystem = new BankingSystem();

        // Creating accounts
        bankingSystem.createAccount("123456789", AccountType.SAVINGS);
        bankingSystem.createAccount("987654321", AccountType.CHECKING);

        // Performing transactions
        bankingSystem.transferFunds("123456789", "987654321", 1000);
        bankingSystem.transferFunds("987654321", "123456789", 500);

        // Displaying transaction history
        System.out.println("Transaction History:");
        bankingSystem.displayTransactionHistory();

        // Checking account balances
        double balance1 = bankingSystem.checkBalance("123456789");
        double balance2 = bankingSystem.checkBalance("987654321");
        System.out.println("Balance of account 123456789: " + balance1);
        System.out.println("Balance of account 987654321: " + balance2);
    }
}
