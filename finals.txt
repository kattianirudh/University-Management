#include<iostream>
#include<stdio.h>
#include<stdlib.h>
#include<conio.h>
#include<string>
#include<fstream>
using namespace std;
int n;
class record
{
public:
	char index[10], colname[30], colrank[20], branches[10], city[20], elrank[10];
}rec[40], found[40], s[50], r[50];
class temp
{
public:
	char index[10], colname[30], colrank[20], branches[10], city[20], elrank[10];
}t[50];
int m = 0;
class student
{
public:
	void add()
	{
		int i;
		cout << "Enter number of colleges: ";
		cin >> n;
		cout << "Enter college name,college rank,no.of branches,city,eligibility rank\n";
		n = m + n;
		fstream n2("n.txt", ios::in);
		int pp = 0;
		n2 >> pp;
		int z = n + pp;
		for (i = pp; i < z; i++)
		{
			cout << "college " << i + 1 << " :\n";
			cin >> rec[i].colname >> rec[i].colrank >> rec[i].branches >> rec[i].city >> rec[i].elrank;
		}
	}
	void sort_records()
	{
		int i, j, no;
		fstream is("n.txt", ios::in);
		fstream f1("record.txt", ios::in);
		is >> no;
		for (i = 0; i < no; i++)
		{
			f1 >> s[i].index >> s[i].colrank >> s[i].colname >> s[i].branches >> s[i].city >> s[i].elrank;
		}
		record temp;
		for (i = 0; i < no - 1; i++)
		{
			for (j = 0; j < no - i - 1; j++)
			{
				if (strcmp(s[j].colname, s[j + 1].colname) > 0)
				{
					temp = s[j];
					s[j] = s[j + 1];
					s[j + 1] = temp;
				}
				else if (strcmp(s[j].colname, s[j + 1].colname) == 0)
				{
					if (strcmp(s[j].colrank, s[j + 1].colrank) > 0)
					{
						temp = s[j];
						s[j] = s[j + 1];
						s[j + 1] = temp;
					}
				}
			}
		}
		for (i = 0; i < no; i++)
			cout << "COLLEGE RANK:  " << s[i].colrank << " COLLEGE Name:  " << s[i].colname << " BRANCHES: " << s[i].branches << " city:  " << s[i].city << "CUTOFF RANK:  " << s[i].elrank << endl;
	}

	void ranksort_records()
	{
		int i, j, no;
		fstream is("n.txt", ios::in);
		fstream f1("record.txt", ios::in);
		is >> no;;
		for (i = 0; i < no; i++)
		{
			f1 >> r[i].index >> r[i].colrank >> r[i].colname >> r[i].branches >> r[i].city >> r[i].elrank;
		}
		record temp;
		for (i = 0; i < no - 1; i++)
		{
			for (j = 0; j < no - i - 1; j++)
			{
				long a = atol(r[j].colrank);
				long b = atol(r[j + 1].colrank);
				//if (strcmp(r[j].colrank, r[j + 1].colrank) > 0)
				if (a > b)
				{
					temp = r[j];
					r[j] = r[j + 1];
					r[j + 1] = temp;
				}
				//else if (strcmp(r[j].colrank, r[j + 1].colrank) == 0)
				else if (a == b)
				{
					if (strcmp(r[j].colname, r[j + 1].colname) > 0)
					{
						temp = r[j];
						r[j] = r[j + 1];
						r[j + 1] = temp;
					}
				}
			}
		}
		for (i = 0; i < no; i++)
			cout << "COLLEGE RANK:  " << r[i].colrank << " COLLEGE Name:  " << r[i].colname << " BRANCHES: " << r[i].branches << " city:  " << r[i].city << "CUTOFF RANK:  " << r[i].elrank << endl;
	}

