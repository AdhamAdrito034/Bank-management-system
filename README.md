# Bank-management-system

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_ACCOUNTS 100

typedef struct
{
    int accNum;
    char name[50];
    double balance;
} Account;

Account accounts[MAX_ACCOUNTS];
int totalAccounts = 0;

void createAccount()
{
    if (totalAccounts >= MAX_ACCOUNTS)
    {
        printf("Account limit reached!\n");
        return;
    }

    printf("\nEnter Account Number: ");
    scanf("%d", &accounts[totalAccounts].accNum);
    printf("Enter Name: ");
    scanf(" %[^\n]", accounts[totalAccounts].name);
    printf("Enter Initial Balance: ");
    scanf("%lf", &accounts[totalAccounts].balance);
    printf("\nAccount Created Successfully!\n");
    totalAccounts++;
}

Account* findAccount(int accNum)
{
    for (int i = 0; i < totalAccounts; i++)
    {
        if (accounts[i].accNum == accNum)
            return &accounts[i];
    }
    return NULL;
}

void deposit()
{
    int accNum;
    double amount;
    printf("\nEnter Account Number: ");
    scanf("%d", &accNum);

    Account* acc = findAccount(accNum);
    if (!acc)
    {
        printf("\nAccount Not Found!\n");
        return;
    }

    printf("Enter Deposit Amount: ");
    scanf("%lf", &amount);
    if (amount <= 0)
    {
        printf("\nInvalid Amount!\n");
        return;
    }

    acc->balance += amount;
    printf("\nDeposit Successful! \n\nNew Balance: %.2f\n", acc->balance);
}

void withdraw()
{
    int accNum;
    double amount;
    printf("\nEnter Account Number: ");
    scanf("%d", &accNum);

    Account* acc = findAccount(accNum);
    if (!acc)
    {
        printf("\nAccount Not Found!\n");
        return;
    }

    printf("Enter Withdrawal Amount: ");
    scanf("%lf", &amount);
    if (amount <= 0 || amount > acc->balance)
    {
        printf("\nInvalid or Insufficient Funds!\n");
        return;
    }

    acc->balance -= amount;
    printf("\nWithdrawal Successful! \n\nCurrent Balance: %.2f\n", acc->balance);
}

void displayAccounts()
{
    if (totalAccounts == 0)
    {
        printf("\nNo Accounts Available!\n");
        return;
    }

    printf("\nAccounts Details:\n");
    for (int i = 0; i < totalAccounts; i++)
    {

        printf("\n=====================================\n");
        printf("            Account Details          \n");
        printf("=====================================\n");
        printf("\nAccount Number: %d\nName: %s\nBalance: %.2f\n",
               accounts[i].accNum, accounts[i].name, accounts[i].balance);
    }
}

void menu()
{
    int choice;
    while (1)
    {
        printf("\n       Welcome to \n");
        printf("United Commercial Bank Ltd.\n");
        printf("\n1. Create Account\n2. Deposit Money\n3. Withdraw Money\n4. Accounts Details\n5. Exit\n\nEnter choice: ");
        scanf("%d", &choice);

        switch (choice)
        {
        case 1:
            createAccount();
            break;
        case 2:
            deposit();
            break;
        case 3:
            withdraw();
            break;
        case 4:
            displayAccounts();
            break;
        case 5:
            printf("\nThank you for your trust in United Commercial Bank.\n     Goodbye!\n");
            exit(0);
        default:
            printf("\nInvalid Choice!\n");
        }
    }
}

int main()
{
    menu();
    return 0;
}
