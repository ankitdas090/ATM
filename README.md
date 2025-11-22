#include <stdio.h>
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