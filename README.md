#include <stdio.h>
#include <stdlib.h>
#include <string.h>

typedef struct Book {
    int id;
    char title[50];
    char author[50];
    struct Book* next; 
} Book;

Book* head = NULL; 


void addBook() {
 
    Book* newBook = (Book*)malloc(sizeof(Book));

   
    printf("Enter Book ID: ");
    scanf("%d", &newBook->id);
    getchar(); 

    printf("Enter Book Title: ");
    fgets(newBook->title, 50, stdin);
    newBook->title[strcspn(newBook->title, "\n")] = 0; 

    printf("Enter Author Name: ");
    fgets(newBook->author, 50, stdin);
    newBook->author[strcspn(newBook->author, "\n")] = 0; 

    newBook->next = NULL; 


    if (head == NULL) {
        head = newBook;
    } else {
       
        Book* temp = head;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = newBook;
    }

    printf("Book added successfully!\n\n");
}

void displayBooks() {
    if (head == NULL) {
        printf("No books in library.\n\n");
        return;
    }

    Book* temp = head;
    printf("Books in Library:\n");
    printf("ID\tTitle\t\tAuthor\n");
    printf("------------------------------------\n");

    while (temp != NULL) {
        printf("%d\t%-15s\t%s\n", temp->id, temp->title, temp->author);
        temp = temp->next;
    }
    printf("\n");
}

void searchBook() {
    if (head == NULL) {
        printf("No books to search.\n\n");
        return;
    }

    int id;
    printf("Enter Book ID to search: ");
    scanf("%d", &id);

    Book* temp = head;

    while (temp != NULL) {
        if (temp->id == id) {
          
            printf("Book found:\n");
            printf("ID: %d\nTitle: %s\nAuthor: %s\n\n", temp->id, temp->title, temp->author);
            return;
        }
        temp = temp->next;
    }

    printf("Book with ID %d not found.\n\n", id);
}

void deleteBook() {
    if (head == NULL) {
        printf("No books to delete.\n\n");
        return;
    }

    int id;
    printf("Enter Book ID to delete: ");
    scanf("%d", &id);

    Book* temp = head;
    Book* prev = NULL;

    while (temp != NULL && temp->id != id) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == NULL) {
        printf("Book with ID %d not found.\n\n", id);
        return;
    }

    if (prev == NULL) {
        head = temp->next;
    } else {
        prev->next = temp->next;
    }

    free(temp); 
    printf("Book deleted successfully!\n\n");
}

int main() {
    int choice;

    while (1) {
      
        printf("Library Management System\n");
        printf("1. Add Book\n");
        printf("2. Display Books\n");
        printf("3. Search Book\n");
        printf("4. Delete Book\n");
        printf("5. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);
        printf("\n");

        switch (choice) {
            case 1: addBook(); break;
            case 2: displayBooks(); break;
            case 3: searchBook(); break;
            case 4: deleteBook(); break;
            case 5:
                printf("Exiting program.\n");
                exit(0);
            default:
                printf("Invalid choice! Try again.\n\n");
        }
    }

    return 0;
}
