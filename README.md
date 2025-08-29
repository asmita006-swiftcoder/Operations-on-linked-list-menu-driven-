# Operations-on-linked-list-menu-driven-
Menu driven program of operations on single linked list

#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *next;
};

void traverseList(struct node *head) {
    if (head == NULL) {
        printf("List is empty\n");
        return;
    }
    struct node *temp = head;
    printf("The list is: ");
    while (temp != NULL) {
        printf("%d", temp->data);
        if (temp->next != NULL) printf("->");
        temp = temp->next;
    }
    printf("\n");
}
void countNodes(struct node *head) {
    int count = 0;
    struct node *temp = head;
    while (temp != NULL) {
        count++;
        temp = temp->next;
    }
    printf("The total number of nodes: %d\n", count);
}
struct node* insertAtPosition(struct node *head, int data, int pos) {
    struct node *new_node = (struct node *)malloc(sizeof(struct node));
    new_node->data = data;
    new_node->next = NULL;

    if (pos == 1) { // insert at beginning
        new_node->next = head;
        head = new_node;
    } else {
        struct node *temp = head;
        for (int i = 1; temp != NULL && i < pos - 1; i++) {
            temp = temp->next;
        }
        if (temp == NULL) {
            printf("Invalid position!\n");
            free(new_node);
            return head;
        }
        new_node->next = temp->next;
        temp->next = new_node;
    }
     printf("Node inserted\n");
    traverseList(head);
    return head;
}
struct node* deleteAtPosition(struct node *head, int pos) {
    if (head == NULL) {
        printf("List is empty\n");
        return head;
    }

    struct node *temp = head;

    if (pos == 1) {  // delete first node
        head = head->next;
        free(temp);
        printf("Node deleted\n");
        traverseList(head);
        return head;
    }

    for (int i = 1; temp != NULL && i < pos - 1; i++) {
        temp = temp->next;
    }

    if (temp == NULL || temp->next == NULL) {
        printf("Invalid position!\n");
        return head;
    }
     struct node *toDelete = temp->next;
    temp->next = toDelete->next;
    free(toDelete);
    printf("Node deleted\n");
    traverseList(head);
    return head;
}

int main() {
    struct node *head = NULL;  // local head
    int n, choice;

    printf("Enter number of nodes: ");
    scanf("%d", &n);

    printf("Enter the elements:\n");
    for (int i = 0; i < n; i++) {
        struct node *new_node = (struct node *)malloc(sizeof(struct node));
        scanf("%d", &new_node->data);
        new_node->next = NULL;

        if (head == NULL) {
            head = new_node;
        } else {
            struct node *temp = head;
            while (temp->next != NULL) {
                temp = temp->next;
            }
            temp->next = new_node;
        }
    }
     do {
        printf("\nMENU:\n");
        printf("1. Insert the node at a position\n");
        printf("2. Delete a node from specific position\n");
        printf("3. Count nodes\n");
        printf("4. Traverse\n");
        printf("5. Exit\n");

        printf("Enter choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: {
                int data, pos;
                printf("Enter element: ");
                scanf("%d", &data);
                printf("Enter position: ");
                scanf("%d", &pos);
                head = insertAtPosition(head, data, pos);
                break;
            }
            case 2: {
                int pos;
                printf("Enter position: ");
                scanf("%d", &pos);
                head = deleteAtPosition(head, pos);
                break;
            }
            case 3: countNodes(head); break;
            case 4: traverseList(head); break;
            case 5: printf("Exiting...\n"); break;
            default: printf("Invalid choice\n");
        }
          } while (choice != 5);

    return 0;
}
