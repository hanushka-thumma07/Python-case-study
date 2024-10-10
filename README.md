# Python-case-study
# A simple product class for managing products
class Product:
    def __init__(self, pid, name, category, price):
        self.pid = pid
        self.name = name
        self.category = category
        self.price = price

    def __str__(self):
        return f"ID: {self.pid}, Name: {self.name}, Category: {self.category}, Price: ${self.price}"


# Product Manager Class
class ProductManager:
    def __init__(self):
        self.products = {}

    # 1. Add product
    def add_product(self, pid, name, category, price):
        if pid in self.products:
            print("Product ID already exists!")
        else:
            self.products[pid] = Product(pid, name, category, price)
            print("Product added successfully!")

    # 2. Update product
    def update_product(self, pid, name=None, category=None, price=None):
        if pid in self.products:
            if name:
                self.products[pid].name = name
            if category:
                self.products[pid].category = category
            if price:
                self.products[pid].price = price
            print("Product updated successfully!")
        else:
            print("Product not found!")

    # 3. Delete product
    def delete_product(self, pid):
        if pid in self.products:
            del self.products[pid]
            print("Product deleted successfully!")
        else:
            print("Product not found!")

    # 4. Get product by PID
    def get_product_by_pid(self, pid):
        if pid in self.products:
            print(self.products[pid])
        else:
            print("Product not found!")

    # 5. Get all products
    def get_all_products(self):
        if self.products:
            for product in self.products.values():
                print(product)
        else:
            print("No products available!")

    # 6. Get product by category
    def get_products_by_category(self, category):
        found = False
        for product in self.products.values():
            if product.category == category:
                print(product)
                found = True
        if not found:
            print("No products found in this category.")

    # 7. Get products between prices
    def get_products_between_prices(self, low_price, high_price):
        found = False
        for product in self.products.values():
            if low_price <= product.price <= high_price:
                print(product)
                found = True
        if not found:
            print("No products found in this price range.")


# Menu-driven application
def product_app():
    manager = ProductManager()

    while True:
        print("\nProduct App Menu:")
        print("1. Add product")
        print("2. Update product")
        print("3. Delete product")
        print("4. Get product by PID")
        print("5. Get all products")
        print("6. Get product by category")
        print("7. Get products between prices")
        print("8. Exit")

        choice = int(input("Enter your choice (1-8): "))

        if choice == 1:
            pid = input("Enter Product ID: ")
            name = input("Enter Product Name: ")
            category = input("Enter Product Category: ")
            price = float(input("Enter Product Price: "))
            manager.add_product(pid, name, category, price)

        elif choice == 2:
            pid = input("Enter Product ID to update: ")
            name = input("Enter new Product Name (leave blank to skip): ")
            category = input("Enter new Product Category (leave blank to skip): ")
            price_input = input("Enter new Product Price (leave blank to skip): ")
            price = float(price_input) if price_input else None
            manager.update_product(pid, name, category, price)

        elif choice == 3:
            pid = input("Enter Product ID to delete: ")
            manager.delete_product(pid)

        elif choice == 4:
            pid = input("Enter Product ID to fetch: ")
            manager.get_product_by_pid(pid)

        elif choice == 5:
            manager.get_all_products()

        elif choice == 6:
            category = input("Enter Product Category to search: ")
            manager.get_products_by_category(category)

        elif choice == 7:
            low_price = float(input("Enter minimum price: "))
            high_price = float(input("Enter maximum price: "))
            manager.get_products_between_prices(low_price, high_price)

        elif choice == 8:
            print("Exiting the app.")
            break

        else:
            print("Invalid choice! Please try again.")


# Running the app
if __name__ == "__main__":
    product_app()
