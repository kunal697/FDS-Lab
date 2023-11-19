```c
#include<stdio.h>
#include<stdlib.h>

struct queue{
    char name[100];
    int prio;
    struct queue *next;
};

struct queue *front = NULL;
struct queue *rear = NULL;

struct queue *create()
{
    struct queue *newNode = (struct queue*)malloc(sizeof(struct queue));
    printf("Enter The Name : ");
    scanf("%s", newNode->name);
    printf("Enter The priority : ");
    scanf("%d", &(newNode->prio));
    newNode->next = NULL;

    return newNode;
}

void add(){
    struct queue *newNode = create();
    if(front == NULL || newNode->prio < front->prio){
        newNode->next = front;
        front = newNode;
    } else {
        struct queue *current = front;
        while(current->next != NULL && current->next->prio <= newNode->prio) {
            current = current->next;
        }
        newNode->next = current->next;
        current->next = newNode;
    }
}

void display()
{
    struct queue *temp = front;

    while(temp != NULL)
    {
        printf("%s - Priority: %d\n", temp->name, temp->prio);
        temp = temp->next;
    }
}

int main(){
    while(1)
    {
        int ch;
        printf("Enter choice (1: Add, 2: Display, 0: Exit): ");
        scanf("%d", &ch);
        switch (ch)
        {
            case 1: 
                add();
                break;
            case 2: 
                display();
                break;
            case 0:
                exit(0);
            default:
                printf("Invalid choice\n");
        }
    }
    return 0;
}
