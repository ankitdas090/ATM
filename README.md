#include <stdio.h>
#include <stdlib.h>

// Global variables for simplicity (in a real app, use structs or files)
float balance = 1000.0;  // Initial balance
int pin = 1234;          // Default PIN

// Function to authenticate user
int authenticate() {
    int enteredPin;
    printf("Enter your PIN: ");
    scanf("%d", &enteredPin);
    if (enteredPin == pin) {
        return 1;  // Success
    } else {
        printf("Invalid PIN. Try again.\n");
        return 0;  // Failure
    }
}

// Function to check balance
void checkBalance() {
    printf("Your current balance is: $%.2f\n", balance);
}

// Function to withdraw money
void withdraw() {
    float amount;
    printf("Enter amount to withdraw: $");
    scanf("%f", &amount);
    if (amount > balance) {
        printf("Insufficient funds!\n");
    } else if (amount <= 0) {
        printf("Invalid amount!\n");
    } else {
        balance -= amount;
        printf("Withdrawal successful. New balance: $%.2f\n", balance);
    }
}

// Function to deposit money
void deposit() {
    float amount;
    printf("Enter amount to deposit: $");
    scanf("%f", &amount);
    if (amount <= 0) {
        printf("Invalid amount!\n");
    } else {
        balance += amount;
        printf("Deposit successful. New balance: $%.2f\n", balance);
    }
}

// Main function
int main() {
    int choice;
    if (!authenticate()) {
        return 1;  // Exit if authentication fails
    }
    
    while (1) {
        printf("\nATM Menu:\n");
        printf("1. Check Balance\n");
        printf("2. Withdraw Money\n");
        printf("3. Deposit Money\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        
        switch (choice) {
            case 1:
                checkBalance();
                break;
            case 2:
                withdraw();
                break;
            case 3:
                deposit();
                break;
            case 4:
                printf("Thank you for using the ATM. Goodbye!\n");
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }
    return 0;
}
