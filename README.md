"""
# 🛍️ Modern E-Commerce App in Python

> A clean, modular, object-oriented e-commerce simulation built with Python.  
> Handles products, deals, ratings, orders, delivery charges, and category-specific features.

![Python](https://img.shields.io/badge/Python-3.10-blue.svg?style=for-the-badge&logo=python)
![OOP](https://img.shields.io/badge/Concepts-OOP-orange.svg?style=for-the-badge&logo=code)


---

## 🔥 Features

- 🎯 Clean OOP Design: Product, ElectronicItems, Laptop, GroceryItems, and Order classes
- 💵 Auto Deal Price Calculation & Savings Summary
- 🛒 Cart System: Add multiple items with quantity
- 🚚 Delivery Mode Selection + Charges
- 📦 Class-Specific Details (Warranty, RAM, Storage, Expiry Dates)
- 📊 Total Bill Generator with Real-Time Calculation
"""

# ------------------------------
# 📦 CLASS DEFINITIONS
# ------------------------------

class Product:
    def __init__(self, name, price, deal_price, ratings):
        self.name = name
        self.price = price
        self.deal_price = deal_price
        self.ratings = ratings
        self.you_saved = price - deal_price

    def display_product_details(self):
        print(f"Product     : {self.name}")
        print(f"Price       : ₹{self.price}")
        print(f"Deal Price  : ₹{self.deal_price}")
        print(f"Rating      : {self.ratings}⭐")
        print(f"You Saved   : ₹{self.you_saved}")

    def get_deal_price(self):
        return self.deal_price


class ElectronicItems(Product):
    def __init__(self, name, price, deal_price, ratings, warranty_in_months):
        super().__init__(name, price, deal_price, ratings)
        self.warranty_in_months = warranty_in_months

    def display_product_details(self):
        super().display_product_details()
        print(f"Warranty    : {self.warranty_in_months} months\n")


class Laptop(ElectronicItems):
    def __init__(self, name, price, deal_price, ratings, warranty_in_months, RAM, storage):
        super().__init__(name, price, deal_price, ratings, warranty_in_months)
        self.RAM = RAM
        self.storage = storage

    def display_product_details(self):
        super().display_product_details()
        print(f"RAM         : {self.RAM}")
        print(f"Storage     : {self.storage}\n")


class GroceryItems(Product):
    def __init__(self, name, price, deal_price, ratings, expiry_date):
        super().__init__(name, price, deal_price, ratings)
        self.expiry_date = expiry_date

    def display_product_details(self):
        super().display_product_details()
        print(f"Expiry Date : {self.expiry_date}\n")


class Order:
    Delivery_charges = {
        "Normal": 0,
        "Prime": 100
    }

    def __init__(self, Delivery_method, Delivery_add):
        self.items_in_cart = []
        self.Delivery_method = Delivery_method
        self.Delivery_add = Delivery_add

    def add_items(self, product, quantity):
        self.items_in_cart.append((product, quantity))

    def get_total_bill(self):
        total = sum(p.get_deal_price() * q for p, q in self.items_in_cart)
        delivery = Order.Delivery_charges[self.Delivery_method]
        return total + delivery

    def display_order_details(self):
        print(f"\n🛒 Delivery Method : {self.Delivery_method}")
        print(f"🏠 Delivery Address: {self.Delivery_add}")
        print("📦 Products:")
        print("------------")
        for product, quantity in self.items_in_cart:
            product.display_product_details()
            print(f"Quantity     : {quantity}\n")
        print(f"💰 Total Bill : ₹{self.get_total_bill()}")
        print("------------\n")

    @classmethod
    def update_delivery_charges(cls, method, charge):
        cls.Delivery_charges[method] = charge

# ------------------------------
# 🚀 USAGE EXAMPLE
# ------------------------------

if __name__ == "__main__":
    tv = ElectronicItems("TV", 35000, 30000, 4.5, 24)
    milk = GroceryItems("Milk", 40, 30, 4.2, "Aug 2025")
    laptop = Laptop("Lenovo ABC", 45000, 40000, 4.5, 24, "16GB", "1TB SSD")

    order = Order("Normal", "Sangamner")
    order.add_items(tv, 1)
    order.add_items(milk, 4)
    order.add_items(laptop, 1)

    order.display_order_details()

"""
## 🧠 Concepts Practiced

- Inheritance & Superclass Initialization  
- Class Methods & Class Variables  
- Polymorphism via display_product_details()  
- Realistic Simulation of E-Commerce Models

## 🛠 Future Enhancements

- ✅ GUI with Tkinter or Flask web frontend  
- ✅ Add remove_items() and search feature  
- ✅ Add discount coupons or promo code handling  
- ✅ Add stock/inventory management  



## 🙌 Connect with Me

Made with ❤️ by Pranav – Innovating the future of code.
"""
