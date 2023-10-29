# 2010213620-ABDELRAHMAN-YOUSRY-HAMED-GOMAA-MORSY



//                                                               Question-1

#include <stdio.h>
#include <stdlib.h>

// Structure for a node
struct Node {
    int data;
    struct Node* next;
};

// Function to insert a new node at the beginning
void insertAtBeginning(struct Node** head_ref, int new_data) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to the node
    new_node->data = new_data;

    // Adjust the next pointer of the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to insert a new node at the end
void insertAtEnd(struct Node** head_ref, int new_data) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Create a pointer to traverse the list
    struct Node* last = *head_ref;

    // Assign data to the node
    new_node->data = new_data;

    // This new node is going to be the last node, so make next of it as NULL
    new_node->next = NULL;

    // If the linked list is empty, then make the new node as the head
    if (*head_ref == NULL) {
        *head_ref = new_node;
        return;
    }

    // Else traverse till the last node
    while (last->next != NULL)
        last = last->next;

    // Change the next of the last node
    last->next = new_node;
}

// Function to print the linked list
void printList(struct Node* node) {
    while (node != NULL) {
        printf(" %d ", node->data);
        node = node->next;
    }
}

// Function to add numbers to the list
void addNumbersToList() {
    int num;
    struct Node* head = NULL; // Initialize head pointer to NULL

    printf("Enter numbers (enter -1 to stop): \n");

    while (1) {
        scanf("%d", &num);
        if (num == -1) {
            break; // Break the loop if -1 is entered
        }

        if (num % 2 == 0) {
            // If the number is even, add it to the end of the list
            insertAtEnd(&head, num);
        } else {
            // If the number is odd, add it to the beginning of the list
            insertAtBeginning(&head, num);
        }
    }

    // Print the final list
    printf("The final list is: \n");
    printList(head);
}

// Main function
int main() {
    addNumbersToList(); // Call the function to add numbers to the list
    return 0;
}




//                                                            Question 2




#include <stdio.h>
#include <stdlib.h>

// Structure for a node
struct Node {
    int data;
    struct Node* next;
};

// Function to insert a new node at the beginning
void insertAtBeginning(struct Node** head_ref, int new_data) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to the node
    new_node->data = new_data;

    // Adjust the next pointer of the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to print the linked list
void printList(struct Node* node) {
    while (node != NULL) {
        printf("->%d", node->data);
        node = node->next;
    }
}

// Function to sort the list in descending order
void sortList(struct Node** head_ref) {
    struct Node *current, *next;
    int temp;
    current = *head_ref;

    // Bubble sort algorithm
    for (current = *head_ref; current != NULL; current = current->next) {
        for (next = current->next; next != NULL; next = next->next) {
            if (current->data < next->data) {
                temp = current->data;
                current->data = next->data;
                next->data = temp;
            }
        }
    }
}

// Function to generate random numbers and add them to the list
void addRandomNumbersToList(struct Node** head_ref) {
    int i;
    for (i = 0; i < 100; i++) {
        int num = rand() % 1000; // Generate random numbers less than 1000
        insertAtBeginning(head_ref, num); // Insert the generated number at the beginning of the list
    }
}

// Main function
int main() {
    struct Node* head = NULL; // Initialize head pointer to NULL
    addRandomNumbersToList(&head); // Call the function to add 100 random numbers to the list

    printf("List before sorting: ");
    printList(head); // Print the list before sorting

    sortList(&head); // Sort the list in descending order

    printf("\nList after sorting: ");
    printList(head); // Print the list after sorting

    return 0;
}




//                                                            Question 4


#include <stdio.h>
#include <stdlib.h>

// Structure for a node
struct Node {
    int studentNumber;
    char name[50];
    int age;
    struct Node* next;
};

// Function to insert a new node at the beginning
void insertAtBeginning(struct Node** head_ref, int studentNumber, char name[], int age) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to the node
    new_node->studentNumber = studentNumber;
    strcpy(new_node->name, name);
    new_node->age = age;

    // Adjust the next pointer of the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to traverse and print the list
void printStudentInfo(struct Node* node) {
    int count = 0;
    while (node != NULL) {
        count++;
        printf("%d- %s %d %d\n", node->studentNumber, node->name, node->age, 200 + count);
        node = node->next;
    }
}

// Main function
int main() {
    struct Node* head = NULL; // Initialize head pointer to NULL

    // Inserting some sample student data into the list
    insertAtBeginning(&head, 201, "Saliha", 27);
    insertAtBeginning(&head, 203, "Ece", 19);

    // Printing the student information
    printf("Student Information:\n");
    printStudentInfo(head);

    return 0;
}






//                                                                 Question 5


