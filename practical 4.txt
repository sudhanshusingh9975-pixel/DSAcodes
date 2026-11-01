#include <iostream>
using namespace std;

#define SIZE 5

int queue[SIZE];
int front = -1, rear = -1;

// Insertion
void insert(int value)
{
    if ((front == 0 && rear == SIZE - 1) ||
        (rear + 1 == front))
    {
        cout << "Queue is Full!" << endl;
        return;
    }

    if (front == -1)
        front = 0;

    rear = (rear + 1) % SIZE;
    queue[rear] = value;

    cout << "Inserted: " << value << endl;
}

// Deletion
void Delete()
{
    if (front == -1)
    {
        cout << "Queue is Empty!" << endl;
        return;
    }

    cout << "Deleted: " << queue[front] << endl;

    if (front == rear)
    {
        front = rear = -1;
    }
    else
    {
        front = (front + 1) % SIZE;
    }
}

// Display
void display()
{
    if (front == -1)
    {
        cout << "Queue is Empty!" << endl;
        return;
    }

    cout << "Queue Elements: ";

    int i = front;

    while (true)
    {
        cout << queue[i] << " ";

        if (i == rear)
            break;

        i = (i + 1) % SIZE;
    }

    cout << endl;
}

// Main Function
int main()
{
    int choice, value;

    while (true)
    {
        cout << "\n--- Circular Queue Menu ---" << endl;
        cout << "1. Insertion" << endl;
        cout << "2. Deletion" << endl;
        cout << "3. Display" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                cout << "Enter value: ";
                cin >> value;
                insert(value);
                break;

            case 2:
                Delete();
                break;

            case 3:
                display();
                break;

            default:
                cout << "Invalid Choice!" << endl;
        }
    }

    return 0;
}