	void create_file()
	{
		fstream index("secindex.txt", ios::out | ios::app);
		fstream file("record.txt", ios::out | ios::app);
		fstream n2("n.txt", ios::in);
		int pp = 0;
		n2 >> pp;
		fstream ns("n.txt", ios::out);
		int z = n + pp;
		ns << z;
		for (int i = pp; i < z; i++)
		{
			index << rec[i].colname << " " << rec[i].colrank << " " << rec[i].city << " " << i << "\n";
			file << i << " " << rec[i].colrank << " " << rec[i].colname << " " << rec[i].branches << " " << rec[i].city << " " << rec[i].elrank << "\n";
		}
		index.close();
		file.close();
	}
	void display(temp t[])
	{
		int j = 0;
		fstream f1("record.txt", ios::in);
		while (!f1.eof())
		{
			f1 >> t[j].index >> t[j].colrank >> t[j].colname >> t[j].branches >> t[j].city >> t[j].elrank;



			/*f1.getline(t[i].index, 2, '|');
			f1.getline(t[i].colrank, 4, '|');
			f1.getline(t[i].colname, 10, '|');
			f1.getline(t[i].branches, 10, '|');
			f1.getline(t[i].city, 20, '|');
			f1.getline(t[i].elrank, 5, '||');*/
			cout << "COLLEGENAME: " << t[j].colname << "\tRank: " << t[j].colrank << "\tNO OF BRANCHES: " << t[j].branches << "\tcity: " << t[j].city << "\tELIGIBLERANK: " << t[j].elrank << endl;
			j++;
		}
	}
	/*void retrieve_record(char index[20])
	{
		fstream f1("record.txt", ios::in);
		int i;
		char ind[3], colname[30], colrank[20], branches[10], city[20], elrank[10];
		for (i = 0; i<4; i++)
		{
			f1.getline(ind, 3, ' ');
			f1.getline(colrank, 20, ' ');
			f1.getline(colname, 30, ' ');
			f1.getline(branches, 10, ' ');
			f1.getline(city, 20, ' ');
			f1.getline(elrank, 10, '\n');

			if (strcmp(index, ind) == 0)
				cout << "COLLEGE RANK:  " << colrank << " COLLEGE Name:  " << colname << " BRANCHES: " << branches << " city:  " << city << "CUTOFF RANK:  " << elrank << endl;
			f1.seekg(2, ios::cur);
		}
		f1.close();
	}*/

	void retrieve_record(char index[20])
	{
		fstream f1("record.txt", ios::in);
		fstream f2("n.txt", ios::in);
		f2 >> n;
		int i = 0;
		char ind[3], colname[30], colrank[20], branches[10], city[20], elrank[10];
		for (i = 0; i < n; i++)
		{
			f1 >> t[i].index >> t[i].colrank >> t[i].colname >> t[i].branches >> t[i].city >> t[i].elrank;
			cout << t[i].index;
			//system("pause");
			if (strcmp(index, t[i].index) == 0)
				cout << "COLLEGE RANK:  " << t[i].colrank << " COLLEGE Name:  " << t[i].colname << " BRANCHES: " << t[i].branches << " city:  " << t[i].city << "CUTOFF RANK:  " << t[i].elrank << endl;
			f1.seekg(2, ios::cur);
		}
		f1.close();
	}
	void search()
	{
		int k = 0, i, flag;
		fstream f1("secindex.txt", ios::in);
		fstream f2("n.txt", ios::in);
		int n;
		f2 >> n;
		char colname[30], colrank[20], city[20], ind[3], key_rank[10], key_colname[20], key_city[20];
		char index[20][20];
		cout << "Enter the name for search: ";
		cin >> key_colname;
		for (i = 0; i < n; i++)
		{
			f1.getline(colname, 30, ' ');
			f1.getline(colrank, 20, ' ');
			f1.getline(city, 20, ' ');
			f1.getline(ind, 3, '\n');
			if (strcmp(key_colname, colname) == 0)
			{
				strcpy_s(found[k].colname, colname);
				strcpy_s(found[k].colrank, colrank);
				strcpy_s(index[k], ind);
				k++;
			}
		}
		f1.close();
		if (k == 0)
			cout << "Search failed!!\n";
		else if (k == 1)
			retrieve_record(index[0]);
		else
		{
			cout << "Choose collegerank from the list:\n";
			for (i = 0; i < k; i++)
				cout << found[i].colrank << endl;
			cin >> key_rank;
			flag = 0;
			for (i = 0; i < k; i++)
			{
				if (strcmp(key_rank, found[i].colrank) == 0)
				{
					retrieve_record(index[i]);
					flag = 1;
				}
			}
			if (!flag)
				cout << "Invalid entry!!\n";
		}
	}

