## Stack implementation using Array
```cpp
 #include<stdio.h>
#include<stdlib.h>

int stack[100];
int top = -1;  

void push();
void display();
int pop();

int main() {
    while (1) {
        int ch;
        printf("Stack Operations:\n");
        printf("---------------------\n");

        printf("1. Push\n2. Pop\n3. Display\n4. Size of Stack\n5. Exit\n");
        printf("Enter your Operation: ");
        scanf("%d", &ch);

        switch (ch) {
            case 1:
                push();
                break;
            case 2:
                if (top == -1) {
                    printf("Stack is empty. Cannot pop.\n");
                } else {
                    int data = pop();
                    if (data != -1) {
                        printf("Popped data: %d\n", data);
                    }
                }
                break;
            case 3:
                display();
                break;
            case 4:
                printf("Size of stack is: %d\n", top + 1); 
                break;
            case 5:
                exit(0);
                break;
            default:
                printf("Enter the right Choice!\n");
        }

        printf("\n\n");
    }
    return 0;
}

void push() {
    if (top >= 99) {  
        printf("Stack is Overflow!\n");
    } else {
        top++;
        printf("Enter the data: ");
        scanf("%d", &stack[top]);
        printf("Data is pushed in stack ");
    }
}

int pop() {
    if (top < 0) {
        printf("Stack Underflow!\n");
        return -1;
    } else {
        return stack[top--];
    }
}

 void display() {
    if (top == -1) {
        printf("Stack is Empty!\n");
        return;
    }
    for (int i = top; i >= 0; i--) { 
        printf("%d\n", stack[i]);
    }
    printf("\n");
}

