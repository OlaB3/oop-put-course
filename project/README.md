# This directory contains solution to the project

#include <iostream>
#include <string>
#include <fstream>
#include <vector>
using namespace std;

class Book
{
private:
    vector<int> selectedBooks;
    vector<Book> books;
protected:
    double price;
    int index, quant;
    string cat, bcode, name, author;
public:
    Book(int id, const string n, const string aut, const string catg, int q, double p, const string bc) 
        : index(id), name(n), author(aut), cat(catg), quant(q), price(p), bcode(bc) {}
    Book(int x, int y) {}

    double getPrice() const
    {
        return price;
    }

    int getQuantity() const
    {
        return quant;
    }
    string getBarcode() const
    {
        return bcode;
    }
    int getID() const
    {
        return index;
    }

    void selectBook(int book_id)
    {
        selectedBooks.push_back(book_id);
    }

    void ChangeQ(int id, int amount)
    {
        if (amount <= 0)
        {
            throw - 1;
        }
        else
        {
            for (int bookId : selectedBooks)
            {
                for (const Book& book : books)
                {
                    if (book.getID() == bookId)
                    {
                        quant += amount;
                    }
                }
            }
        }

    }

    void AddBook()
    {
        ofstream File;
        File.open("DataBase.txt", ios::app);
        if (File.is_open())
        {
            string text;
            cout << "Book ID: ";
            getline(cin, text);
            File << text << "\n";
            cout << "Name the title: ";
            getline(cin, text);
            File << text << "\n";
            cout << "Enter the author: ";
            getline(cin, text);
            File << text << "\n";
            cout << "Enter a category: ";
            getline(cin, text);
            File << text << "\n";
            cout << "Enter quantity: ";
            getline(cin, text);
            File << text << "\n";
            cout << "Enter the price: ";
            getline(cin, text);
            File << text << "\n";
            cout << "Scan the barcode: ";
            getline(cin, text);
            File << text << "\n";
            File.close();
        }
    }

    void Show()
    { 
        string tab[7] = { "ID", "Name", "Author", "Category", "Quantity", "Price", "Barcode" };
        cout << tab[0] << " | " << tab[1] << " | " << tab[2] << " | " << tab[3] << " | " << tab[4] << " | " << tab[5] << " | " << tab[6] << endl;

        ifstream FileOpen2("DataBase.txt");
        if (FileOpen2.is_open())
        {
            int i = 0;
            string line;
            while (getline(FileOpen2, line))
            {
                cout << line << " | ";
                i++;
                if (i % 7 == 0)
                {
                    cout << endl;
                }
            }
            FileOpen2.close();
        }
        cout << endl;
        
    }
};

class Customer
{
private:
    string full_name;
public:
    int id, card;
    Customer(int a, string b, int c) : id(a), full_name(b), card(c) {}
};

class Bill : public Customer, public Book
{
private: 
    vector<int> selectedBooks;
    vector<string> selectedCode;
    vector<Book> books;

public: 
    Bill(int cust_id, string name, int card_num) : Book(0,"", "", "", 0.0, 0, ""), Customer(cust_id,"", card_num) {}

    void selectBook(int book_id)
    {
        selectedBooks.push_back(book_id);
    }

    void addBookByBarcode(const string& barcode) 
    {
        selectedCode.push_back(barcode);
    }

    double Sum(const vector<Book>& books)
    {
        double sum = 0.0;
        for (int bookId : selectedBooks)
        {
            for (const Book& book : books)
            {
                if (book.getID() == bookId)
                {
                    sum += book.getPrice();
                    break;
                }
                if (book.getID() == bookId)
                {
                    sum += book.getPrice();
                    break;
                }
            }
        }
        return sum;
    }
    
        
    double Sum2(const vector<Book>&books)
    {
        double sum2 = 0.0;
        for (string bookBcode : selectedCode)
        {
            for (const Book& book : books)
            {
                if (book.getBarcode() == bookBcode)
                {
                    sum2 += book.getPrice();
                    break;
                }
                if (book.getBarcode() == bookBcode)
                {
                    sum2 += book.getPrice();
                    break;
                }
            }
        }

        return sum2;
    }
};

int main()
{
    int num;
    string name = "BookShop";

    do
    {
        cout << "Welcom in " << name << " !" << endl;
        cout << "What would you like to do?" << endl;
        cout << "0 - close system" << endl << "1 - See database" << endl << "2 - Add book" << endl << "3 - Open receipt" << endl << "4 - Change quantity" << endl;
        cin >> num;
        if (num < 0 || num > 4)
        {
            cout << "There is no such option" << endl << endl;
            continue;
        }
        Book b1(1, "Wesele", "Stanislaw Wyspianski", "moral", 4, 24.99, "A9788388435027");
        Book b2(2, "Slownik Angielsko-Polski", "Tomasz Wyzynski", "dictionary", 10, 34, "A9788372274236");
        Book b3(3, "The Valley of Fear", "Arthur Conan Doyle", "cryminal", 16, 19.99, "A9788365884879");
        Book b4(4, "Harry Potter", "J. K. Rowling ", "fantasy", 20, 39.99, "-");
        Book b5(5, "Zaklety w czasie", "Artur Skura", "comics", 6, 26.99, "A9788328199521");

        vector<Book> books = { b1, b2, b3, b4, b5 };

        Customer c1(1, "Jane Doe", 111);
        Customer c2(2, "John Doe", 0);
        Customer c3(3, "Anne Smith", 333);

        
        if (num == 1)
        {
            b1.Show();
        }
        if (num == 2)
        {
            b1.AddBook();
        }
        if (num == 3)
        {
            Bill bill(c1.id, "", c1.card);

            bill.selectBook(5);
            bill.addBookByBarcode("A9788372274236");
            bill.addBookByBarcode("A9788388435027");
            bill.selectBook(2);

            double total = bill.Sum(books) + bill.Sum2(books);
            if (bill.card != 0)
            {
                total = total * 0.95;
            }

            cout << "Total sum: " << total << "zl" << endl << endl;
        }
        if (num == 4)
        {
            int new_quant, x;
            cout << "Enter quantity: ";
            cin >> new_quant;
            cout << "Enter index: ";
            cin >> x;
            try
            {
                Book book(x, new_quant);
                book.ChangeQ(x, new_quant);
            }
            catch(int)
            {
                cout << "Quantity can't be less than 0" << endl << endl;
            }
            

        }


    } while (num != 0);


    return 0;

}
