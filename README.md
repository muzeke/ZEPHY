# CODE

```c++
#include <iostream>
#include <vector>
#include <string>
#include <limits>

#ifdef _WIN32
#include <windows.h>
#else
#include <cstdlib>
#endif

using namespace std;

struct Account {
    string name;
    int balance;
};

void displayMenu() {
    cout << "\n1. Add Account\n";
    cout << "2. Edit Account\n";
    cout << "3. Delete Account\n";
    cout << "4. Deposit\n";
    cout << "5. Withdraw\n";
    cout << "6. Display All Accounts\n";
    cout << "7. Exit\n";
    cout << "Enter your choice: ";
}

void addAccount(vector<Account>& accounts) {
    Account newAccount;
    cout << "Enter name: ";
    cin >> newAccount.name;
    cout << "Enter initial balance: ";
    cin >> newAccount.balance;
    accounts.push_back(newAccount);
    cout << "Account added successfully.\n";
}

void displayAllAccounts(const vector<Account>& accounts) {
    cout << "\nAll Accounts:\n";
    int count = 1;
    for (const auto& acc : accounts) {
        cout << count << ". Name: " << acc.name << ", Balance: " << acc.balance << "\n";
        count++;
    }
}

void editAccount(vector<Account>& accounts) {
    displayAllAccounts(accounts);
    int choice;
    cout << "Enter the number of the account to edit: ";
    cin >> choice;
    if (choice >= 1 && choice <= accounts.size()) {
        cout << "Enter new name: ";
        cin >> accounts[choice - 1].name;
        cout << "Account updated successfully.\n";
    } else {
        cout << "Invalid selection.\n";
    }
}

void deleteAccount(vector<Account>& accounts) {
    displayAllAccounts(accounts);
    int choice;
    cout << "Enter the number of the account to delete: ";
    cin >> choice;
    if (choice >= 1 && choice <= accounts.size()) {
        accounts.erase(accounts.begin() + choice - 1);
        cout << "Account deleted successfully.\n";
    } else {
        cout << "Invalid selection.\n";
    }
}

void deposit(vector<Account>& accounts) {
    displayAllAccounts(accounts);
    int choice;
    cout << "Enter the number of the account to deposit into: ";
    cin >> choice;
    if (choice >= 1 && choice <= accounts.size()) {
        int amount;
        cout << "Enter the amount to deposit: ";
        cin >> amount;
        accounts[choice - 1].balance += amount;
        cout << "Deposit successful.\n";
    } else {
        cout << "Invalid selection.\n";
    }
}

void withdraw(vector<Account>& accounts) {
    displayAllAccounts(accounts);
    int choice;
    cout << "Enter the number of the account to withdraw from: ";
    cin >> choice;
    if (choice >= 1 && choice <= accounts.size()) {
        int amount;
        cout << "Enter the amount to withdraw: ";
        cin >> amount;
        if (amount <= accounts[choice - 1].balance) {
            accounts[choice - 1].balance -= amount;
            cout << "Withdrawal successful.\n";
        } else {
            cout << "Insufficient funds.\n";
        }
    } else {
        cout << "Invalid selection.\n";
    }
}

int main() {
    vector<Account> accounts;
    int choice;

    do {
        displayMenu();
        if (!(cin >> choice)) {
            cin.clear();  // Clear error flags
            cin.ignore(numeric_limits<streamsize>::max(), '\n');  // Discard invalid input
            cout << "Error: Please enter a number.\n";
            continue;  // Skip to the next iteration of the loop
        }

        switch (choice) {
            case 1:
                addAccount(accounts);
                break;
            case 2:
                editAccount(accounts);
                break;
            case 3:
                deleteAccount(accounts);
                break;
            case 4:
                deposit(accounts);
                break;
            case 5:
                withdraw(accounts);
                break;
            case 6:
                displayAllAccounts(accounts);
                break;
            case 7:
                cout << "Exiting program.\n";
                break;
            default:
                cout << "Error: Please enter a number between 1 and 8.\n";
        }
    } while (choice != 7);

    return 0;
}

```

## Explanation

## C++ Account Management System

This C++ program implements a simple account management system where users can perform various operations on accounts such as adding, editing, deleting, depositing, withdrawing, and displaying all accounts. Below is an explanation of each component of the code:

### Libraries
- `iostream`: Input/output stream library for handling input/output operations.
- `vector`: Dynamic array container from the Standard Template Library (STL) used to store accounts.
- `string`: String class from the STL for handling string data.
- `limits`: Header for handling limits of various data types.
- `windows.h` (Windows only): Header file for Windows-specific functions like clearing the screen.
- `cstdlib` (Unix/Linux): Header for standard library functions like clearing the screen.

### Struct Account
- Defines a structure `Account` with two members: `name` (string) for account holder's name and `balance` (integer) for account balance.

### Function `displayMenu()`
- Displays the menu options for the user to choose from:
  1. Add Account
  2. Edit Account
  3. Delete Account
  4. Deposit
  5. Withdraw
  6. Display All Accounts
  7. Exit
  8. Clear Terminal (Windows: `cls`, Unix/Linux: `clear`)

### Function `addAccount()`
- Prompts the user to enter the name and initial balance for a new account, then adds it to the `accounts` vector.

### Function `displayAllAccounts()`
- Displays all accounts stored in the `accounts` vector along with their names and balances.

### Functions for Account Operations
1. **Edit Account (`editAccount()`):**
   - Displays all accounts and prompts the user to select an account to edit by its number.
   - Allows the user to update the name of the selected account.

2. **Delete Account (`deleteAccount()`):**
   - Displays all accounts and prompts the user to select an account to delete by its number.
   - Deletes the selected account from the `accounts` vector.

3. **Deposit (`deposit()`):**
   - Displays all accounts and prompts the user to select an account to deposit into by its number.
   - Asks the user to enter the amount to deposit and adds it to the selected account's balance.

4. **Withdraw (`withdraw()`):**
   - Displays all accounts and prompts the user to select an account to withdraw from by its number.
   - Asks the user to enter the amount to withdraw and deducts it from the selected account's balance if sufficient funds are available.

### Function `main()`
- Initializes the `accounts` vector and handles the main menu loop for user interaction.
- Calls the respective functions based on the user's menu choice.
- Handles input validation and error messages for invalid input.

### Cross-Platform Clear Screen
- Uses conditional compilation (`#ifdef _WIN32`) to include appropriate header files for clearing the screen based on the operating system (Windows or Unix/Linux).

### Error Handling
- Checks for invalid input (non-numeric) and clears the input buffer to prevent infinite loops.
- Displays error messages for invalid menu choices and selection of non-existing accounts.

### Loop and Exit
- Loops through the menu options until the user chooses to exit (`7. Exit`).
- Upon exit, displays "Exiting program." and terminates the application.

---

