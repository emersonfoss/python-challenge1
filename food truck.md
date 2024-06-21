# menu.py

# Define the menu items
menu_items = {
    1: {"Item name": "Apple", "Price": 0.49},
    2: {"Item name": "Tea - Thai iced", "Price": 3.99},
    3: {"Item name": "Fried banana", "Price": 4.49}
}

# Function to print the menu
def print_menu():
    print("Menu:")
    for key, value in menu_items.items():
        print(f"{key}: {value['Item name']} - ${value['Price']:.2f}")
    print()

# Function to take the order
def take_order():
    order = []
    while True:
        print_menu()
        menu_selection = input("Enter the number of the item you would like to order: ")
        if not menu_selection.isdigit():
            print("Invalid input. Please enter a number.")
            continue

        menu_selection = int(menu_selection)
        if menu_selection not in menu_items:
            print("Invalid selection. Please choose a valid item number.")
            continue

        item_name = menu_items[menu_selection]["Item name"]
        price = menu_items[menu_selection]["Price"]
        
        quantity_input = input(f"How many {item_name}s would you like? (Default is 1 if input is invalid): ")
        if not quantity_input.isdigit():
            quantity = 1
        else:
            quantity = int(quantity_input)

        order.append({"Item name": item_name, "Price": price, "Quantity": quantity})
        
        while True:
            continue_ordering = input("Would you like to order another item? (y/n): ").lower()
            match continue_ordering:
                case 'y':
                    break
                case 'n':
                    print("Thank you for your order.")
                    return order
                case _:
                    print("Invalid input. Please enter 'y' or 'n'.")

# Function to print the receipt
def print_receipt(order):
    print("\nReceipt:")
    print(f"{'Item name':<25} | {'Price':<6} | {'Quantity':<8}")
    print("-" * 45)
    total_price = 0
    for item in order:
        item_name = item["Item name"]
        price = item["Price"]
        quantity = item["Quantity"]
        total_price += price * quantity

        print(f"{item_name:<25} | ${price:<5.2f} | {quantity:<8}")

    print("-" * 45)
    print(f"{'Total':<25} | ${total_price:<5.2f}")
    print()

def main():
    order = take_order()
    print_receipt(order)

if __name__ == "__main__":
    main()
