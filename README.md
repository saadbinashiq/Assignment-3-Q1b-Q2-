# Assignment-3-Q1b-Q2-
     QUESTION 1 PART B "CODE"
#include <iostream>
#include <string>
using namespace std;

class Vehicle 
{
  public:
    virtual void showDetails() const = 0;
    virtual ~Vehicle() {}
};

class CompactCar : public Vehicle 
{ 
  private:
    string brand;
    string model;

  public:
    CompactCar(const string& brand, const string& model) : brand(brand), model(model) {}
    void showDetails() const 
    {
        cout << "Compact Car: " << brand << " " << model << endl;
    }
};

class Crossover : public Vehicle 
{
  private:
    string brand;
    string model;
  public:
    Crossover(const string& brand, const string& model) : brand(brand), model(model) {}
    void showDetails() const
    {
        cout << "Crossover: " << brand << " " << model << endl;
    }
};

void displayVehicleInfo(const Vehicle& vehicle)
{
    vehicle.showDetails();
}

int main() 
{
    CompactCar compact("Honda", "Civic");
    Crossover crossover("Haval", "H6");
    displayVehicleInfo(compact);
    displayVehicleInfo(crossover);
    return 0;
}


    QUESTION 2 "CODE"
#include <iostream>
#include <string>
using namespace std;

class ProductItem
{
  private:
    int itemCode;
    string itemName;
  public:
    double cost;
    ProductItem() : itemCode(0), itemName("Unknown"), cost(0.0) {}
    ProductItem(int code, const string& name, double price) : itemCode(code), itemName(name), cost(price) {}
    void displayProductItemDetails()
    {
        cout << "Item Code: " << itemCode << ", Name: " << itemName << ", Cost: $" << cost << endl;
    }
};

class ShoppingBasket
{
  private:
    static const int maxCapacity = 5;
    ProductItem items[maxCapacity];
    int itemCount;
    double totalAmount;
  public:
    ShoppingBasket() : itemCount(0), totalAmount(0.0) {}
    void addItemToBasket(const ProductItem& item)
    {
        if (itemCount < maxCapacity)
        {
            items[itemCount++] = item;
            totalAmount += item.cost;
        }
        else
        {
            cout << "Shopping Basket is full. Cannot add more items." << endl;
        }
    }

void displayAllItems() 
    {
        for (int i = 0; i < itemCount; ++i)
        {
            items[i].displayProductItemDetails();
        }
    }
    double calculateTotalAmount() 
    {
        return totalAmount;
    }
};

class Customer
{
  public:
    int customerID;
    Customer(int id) : customerID(id) {}
    void displayCustomerDetails() 
    {
        cout << "Customer ID: " << customerID << endl;
    }
};

class Order
{
  public:
    Customer* customer;
    ShoppingBasket* basket;
    Order(Customer* cust, ShoppingBasket* basket) : customer(cust), basket(basket) {}
    void displayOrderDetails() 
    {
        cout << "Order Details:" << endl;
        customer->displayCustomerDetails();
        cout << "Items in Basket:" << endl;
        basket->displayAllItems();
        cout << "Total Amount: $" << basket->calculateTotalAmount() << endl;
    }
};
int main() 
{
    ShoppingBasket basket;
    ProductItem item1(1, "Smartwatch", 149.99);
    ProductItem item2(2, "Bluetooth Earbuds", 39.99);
    basket.addItemToBasket(item1);
    basket.addItemToBasket(item2);
    cout << "All Items in Basket:" << endl;
    basket.displayAllItems();
    cout << "Total Amount: $" << basket.calculateTotalAmount() << endl;

  Customer customer1(201);
  customer1.displayCustomerDetails();

  Order order(&customer1, &basket);
    order.displayOrderDetails();
    return 0;
}
