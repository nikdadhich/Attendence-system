# Attendence-system
This is a simple console-based Attendance Management System built using C++. It demonstrates basic file handling, struct usage, and menu-driven program logic.
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

struct Student {
    int rollNo;
    string name;
};

void addStudent() {
    ofstream file("students.txt", ios::app);
    Student s;
    cout << "Enter Roll No: ";
    cin >> s.rollNo;
    cout << "Enter Name: ";
    cin.ignore();
    getline(cin, s.name);

    file << s.rollNo << "," << s.name << endl;
    file.close();
    cout << "Student added successfully.\n";
}

void markAttendance() {
    ifstream infile("students.txt");
    ofstream outfile("attendance.txt", ios::app);
    string line;
    string status;
    cout << "Marking attendance:\n";
    while (getline(infile, line)) {
        cout << "Is " << line << " present? (P/A): ";
        cin >> status;
        outfile << line << "," << status << endl;
    }
    infile.close();
    outfile.close();
    cout << "Attendance marked successfully.\n";
}

void viewAttendance() {
    ifstream file("attendance.txt");
    string line;
    cout << "Attendance Records:\n";
    while (getline(file, line)) {
        cout << line << endl;
    }
    file.close();
}

int main() {
    int choice;
    do {
        cout << "\n*** Attendance System ***\n";
        cout << "1. Add Student\n";
        cout << "2. Mark Attendance\n";
        cout << "3. View Attendance\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) {
            case 1: addStudent(); break;
            case 2: markAttendance(); break;
            case 3: viewAttendance(); break;
            case 4: cout << "Exiting...\n"; break;
            default: cout << "Invalid choice.\n";
        }
    } while(choice != 4);

    return 0;
}
