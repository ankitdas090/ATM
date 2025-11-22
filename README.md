#include <stdio.h>
#include <stdlib.h>

float balance = 1000.0;
int pin = 1234;

int authenticate() {
    int enteredPin;
    printf("Enter your PIN: ");
    scanf("%d", &enteredPin);
    return (enteredPin == pin);
}

void checkBalance() { printf("Balance: $%.2f\n", balance); }

void withdraw() {
    float amount;
    printf("Withdraw amount: $");
    scanf("%f", &amount);
    if (amount <= 0) printf("Invalid amount!\n");
    else if (amount > balance) printf("Insufficient funds!\n");
    else { balance -= amount; printf("New balance: $%.2f\n", balance); }
}

void deposit() {
    float amount;
    printf("Deposit amount: $");
    scanf("%f", &amount);
    if (amount <= 0) printf("Invalid amount!\n");
    else { balance += amount; printf("New balance: $%.2f\n", balance); }
}

int main() {
    int choice;
    if (!authenticate()) { printf("Invalid PIN!\n"); return 1; }
    while (1) {
        printf("\n1.Check Balance\n2.Withdraw\n3.Deposit\n4.Exit\nChoice: ");
        scanf("%d", &choice);
        switch (choice) {
            case 1: checkBalance(); break;
            case 2: withdraw(); break;
            case 3: deposit(); break;
            case 4: printf("Goodbye!\n"); exit(0);
            default: printf("Invalid choice!\n");
        }
    }
}