	void ranksearch()
	{
		int k = 0, i, flag;
		fstream f1("secindex.txt", ios::in);
		fstream f2("n.txt", ios::in);
		f2 >> n;
		char colname[30], colrank[20], city[20], ind[3], key_rank[10], key_colname[20], key_city[20];
		char index[20][20];
		cout << "Enter the rank for search: \n";
		cin >> key_rank;
		for (i = 0; i < n; i++)
		{
			f1.getline(colname, 30, ' ');
			f1.getline(colrank, 20, ' ');
			f1.getline(city, 20, ' ');
			f1.getline(ind, 3, '\n');
			//long crank = atol(colrank);
			//long krank = atol(key_rank);
			if (strcmp(key_rank, colrank) == 0)
			{
				strcpy_s(found[k].colname, colname);
				strcpy_s(found[k].colrank, colrank);
				strcpy_s(index[k], ind);
				k++;
			}
		}
		f1.close();
		if (k == 0)
			cout << "Search failed!!\n";
		else if (k == 1)
			retrieve_record(index[0]);
		else
		{
			cout << "Choose college name from the list:\n";
			for (i = 0; i < k; i++)
				cout << found[i].colname << endl;
			cin >> key_colname;
			flag = 0;
			for (i = 0; i < k; i++)
			{
				if (strcmp(key_colname, found[i].colname) == 0)
				{
					retrieve_record(index[i]);
					flag = 1;
				}
			}
			if (!flag)
				cout << "Invalid entry!!\n";
		}
	}

