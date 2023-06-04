#include <iostream>

using namespace std;

class Interface {
public:
    virtual int Number() const = 0;
};

class MyNumber : public Interface {
private:
    const int number;

public:
    MyNumber(int num) : number(num) {}

    int Number() const {
        return number;
    }
};

int main()
{
    MyNumber a1(8);
    cout << a1.Number() << endl;

    MyNumber a2(22);
    cout << a2.Number() << endl;

    return 0;
}
