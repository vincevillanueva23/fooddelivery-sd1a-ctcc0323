# fooddelivery-sd1a-ctcc0323
import java.util.Scanner;

public class MilkTeaOrderSystem {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Collecting order details
        System.out.println("Welcome to the Milk Tea Ordering System!");
        String customerName = getUserInput("Enter your name: ");
        String flavor = getUserInput("Select milk tea flavor (e.g., Chai): ");
        String size = getUserInput("Select size (e.g., Medium): ");
        boolean withTapioca = getBooleanInput("Do you want tapioca? (yes/no): ");

        // Displaying order details
        displayOrderSummary(customerName, flavor, size, withTapioca);

        // Handling payment
        double totalAmount = getDoubleInput("\nEnter the total amount to pay: $");
        double paymentAmount = getDoubleInput("Enter your payment amount: $");

        // Check if payment is sufficient
        processPayment(totalAmount, paymentAmount);

        scanner.close();
    }

    private static String getUserInput(String prompt) {
        System.out.print(prompt);
        return new Scanner(System.in).nextLine();
    }

    private static boolean getBooleanInput(String prompt) {
        String input = "";
        while (!input.equalsIgnoreCase("yes") && !input.equalsIgnoreCase("no")) {
            input = getUserInput(prompt);
            if (!input.equalsIgnoreCase("yes") && !input.equalsIgnoreCase("no")) {
                System.out.println("Invalid input. Please enter 'yes' or 'no'.");
            }
        }
        return input.equalsIgnoreCase("yes");
    }

    private static double getDoubleInput(String prompt) {
        double value = 0;
        boolean isValid = false;
        while (!isValid) {
            try {
                System.out.print(prompt);
                value = Double.parseDouble(new Scanner(System.in).nextLine());
                isValid = true;
            } catch (NumberFormatException e) {
                System.out.println("Invalid input. Please enter a valid number.");
            }
        }
        return value;
    }

    private static void displayOrderSummary(String customerName, String flavor, String size, boolean withTapioca) {
        System.out.println("\nOrder Summary:");
        System.out.println("Customer: " + customerName);
        System.out.println("Flavor: " + flavor);
        System.out.println("Size: " + size);
        System.out.println("Tapioca: " + (withTapioca ? "Yes" : "No"));
    }

    private static void processPayment(double totalAmount, double paymentAmount) {
        if (paymentAmount >= totalAmount) {
            double change = paymentAmount - totalAmount;
            System.out.println("Payment successful! Your change: $" + change);
        } else {
            System.out.println("Insufficient payment. Please try again.");
        }
    }
}
