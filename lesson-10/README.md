#include <iostream>
#include <vector>
#include <thread>
#include <mutex>
#include <atomic>

using namespace std;

mutex mtx; 
atomic<int> counter[4];


	void Count(const string& sequence, int start, int stop)
	{
		unique_lock<std::mutex> lock(mtx);
		int a = 0, c = 0, g = 0, t = 0;
		for (int i = 0; i < stop; i++)
		{
			char nucleotide = sequence[i];
			if (nucleotide == 'A')
			{
				a++;
			}
			else if (nucleotide == 'C')
			{
				c++;
			}
			else if (nucleotide == 'G')
			{
				g++;
			}
			else if (nucleotide == 'T')
			{
				t++;
			}
		}
		counter[0] += a;
		counter[1] += c;
		counter[2] += g;
		counter[3] += t;
	}

	void Thread(const string& sequence, int length)
	{
		vector<thread> thread;
		for (int i = 0; i < 4; ++i)
		{
			int start = i * (length / 4);
			int end = (i == 3) ? length : (i + 1) * (length / 4);
			thread.emplace_back(Count, ref(sequence), start, end);
		}
		for (auto& thread : thread) 
		{
			thread.join();
		}
	}



int main()
{
	string sequence("ACGTGTTCATGATCTACAGTCAGCTATGGCTACGAGTCAGACTATGCA");
	int length = sequence.length();
	
	Thread(sequence, length);

	cout << "A: " << counter[0] << endl << "C: " << counter[1] << endl << "G: " << counter[2] << endl << "T: " << counter[3] << endl;

	return 0;
}
