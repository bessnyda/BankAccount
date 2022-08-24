# BankAccount


    import java.util.Scanner;
    import java.util.regex.Matcher;
    import java.util.regex.Pattern;

    public class Main {

    public static void main(String[] args) throws Exception {

        BankAccount account1 = new BankAccount("Alisa", "Alexiv", 23, "12345678988834567890123", "6366");
        BankAccount account2 = new BankAccount("Alex", "Pravo", 18, "32145678988839877890678", "9316");

        System.out.println(account1);
        //System.out.println();
        //System.out.println(account2);
        //System.out.println();
        // account1.TopUpABankAccountOnline(account1,1);
        //account1.TransferToAnotherUser(account1,account2,1100);
        //account1.TransferToAnotherUser(account1,account2,1170);
        //System.out.println();
        //System.out.println(account1);
        //System.out.println();
        //System.out.println(account2);
        account1.TopUpABankAccountOnline(account1, 30);
        account1.MoneyTransfer(account1);
        account1.MoneyTransfer(account1);
        System.out.println();
        System.out.println(account1);


    }

    }

    class BankAccount {
    private static long serialVersionUID = 001;
    private String name, surname, card, pin;
    private int age, CompletePurchases;
    private double balance;
    private String History = "";
    private double commission = 0.90;
    private double cost = 2.0;


    public BankAccount(String name, String surname, int age, String card, String pin) {

        if (age > 14 && age < 150 && name.length() > 1 && name.length() < 50 && surname.length() > 1 && surname.length() < 50 && card.length() == 23 && pin.length() == 4) {
            Pattern pattern = Pattern.compile("(\\d{4})(\\d{4})(\\d{4})(\\d{4})(\\d{2})(\\d{2})(\\d{3})");
            Matcher matcher = pattern.matcher(card);
            String replaced = matcher.replaceAll(" $1 $2 $3 $4 $5/$6 ($7) ");
            card = replaced;
            this.name = name;
            this.surname = surname;
            this.age = age;
            this.card = card;
            this.pin = pin;

        } else {
            System.out.println("Creation error");
        }
    }


    @Override
    public String toString() {
        return "BankAccount{ " +
                "name= '" + name + '\'' +
                ", surname= '" + surname + '\'' +
                ", card= '" + card + '\'' +
                ", age= " + age +
                ", CompletePurchases= " + CompletePurchases +
                ", balance= " + balance +
                ", History= " + History +
                '}';
    }


    public void TransferToAnotherUser(BankAccount FromWhichBankAccount, BankAccount ToWhichBankAccount, double HowMuch) {
        if (HowMuch <= 0 && HowMuch >= 75001) {
            System.out.println("Unavailable number. Contact the bank directly!");
        } else {

            double HowMuch2 = (HowMuch * (commission));
            if (HowMuch2 <= FromWhichBankAccount.balance) {
                System.out.println("Are you sure you want to top up the balance " + ToWhichBankAccount.name + " and commission(10%) on the: " + HowMuch2 + "?" +
                        "\n Enter \"Yes\" or \"No\"");
                Scanner scanner = new Scanner(System.in);
                String answer = scanner.nextLine();
                if (answer.equals("Yes")) {
                    System.out.println("Balance before replenishment: " + ToWhichBankAccount.balance);
                    System.out.println("Balance " + ToWhichBankAccount.name + " is charged: " + HowMuch2);
                    ToWhichBankAccount.balance += HowMuch2;
                    System.out.println("Balance after replenishment: " + ToWhichBankAccount.balance);
                    ToWhichBankAccount.History += "\nTopped up balance with " + HowMuch2 + ";";
                    FromWhichBankAccount.History += "\nTook off balance on " + HowMuch2 + ";";

                } else if (answer.equals("No")) {
                    scanner.close();
                } else {
                    scanner.close();
                }
            } else {
                System.out.println("There is no specified amount on the account: " + HowMuch2);
                System.out.println("Balance :" + FromWhichBankAccount.balance);
            }

        }
    }

    public void TopUpABankAccountOnline(BankAccount bankAccount, double HowMuch) {
        if (HowMuch <= 0 && HowMuch >= 75_001) {
            System.out.println("Unavailable number. Contact the bank directly!");
        } else {
            double HowMuch2 = (HowMuch * (commission));
            System.out.println("Are you sure you want to top up the balance and commission(10%) on the: " + HowMuch2 + "?" +
                    "\n Enter \"Yes\" or \"No\"");
            Scanner scanner = new Scanner(System.in);
            String answer = scanner.nextLine();
            if (answer.equals("Yes")) {
                System.out.println("Balance before replenishment: " + bankAccount.balance);
                System.out.println("The balance is charged: " + HowMuch2);
                bankAccount.balance += HowMuch2;
                System.out.println("Balance after replenishment: " + bankAccount.balance);
                bankAccount.History += "\nYou topped up your balance with " + HowMuch2 + ";";

            } else if (answer.equals("No")) {
                scanner.close();
            } else {
                scanner.close();
            }
        }
    }

    public void WithdrawFromBankAccountOnline(BankAccount bankAccount, double HowMuch) {
        if (HowMuch <= 0 && HowMuch >= 75_001) {
            System.out.println("Unavailable number. Contact the bank directly!");
        } else {
            double HowMuch2 = (HowMuch * (commission));
            if (HowMuch2 <= bankAccount.balance) {
                System.out.println("Are you sure you want to withdraw from your balance and commission(10%): " + (HowMuch2 * (commission)) + "?" +
                        "\n Enter \"Yes\" or \"No\"");
                Scanner scanner = new Scanner(System.in);
                String answer = scanner.nextLine();
                if (answer.equals("Yes")) {
                    System.out.println("Balance before withdrawal: " + bankAccount.balance);
                    System.out.println("Removed from balance: " + HowMuch2);
                    bankAccount.balance -= HowMuch2;
                    System.out.println("Balance after withdrawal: " + bankAccount.balance);
                    bankAccount.History += "\nYou took off your balance on " + HowMuch2 + ";";
                } else if (answer.equals("No")) {
                    scanner.close();
                } else {
                    scanner.close();
                }
            } else {
                System.out.println("There is no specified amount on the account: " + HowMuch2);
                System.out.println("Balance :" + bankAccount.balance);
            }
        }
    }


    public void MoneyTransfer(BankAccount bankAccount) {

        System.out.println("What would you like to buy? : " +
                "\n Enter \"Water (2$)\" or \"Bread (2$)\" or \"3 Bananas( 2$)\"  or \"3 Apple (2$)\" or \"Sandwich (2$)\" ");

        Scanner scanner = new Scanner(System.in);
        String answer = scanner.nextLine();

        if (bankAccount.balance >= 2) {

            if (answer.equals("Water")) {
                System.out.println("Balance before withdrawal: " + bankAccount.balance);
                System.out.println("Removed from balance: " + cost + "(Water)");
                bankAccount.balance -= cost;
                System.out.println("Balance after withdrawal: " + bankAccount.balance);
                bankAccount.History += "\nYou took off your balance on " + cost + "$(Water);";
                CompletePurchases++;
            } else if (answer.equals("Bread")) {
                System.out.println("Balance before withdrawal: " + bankAccount.balance);
                System.out.println("Removed from balance: " + cost + "$(Bread)");
                bankAccount.balance -= cost;
                System.out.println("Balance after withdrawal: " + bankAccount.balance);
                bankAccount.History += "\nYou took off your balance on " + cost + "$(Bread);";
                CompletePurchases++;
            } else if (answer.equals("Bananas")) {
                System.out.println("Balance before withdrawal: " + bankAccount.balance);
                System.out.println("Removed from balance: " + cost + "$(Bananas)");
                bankAccount.balance -= cost;
                System.out.println("Balance after withdrawal: " + bankAccount.balance);
                bankAccount.History += "\nYou took off your balance on " + cost + "$(3 Bananas);";
                CompletePurchases++;
            } else if (answer.equals("Apple")) {
                System.out.println("Balance before withdrawal: " + bankAccount.balance);
                System.out.println("Removed from balance: " + cost + "$(Apple)");
                bankAccount.balance -= cost;
                System.out.println("Balance after withdrawal: " + bankAccount.balance);
                bankAccount.History += "\nYou took off your balance on " + cost + "$(3 Apple);";
                CompletePurchases++;
            } else if (answer.equals("Sandwich")) {
                System.out.println("Balance before withdrawal: " + bankAccount.balance);
                System.out.println("Removed from balance: " + cost + "$(Sandwich)");
                bankAccount.balance -= cost;
                System.out.println("Balance after withdrawal: " + bankAccount.balance);
                bankAccount.History += "\nYou took off your balance on " + cost + "$(Sandwich);";
                CompletePurchases++;
            } else {
            }

        } else {
            System.out.println("There is no specified amount on the account: " + 2 + "$");
            System.out.println("Balance : " + bankAccount.balance);
        }


    }

    }
