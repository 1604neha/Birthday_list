#include <stdio.h>
#include <string.h>

#define MAX_RECORDS 100

// Structure to represent a birthday record
struct Birthday {
    char name[50];
    int day;
    int month;
};

// Function to check for duplicate names
int isDuplicate(struct Birthday records[], int count, char *name) {
    for (int i = 0; i < count; i++) {
        if (strcmp(records[i].name, name) == 0) {
            return 1; // Duplicate name found
        }
    }
    return 0; // No duplicate name found
}

// Function to add a birthday record
void addRecord(struct Birthday records[], int *count) {
    if (*count >= MAX_RECORDS) {
        printf("Sorry, the maximum number of records (%d) has been reached.\n", MAX_RECORDS);
        return;
    }

    struct Birthday newRecord;

    printf("Enter name: ");
    scanf("%s", newRecord.name);

    if (isDuplicate(records, *count, newRecord.name)) {
        printf("Name already exists in the list. Duplicate names are not allowed.\n");
        return;
    }

    printf("Enter day of birth: ");
    scanf("%d", &newRecord.day);

    printf("Enter month of birth: ");
    scanf("%d", &newRecord.month);

    records[*count] = newRecord;
    (*count)++;
    printf("Record added successfully!\n");
}

// Function to display all birthday records
void displayRecords(struct Birthday records[], int count) {
    if (count == 0) {
        printf("No records to display.\n");
        return;
    }

    printf("Birthday Records:\n");
    for (int i = 0; i < count; i++) {
        printf("%s - %d/%d\n", records[i].name, records[i].day, records[i].month);
    }
}

int main() {
    // Define the login credentials
    char username[] = "poojanoorneha";
    char password[] = "121916";

    char inputUsername[50];
    char inputPassword[50];

    // Get user input for login
    printf("Username: ");
    scanf("%s", inputUsername);
    printf("Password: ");
    scanf("%s", inputPassword);

    // Check if the input username and password are correct
    if (strcmp(inputUsername, username) != 0 || strcmp(inputPassword, password) != 0) {
        printf("Login failed. Exiting...\n");
        return 1; // Exit the program
    }

    // If login is successful, proceed to the birthday list menu
    struct Birthday records[MAX_RECORDS];
    int count = 0;
    int choice;

    while (1) {
        printf("\nBirthday List Menu:\n");
        printf("1. Add a record\n");
        printf("2. Display all records\n");
        printf("3. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                addRecord(records, &count);
                break;
            case 2:
                displayRecords(records, count);
                break;
            case 3:
                return 0;
            default:
                printf("Invalid choice. Please try again.\n");
        }
    }

    return 0;
}
