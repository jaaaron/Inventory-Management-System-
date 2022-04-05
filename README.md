# Inventory Management System

###### Manage products in a stockroom with features include loading data from a file displaying items and products with barcode lookup

![Software Example](https://github.com/jaaaron/Inventory-Management-System-/blob/main/inventory.gif)
'''
#include <iostream>
#include <fstream>
using namespace std;

#define MAX 50
//declare functions
int getData(ifstream& inFile,int id[],double price[],int qty[],int rop[]);
void output(int id[],double price[],int qty[],int rop[],int num);
int seqSearch(int id[], int n, int target);
void sortSelection(double arr[],int n, int id[], int qty[], int rop[]);

int main(void)
{
    //Declare variables
    ifstream inFile;
    int id[MAX];
    double price[MAX];
    int qty[MAX];
    int rop[MAX];
    int number; int target; int loc;

    //Open file
    inFile.open("products.txt");
    if(inFile.fail()){
        cout << "No Such File" << endl;
    }
    
    //Input the entire contents of the product file
    number = getData(inFile, id, price, qty, rop);
    //Output each product's id, quantity on hand, re-order point, and price
    output(id, price, qty, rop, number);
    
    //Looking for a particular product - next webinar
    cout << "Enter product number you are looking for: ";
    cin >> target;
    loc = seqSearch(id, number, target);
    if (loc == -1){
        cout << "No such product!" << endl;
    } else {
        cout << "Price: " << price[loc] << " " << "Quantity: " << qty[loc] << endl;
    }

    //Sort by the product id - next webinar
    sortSelection(price, number, id, qty, rop);

    //Output each product's id, quantity on hand, re-order point, and price
    output(id, price, qty, rop, number);
    system("pause");
    return 0;
}
int getData(ifstream& inFile,int id[],double price[],int qty[],int rop[]){
    /* Pre: infile - reference to the data file
     id[] - array of product identification numbers
     price[] - array of cost for each product
     qty[] - array of numbers of product in the warehouse
     rop[] - array of when to reorder that product
     Post: how many products
     Purpose: Input the inventory from the data file
     */
    int count = 0;
    
    while(count < MAX && !inFile.eof()){
        inFile >> id[count] >> price[count] >> qty[count] >> rop[count];
        count++;
    }
    
    return count;
}
int seqSearch(int arr[], int n, int target){
    /* Pre: arr - array of values
     n - number of defined values
     target - what we are looking for
     Post: Location of what we are looking for or -1 if not found
     Purpose: Find the location of value
     */
    int loc = -1;
    for (int i = 0; i < n; i++){
        if (target == arr[i]){
            loc = i;
        }
    }
    
    return loc;
}//seqSearch
void sortSelection(double arr[],int n, int id[], int qty[], int rop[]){
    /* Pre:
     arr[] - array of values
     number - number of elements
     Post: Nothing
     Purpose: sort elements from low to high
     */
    int walker; int current; int tempInt;
    int smallestIndex; double tempDouble;
    
    for (current = 0; current < n - 1; current++)
        {
           smallestIndex = current;
           for(walker = current + 1; walker < n; walker++)
           {
            if(arr[walker] < arr[smallestIndex])
              smallestIndex = walker;
           }//for walker
        
    //Swap
    tempDouble = arr[current];
    arr[current] = arr[smallestIndex];
    arr[smallestIndex] = tempDouble;

    tempInt = id[current];
    id[current] = id[smallestIndex];
    id[smallestIndex] = tempInt;
        
    tempInt = qty[current];
    qty[current] = qty[smallestIndex];
    qty[smallestIndex] = tempInt;
        
    tempInt = rop[current];
    rop[current] = rop[smallestIndex];
    rop[smallestIndex] = tempInt;

    }//for current
    
}
void output(int id[],double price[],int qty[],int rop[],int n){
    /* Pre:
     id[] - array of product identification numbers
     price[] - array of cost for each product
     qty[] - array of numbers of product in the warehouse
     rop[] - array of when to reorder that product
     n - number of products in our inventoru
     Post: nothing
     Purpose: Output inventory to screen
     */
    for (int i=0; i<n;i++)
        cout << id[i] << " " << price[i] << " " << qty[i] << " " << rop[i] << endl;
    
    return;
}// output
'''
