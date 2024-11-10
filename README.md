# Cafe-management-system
\\\Swayam - Arrays for storing menu details and storing orders.

\\\Jaya - Function to display menu and input choice from the customer.

\\\Ishu - Function to take an order from the customer.

\\\Ria - Function to generate bill.

\\\Gaurav - Totalling of all items and calling all functions in main function.

Macro functions used are :- #define MAX_ITEMS 7, #define MAX_ORDERS 10

Arrays used are :- item_ids[MAX_ITEMS], item_names[MAX_ITEMS][30], item_prices[MAX_ITEMS], orderitem_ids[MAX_ORDERS], orderquantities[MAX_ORDERS] 

Functions used are :- displayMenu(), takeOrder(), generateBill(), main()

Loops used :- for, while 
````
#include <stdio.h>
#include <string.h>

#define MAX_ITEMS 7
#define MAX_ORDERS 10

int item_ids[MAX_ITEMS] = {1, 2, 3, 4, 5,6,7};
char item_names[MAX_ITEMS][30] = {"Coffee", "Tea", "Sandwich", "Cake", "Burger","Salad","Coke",};
int item_prices[MAX_ITEMS] = {250, 100, 100, 300, 200,100,150};


int orderitem_ids[MAX_ORDERS];
int orderquantities[MAX_ORDERS];
int ordercount = 0;


void displayMenu() {
    printf("---- Cafe Menu ----\n");
    for (int i = 0; i < MAX_ITEMS; i++) {
        printf("%d. %s - %d\n", item_ids[i], item_names[i], item_prices[i]);
    }
    printf("-------------------\n");
}


void takeOrder() {
    int choice, quantity;
    ordercount = 0;
    
    while (1) {
        printf("Enter item ID to order (0 to finish): ");
        scanf("%d", &choice);

        if (choice == 0) break;

        int found = -1;
        for (int i = 0; i < MAX_ITEMS; i++) {
            if (item_ids[i] == choice) {
                found = i;
                break;
            }
        }

        if (found == -1) {
            printf("Invalid item ID. Please try again.\n");
        } else {
            printf("Enter quantity for %s: ", item_names[found]);
            scanf("%d", &quantity);

            orderitem_ids[ordercount] = choice;
            orderquantities[ordercount] = quantity;
            ordercount++;
        }
    }
}


void generateBill() {
    float total = 0.0;
    printf("----- Order Bill -----\n");
    for (int i = 0; i < ordercount; i++) {
        int item_id = orderitem_ids[i];
        int quantity = orderquantities[i];

        
        int item_index = -1;
        for (int j = 0; j < MAX_ITEMS; j++) {
            if (item_ids[j] == item_id) {
                item_index = j;
                break;
            }
        }

        if (item_index != -1) {
            float item_total = item_prices[item_index] * quantity;
            total += item_total;
            printf("%s x %d = %.2f\n", item_names[item_index], quantity, item_total);
        }
    }
    printf("----------------------\n");
    printf("Total: %.2f\n", total);
}

int main() {
    printf("Welcome to the Cafe!\n");
    displayMenu();
    
    takeOrder();
    generateBill();

    printf("Thank you for your order!\n");
    return 0;
}
````
