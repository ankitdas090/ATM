#include <stdio.h>
#include <stdlib.h>

// Initial user data (simulate stored data)
int userPin = 1234;
float balance = 5000.00;

// Function declarations
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

// Login function
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

// ATM Menu
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

// Feature 1: Check Balance
void checkBalance() {
    printf("\nYour Available Balance: ₹%.2f\n", balance);
}

// Feature 2: Deposit Money
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

// Feature 3: Withdraw Money
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

// Feature 4: Change PIN
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
}#include <stdio.h>
#include <stdlib.h>

float bal = 1000;
int pin = 1234;

int main() {
    int p, ch; float amt;
    printf("Enter PIN: "); scanf("%d", &p);
    if (p != pin){ return printf("Wrong PIN!\n"), 0;}

    while (1) {
        printf("\n1.Balance 2.Withdraw 3.Deposit 4.Exit\nChoice: ");
        scanf("%d", &ch);
        if (ch == 1) printf("Balance: $%.2f\n", bal);
        else if (ch == 2) {
            printf("Withdraw: $"); scanf("%f", &amt);
            if (amt > 0 && amt <= bal) bal -= amt, printf("New: $%.2f\n", bal);
            else printf("Invalid!\n");
        }
        else if (ch == 3) {
            printf("Deposit: $"); scanf("%f", &amt);
            if (amt > 0) bal += amt, printf("New: $%.2f\n", bal);
            else printf("Invalid!\n");
        }
        else if (ch == 4) return printf("Bye!\n"), 0;
        else printf("Invalid choice!\n");
    }
}