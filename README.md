QUESTION 1 PART B
#include <iostream>
#include <string>
using namespace std;
class Vehicle
 {
public:
    virtual void start() = 0;  // First pure virtual function
    virtual void stop() = 0;   // Second pure virtual function
};
class Car : public Vehicle
{
private:
    string car_type;

public:
    void get_car_type(string type)
     {
        car_type = type;
        cout << "The type of the car is: " << car_type << endl;
    }
    void start() //overriding function
    {
        cout << "Your engine of " << car_type << " is working now" << endl;
    }
    void stop() //overriding function
    {
        cout << "Your engine of " << car_type << " is not working now" << endl;
    }
};
class Motorbike : public Vehicle
{
private:
    string motorbike_type;

public:
    void get_motorbike_type(string type)
     {
        motorbike_type = type;
        cout << "The type of motor bike is: " << motorbike_type << endl;
    }
    void start() //override function
     {
        cout << "Your engine of " << motorbike_type << " is working properly" << endl;
    }
    void stop() //override function
    {
        cout << "Your engine of " << motorbike_type << " is not working properly" << endl;
    }
};
int main()
{
    Car car1;
    Motorbike bike1;
    Vehicle *firstvehicle = &car1;
    Vehicle *secondvehicle = &bike1;
    cout << "*********CAR INFORMATION *********" << endl;
    car1.get_car_type("AUDI");
    firstvehicle->start();
    firstvehicle->stop();
    cout << "*********MOTORBIKE INFORMATION*********" << endl;
    bike1.get_motorbike_type("SPORTS");
    secondvehicle->start();
    secondvehicle->stop();
    return 0;
}
QUESTION 2:
#include<iostream>
#include<string>
using namespace std;
class Product
 {
public:
    int product_id;
    string product_name;
    double product_price;

    Product(int id, string name, double price)
     {
        product_id = id;
        product_name = name;
        product_price = price;
    }

    void display_product_details()
     {
        cout << "ID of product is " << product_id << endl;
        cout << "Name of the product is " << product_name << endl;
        cout << "Price of the product is $" << product_price << endl;
    }
};
class Shopping_cart
{
private:
    Product** products;
    int capacity;
    int size;

public:
    Shopping_cart(int capacity) : capacity(capacity), size(0)
     {
        products = new Product*[capacity];
    }
    ~Shopping_cart()
    {
        delete[] products;
    }
    void add_product(Product* product)
    {
        if (size < capacity)
            {
            products[size++] = product;
        }
        else
        {
            cout << "You cannot add more items because the shopping cart is full." << endl;
        }
    }

    void display_all_products()
     {
        cout << "Products in your cart are" << endl;
        for (int i = 0; i < size; ++i)
            {
            products[i]->display_product_details();
        }
    }
    double calculate_total_cost()
    {
        double totalCost = 0.0;
        for (int i = 0; i < size; ++i)
            {
            totalCost += products[i]->product_price;
        }
        return totalCost;
    }
};
class User
 {
public:
    int userId;
    Shopping_cart* shopping_cart;

    User(int id) : userId(id), shopping_cart(nullptr) {}

    void display_user_details()
     {
        cout << "Id used by user is " << userId << endl;
        if (shopping_cart)
            {
            cout << "DETAILS OF SHOPPING CART" << endl;
            shopping_cart->display_all_products();
            cout << "Total cost of products: $" << shopping_cart->calculate_total_cost() << endl;
        }
        else
        {
            cout << "No shopping cart is associated with this id." << endl;
        }
    }
};

int main()
 {
    // Creating some products
    Product product1(1, "watch", 889.97);
    Product product2(2, "Television", 400.77);
    // Creating a user
    User user1(110);
    // Creating a shopping cart
    Shopping_cart cart(2);
    // Adding products to the shopping cart
    cart.add_product(&product1);
    cart.add_product(&product2);
    // Associating the shopping cart with the user
    user1.shopping_cart = &cart;
    // Displaying user details
    user1.display_user_details();
    return 0;
}

