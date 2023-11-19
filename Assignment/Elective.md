```c
#include<stdio.h>
#include<stdlib.h>

void all_elective(int A[],int B[],int n,int m){
 int C[n+m];
 for(int i = 0;i<n;i++){
    C[i]=A[i];
 }
  int size = n,present;
  for(int i = 0;i<m;i++){
    present = 0;
    for(int j = 0;j<n;j++){
        if(B[i]==C[j]){
            present = 1;
            break;
        }
    }
    if(present==0){
        C[size++]=B[i];
    }
  }
  printf("List of students opted All elective : ");
  for(int k = 0;k<size;k++){
    printf("%d ",C[k]);
  }
   
}

void both_elective(int A[],int B[],int n,int m){
      int C[n+m];
      int size = 0;

      for(int i =0;i<n;i++){
        for(int j = 0;j<m;j++){
            if(A[i]==B[j]){
                C[size++]=A[i];
                break;
            }
        }
      }

    for(int k = 0;k<size;k++){
    printf("%d ",C[k]);
  }

}

void only_devops(int A[],int B[],int n,int m){
         int C[n+m];
         int size = 0;
         int present;
         for(int i = 0;i<m;i++){
            present = 0;
            for(int j  = 0;j<n;j++){
                if(B[i]==A[j]){
                    present = 1;
                    break;
                }
            }
            if(present==0){
                C[size++]=B[i];
            }
         }

    for(int k = 0;k<size;k++){
    printf("%d ",C[k]);
  }
}

void only_blockchain(int A[],int B[],int n,int m){

          int C[n+m];
         int size = 0;
         int present;
         for(int i = 0;i<n;i++){
            present = 0;
            for(int j  = 0;j<m;j++){
                if(B[j]==A[i]){
                    present = 1;
                    break;
                }
            }
            if(present==0){
                C[size++]=A[i];
            }
         }

    for(int k = 0;k<size;k++){
    printf("%d ",C[k]);
  }

}

void only_one(int A[],int B[],int n,int m){
            //only devops+only blockchain 
}


int main(){
    int n ,m ,ch;
    printf("Enter the number of students otped Blockchain : ");
    scanf("%d",&n);
     printf("Enter the number of students otped Devops: ");
    scanf("%d",&m);
    int blockchain[n],devops[m];
    printf("Enter the Bloackchain students : ");
    for(int i  = 0;i<n;i++) scanf("%d",&blockchain[i]);

    printf("Enter the Devops students : ");
    for(int i  = 0;i<m;i++) scanf("%d",&devops[i]);

    while(1){
    printf("\n1.All students \n2.All students opted Both\n3.Students opted only Devops\n4.Students opted only blockchain\n5.Students opted only one subject\t : ");
    scanf("%d",&ch);
    switch (ch)
    {
    case 1: all_elective(blockchain,devops,n,m);
             break;
    case 2: both_elective(blockchain,devops,n,m);
             break;
    case 3: only_devops(blockchain,devops,n,m);
             break;
    case 4: only_blockchain(blockchain,devops,n,m);
             break;
    case 5: only_one(blockchain,devops,n,m);
             break;
    default:
        exit(0);
    }
    }
}
