#include <iostream>
#include <cmath>

using namespace std;
class LogExeption : public runtime_error{
 public:
  explicit LogExeption(const string& message)
    : runtime_error(message) {}
};
class Logarithm{
 public:
  Logarithm(double base, double number) {
      base_ = base;
      number_ = number;
  }
  double Calculate() const {
      if(base_<=0){
          throw LogExeption("Base less or equal to zero");
      }
      if(base_ == 1){
          throw LogExeption("Base is equal to one");
      }
      if(number_ <=0){
          throw LogExeption("Number less than zero");
      }
      else{
          return log(number_) / log(base_);
      }
  }
 private:
  double number_;
  double base_;
};

int main()
{
    double base, number;
    cin>>base;
    cin>>number;
    try{
        Logarithm a(base,number);
    cout<<a.Calculate();
    }catch(LogExeption& e){
        cerr<<"Error: "<<e.what()<<endl;
    }
    
}
