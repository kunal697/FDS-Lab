## Merge the two Linked list and Display.
### first linked list take char as input and second takes integer as input.

```c
 #include <stdio.h>
#include <stdlib.h>

struct node
{
  char ch;
  int data;
  struct node *next;
};

void display(struct node *head, struct node *head2)
{
  struct node *temp = head;
  while (temp != head2)
  {
     
      printf("%c", temp->ch);
   

    temp = temp->next;  
  }
  while(temp!=NULL)
  {
       printf("%d", temp->data);
   

    temp = temp->next;  
  }
}

struct node *merge(struct node *head1, struct node *head2)
{
  struct node *temp = head1;
  while (temp->next != NULL)
  {
    temp = temp->next;
  }
  temp->next = head2;

  return head1;
}

int main()
{
  struct node *head1 = NULL, *temp1, *q,*head2 = NULL, *p, *temp2;

  int num1, num2;
  printf("Enter the size of first linked list : ");
  scanf("%d", &num1);
  printf("Enter the size of second linked list : ");
  scanf("%d", &num2);
  printf("Enter the data in first Linked list  : \n");
  
  for (int i = 0; i < num1; i++)
  {
    if (head1 == NULL)
    {
      head1 = (struct node *)malloc(sizeof(struct node));
      printf("Enter the data in %d node: ", i + 1);
      scanf(" %c", &head1->ch); 
      head1->next = NULL;
      q = head1;
    }
    else
    {
      temp1 = (struct node *)malloc(sizeof(struct node));
      printf("Enter the data in %d node: ", i + 1);
      scanf(" %c", &temp1->ch);  
      temp1->next = NULL;
      q->next = temp1;
      q = temp1;
    }
  }
  printf("Enter the data in second Linked list  : \n");
 
  for (int i = 0; i < num2; i++)
  {
    if (head2 == NULL)
    {
      head2 = (struct node *)malloc(sizeof(struct node));
      printf("Enter the data in %d node: ", i + 1);
      scanf("%d", &head2->data);
      head2->next = NULL;
      p = head2;
    }
    else
    {
      temp2 = (struct node *)malloc(sizeof(struct node));
      printf("Enter the data in %d node: ", i + 1);
      scanf("%d", &temp2->data);
      temp2->next = NULL;
      p->next = temp2;
      p = temp2;
    }
  }

  head1 = merge(head1, head2);
  display(head1, head2);

  return 0;
}
