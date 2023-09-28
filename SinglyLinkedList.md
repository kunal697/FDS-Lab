## Singly Linked List

```cpp
#include<iostream>
using namespace std;

class node
{
  public :
  int data;
  node *next;

};

node* deletenode(node* head, int data)
{
  node *current = head,*prev;
 if(data==head->data)
 {
   head = head->next;
   delete current;

   return head;
 }

  while(current->data!=data)
  {
    prev = current;
    current = current->next;

  }
  prev->next = current->next;
  delete current;
  return head;
}

node* add(node *head, int data, int position)
{
  node *temp = nullptr;
  node *current = head;
  temp = new node();
  if(position == 0 || position == 1)
  {
    temp->data = data;
    temp->next=head;
    head = temp;
  }
  
  while(position!=1 && current->next!=nullptr)
  {
     current = current->next;
     position--;
  }
  temp->next = current->next;
  current->next = temp;

  return head;
}

void display(node *head)
{
  while(head!=nullptr)
  {
    cout<<head->data<<"->";
    head = head->next;
  }
  cout<<"nullptr";
}

int main() {
  
    int choice, value,number;
    node *head=nullptr,*temp=nullptr,*prev=nullptr;
   cout<<"Enter the number of nodes :";
   cin>>number;
   for(int i=0;i<number;i++)
   {
    if(head==nullptr)
    {
      cout<<"Enter data in "<<i+1<<"Node : ";
      head = new node();
      cin>>head->data;
      head->next = nullptr;
      prev=head;
    }
    else{
      cout<<"Enter data in "<<i+1<<"Node : ";
      temp = new node();
      cin>>temp->data;
      temp->next=nullptr;
      prev->next=temp;
      prev = temp;
    }
   }
    do {
        cout << "\nMenu:\n";
        cout << "1. Add a value to the end of the list\n";
        cout << "2. Delete a value from the list\n";
        cout << "3. Display the list\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter a value to add: ";
                cin >> value;
                head  = add(head,value,1);
                break;

            case 2:
                cout << "Enter a value to delete: ";
                cin >> value;
                head = deletenode(head,value);
                break;

            case 3:
                cout << "Current list: ";
                display(head);
                break;

            case 4:
                cout << "Exiting program." << endl;
                break;

            default:
                cout << "Invalid choice. Please try again." << endl;
        }
    } while (choice != 4);

    return 0;
}
