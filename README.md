# Assignment-3-Q1b-Q2-
QUESTION 1 PART B "CODE"
#include <iostream>
#include <string>
using namespace std;
class Car
{
public:
    virtual void displayInfo() const = 0;
    virtual ~Car() {}
};
class Sedan : public Car
{
private:
    string make;
    string model;
public:
    Sedan(const string& make, const string& model) : make(make), model(model) {}
    void displayInfo() const
    {
        cout << "Sedan: " << make << " " << model << endl;
    }
};
class SUV : public Car
{
private:
    string make;
    string model;

public:
    SUV(const string& make, const string& model) : make(make), model(model) {}
    void displayInfo() const
    {
        cout << "SUV: " << make << " " << model << endl;
    }
};
void displayCarInfo(const Car& car)
{
    car.displayInfo();
}

int main()
{
    Sedan sedan("Toyota", "Grande");
    SUV suv("Ford", "Explorer");
    displayCarInfo(sedan);
    displayCarInfo(suv);
    return 0;
}

QUESTION 2 "CODE"
#include <iostream>
#include <string>
using namespace std;
class Product 
{
 public:
    Product() : productId(0), productName("Unknown"), price(0.0) {}
    int productId;
    string productName;
    double price;
     Product(int id, const string& name, double p) : productId(id), productName(name), price(p) {}
    void displayProductDetails()
    {
        cout << "Product ID: " << productId << ", Name: " << productName << ", Price: $" << price << endl;
    }
};
 class ShoppingCart 
 {
   private:
    static const int maxCapacity = 5;
    Product products[maxCapacity];
    int size;
    double totalCost;
   public:
    ShoppingCart() : size(0), totalCost(0.0) {}
     void addProduct(const Product& product) 
     {
        if (size < maxCapacity)
        {
            products[size++] = product;
            totalCost += product.price;
        }
        else 
        {
            cout << "Shopping Cart is full. Cannot add more products." << endl;
        }
     }
         void displayAllProducts() 
         {
           for (int i = 0; i < size; ++i)
           {
             products[i].displayProductDetails();
           }
         }
             double calculateTotalCost() 
             {
                return totalCost;
             }
};
 class User 
 {
   public:
    int userId;
    ShoppingCart* cart;  // Aggregation - pointer to ShoppingCart
        User(int id) : userId(id), cart(nullptr) {}

    void displayUserDetails() 
    {
        cout << "User ID: " << userId << endl;
    }
};

int main()
{
    // Demonstrating Composition
    ShoppingCart cart;
    Product p1(1, "washing machine", 10.99);
    Product p2(2, "refrigerator", 5.99);
    cart.addProduct(p1);
    cart.addProduct(p2);
    cout << "All Products in Cart:" << endl;
    cart.displayAllProducts();
    cout << "Total Cost: $" << cart.calculateTotalCost() << endl;
    // Demonstrating Association
    User user1(101);
    user1.cart = &cart;  // Assigning the address of cart to the pointer in User
    user1.displayUserDetails();
    cout << "User's Cart Details:" << endl;
    user1.cart->displayAllProducts();  // Accessing the ShoppingCart through the pointer
    return 0;
}
