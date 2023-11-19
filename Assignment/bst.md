```c
#include<stdio.h>
#include<stdlib.h>

struct tree {
    int data;
    struct tree *right, *left, *next;
};

struct tree *create(int d) {
    struct tree *newNode = (struct tree*)malloc(sizeof(struct tree));
    newNode->data = d;
    newNode->right = NULL;
    newNode->left = NULL;
    newNode->next = NULL;

    return newNode;
}

struct tree *add(struct tree *root, int d) {
    if (root == NULL) {
        return create(d);
    } else if (root->data > d) {
        root->left = add(root->left, d);
    } else {
        root->right = add(root->right, d);
    }
    return root;
}

void inorder(struct tree *root) {
    if (root != NULL) {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

void preorder(struct tree *root) {
    if (root != NULL) {
        printf("%d ", root->data);
        preorder(root->left);
        preorder(root->right);
    }
}

void postorder(struct tree *root) {
    if (root != NULL) {
        postorder(root->left);
        postorder(root->right);
        printf("%d ", root->data);
    }
}

void search(struct tree *root,int d){
     if(root==NULL){
        printf("Data not Found");
    }
    
    if(root->data==d){
        printf("Data Found!");
    }
    else if(d<root->data){
        search(root->left,d);
    }
    else{
         search(root->right,d);
    }
}

struct tree *findMin(struct tree *root) {
    while (root->left != NULL) {
        root = root->left;
    }
    return root;
}

struct tree *deleteNode(struct tree *root, int key) {
    if (root == NULL) {
        return root;
    } else if (key < root->data) {
        root->left = deleteNode(root->left, key);
    } else if (key > root->data) {
        root->right = deleteNode(root->right, key);
    } else {
       
        if (root->left == NULL) {
            struct tree *temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            struct tree *temp = root->left;
            free(root);
            return temp;
        }

        struct tree *temp = findMin(root->right);
        root->data = temp->data;
        root->right = deleteNode(root->right, temp->data);
    }
    return root;
}  

int main() {
    struct tree *root = NULL;

    root = add(root, 4);
    add(root, 2);
    add(root,3);
    add(root,6);
    add(root, 1);

    printf("Inorder: ");
    inorder(root);
    printf("\n");

    printf("Postorder: ");
    postorder(root);
    printf("\n");

    printf("Preorder: ");
    preorder(root);
    printf("\n");


    search(root,10);
    

    return 0;
}
