#include <iostream>
#include <string>
#include <vector>

using namespace std;

class Product {
protected:
    string name;
    int price;
    int id;

public:
    Product(const string name, double price, int id) : name(name), price(price), id(id) {}
    const string getName() const {
        return name;
    }
    int getPrice() const {
        return price;
    }
    int getId() const {
        return id;
    }
};

class Customer {
protected:
    string name;
    string email;
    int id;

public:
    Customer(const string name, const string email, int id) : name(name), email(email), id(id) {}
    const string getName() const {
        return name;
    }
    const string getEmail() const {
        return email;
    }
    int getId() const {
        return id;
    }
};

class Order {
private:
    int id;
    Customer customer;
    vector<Product> products;

public:
    Order(int id, const Customer& customer) : id(id), customer(customer) {}

    int getId() const {
        return id;
    }
    
    void addProduct(const Product& product) {
        products.push_back(product);
    }
    
    double getTotalCost() const {
        double total = 0;
        for (const auto& product : products) {
            total += product.getPrice();
        }
        return total;
    }
};

int main() {
    Product p1("Product_1", 9, 1);
    Product p2("Product_2", 14, 2);
    Product p3("Product_3", 21, 3);
    Product p4("Product_4", 62, 4);

    Customer c1("Anna Nowak", "anna.nowak@gmail.com", 1);

    Order o1(1, c1);

    o1.addProduct(p1);
    o1.addProduct(p2);
    o1.addProduct(p3);

    double total = o1.getTotalCost();

    cout << "Order #" << o1.getId() << endl;
    cout << "Total cost: " << total << endl;
    
    Customer c2("Jan Kowalski", "j.k@gmail.com", 2);
    
    Order o2(2, c2);
    
    o2.addProduct(p1);
    o2.addProduct(p4);
    
    double total2 = o2.getTotalCost();
    
    cout << "Order #" << o2.getId() << endl;
    cout << "Total cost: " << total2 << endl;

    return 0;
}
