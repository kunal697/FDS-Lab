## Circular Linked  List : 
```cpp

#include <iostream>
using namespace std;

class node
{
public:
    int data;
    node* next;
    node* prev;
};

node* deletenode(node* head, int data)
{
    if (head == nullptr)
    {
        cout << "List is empty" << endl;
        return head;
    }
    node* current = head;

   if (head->data == data)
    {
                head = head->next;

            delete current;
            return head;
    }
    do
    {
        if (current->data == data)
        {
       
                current->prev->next = current->next;
                current->next->prev = current->prev;

            delete current;
            return head;
        }
        current = current->next;
    } while (current != head);

    cout << "Value not found in the list" << endl;
    return head;
}

node* add(node* head, int data, int position)
{
    node* temp = new node();
    temp->data = data;

    if (position == 0 || head == nullptr)
    {
        if (head != nullptr)
        {
            temp->next = head;
            temp->prev = head->prev;
            head->prev->next = temp;
            head->prev = temp;
        }
        head = temp;
    }
    else
    {
        node* current = head;
        int count = 1;

        while (count < position && current->next != head)
        {
            current = current->next;
            count++;
        }

        temp->prev = current;
        temp->next = current->next;

        if (current->next != head)
            current->next->prev = temp;

        current->next = temp;
    }

    return head;
}

void display(node* head)
{
    if (head == nullptr)
    {
        cout << "List is empty." << endl;
        return;
    }
int x =1;
    node* current = head;
  do
  {
    cout<<"Data in "<<x<<" node : "<<current->data;
    x++;
    cout<<endl;
    current = current->next;
    
  } while(current!=head);
}

int main()
{
    int choice, value, number;
    node* head = nullptr;
    node* temp = nullptr;
    node* p = nullptr;

    cout << "Enter the number of nodes: ";
    cin >> number;

    for (int i = 0; i < number; i++)
    {
        if (head == nullptr)
        {
            cout << "Enter data in " << i + 1 << " Node: ";
            head = new node();
            cin >> head->data;
            head->next = head;
            head->prev = head;
            p = head;
        }
        else
        {
            cout << "Enter data in " << i + 1 << " Node: ";
            temp = new node();
            cin >> temp->data;
            temp->next = p;
            temp->prev = p->prev;
            p->prev->next = temp;
            p->prev = temp;
        }
    }

    do
    {
        cout << "\nMenu:\n";
        cout << "1. Add a value\n";
        cout << "2. Delete a value from the list\n";
        cout << "3. Display\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
        case 1:
            cout << "Enter a value to add: ";
            cin >> value;
            int x;
            cout << "Enter the position to add : ";
            cin >> x;
            head = add(head, value, x - 1);
            break;

        case 2:
            cout << "Enter a value to delete: ";
            cin >> value;
            head = deletenode(head, value);
            break;

        case 3:
            cout << "Current list: ";
            display(head);
            break;

        case 4:
            cout << "Exiting program." << endl;
            break;

        default:
            cout << "Invalid choice" << endl;
        }
    } while (choice != 4);

    return 0;
}
