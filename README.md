# ATM
import java.util.Scanner;
class Account{
  private String acc_Num;
  private String pin_Num;
  private double acc_Bal;
  public Account(String acc_num,String pin_Num,double initialBal){
    this.acc_Num=acc_Num;
    this.pin_Num=pin_Num;
    this.acc_Bal=initialBal;
  }
  public String getAccountNum(){
   return acc_Num;
  }
  public boolean verifyPin(String enteredPin){
   return pin_Num.equals(enteredPin);
  }
  public double getBalance(){
   return acc_Bal;
  }
  public void withdraw(double amount){
    acc_Bal -= amount;
  }
   public void deposit(double amount) {
    acc_Bal += amount;
  }
public class ATMInterface {
    public static void main(String[] args) {
        
        Account account = new Account("9786534210", "1324", 1000.0);

        
        Scanner scanner = new Scanner(System.in);
        System.out.println("Welcome to the ATM!");
        System.out.print("Enter your account number: ");
        String enteredAccountNumber = scanner.nextLine();

        
        if (!enteredAccountNumber.equals(account.getAccountNum())) {
            System.out.println("Invalid account number. Exiting...");
            return;
        }

        System.out.print("Enter your PIN: ");
        String enteredPin = scanner.nextLine();

        
        if (!account.verifyPin(enteredPin)) {
            System.out.println("Invalid PIN. Exiting...");
            return;
        }

       
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
}
