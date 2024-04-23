
```cpp
#include<PIC18F4550.h>
#include<xc.h>

int main(){
   int a,b,x;
   TRISB = 0;
   LATB = 0;
   a = 0x004;
   b = 0x005;
   x = a+b;
   PORTB = x;
   PORTA = a;
   PORTC = b;
   
  return 0;
}
```
```cpp
#include<PIC18F4550.h>

int main(){
   int arr[]={1,2,3,4,5};
   int sum =0;
   TRISB=0;
   LATB=0;
   for(int i=0;i<5;i++) sum+=arr[i];
   
   PORTB= sum;
}
```
```cpp
#include<PIC18F4550.h>

int main(){
   int arr[]={1,2,3,4,5};
   int brr[5];
  TRISB = 0;
  LATB =0;
   for(int i=0;i<5;i++){
       brr[i]=arr[i];
   }
   for(int i=0;i<5;i++){ 
       LATB=brr[i];
       __delay_ms(1000);
   }
}
```

```cpp
#include<PIC18F4550.h>

int main(){
   int arr[]={5,4,3,2,1};
   TRISB = 0;
   LATB = 0;
   for(int i=0;i<5;i++){
       for(int j=0;j<n-i-1;j++){
          int temp = arr[i];
          arr[i] = arr[j];  
          arr[j] = arr[i];     
    }
  }   
   for(int i=0;i<5;i++){
      LATB=arr[i];
       __delay_ms(1000);
    }
}
```

```cpp
#include<PIC18F4550.h>
include <xc.h>
#define _XTAL_FREQ 4000000

int main(){
  
   TRISC =0;
   LATC =0;
   while(1){
     PORTC = 1;
      __delay_ms(1000);
      PORTC =0;
      __delay_ms(1000);
   }
}
```

```

input macro
        mov ah,01H
        int 21H
endm

output macro
        mov ah,02H
        int 21H
endm

disp macro var
        lea dx,var
        mov ah,09H
        int 21H
endm
.model small
.stack 100H
.data
        m1 db 10,13,"Enter array size :- $"
        m2 db 10,13, "Enter Numbers:- $"
        m3 db 10,13,"Addition =$"
        m4 db 10,13,"$"
        array db 10 dup(0)
        count db 0

.code
        mov ax,@data
        mov ds,ax

        lea si,array
        disp m1
        input
        sub al,30H

        mov count,al
        mov cl,count
        disp m4

        s1: disp m2
            input
            sub al,30
            mov [si],al
            inc si
            loop s1

            disp m4
            disp m3

            mov ax,0000H
            mov cl,count

            lea si,array
          s2:add al,[si]
             ;sub al,30H
             inc si
             loop s2

             mov ch,02H
             mov cl,04H
             mov bl,al

         s3: rol bl,cl
             mov dl,bl
             and dl,0FH
             cmp dl,09       ; dl=dl-09
             jbe s4
             add dl,07

         s4: add dl,30H





             output
             dec ch
             jnz s3

             mov ah,4CH
             int 21H
end
             
```
