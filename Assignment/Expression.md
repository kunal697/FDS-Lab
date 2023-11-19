```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <math.h>
#include <ctype.h>

struct stack {
    char data;
    struct stack *next;
};

char infix[50];
char postfix[50];
char prefix[50];
struct stack *top = NULL;

char reverse(char p[]) {
    int i = 0;
    int j = strlen(p) - 1;
    while (i < j) {
        char t = p[i];
        p[i] = p[j];
        p[j] = t;
        j--;
        i++;
    }
    return *p;
}

int cheak(char x) {
    switch (x) {
        case '^':
            return 3;
        case '*':
            return 2;
        case '/':
            return 2;
        case '+':
            return 1;
        case '-':
            return 1;
    }
}

void push(char x) {
    struct stack *temp;
    temp = (struct stack *)malloc(sizeof(struct stack));
    temp->data = x;
    temp->next = NULL;
    if (top == NULL) {
        top = temp;
    } else {
        temp->next = top;
        top = temp;
    }
}

char pop() {
    char op;
    struct stack *p;
    op = top->data;
    p = top;
    top = top->next;
    free(p);
    return op;
}

void Postfix() {
    int i = 0, j = 0;
    while (infix[i] != '\0') {
        if (isdigit(infix[i])) {
            postfix[j++] = infix[i];
        } else {
            if (top == NULL) {
                push(infix[i]);
            } else {
                while (top != NULL && cheak(top->data) >= cheak(infix[i])) {
                    postfix[j++] = pop();
                }
                push(infix[i]);
            }
        }
        i++;
    }
    while (top != NULL) {
        postfix[j++] = pop();
    }
    postfix[j] = '\0';
    printf("%s", postfix);
}

void Prefix() {
    reverse(infix);
    int i = 0, j = 0;
    while (infix[i] != '\0') {
        if (isalnum(infix[i])) {
            prefix[j++] = infix[i];
        } else {
            if (top == NULL) {
                push(infix[i]);
            } else {
                while (top != NULL && cheak(top->data) >= cheak(infix[i])) {
                    prefix[j++] = pop();
                }
                push(infix[i]);
            }
        }
        i++;
    }
    while (top != NULL) {
        prefix[j++] = pop();
    }
    prefix[j] = '\0';
    reverse(prefix);
    printf("%s", prefix);
}

void evaluatePostfix() {
    top = NULL;
    char A, B, op;
    int i = 0, a, b, t;
    while (postfix[i] != '\0') {
        if (isdigit(postfix[i]))
            push(postfix[i]);
        else {
            A = pop();
            B = pop();
            op = postfix[i];
            a = A - 48;
            b = B - 48;
            switch (op) {
                case '+':
                    t = a + b;
                    break;
                case '-':
                    t = b - a;
                    break;
                case '*':
                    t = b * a;
                    break;
                case '/':
                    t = b / a;
                    break;
                case '^':
                    t = b ^ a;
                    break;
            }
            op = t + 48;
            push(op);
        }
        i++;
    }
    op = pop();
    t = op - 48;
    printf("\nAns = %d\n", t);
}

void evaluatePrefix() {
    prefix[50] = reverse(prefix);
    top = NULL;
    char A, B, op;
    int i = 0, a, b, t;
    while (prefix[i] != '\0') {
        if (isdigit(prefix[i]))
            push(prefix[i]);
        else {
            A = pop();
            B = pop();
            op = prefix[i];
            a = A - 48;
            b = B - 48;
            switch (op) {
                case '+':
                    t = a + b;
                    break;
                case '-':
                    t = a - b;
                    break;
                case '*':
                    t = a * b;
                    break;
                case '/':
                    t = a / b;
                    break;
                case '^':
                    t = a ^ b;
                    break;
            }
            op = t + 48;
            push(op);
        }
        i++;
    }
    op = pop();
    t = op - 48;
    printf("\nAns = %d\n", t);
}

int main() {
    int ch, y = 0;
    printf("Enter the Infix Expression :");
    scanf("%s", infix);
    do {
        printf("1.Infix to Postfix\n2.Infix to Prefix\n3.Evaluate Postfix\n4.Evaluate Prefix\n");
        scanf("%d", &ch);
        switch (ch) {
            case 1:
                Postfix();
                break;
            case 2:
                Prefix();
                break;
            case 3:
                evaluatePostfix();
                break;
            case 4:
                evaluatePrefix();
                break;
        }
        printf("\nDo you want to do again ? (YES=1||NO=0)\n ");
        scanf("%d", &y);
    } while (y == 1);
    return 0;
}
