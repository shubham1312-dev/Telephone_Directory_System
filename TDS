#include <iostream>
#include <fstream>
#include <string>
using namespace std;

class stud {
public:
    string name;
    string address;
    unsigned int ph_no;

    void get();
    void show();
    void modify();
};

void stud::get() {
    cout << "\nEnter name: ";
    cin.ignore();
    getline(cin, name);

    cout << "Enter address: ";
    getline(cin, address);

    cout << "Enter phone number: ";
    cin >> ph_no;
}

void stud::show() {
    cout << "\nNAME      : " << name << "\n";
    cout << "ADDRESS   : " << address << "\n";
    cout << "PHONE NO  : " << ph_no << "\n";
}

void stud::modify() {
    cout << "\nCurrent details:\n";
    show();

    cout << "\nEnter new name: ";
    cin.ignore();
    getline(cin, name);

    cout << "Enter new address: ";
    getline(cin, address);

    cout << "Enter new phone number: ";
    cin >> ph_no;
}

int main() {
    char pass[] = "RPV";
    char ppass[20];
    stud s;
    int choice;

    cout << "TELEPHONE DIRECTORY SYSTEM\n";

    while (true) {
        cout << "\n1. Add Record\n";
        cout << "2. Show All Records\n";
        cout << "3. Search Record\n";
        cout << "4. Modify Record\n";
        cout << "5. Delete Record\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1: {
                ofstream fout("rec", ios::binary | ios::app);
                s.get();
                fout.write((char *)&s, sizeof(s));
                fout.close();
                break;
            }
            case 2: {
                ifstream fin("rec", ios::binary);
                while (fin.read((char *)&s, sizeof(s))) {
                    s.show();
                    cout << "\n";
                }
                fin.close();
                break;
            }
            case 3: {
                ifstream fin("rec", ios::binary);
                string searchName;
                bool found = false;
                cout << "Enter name to search: ";
                cin.ignore();
                getline(cin, searchName);
                while (fin.read((char *)&s, sizeof(s))) {
                    if (s.name == searchName) {
                        s.show();
                        found = true;
                        break;
                    }
                }
                fin.close();
                if (!found) {
                    cout << "Record not found\n";
                }
                break;
            }
            case 4: {
                fstream file("rec", ios::binary | ios::in | ios::out);
                unsigned int searchPhone;
                bool found = false;
                cout << "Enter phone number to modify: ";
                cin >> searchPhone;
                while (file.read((char *)&s, sizeof(s))) {
                    if (s.ph_no == searchPhone) {
                        s.modify();
                        file.seekp(-sizeof(s), ios::cur);
                        file.write((char *)&s, sizeof(s));
                        found = true;
                        break;
                    }
                }
                file.close();
                if (!found) {
                    cout << "Record not found\n";
                }
                break;
            }
            case 5: {
                ifstream fin("rec", ios::binary);
                ofstream fout("temp", ios::binary);
                unsigned int deletePhone;
                bool found = false;
                cout << "Enter phone number to delete: ";
                cin >> deletePhone;
                while (fin.read((char *)&s, sizeof(s))) {
                    if (s.ph_no != deletePhone) {
                        fout.write((char *)&s, sizeof(s));
                    } else {
                        found = true;
                    }
                }
                fin.close();
                fout.close();
                remove("rec");
                rename("temp", "rec");
                if (found) {
                    cout << "Record deleted successfully\n";
                } else {
                    cout << "Record not found\n";
                }
                break;
            }
            case 6: {
                cout << "Exiting...\n";
                return 0;
            }
            default:
                cout << "Invalid choice. Please try again.\n";
        }
    }

    return 0;
}
