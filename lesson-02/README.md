#include <iostream>

using namespace std;

class Human
{
public:
    string name;
    int age;
    int weight;
    int growth;
};

class Nature
{
public:
    string flora;
    string fauna;
    int temperature;
};

class Date
{
public:
    int day;
    int month;
    int year;
    int hour;
};

class Building
{
public:
    string residential;
    string services;
    string street;
    int adress;
};

int main()
{
    Human a;
    Nature b;
    Date c;
    Building d;
    a.name = "Anna Nowak";
    a.age = 25;
    a.weight = 55;
    a.growth = 170;
    b.flora = "Plants";
    b.fauna = "Animals";
    b.temperature = 20;
    c.day = 13;
    c.month = 3;
    c.year = 2023;
    c.hour = 14;
    d.residential = "House";
    d.services = "hospital";
    d.street = "Main street";
    d.adress = 26;
    
    return 0;
}
