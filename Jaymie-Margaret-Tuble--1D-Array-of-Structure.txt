#include <iostream>
#include <string>
#include <iomanip>
#include <algorithm> 
using namespace std;

struct Student {
    int id;
    string firstName;
    string lastName;
    string course;
    float gpa;
};

void addStudent(Student students[], int &count);
void editStudent(Student students[], int count);
void deleteStudent(Student students[], int &count);
void viewStudents(Student students[], int count);
void displayMenu();
void sortAlphabetically(Student students[], int count);
void sortByGPA(Student students[], int count);

int main() {
    const int MAX_STUDENTS = 100; 
    Student students[MAX_STUDENTS]; 
    int count = 0;
    int option;

    do {
        displayMenu();
        cout << "Select option: ";
        cin >> option;

        switch (option) {
            case 1:
                addStudent(students, count);
                break;
            case 2:
                editStudent(students, count);
                break;
            case 3:
                deleteStudent(students, count);
                break;
            case 4:
                viewStudents(students, count);
                break;
            case 5:
                cout << "Exiting program." << endl;
                break;
            default:
                cout << "Invalid option! Please try again." << endl;
        }

    } while (option != 5);

    return 0;
}

void displayMenu() {
    cout << "\n--- Menu ---" << endl;
    cout << "[1] Add Student" << endl;
    cout << "[2] Edit Student" << endl;
    cout << "[3] Delete Student" << endl;
    cout << "[4] View Student" << endl;
    cout << "[5] Exit Program" << endl;
}

void addStudent(Student students[], int &count) {
    if (count < 100) {
        cout << "Enter Student ID: ";
        cin >> students[count].id;

        for (int i = 0; i < count; i++) {
            if (students[i].id == students[count].id) {
                cout << "Duplicate ID found! Student not added." << endl;
                return;
            }
        }

        cout << "Enter First Name: ";
        cin >> students[count].firstName;
        cout << "Enter Last Name: ";
        cin >> students[count].lastName;
        cout << "Enter Course: ";
        cin >> students[count].course;
        cout << "Enter Previous Semestral GPA: ";
        cin >> students[count].gpa;

        count++;
        cout << "Student added successfully!" << endl;
    } else {
        cout << "Student record is full!" << endl;
    }
}

void editStudent(Student students[], int count) {
    int id, foundIndex = -1;
    cout << "Enter Student ID to edit: ";
    cin >> id;

    for (int i = 0; i < count; i++) {
        if (students[i].id == id) {
            foundIndex = i;
            break;
        }
    }

    if (foundIndex != -1) {
        cout << "Editing Student: " << students[foundIndex].firstName << " " << students[foundIndex].lastName << endl;
        cout << "Enter new First Name: ";
        cin >> students[foundIndex].firstName;
        cout << "Enter new Last Name: ";
        cin >> students[foundIndex].lastName;
        cout << "Enter new Course: ";
        cin >> students[foundIndex].course;
        cout << "Enter new Previous Semestral GPA: ";
        cin >> students[foundIndex].gpa;

        cout << "Student data updated successfully!" << endl;
    } else {
        cout << "No student record found with ID " << id << endl;
    }
}

void deleteStudent(Student students[], int &count) {
    int id, foundIndex = -1;
    cout << "Enter Student ID to delete: ";
    cin >> id;

    for (int i = 0; i < count; i++) {
        if (students[i].id == id) {
            foundIndex = i;
            break;
        }
    }

    if (foundIndex != -1) {
        for (int i = foundIndex; i < count - 1; i++) {
            students[i] = students[i + 1];
        }
        count--;
        cout << "Student record deleted successfully!" << endl;
    } else {
        cout << "No student record found with ID " << id << endl;
    }
}

void viewStudents(Student students[], int count) {
    if (count == 0) {
        cout << "No student records available!" << endl;
        return;
    }

    int sortOption;
    cout << "How would you like to sort the records?" << endl;
    cout << "[1] Alphabetically" << endl;
    cout << "[2] By GPA" << endl;
    cout << "Select option: ";
    cin >> sortOption;

    if (sortOption == 1) {
        sortAlphabetically(students, count);
    } else if (sortOption == 2) {
        sortByGPA(students, count);
    } else {
        cout << "Invalid option!" << endl;
        return;
    }

    cout << "\n--- Student Records ---" << endl;
    for (int i = 0; i < count; i++) {
        cout << "ID: " << students[i].id << endl;
        cout << "Name: " << students[i].firstName << " " << students[i].lastName << endl;
        cout << "Course: " << students[i].course << endl;
        cout << "Previous Semestral GPA: " << students[i].gpa << endl;
        cout << "--------------------" << endl;
    }
}

void sortAlphabetically(Student students[], int count) {
    sort(students, students + count, [](const Student &a, const Student &b) {
        return a.lastName < b.lastName || (a.lastName == b.lastName && a.firstName < b.firstName);
    });
}

void sortByGPA(Student students[], int count) {
    sort(students, students + count, [](const Student &a, const Student &b) {
        return a.gpa < b.gpa;
    });
}