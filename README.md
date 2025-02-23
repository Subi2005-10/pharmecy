#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_MEDICINES 100

typedef struct {
    int id;
    char name[50];
    int quantity;
    float price;
    char expiry_date[15];
} Medicine;

Medicine inventory[MAX_MEDICINES];
int count = 0;

// Add a new medicine
void add_medicine() {
    if (count >= MAX_MEDICINES) {
        printf("Inventory full!\n");
        return;
    }
    printf("Enter Medicine ID: ");
    scanf("%d", &inventory[count].id);
    printf("Enter Name: ");
    scanf("%s", inventory[count].name);
    printf("Enter Quantity: ");
    scanf("%d", &inventory[count].quantity);
    printf("Enter Price: ");
    scanf("%f", &inventory[count].price);
    printf("Enter Expiry Date (YYYY-MM-DD): ");
    scanf("%s", inventory[count].expiry_date);

    count++;
    printf("Medicine added successfully!\n");
}

// Display all medicines
void display_medicines() {
    if (count == 0) {
        printf("No medicines in inventory.\n");
        return;
    }
    printf("\nID\tName\t\tQuantity\tPrice\tExpiry Date\n");
    printf("---------------------------------------------------------\n");
    for (int i = 0; i < count; i++) {
        printf("%d\t%s\t\t%d\t\t%.2f\t%s\n", inventory[i].id, inventory[i].name, inventory[i].quantity, inventory[i].price, inventory[i].expiry_date);
    }
}

// Search for a medicine
void search_medicine() {
    char name[50];
    printf("Enter medicine name to search: ");
    scanf("%s", name);

    for (int i = 0; i < count; i++) {
        if (strcmp(inventory[i].name, name) == 0) {
            printf("Medicine Found!\n");
            printf("ID: %d, Name: %s, Quantity: %d, Price: %.2f, Expiry Date: %s\n",
                   inventory[i].id, inventory[i].name, inventory[i].quantity, inventory[i].price, inventory[i].expiry_date);
            return;
        }
    }
    printf("Medicine not found.\n");
}

// Update medicine details
void update_medicine() {
    int id, choice;
    printf("Enter Medicine ID to update: ");
    scanf("%d", &id);

    for (int i = 0; i < count; i++) {
        if (inventory[i].id == id) {
            printf("1. Update Quantity\n2. Update Price\nChoose option: ");
            scanf("%d", &choice);
            if (choice == 1) {
                printf("Enter new quantity: ");
                scanf("%d", &inventory[i].quantity);
            } else if (choice == 2) {
                printf("Enter new price: ");
                scanf("%f", &inventory[i].price);
            } else {
                printf("Invalid option.\n");
            }
            printf("Medicine updated successfully!\n");
            return;
        }
    }
    printf("Medicine ID not found.\n");
}

// Delete expired medicines
void delete_expired_medicine() {
    char expiry[15];
    printf("Enter expiry date to delete medicines (YYYY-MM-DD): ");
    scanf("%s", expiry);

    int new_count = 0;
    for (int i = 0; i < count; i++) {
        if (strcmp(inventory[i].expiry_date, expiry) > 0) {
            inventory[new_count++] = inventory[i];
        }
    }
    count = new_count;
    printf("Expired medicines deleted.\n");
}

// Main menu
void menu() {
    int choice;
    while (1) {
        printf("\nPharmacy Store Management System\n");
        printf("1. Add Medicine\n");
        printf("2. Display Medicines\n");
        printf("3. Search Medicine\n");
        printf("4. Update Medicine\n");
        printf("5. Delete Expired Medicine\n");
        printf("6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: add_medicine(); break;
            case 2: display_medicines(); break;
            case 3: search_medicine(); break;
            case 4: update_medicine(); break;
            case 5: delete_expired_medicine(); break;
            case 6: exit(0);
            default: printf("Invalid choice!\n");
        }
    }
}

int main() {
    menu();
    return 0;
}
