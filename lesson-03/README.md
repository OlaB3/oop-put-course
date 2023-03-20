#include <bits/stdc++.h>

using namespace std;

class Bouquet{
 public:
    std::string flower;
};

class Vase{
 public:
    string contents;
    int capacity;
    void Put(string flower, string contents){
        contents = flower;
        cout<<contents;
    };
};


int main()
{
    Vase a;
    Bouquet b;
    string flow;
    a.contents = "empty";
    cout<<"Flower type\n";
    cin>>b.flower;
    a.Put(b.flower, a.contents);

}