	void citysearch()
	{
		int k = 0, i, flag;
		fstream f1("secindex.txt", ios::in);
		fstream f2("n.txt", ios::in);
		f2 >> n;
		char colname[30], colrank[20], city[20], ind[3], key_rank[10], key_colname[20], key_city[20];
		char index[20][20];
		cout << "Enter the city your looking for: \n";
		cin >> key_city;
		for (i = 0; i < n; i++)
		{
			f1.getline(colname, 30, ' ');
			f1.getline(colrank, 20, ' ');
			f1.getline(city, 20, ' ');
			f1.getline(ind, 3, '\n');
			if (strcmp(key_city, city) == 0)
			{
				strcpy_s(found[k].colname, colname);
				strcpy_s(found[k].colrank, colrank);
				strcpy_s(index[k], ind);
				k++;
			}
		}
		f1.close();
		if (k == 0)
			cout << "Search failed!!\n";
		else if (k == 1)
			retrieve_record(index[0]);
		else
		{
			cout << "The following colleges avaiable,please choose one :\n";
			for (i = 0; i < k; i++)
				cout << found[i].colname << endl;
			cin >> key_colname;
			flag = 0;
			for (i = 0; i < k; i++)
			{
				if (strcmp(key_colname, found[i].colname) == 0)
				{
					retrieve_record(index[i]);
					flag = 1;
				}
			}
			if (!flag)
				cout << "Invalid entry!!\n";
		}
	}
	void delete_record(char *indx)
	{
		int i, flag;
		fstream is("n.txt", ios::in);
		char ch; is >> n;
		fstream f1("record.txt", ios::in);
		char index[20][20];
		for (i = 0; i < n; i++)
		{
			/*f1.getline(index[i], 3, ' ');
			f1.getline(rec[i].colrank, 20, ' ');
			f1.getline(rec[i].colname, 30, ' ');
			f1.getline(rec[i].branches, 10, ' ');
			f1.getline(rec[i].city, 20, ' ');
			f1.getline(rec[i].elrank, 10, ' \n');*/

			f1 >> t[i].index >> t[i].colrank >> t[i].colname >> t[i].branches >> t[i].city >> t[i].elrank;
			f1.seekg(2, ios::cur);
		}
		flag = -1;
		for (i = 0; i < n; i++)
			if (strcmp(t[i].index, indx) == 0)
				flag = i;
		if (flag != n - 1)
		{
			for (i = flag; i < n; i++)
				t[i] = t[i + 1];
		}
		n--;
		cout << "Record deleted!!\n";
		fstream os("n.txt", ios::out);
		os << n;
		system("pause");
		f1.close();
		f1.open("secindex.txt", ios::out);
		fstream f2("record.txt", ios::out);
		for (i = 0; i < n; i++)
		{
			f1 << t[i].colname << " " << t[i].colrank << " " << t[i].city << " " << i << "\n";
			f2 << i << " " << t[i].colrank << " " << t[i].colname << " " << t[i].branches << " " << t[i].city << " " << t[i].elrank << " " << "\n";

		}
		f1.close();
		f2.close();
	}
	void del()
	{
		int k = 0, i, flag;
		fstream f1("secindex.txt", ios::in);
		char colname[30], colrank[10], city[20], ind[3], key_rank[10], key_colname[20], key_city[20];
		char index[20][20];
		fstream is("n.txt", ios::in);
		is >> n;
		cout << "Enter the name to delete: ";
		cin >> key_colname;
		for (i = 0; i < n; i++)
		{
			f1.getline(colname, 30, ' ');
			f1.getline(colrank, 20, ' ');
			f1.getline(city, 20, ' ');
			f1.getline(ind, 3, '\n');
			if (strcmp(key_colname, colname) == 0)
			{
				strcpy_s(found[k].colname, colname);
				strcpy_s(found[k].colrank, colrank);
				strcpy_s(index[k], ind);
				k++;
			}
		}
		f1.close();
		if (k == 0)
			cout << "Deletion failed!!\n";
		else if (k == 1)
			delete_record(index[0]);
		else
		{
			cout << "Choose rank from the list:\n";
			for (i = 0; i < k; i++)
				cout << found[i].colrank << endl;
			cin >> key_rank;
			flag = 0;
			for (i = 0; i < k; i++)
			{
				if (strcmp(key_rank, found[i].colrank) == 0)
				{
					delete_record(index[i]);
					flag = 1;
				}
			}
			if (!flag)
				cout << "Invalid entry!!\n";
		}
	}

