#include <stdio.h>
#include <stdlib.h>

struct Node {
    int data;
    struct Node *next;
};

struct Node *head = NULL;

void display();
void insertAtBeginning(int value);
void insertAtEnd(int value);
void insertAtPosition(int value, int position);
void deleteFromBeginning();
void deleteFromEnd();
void deleteFromPosition(int position);

int main() {
    int choice, value, position;

    while (1) {
        printf("\nLinked List Operations:\n");
        printf("a. Display\n");
        printf("b. Insert at Beginning\n");
        printf("c. Insert at End\n");
        printf("d. Insert at a specified Position\n");
        printf("e. Delete from Beginning\n");
        printf("f. Delete from End\n");
        printf("g. Delete from a specified Position\n");
        printf("h. Exit\n");

        printf("Enter your choice: ");
        scanf(" %c", &choice);

        switch (choice) {
            case 'a':
                display();
                break;
            case 'b':
                printf("Enter the value to insert: ");
                scanf("%d", &value);
                insertAtBeginning(value);
                break;
            case 'c':
                printf("Enter the value to insert: ");
                scanf("%d", &value);
                insertAtEnd(value);
                break;
            case 'd':
                printf("Enter the value to insert: ");
                scanf("%d", &value);
                printf("Enter the position to insert at: ");
                scanf("%d", &position);
                insertAtPosition(value, position);
                break;
            case 'e':
                deleteFromBeginning();
                break;
            case 'f':
                deleteFromEnd();
                break;
            case 'g':
                printf("Enter the position to delete from: ");
                scanf("%d", &position);
                deleteFromPosition(position);
                break;
            case 'h':
                exit(0);
            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    }

    return 0;
}

void display() {
    struct Node *temp = head;

    if (temp == NULL) {
        printf("The list is empty.\n");
        return;
    }

    printf("Linked List: ");
    while (temp != NULL) {
        printf("%d ", temp->data);
        temp = temp->next;
    }
    printf("\n");
}

void insertAtBeginning(int value) {
    struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = head;
    head = newNode;
    printf("%d inserted at the beginning.\n", value);
}

void insertAtEnd(int value) {
    struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = value;
    newNode->next = NULL;

    if (head == NULL) {
        head = newNode;
    } else {
        struct Node *temp = head;
        while (temp->next != NULL) {
            temp = temp->next;
        }
        temp->next = newNode;
    }

    printf("%d inserted at the end.\n", value);
}

void insertAtPosition(int value, int position) {
    struct Node *newNode = (struct Node *)malloc(sizeof(struct Node));
    newNode->data = value;

    if (position == 1) {
        newNode->next = head;
        head = newNode;
    } else {
        struct Node *temp = head;
        for (int i = 1; i < position - 1 && temp != NULL; i++) {
            temp = temp->next;
        }

        if (temp == NULL) {
            printf("Invalid position. Insertion failed.\n");
            free(newNode);
            return;
        }

        newNode->next = temp->next;
        temp->next = newNode;
    }

    printf("%d inserted at position %d.\n", value, position);
}

void deleteFromBeginning() {
    if (head == NULL) {
        printf("The list is empty. Deletion failed.\n");
        return;
    }

    struct Node *temp = head;
    head = head->next;
    free(temp);

    printf("Deleted from the beginning.\n");
}

void deleteFromEnd() {
    if (head == NULL) {
        printf("The list is empty. Deletion failed.\n");
        return;
    }

    if (head->next == NULL) {
        free(head);
        head = NULL;
    } else {
        struct Node *temp = head;
        while (temp->next->next != NULL) {
            temp = temp->next;
        }

        free(temp->next);
        temp->next = NULL;
    }

    printf("Deleted from the end.\n");
}

void deleteFromPosition(int position) {
    if (head == NULL) {
        printf("The list is empty. Deletion failed.\n");
        return;
    }

    if (position == 1) {
        struct Node *temp = head;
        head = head->next;
        free(temp);
    } else {
        struct Node *temp = head;
        for (int i = 1; i < position - 1 && temp != NULL; i++) {
            temp = temp->next;
        }

        if (temp == NULL || temp->next == NULL) {
            printf("Invalid position. Deletion failed.\n");
            return;
        }

        struct Node *nodeToDelete = temp->next;
        temp->next = temp->next->next;
        free(nodeToDelete);
    }

    printf("Deleted from position %d.\n", position);
}
