# pro
#include <iostream>
#include <fstream>
#include <string>
using namespace std;
class Bibl {
private:
	string name;
	int kolvo_book;
	int kolvo_personal;
public:
	Bibl()
	{
		name = "Национальная библиотке";
		kolvo_book = 5000;
		kolvo_personal = 150;
	}
	Bibl(string n, int personal, int book)
	{
		name = n;
		kolvo_personal = personal;
		kolvo_book = book;
	}
	Bibl(const Bibl& bibl) : name(bibl.name), kolvo_book(bibl.kolvo_book), kolvo_personal(bibl.kolvo_personal)
	{

	}
	friend ostream& operator<<(std::ostream& out, const Bibl& b1);
	Bibl& operator += (int s)
	{
		kolvo_book += s;
		return *this;
	}


	Bibl& operator -= (int s)
	{
		kolvo_personal -= s;
		return *this;
	}


};
ostream& operator<<(std::ostream& out, const Bibl& b1)
{
	out << "Название библиотеки - " << b1.name << endl << "Количесвто персонала - " << b1.kolvo_personal << endl << "Количество книг в библиотеке - " << b1.kolvo_book << endl;
	return out;
}
class Book :public Bibl {
private:
	string name_book;
	int year_izdan;
	int kolvo_str;
	string avtor;
public:
	Book(string book, int year, int str, string av)
	{
		name_book = book;
		year_izdan = year;
		kolvo_str = str;
		avtor = av;
	}
	friend void show(Book& b);
};
void show(Book& b)
{
	cout << "Название книги - " << b.name_book << endl;
	cout << "Год издания - " << b.year_izdan << endl;
	cout << "Количество страниц в книге - " << b.kolvo_str << endl;
	cout << "Автор книги - " << b.avtor << endl << endl;
}
class Klient :public Bibl
{
private:
	string login;
	string password;
	string first_name;
	string second_name;
	int age;
public:
	Klient(string f_name, string s_name, int ag, string log, string pass)
	{
		login = log;
		password = pass;
		first_name = f_name;
		second_name = s_name;
		age = ag;
	}
	friend ostream& operator<<(std::ostream& out, const Klient& k);
	Klient& operator= (int s)
	{
		age = s;
		return *this;
	}
	~Klient() {}
};
ostream& operator<<(std::ostream& out, const Klient& k)
{
	out << "Логин - " << k.login << endl << "Пароль - " << k.password << endl << "Имя - " << k.first_name << endl << "Фамилия - " << k.second_name << endl << "Возраст - " << k.age << endl;
	return out;
}
int main()
{
	setlocale(LC_ALL, "russian");
	string name_b, log, pass, f_name, s_name;
	int kolvo_b, kolvo_p, ag;
	cout << "\t\t\t Онлайн библиотеки \n";

	cout << "\t 1 - Регистрация \n\n\n";
	int choose;
	cin >> choose;
	switch (choose)
	{

	case 1: {
		string login, password, password1, first_name, second_name;
		int age;
		cout << "\t\t\tРегистрация\n";
		cout << "Введите логин - ";

		cin >> login;
		cout << "Введите пароль - ";
		cin >> password;
		while (true) {
			cout << "Подтвердите пароль - ";
			cin >> password1;
			if (password != password1) {
				cout << "\n\tПароль не совподает.";
			}
			else break;
		}
		cout << "Введите имя и фамилию - ";
		cin >> first_name >> second_name;
		cout << "Введите возраст - ";
		cin >> age;
		ofstream account;
		account.open("C://account.txt");
		if (account.is_open())
		{
			account << "\nЛогин: " << login << "\nПароль: " << password << "\nИмя - " << first_name << "\n Фамилия - " << second_name << "\nВозраст - " << age << endl;
		}
		account.close();
		Klient accountt(first_name, second_name, age, login, password);
		f_name = first_name;
		s_name = second_name;
		ag = age;
		log = login;
		pass = password;

	}; break;
	default:
		break;
	}
	bool a = true;
	while (a)
	{
		cout << "\n\t\t\tМеню\n";
		cout << "1 - Добавить информацию про библиотеку\n";
		cout << "2 - Изменить  информацию о библиотеке\n";
		cout << "3 - Просмотреть аккаунт\n";
		cout << "4 - Изменить информацию об аккаунте\n";
		cout << "5 - Удалить учетную запись\n";
		cout << "0 - Покинуть сервис\n ";
		int choose1;
		cout << "\n\tВведите номер пункта - ";
		cin >> choose1;
		system("cls");
		switch (choose1)
		{
		case 1:
		{
			string name;
			int kolvo_book, kolvo_personal;
			cout << "\n\n\t\tДобавление информации про библиотеку\n";
			cout << "Введите название бибилиотеки - ";
			cin >> name;
			cout << "Введите количесвто книг в библиотеке - ";
			cin >> kolvo_book;
			cout << "Введите количество персонала,работающего в библиотеке - ";
			cin >> kolvo_personal;
			ofstream bibl;
			bibl.open("C://bibl.txt");
			if (bibl.is_open())
			{
				bibl << "\n---------------------------------------------\n" << "Название библиотеки - " << name << endl << "Количество книг - " << kolvo_book << endl << "Количесвто персонала - " << kolvo_personal << endl;
			}
			bibl.close();
			name_b = name;
			kolvo_b = kolvo_book;
			kolvo_p = kolvo_personal;
			Bibl b1;
			Bibl b2(name, kolvo_personal, kolvo_book);
			Bibl b3(b2);
			cout << "\nДобавленная информация:\n";
			cout << b3;
			cout << "\n\t\tИнформация успешна добавлена!\n";
		}; break;
		case 2:
		{
			system("cls");
			cout << "\n\t\tИзменение информации о библиотеке\n";
			cout << "Можно  \n1 - Увеличеть количество книг  \n2 - Уменшить количесвто персонала! \n";
			int izmen;
			cout << "Введите номер пункта - ";
			cin >> izmen;
			switch (izmen)
			{
			case 1: {
				cout << "\tИзменение количества книг\n";
				cout << "Будем изменять информации данной библиотеки:\n";
				string line;

				ifstream in("C://bibl.txt");
				if (in.is_open())
				{
					while (getline(in, line))
					{
						cout << line << std::endl;
					}
				}
				in.close();

				Bibl b4(name_b, kolvo_p, kolvo_b);
				cout << "Введите количесвто книг на которое надо увеличить - ";
				int yvel;
				cin >> yvel;
				b4 += yvel;
				kolvo_b += yvel;
				ofstream bibl;
				bibl.open("C://bibl.txt");
				if (bibl.is_open())
				{
					bibl << "\n---------------------------------------------\n" << "Название библиотеки - " << name_b << endl << "Количество книг - " << kolvo_b << endl << "Количесвто персонала - " << kolvo_p << endl;
				}
				bibl.close();
				cout << b4;
			}; break;
			case 2: {
				cout << "\n\tИзменение количества персонала\n";
				string line;

				ifstream in("C://bibl.txt");
				if (in.is_open())
				{
					while (getline(in, line))
					{
						cout << line << std::endl;
					}
				}
				in.close();
				Bibl b4(name_b, kolvo_p, kolvo_b);
				int ymen;
				cout << "Введите число на которое нужно уменьшить кол-во персонала - ";
				cin >> ymen;
				b4 -= ymen;
				kolvo_p -= ymen;
				ofstream bibl;
				bibl.open("C://bibl.txt");
				if (bibl.is_open())
				{
					bibl << "\n---------------------------------------------\n" << "Название библиотеки - " << name_b << endl << "Количество книг - " << kolvo_b << endl << "Количесвто персонала - " << kolvo_p << endl;
				}
				bibl.close();
				cout << b4;
			}; break;

			default:
				break;
			}
		}; break;
		case 3:
		{
			system("cls");
			cout << "\n\t\tПросмотр информации об аккаунте\n";
			string line;

			ifstream in("C://account.txt");
			if (in.is_open())
			{
				while (getline(in, line))
				{
					cout << line << endl;
				}
			}
			in.close();
		}; break;
		case 4:
		{
			system("cls");
			Klient account(f_name, s_name, ag, log, pass);
			cout << "\t\tИзменение информации об аккаунте\n";
			cout << "Вохможно изменить только возраст\n";
			cout << "Введите новый возраст - ";
			int newage;
			cin >> newage;
			account = newage;
			cout << account;
			ag = newage;

		}; break;
		case 5:
		{
			system("cls");
			Klient* acc = new Klient(f_name, s_name, ag, log, pass);
			delete acc;
			cout << "\n\t\tАккаунт успешно удален!\n";
			ofstream account;
			account.open("C://account.txt");
			if (account.is_open())
			{
				account <<"";
			}
			account.close();
		}; break;
		case 0:a = false; break;
		default:
			break;
		}
	}
	system("cls");
	cout << "\t\t\t\tВы покинули сервис!\n";
	return 0;
}
