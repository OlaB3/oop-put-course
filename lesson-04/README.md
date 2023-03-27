#include <iostream>

using namespace std;


class Nature{ 
private: 
    double temperature; 
    
public:
    double Temp() {return this -> temperature;};
    Nature() {this -> temperature = 8.56;};
    Nature(double x) {this -> temperature = x;};
    Nature(int x) : Nature(static_cast<double>(x)) {};
   
    
};

int main(){
    
    Nature mynat;
    cout<<mynat.Temp()<<endl;
    Nature x(8);
    cout<<x.Temp();

return 0;
}
