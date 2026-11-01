#include <iostream>
#include <string>
#include <cctype>
using namespace std;

// Node structure
struct Node
{
    char data;
    Node* next;
};

// Stack using Singly Linked List
class Stack
{
private:
    Node* top;

public:

    Stack()
    {
        top = NULL;
    }

    // Check whether stack is empty
    bool isEmpty()
    {
        return top == NULL;
    }

    // Push operation
    void push(char value)
    {
        Node* newNode = new Node();

        newNode->data = value;
        newNode->next = top;
        top = newNode;
    }

    // Pop operation
    char pop()
    {
        if (isEmpty())
            return '\0';

        Node* temp = top;
        char value = top->data;

        top = top->next;
        delete temp;

        return value;
    }

    // Return top element
    char peek()
    {
        if (isEmpty())
            return '\0';

        return top->data;
    }
};

// Check operand
bool isOperand(char ch)
{
    return isalnum(ch);
}

// Operator precedence
int precedence(char ch)
{
    if (ch == '^')
        return 3;

    if (ch == '*' || ch == '/')
        return 2;

    if (ch == '+' || ch == '-')
        return 1;

    return 0;
}

// Infix to Postfix conversion
string infixToPostfix(string infix)
{
    Stack s;
    string postfix = "";

    for (int i = 0; i < (int)infix.length(); i++)
    {
        char ch = infix[i];

        if (isOperand(ch))
        {
            postfix += ch;
        }

        else if (ch == '(')
        {
            s.push(ch);
        }

        else if (ch == ')')
        {
            while (!s.isEmpty() && s.peek() != '(')
            {
                postfix += s.pop();
            }

            s.pop();
        }

        else
        {
            while (!s.isEmpty() &&
                   s.peek() != '(' &&
                   precedence(s.peek()) >= precedence(ch))
            {
                postfix += s.pop();
            }

            s.push(ch);
        }
    }

    // Pop remaining operators
    while (!s.isEmpty())
    {
        postfix += s.pop();
    }

    return postfix;
}

// Main function
int main()
{
    string infix;

    cout << "Enter Infix Expression: ";
    cin >> infix;

    cout << "Postfix Expression: "
         << infixToPostfix(infix) << endl;

    return 0;
}