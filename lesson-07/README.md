#include <iostream>
#include <string>

using namespace std;

class Sequence {
public:
    virtual int Length() = 0;
};

class FakeSequence : public Sequence {
public:
    int Length() override { return 100; }
};

class Gene {
private:
    Sequence* sequence;
    string name;

public:
    Gene(Sequence* sequence, const string& name) : sequence(sequence), name(name) {}

    void JSON() {
        cout << "{\n";
        cout << "\t\"Name\": \"" << name << "\",\n";
        cout << "\t\"length\": " << sequence->Length() <<endl;
        cout << "}\n";
    }
};
int main() {
    FakeSequence x;
    Gene gene(&x, "BALF5");

    gene.JSON();

    return 0;
}
