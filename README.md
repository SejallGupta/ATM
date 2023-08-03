# ATM
import java.util.Scanner;

class Account {
    private String accountNumber;
    private String pin;
    private double balance;

    public Account(String accountNumber, String pin, double initialBalance) {
        this.accountNumber = accountNumber;
        this.pin = pin;
        this.balance = initialBalance;
    }

    public String getAccountNumber() {
        return accountNumber;
    }

    public boolean verifyPin(String enteredPin) {
        return pin.equals(enteredPin);
    }

    public double getBalance() {
        return balance;
    }

    public void withdraw(double amount) {
        balance -= amount;
    }

    public void deposit(double amount) {
        balance += amount;
    }
}

public class ATMInterface {
    public static void main(String[] args) {
        // Initialize an example account (replace this with your account management system)
        Account account = new Account("1234567890", "1234", 1000.0);

        // Start the ATM interface
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the ATM!");
        System.out.print("Enter your account number: ");
        String enteredAccountNumber = scanner.nextLine();

        // Verify the account number (in a real application, you'd look up the account in the database)
        if (!enteredAccountNumber.equals(account.getAccountNumber())) {
            System.out.println("Invalid account number. Exiting...");
            return;
        }

        System.out.print("Enter your PIN: ");
        String enteredPin = scanner.nextLine();

        // Verify the PIN
        if (!account.verifyPin(enteredPin)) {
            System.out.println("Invalid PIN. Exiting...");
            return;
        }

        // Show the main menu
        while (true) {
            System.out.println("\nMain Menu:");
            System.out.println("1. Check Balance");
            System.out.println("2. Withdraw");
            System.out.println("3. Deposit");
            System.out.println("4. Exit");
            System.out.print("Enter your choice: ");
            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    System.out.println("Your balance: ₹" + account.getBalance());
                    break;
                case 2:
                    System.out.print("Enter the amount to withdraw: ");
                    double withdrawAmount = scanner.nextDouble();
                    if (withdrawAmount > account.getBalance()) {
                        System.out.println("Insufficient funds!");
                    } else {
                        account.withdraw(withdrawAmount);
                        System.out.println("Withdrawal successful. Your new balance: ₹" + account.getBalance());
                    }
                    break;
                case 3:
                    System.out.print("Enter the amount to deposit: ");
                    double depositAmount = scanner.nextDouble();
                    account.deposit(depositAmount);
                    System.out.println("Deposit successful. Your new balance: ₹" + account.getBalance());
                    break;
                case 4:
                    System.out.println("Thank you for using the ATM. Goodbye!");
                    return;
                default:
                    System.out.println("Invalid choice. Please try again.");
            }
        }
    }
}
