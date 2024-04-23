```cpp
disp macro msg
   mov ah,09h
   lea dx,msg
   int 21h
endm
.model small
.stack 100h
.data
   str1 db 25,?,25 dup('$')
   str2 db 25,?,25 dup('$')
  
   msg1 db 10,13,'Enter the string : $'
   msg2 db 10,13,'Reverse : $'
   msg3 db 10,13,'String is Palindrome $'
   msg4 db 10,13,'String is not palindrome $'
.code
 start:
    mov ax,@data
    mov ds,ax
    mov es,ax
    
    disp msg1
    mov ah,0Ah
    lea dx,str1
    int 21h
    
    xor ch,ch
    mov cl,str1+1
    sub cl,1
    lea si,str1+2
    add si,cl
    mov cl,str1+1
    lea di,str2+2
  loop1 :
     mov dl,[si]
     mov [di],dl
     inc di
     dec cl
     dec si
     cmp cl,00h
     jne loop1
   
    disp msg2
    mov ah,09h
    lea dx,str2+2
    int 21h

   mov cl,str1+1
   mov si,offset str1+2
   mov di,offset str2+2
 checkpal :
   mov al,[si]
   mov dl,[di]
   cmp al,dl
   jne notpal
   inc si
   inc di
   dec cl
   cmp cl,00h
   je ispal
   jmp checkpal

notpal :
disp msg4
jmp endprg

ispal :
 disp msg3
 jmp endprg

endprg :
  mov ah,4ch
  int 21h

end
```
