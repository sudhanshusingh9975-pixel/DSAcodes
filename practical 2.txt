#include <iostream>
#include <cstdlib>
#include <cstring>
using namespace std;

struct Student
{
    int id;
    char name[50];
    float cgpa;
};

Student *list = NULL;
int count = 0;

// Add Student
void addStudent()
{
    if (list == NULL)
        list = (Student *)malloc(sizeof(Student));
    else
        list = (Student *)realloc(list, (count + 1) * sizeof(Student));

    if (list == NULL)
    {
        cout << "Memory not available!" << endl;
        exit(1);
    }

    cout << "Enter ID: ";
    cin >> list[count].id;

    cout << "Enter Name: ";
    cin >> list[count].name;

    cout << "Enter CGPA: ";
    cin >> list[count].cgpa;

    count++;

    cout << "Student added!" << endl;
}

// Display Students
void displayAll()
{
    if (count == 0)
    {
        cout << "No students to show." << endl;
        return;
    }

    cout << "\nID\tName\tCGPA" << endl;

    for (int i = 0; i < count; i++)
    {
        cout << list[i].id << "\t"
             << list[i].name << "\t"
             << list[i].cgpa << endl;
    }
}

// Bubble Sort by Name
void bubbleSortByName()
{
    for (int i = 0; i < count - 1; i++)
    {
        for (int j = 0; j < count - i - 1; j++)
        {
            if (strcmp(list[j].name, list[j + 1].name) > 0)
            {
                Student temp = list[j];
                list[j] = list[j + 1];
                list[j + 1] = temp;
            }
        }
    }

    cout << "Sorted by Name (A to Z)." << endl;
}

// Selection Sort by CGPA
void selectionSortByCgpa(int choice)
{
    for (int i = 0; i < count - 1; i++)
    {
        int pos = i;

        for (int j = i + 1; j < count; j++)
        {
            if (choice == 1 && list[j].cgpa < list[pos].cgpa)
                pos = j;

            if (choice == 2 && list[j].cgpa > list[pos].cgpa)
                pos = j;
        }

        Student temp = list[i];
        list[i] = list[pos];
        list[pos] = temp;
    }

    if (choice == 1)
        cout << "Sorted by CGPA (Ascending)." << endl;
    else
        cout << "Sorted by CGPA (Descending)." << endl;
}

// Main Function
int main()
{
    int choice;

    do
    {
        cout << "\n===== STUDENT DATABASE =====" << endl;
        cout << "1. Add Student" << endl;
        cout << "2. Display All Students" << endl;
        cout << "3. Bubble Sort by Name" << endl;
        cout << "4. Selection Sort by CGPA Ascending" << endl;
        cout << "5. Selection Sort by CGPA Descending" << endl;
        cout << "0. Exit" << endl;

        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                addStudent();
                break;

            case 2:
                displayAll();
                break;

            case 3:
                bubbleSortByName();
                displayAll();
                break;

            case 4:
                selectionSortByCgpa(1);
                displayAll();
                break;

            case 5:
                selectionSortByCgpa(2);
                displayAll();
                break;

            case 0:
                cout << "Goodbye!" << endl;
                break;

            default:
                cout << "Invalid choice!" << endl;
        }

    } while (choice != 0);

    free(list);

    return 0;
}