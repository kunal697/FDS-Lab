## Doubly Linked List : 

```cpp
#include <iostream>
using namespace std;

class node
{
public:
    int data;
    node* next;
    node* prev;

    node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

node* deletenode(node* head, int data)
{
    node* current = head;
     
    if (head == nullptr)
    {
        cout << "List is empty" << endl;
        return head;
    }

  while(current->data!=data && current->next!=nullptr)
  {
     current = current->next;
  }
  if(current==head)
  {
    head= head->next;
    delete current;
    return head;
  }
  current->prev= current->next;
   delete current;
    return head;
}

node* add(node* head, int data, int position)
{
    node* temp = new node(data);

    if (position == 0 || head == nullptr)
    {
        if (head != nullptr)
        {
            head->prev = temp;
            temp->next = head;
        }
        head = temp;
        return head;
    }

    node* current = head;
    int count = 1;

    while (count < position && current->next != nullptr)
    {
        current = current->next;
        count++;
    }

    temp->prev = current;
    temp->next = current->next;

    if (current->next != nullptr)
        current->next->prev = temp;

    current->next = temp;

    return head;
}

void display(node* head)
{
    while (head != nullptr)
    {
        cout << head->data << " <-> ";
        head = head->next;
    }
    cout << "nullptr" << endl;
}

int main()
{
    int choice, value, number;
    node* head = nullptr;
    node* temp = nullptr;
    node *p = nullptr;

    cout << "Enter the number of nodes: ";
    cin >> number;

    for (int i = 0; i < number; i++)
    {
        if (head == nullptr)
        {
            cout << "Enter data in " << i + 1 << " Node: ";
            head = new node(0);
            cin >> head->data;
            head->next = nullptr;
            head->prev = nullptr;
            p = head;
        }
        else
        {
            cout << "Enter data in " << i + 1 << " Node: ";
            temp = new node(0);
            cin >> temp->data;
            temp->next = nullptr;
            temp->prev = p;
            p->next = temp;
            p = temp;
        }
    }

   

    do
    {
        cout << "\nMenu:\n";
        cout << "1. Add a value \n";
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
            cout<<"Enter the position to add : ";
            cin>>x;
            head = add(head, value, x-1);
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
