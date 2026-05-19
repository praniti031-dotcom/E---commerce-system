#include <iostream>
#include <vector>
#include <iomanip>
using namespace std;
// ================= PRODUCT CLASS =================
class Product {
private:
    int id;
    string name;
    float price;
    string category;

public:
    Product(int i, string n, float p, string c) {
        id = i;
        name = n;
        price = p;
        category = c;
    }
    int getId() {
        return id;
    }
    string getName() {
        return name;
    }
    float getPrice() {
        return price;
    }
    string getCategory() {
        return category;
    }
    void displayProduct() {
        cout << left << setw(10) << id
             << setw(25) << name
             << setw(15) << category
             << "Rs. " << price << endl;
    }
};
// ================= CART ITEM CLASS =================
class CartItem {
private:
    Product product;
    int quantity;

public:
    CartItem(Product p, int q) : product(p), quantity(q) {}
    float getTotal() {
        return product.getPrice() * quantity;
    }
    void displayCartItem() {
        cout << left << setw(20) << product.getName()
             << setw(10) << quantity
             << "Rs. " << getTotal() << endl;
    }
};
// ================= E-COMMERCE SYSTEM =================
class ECommerceSystem {
private:
    vector<Product> products;
    vector<CartItem> cart;
public:
    // Add products to catalog
    void addProduct(Product p) {
        products.push_back(p);
    }
    // Display all products
    void showProducts() {
        cout << "\n========== PRODUCT CATALOG ==========\n";
        cout << left << setw(10) << "ID"
             << setw(25) << "Name"
             << setw(15) << "Category"
             << "Price\n";
        cout << "-----------------------------------------------------\n";
        for (int i = 0; i < products.size(); i++) {
            products[i].displayProduct();
        }
    }
    // Add item to cart
    void addToCart(int productId, int qty) {
        for (int i = 0; i < products.size(); i++) {
            if (products[i].getId() == productId) {
                CartItem item(products[i], qty);
                cart.push_back(item);
                cout << "\nProduct Added Successfully!\n";
                return;
            }
        }
        cout << "\nProduct Not Found!\n";
    }
    // Display cart
    void showCart() {
        if (cart.empty()) {
            cout << "\nCart is Empty!\n";
            return;
        }
        float grandTotal = 0;
        cout << "\n=============== CART ===============\n";
        cout << left << setw(20) << "Product"
             << setw(10) << "Qty"
             << "Total\n";
        cout << "------------------------------------------\n";
        for (int i = 0; i < cart.size(); i++) {
            cart[i].displayCartItem();
            grandTotal += cart[i].getTotal();
        }
        cout << "------------------------------------------\n";
        cout << "Grand Total = Rs. " << grandTotal << endl;
    }
};
// ================= MAIN FUNCTION =================
int main() {
    ECommerceSystem store;
    // Adding Products
    store.addProduct(Product(101, "Laptop", 55000, "Electronics"));
    store.addProduct(Product(102, "Smartphone", 25000, "Electronics"));
    store.addProduct(Product(103, "Headphones", 3000, "Accessories"));
    store.addProduct(Product(104, "T-Shirt", 800, "Clothing"));
    store.addProduct(Product(105, "Shoes", 2500, "Footwear"));
    int choice;
    int id, qty;
    do {
        cout << "\n=========== E-COMMERCE MENU ===========\n";
        cout << "1. View Products\n";
        cout << "2. Add Product to Cart\n";
        cout << "3. View Cart\n";
        cout << "4. Exit\n";
        cout << "Enter Your Choice: ";
        cin >> choice;
        switch(choice) {
            case 1:
                store.showProducts();
                break;
            case 2:
                cout << "\nEnter Product ID: ";
                cin >> id;
                cout << "Enter Quantity: ";
                cin >> qty;
                store.addToCart(id, qty);
                break;
            case 3:
                store.showCart();
                break;
            case 4:
                cout << "\nThank You For Shopping!\n";
                break;
            default:
                cout << "\nInvalid Choice!\n";
        }
    } while(choice != 4);
    return 0;
}