	void modify()
	{
		int k = 0, i, flag;
		fstream f1("secindex.txt", ios::in);
		char colname[30], colrank[10], city[20], ind[3], key_rank[10], key_colname[20], key_city[20];
		char index[20][20];
		fstream is("n.txt", ios::in);
		is >> n;
		cout << "Enter the name to modify: ";
		cin >> key_colname;
		for (i = 0; i < n; i++)
		{
			f1.getline(colname, 30, ' ');
			f1.getline(colrank, 20, ' ');
			f1.getline(city, 20, ' ');
			f1.getline(ind, 3, '\n');
			if (strcmp(key_colname, colname) == 0)
			{
				strcpy_s(found[k].colname, colname);
				strcpy_s(found[k].colrank, colrank);
				strcpy_s(index[k], ind);
				k++;
			}
		}
		f1.close();
		if (k == 0)
			cout << "Deletion failed!!\n";
		else if (k == 1)
			modify_record(index[0]);
		else
		{
			cout << "Choose rank from the list:\n";
			for (i = 0; i < k; i++)
				cout << found[i].colrank << endl;
			cin >> key_rank;
			flag = 0;
			for (i = 0; i < k; i++)
			{
				if (strcmp(key_rank, found[i].colrank) == 0)
				{
					modify_record(index[i]);
					flag = 1;
				}
			}
			if (!flag)
				cout << "Invalid entry!!\n";
		}
	}
	void modify_record(char *indx)
	{
		int i, flag;
		fstream is("n.txt", ios::in);
		char ch; is >> n;
		fstream f1("record.txt", ios::in);
		char index[20][20];
		for (i = 0; i < n; i++)
		{
			f1 >> t[i].index >> t[i].colrank >> t[i].colname >> t[i].branches >> t[i].city >> t[i].elrank;
		}
		flag = -1;
		for (i = 0; i < n; i++)
			if (strcmp(t[i].index, indx) == 0)
				flag = i;

		cout << "enter new record details";
		cout << "Enter the college name,college rank,branch,city,cut-off rank";
		cin >> t[flag].colname >> t[flag].colrank >> t[flag].branches >> t[flag].city >> t[flag].elrank;


		cout << "Record modified!!\n";
		system("pause");
		f1.close();
		f1.open("secindex.txt", ios::out);
		fstream f2("record.txt", ios::out);
		for (i = 0; i < n; i++)
		{
			f1 << t[i].colname << " " << t[i].colrank << " " << t[i].city << " " << i << "\n";
			f2 << i << " " << t[i].colrank << " " << t[i].colname << " " << t[i].branches << " " << t[i].city << " " << t[i].elrank << " " << "\n";

		}
		f1.close();
		f2.close();
	}
};

int main()
{
	record r[20];
	int ch, answer;
	temp t[20];
	student s;
	cout << "-----------------------------------------------";
	cout << "VTU";
	cout << "--------------------------------------------------\n";
	do {
		system("cls");
		cout << "\nChoose an option:\n1. If youre an Admin\n2. If you're an customer\n3. Exit\n";
		cin >> answer;
		if (answer == 1)
		{
			string pass;
			cout << "Enter the password\n";
			cin >> pass;
			if (pass == "hello")
			{
				system("cls");
				cout << "\nAccess granted :P";
				cout << "\nWelcome Admin User";
				cout << "\nEnter on of the possible options";
				cout << "\n1.Add Data\n2.Modify Data\n3.Delete Data\n4.Display\n";
				cin >> ch;
				switch (ch)
				{
				case 1:
					s.add();
					s.create_file();
					break;
				case 2:s.modify();
					break;
				case 3:s.del();
					break;
				case 4:s.sort_records();
					break;
				default:cout << "\nOption not avaiable";
				}
			}
			else
				cout << "\n---Access Denied---\n";
		}
		else if (answer == 2)
		{
			system("cls");
			cout << "\nEnter one of the following options";
			cout << "\n1.Display\n2.Search\n3.Exit";
			cout << "\nEnter your choice:\n ";
			cin >> ch;
			switch (ch)
			{
			case 1:
				int ch2;
				cout << "\n1.Display by alphabetical order";
				cout << "\n2.Display by Rank";
				cout << "\n3.Break";
				cin >> ch2;
				if (ch2 == 1)
					s.sort_records();
				else if (ch2 == 2)
					s.ranksort_records();
				else if (ch2 == 3)
					break;
				else
					cout << "\nWrong option";
				break;
			case 2:
				ch2;
				cout << "\nChoose one of the following options";
				cout << "\n1.To search by rank\n2.To search by college name\n3.To search by city\n4.Exit\n";
				cin >> ch2;
				if (ch2 == 1) 
					s.ranksearch();
				else if (ch2 == 2)
					s.search();
				else if (ch2 == 3)
					s.citysearch();
				else if (ch2 == 4)
					break;
				else
					cout << "wrong option";
				break;
			case 3:
				exit(0);
			}
		}
		else
			cout << "\nWrong choice";
	} while (answer != 3);
}
