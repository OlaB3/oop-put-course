#include <iostream>
#include <map>

using namespace std;

class Cantor {
 public:
  Cantor() = default;
  virtual ~Cantor() = default;

  virtual double Rate(const std::string& abbreviation) const = 0;
};



class FakeUsdCantor : public Cantor {
 public:
  FakeUsdCantor() {
    rates_ = {
      {"EUR", 0.85},
      {"JPY", 110.66},
      {"GBP", 0.73},
      {"CHF", 0.91},
      {"CAD", 1.25},
      {"AUD", 1.34},
      {"CNY", 6.47},
      {"HKD", 7.78},
      {"NZD", 1.44},
      {"KRW", 1153.89}
    };
  }

  double Rate(const std::string& abbreviation) const override {
    auto it = rates_.find(abbreviation);
    if (it != rates_.end()) {
      return it->second;
    }
    // Handle error case when currency abbreviation is not found
    return 0.0;
  }

 private:
  std::map<std::string, double> rates_;
};

class Currency {
 public:
  Currency() = default;
  virtual ~Currency() = default;

  virtual double ConvertedToDollars(const Cantor& cantor) const = 0;
  virtual std::string Abbreviation() const = 0;
  virtual double Amount() const = 0;
};

class Pound : Currency{
 private:
    string abbreviation;
    double amount;
 public:
    Pound(string NewAbbr, double NewAm){
        this -> abbreviation = NewAbbr;
        this -> amount = NewAm;
    }
    string Abbreviation() const{
        return abbreviation;
    }
    double Amount() const{
        return amount;
    }
    double ConvertedToDollars(const Cantor& cantor) const{
        return amount / cantor.Rate(abbreviation) ;
    }
    
};

int main() {
    FakeUsdCantor fake;
    Pound value("GBP", 100);
    cout<<value.ConvertedToDollars(fake)<<endl;
  return 0;
}
