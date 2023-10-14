class GroceryStore:
    def __init__(self):
        self.inventory = {}
        self.shopping_list = {}

    def add_item_to_inventory(self, item_name, quantity, price):
        self.inventory[item_name] = {'quantity': quantity, 'price': price}

    def add_item_to_shopping_list(self, item_name, quantity):
        if item_name in self.inventory:
            if quantity <= self.inventory[item_name]['quantity']:
                if item_name in self.shopping_list:
                    self.shopping_list[item_name] += quantity
                else:
                    self.shopping_list[item_name] = quantity
                self.inventory[item_name]['quantity'] -= quantity
            else:
                print(f"Not enough {item_name} in stock.")
        else:
            print(f"{item_name} not found in inventory.")

    def view_inventory(self):
        print("Inventory:")
        for item, info in self.inventory.items():
            print(f"{item} - Quantity: {info['quantity']}, Price: ${info['price']}")

    def view_shopping_list(self):
        print("Shopping List:")
        for item, quantity in self.shopping_list.items():
            print(f"{item} - Quantity: {quantity}")

# Usage example
store = GroceryStore()
store.add_item_to_inventory("Apples", 10, 1.0)
store.add_item_to_inventory("Bananas", 15, 0.5)

store.view_inventory()
store.add_item_to_shopping_list("Apples", 3)
store.add_item_to_shopping_list("Bananas", 7)

store.view_inventory()
store.view_shopping_list()
