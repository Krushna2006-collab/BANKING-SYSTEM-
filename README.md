#include <iostream>
#include <map>
using namespace std;
class Account {
private:
int accNo;
string name;
double balance;
double dailyWithdrawn;
const double DAILY_LIMIT = 20000;
public:
Account() {}
Account(int accNo, string name, double balance) {
this->accNo = accNo;
this->name = name;
this->balance = balance;
this->dailyWithdrawn = 0;
}
void deposit(double amount) {
if (amount > 0) {
balance += amount;
cout << "Deposit successful!\n";
} else {
cout << "Invalid amount!\n";
}
}
void withdraw(double amount) {
if (amount <= 0) {
cout << "Invalid amount!\n";
} else if (amount > balance) {
cout << "Insufficient balance!\n";
} else if (dailyWithdrawn + amount > DAILY_LIMIT) {
cout << "Daily limit exceeded!\n";
} else {
balance -= amount;
dailyWithdrawn += amount;
cout << "Withdrawal successful!\n";
}
}
void showBalance() {
cout << "Balance: " << balance << endl;
}
void display() {
cout << "Account No: " << accNo << endl;
cout << "Name: " << name << endl;
cout << "Balance: " << balance << endl;
}
};
int main() {
map<int, Account> accounts;
int accCounter = 1001;
int choice, accNo;
string name;
double amount;
while (true) {
cout << "\n1.Create\n2.Deposit\n3.Withdraw\n4.Check Balance\n5.Display Info\n6.Exit\n";
cin >> choice;
switch (choice) {
case 1:
cout << "Enter name: ";
cin >> name;
cout << "Enter initial deposit: ";
cin >> amount;
accounts[accCounter] = Account(accCounter, name, amount);
cout << "Account created! Acc No: " << accCounter++ << endl;
break;
case 2:
cout << "Enter account number: ";
cin >> accNo;
cout << "Enter amount: ";
cin >> amount;
accounts[accNo].deposit(amount);
break;
case 3:
cout << "Enter account number: ";
cin >> accNo;
cout << "Enter amount: ";
cin >> amount;
accounts[accNo].withdraw(amount);
break;
case 4:
cout << "Enter account number: ";
cin >> accNo;
accounts[accNo].showBalance();
break;
case 5:
cout << "Enter account number: ";
cin >> accNo;
accounts[accNo].display();
break;
case 6:
return 0;
default:
cout << "Invalid choice!\n";
}
}
}
