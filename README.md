# -contact-management-system
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// Contact class
class Contact {
public:
    Contact(string name, string phone, string email) : name_(name), phone_(phone), email_(email) {}

    // Getters
    string getName() const { return name_; }
    string getPhone() const { return phone_; }
    string getEmail() const { return email_; }

    // Setters
    void setName(string name) { name_ = name; }
    void setPhone(string phone) { phone_ = phone; }
    void setEmail(string email) { email_ = email; }

private:
    string name_;
    string phone_;
    string email_;
};

// Contact manager class
class ContactManager {
public:
    void addContact(Contact contact) {
        contacts_.push_back(contact);
    }

    void removeContact(int index) {
        contacts_.erase(contacts_.begin() + index);
    }

    void displayContacts() {
        if (contacts_.empty()) {
            cout << "No contacts found." << endl;
            return;
        }

        for (int i = 0; i < contacts_.size(); i++) {
            cout << i + 1 << ". Name: " << contacts_[i].getName() << ", Phone: " << contacts_[i].getPhone() << ", Email: " << contacts_[i].getEmail() << endl;
        }
    }

    void searchContacts(string keyword) {
        vector<Contact> results;

        for (int i = 0; i < contacts_.size(); i++) {
            if (contacts_[i].getName().find(keyword) != string::npos ||
                contacts_[i].getPhone().find(keyword) != string::npos ||
                contacts_[i].getEmail().find(keyword) != string::npos) {
                results.push_back(contacts_[i]);
            }
        }

        if (results.empty()) {
            cout << "No results found." << endl;
            return;
        }

        for (int i = 0; i < results.size(); i++) {
            cout << i + 1 << ". Name: " << results[i].getName() << ", Phone: " << results[i].getPhone() << ", Email: " << results[i].getEmail() << endl;
        }
    }

private:
    vector<Contact> contacts_;
};

// Main function
int main() {
    ContactManager contactManager;

    while (true) {
        cout << "Welcome to the contact management system. Please choose an option:" << endl;
        cout << "1. Add a contact" << endl;
        cout << "2. Remove a contact" << endl;
        cout << "3. Display all contacts" << endl;
        cout << "4. Search for a contact" << endl;
        cout << "5. Exit" << endl;

        int choice;
        cin >> choice;

        switch (choice) {
            case 1: {
                string name, phone, email;
                cout << "Enter name: ";
                cin >> name;
                cout << "Enter phone: ";
                cin >> phone;
                cout << "Enter email: ";
                cin >> email;
                contactManager.addContact(Contact(name, phone, email));
                break;
            }
            case 2: {
                int index;
                cout << "Enter index of contact to remove: ";
                cin >> index;
                contactManager.removeContact(index - 1);
                break;
            }
            case 3: {
                contactManager.displayContacts();
                break
