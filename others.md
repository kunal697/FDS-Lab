
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
