#include <stdio.h>
#include <stdlib.h>


int userPin = 1234;
float balance = 5000.00;


int login();                                            
void menu();
void checkBalance();
void depositMoney();
void withdrawMoney();
void changePIN();

int main() {
    printf("===================================\n");
    printf("         WELCOME TO ATM\n");
    printf("===================================\n");

    if (!login()) {
        printf("\nToo many incorrect attempts! Card blocked.\n");
        return 0;
    }

    menu();
    return 0;
}


int login() {
    int pin, attempts = 0;

    while (attempts < 3) {
        printf("\nEnter your PIN: ");
        scanf("%d", &pin);

        if (pin == userPin) {
            printf("\nLogin Successful!\n");
            return 1;
        } else {
            printf("Incorrect PIN! Try again.\n");
            attempts++;
        }
    }
    return 0;
}


void menu() {
    int choice;

    do {
        printf("\n=========== ATM MENU ===========\n");
        printf("1. Check Balance\n");
        printf("2. Deposit Money\n");
        printf("3. Withdraw Money\n");
        printf("4. Change PIN\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                checkBalance();
                break;
            case 2:
                depositMoney();
                break;
            case 3:
                withdrawMoney();
                break;
            case 4:
                changePIN();
                break;
            case 5:
                printf("\nThank you for using the ATM!\n");
                break;
            default:
                printf("Invalid choice! Please try again.\n");
        }
    } while (choice != 5);
}

void checkBalance() {
    printf("\nYour Available Balance: ₹%.2f\n", balance);
}


void depositMoney() {
    float amount;
    printf("\nEnter amount to deposit: ₹");
    scanf("%f", &amount);

    if (amount <= 0) {
        printf("Invalid amount!\n");
        return;
    }

    balance += amount;
    printf("Amount deposited successfully.\n");
    printf("Updated Balance: ₹%.2f\n", balance);
}


void withdrawMoney() {
    float amount;
    printf("\nEnter amount to withdraw: ₹");
    scanf("%f", &amount);

    if (amount <= 0) {
        printf("Invalid amount!\n");
    } else if (amount > balance) {
        printf("Insufficient balance!\n");
    } else {
        balance -= amount;
        printf("Withdrawal successful.\n");
        printf("Remaining Balance: ₹%.2f\n", balance);
    }
}


void changePIN() {
    int newPin, confirmPin;

    printf("\nEnter new 4-digit PIN: ");
    scanf("%d", &newPin);

    printf("Confirm new PIN: ");
    scanf("%d", &confirmPin);

    if (newPin == confirmPin && newPin >= 1000 && newPin <= 9999) {
        userPin = newPin;
        printf("PIN changed successfully!\n");
    } else {
        printf("PINs do not match or invalid PIN format.\n");
    }
}