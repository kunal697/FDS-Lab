**c program using linked list for libarary where you store bookname and author name and there will 
three operation that you will be perform book deletion , book search by authure name, and add the book**

```c
 #include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to represent a book
struct Book {
    char title[100];
    char author[100];
    struct Book* next;
};
 

 struct Book* addBook(struct Book* library,char* title, char* author) {
     struct Book* newBook = (struct Book*)malloc(sizeof(struct Book));
        strcpy(newBook->title, title);
        strcpy(newBook->author, author);
        newBook->next = NULL;
       newBook->next = library;
    printf("Book \"%s\" by %s added to the library.\n", title, author);
    return newBook;
}

 void searchByAuthor( struct Book* library, char* author) {
    int found = 0;
    const struct Book* current = library;
    
    while (current) {
        if (strcmp(current->author, author) == 0) {
            printf("Book: %s, Author: %s\n", current->title, current->author);
            found = 1;
        }
        current = current->next;
    }
    
    if (!found) {
        printf("No books by %s found in the library.\n", author);
    }
}

 struct Book* deleteBook(struct Book* library, char* title) {
    struct Book* current = library;
    struct Book* prev = NULL;

    while (current != NULL) {
        if (strcmp(current->title, title) == 0) {
            if (prev == NULL) {
                library = current->next;
            } else {
                prev->next = current->next;
            }
            free(current);
            printf("Book \"%s\" deleted from the library.\n", title);
            return library;
        }
        prev = current;
        current = current->next;
    }

    printf("Book \"%s\" not found in the library.\n", title);
    return library;
}

 void displayLibrary( struct Book* library) {
    printf("Library Contents:\n");
    const struct Book* current = library;
    
    while (current) {
        printf("Book: %s, Author: %s\n", current->title, current->author);
        current = current->next;
    }
}

 

int main() {
    struct Book* library = NULL;
    int choice;
    char title[100];
    char author[100];

    while (1) {
         printf("1. Add a Book\n");
        printf("2. Search by Author\n");
        printf("3. Delete a Book\n");
        printf("4. Display Library\n");
        printf("5. Quit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter book title: ");
                scanf(" %s", title);
                printf("Enter author name: ");
                scanf(" %s", author);
                library = addBook(library, title, author);
                break;

            case 2:
                printf("Enter author name to search for books: ");
                scanf(" %s", author);
                searchByAuthor(library, author);
                break;

            case 3:
                printf("Enter the title of the book to delete: ");
                scanf(" %s", title);
                library = deleteBook(library, title);
                break;

            case 4:
                displayLibrary(library);
                break;

            case 5:
                  return 0;

            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