#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure for a node
struct Node {
    int studentNumber;
    char name[50];
    int age;
    struct Node* next;
};

// Function to insert a new node at the beginning
void insertAtBeginning(struct Node** head_ref, int studentNumber, char name[], int age) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to the node
    new_node->studentNumber = studentNumber;
    strcpy(new_node->name, name);
    new_node->age = age;

    // Adjust the next pointer of the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to search for a record by student name
struct Node* searchRecordByName(struct Node* head, char name[]) {
    struct Node* current = head;

    // Traverse the list
    while (current != NULL) {
        // Compare the names
        if (strcmp(current->name, name) == 0) {
            return current; // Return the node if the name matches
        }
        current = current->next;
    }

    return NULL; // Return NULL if the name is not found in the list
}

// Main function
int main() {
    struct Node* head = NULL; // Initialize head pointer to NULL

    // Inserting some sample student data into the list
    insertAtBeginning(&head, 201, "Saliha", 27);
    insertAtBeginning(&head, 203, "Ece", 19);

    // Searching for a record by student name
    char searchName[50];
    printf("Enter the name to search: ");
    scanf("%s", searchName);

    struct Node* result = searchRecordByName(head, searchName);

    if (result != NULL) {
        printf("Record found: %d %s %d\n", result->studentNumber, result->name, result->age);
    } else {
        printf("Record not found.\n");
    }

    return 0;
}






//                                                       Question 6




#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure for a node
struct Node {
    int studentNumber;
    char name[50];
    int age;
    struct Node* next;
};

// Function to insert a new node at the beginning
void insertAtBeginning(struct Node** head_ref, int studentNumber, char name[], int age) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to the node
    new_node->studentNumber = studentNumber;
    strcpy(new_node->name, name);
    new_node->age = age;

    // Adjust the next pointer of the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to search for a node by student name
struct Node* searchRecordByName(struct Node* head, char name[]) {
    struct Node* current = head;

    // Traverse the list
    while (current != NULL) {
        // Compare the names
        if (strcmp(current->name, name) == 0) {
            return current; // Return the node if the name matches
        }
        current = current->next;
    }

    return NULL; // Return NULL if the name is not found in the list
}

// Function to delete the next node from the node with the searched student name
void deleteNextNode(struct Node* node) {
    if (node == NULL || node->next == NULL) {
        return; // If the node is NULL or the next node is NULL, return
    }
    struct Node* nextNode = node->next; // Store the next node
    node->next = nextNode->next; // Adjust the pointers to skip the next node
    free(nextNode); // Free the memory of the next node
}

// Main function
int main() {
    struct Node* head = NULL; // Initialize head pointer to NULL

    // Inserting some sample student data into the list
    insertAtBeginning(&head, 201, "Saliha", 27);
    insertAtBeginning(&head, 203, "Ece", 19);

    // Searching for a record by student name
    char searchName[50];
    printf("Enter the name to search: ");
    scanf("%s", searchName);

    struct Node* result = searchRecordByName(head, searchName);

    if (result != NULL) {
        // Delete the next node
        deleteNextNode(result);
        printf("Next node deleted successfully.\n");
    } else {
        printf("Record not found.\n");
    }

    return 0;
}




//                                                           Question 7


#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure for a node
struct Node {
    int studentNumber;
    char name[50];
    int age;
    struct Node* next;
};

// Function to insert a new node at the beginning
void insertAtBeginning(struct Node** head_ref, int studentNumber, char name[], int age) {
    // Allocate memory for new node
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node));

    // Assign data to the node
    new_node->studentNumber = studentNumber;
    strcpy(new_node->name, name);
    new_node->age = age;

    // Adjust the next pointer of the new node
    new_node->next = (*head_ref);

    // Move the head to point to the new node
    (*head_ref) = new_node;
}

// Function to print the record with the longest name in the list
void printRecordWithLongestName(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }

    int maxLength = 0;
    char longestName[50];
    struct Node* current = head;

    // Traverse the list to find the longest name
    while (current != NULL) {
        if (strlen(current->name) > maxLength) {
            maxLength = strlen(current->name);
            strcpy(longestName, current->name);
        }
        current = current->next;
    }

    // Print the record with the longest name
    printf("The longest name in the list: %s\n", longestName);
    printf("Length: %d\n", maxLength);
}

// Main function
int main() {
    struct Node* head = NULL; // Initialize head pointer to NULL

    // Inserting some sample student data into the list
    insertAtBeginning(&head, 201, "Saliha", 27);
    insertAtBeginning(&head, 203, "Ece", 19);
    insertAtBeginning(&head, 205, "Abdurrahmangazi", 25);

    // Printing the record with the longest name in the list
    printRecordWithLongestName(head);

    return 0;
}
