### Reverse the String using Stack


**here we have taken string input from user and then added to stack and just print the stack in revesre(from top)**
```c
 #include<stdio.h>

 char stack[100];
  int top = -1;

 void push(char data)
 {
    if(top>100)
    {
        printf("Stack Overflow!!");
    }
    else{
        top++;
        stack[top]=data;

    }
 }

 void display()
 {
    for(int i=top;i>=0;i--)
    {
        printf("%c",stack[i]);
    }
 }

 int main()
 {
     char str[100];

     printf("Enter the string : ");
     scanf("%s",str);

     int i = 0;
     while(str[i]!='\0')
     {
        i++;

     }

     for(int k=0;k<i;k++)
     {
        push(str[k]);

     }

 display();



 }
