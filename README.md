#include <stdio.h>
#include <stdlib.h>

#define MAX_SIZE 100

int stack_arr[MAX_SIZE];
int top = 0; // Initialize top to 0

// Function to push an element onto the stack
void push(int value) {
    if (top == MAX_SIZE) {
        printf("Stack is full. Cannot push %d\n", value);
    } else {
        stack_arr[++top] = value;
        printf("%d pushed onto the stack.\n", value);
    }
}

// Function to pop an element from the stack
int pop() {
    if (top == 0) {
        printf("Stack is empty.\n");
        return -1; // Return an error value
    } else {
        int value = stack_arr[top--];
        return value;
    }
}

// Function to display the elements in the stack
void display() {
    if (top == 0) {
        printf("Stack is empty.\n");
        return;
    }

    printf("Stack elements: ");
    for (int i = 1; i <= top; i++) {
        printf("%d ", stack_arr[i]);
    }
    printf("\n");
}

int main() {
    int choice, value, popped;

    while (1) {
        printf("Menu:\n");
        printf("1. Push\n");
        printf("2. Pop\n");
        printf("3. Display\n");
        printf("4. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter the value to push: ");
                scanf("%d", &value);
                push(value);
                break;
            case 2:
                popped = pop();
                if (popped != -1) {
                    printf("Popped element: %d\n", popped);
                }
                break;
            case 3:
                display();
                break;
            case 4:
                exit(0);
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
