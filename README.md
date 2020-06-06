#include <iostream>
#include <string>

using namespace std;

class Rune
{
private:
	int intellect;
	int speed;
	int power;

public:
	Rune()
	{
		intellect = 10;
		speed = 10;
		power = 5;
	}

	Rune(int _intellect, int _speed, int _power)
	{
		intellect = _intellect;
		speed = _speed;
		power = _power;
	}

	Rune(Rune const &one)
	{
		intellect = one.intellect;
		speed = one.speed;
		power = one.power;
	}

	int getIntellect()
	{
		return intellect;
	}
	int getSpeed()
	{
		return speed;
	}
	int getPower()
	{
		return power;
	}

	void setIntellect(int _intellect)
	{
		intellect = _intellect;
	}
	void setSpeed(int _speed)
	{
		speed = _speed;
	}
	void setPower(int _power)
	{
		power = _power;
	}

	void print()
	{
		cout << "Intellect = " << intellect << endl;
		cout << "Speed = " << speed << endl;
		cout << "Power = " << power << endl;
	}
};


class Inventory {
private:
	Rune * runes;
	int current;
	int capacity;
public:
	Inventory()
	{
		runes = new Rune[capacity];
		current = 0;
		capacity = 10;
	}

	void copy(Inventory const &other)
	{
		current = other.current;
		capacity = other.capacity;
		runes = new Rune[capacity];

		for (int i = 0; i < current; i++) {
			runes[i] = other.runes[i];
		}
	}
	Inventory(Inventory const &other)
	{
		copy(other);
	}
	~Inventory() {
		delete[]runes;
	}

	void resize(Rune *helper) {
		helper = new Rune[capacity];

		for (int i = 0; i < capacity; i++)
			runes[i] = helper[i];

		delete[] runes;

		capacity += 10;
		runes = new Rune[capacity];

		for (int i = 0; i < current; i++)
			runes[i] = helper[i];

		delete[] helper;
	}

	void add(Rune const &one) {
		if (current == capacity) {
			resize(runes);
		}
		runes[current] = one;
		current++;
	}

	void remove() {
		Rune * helper;
		helper = new Rune[capacity];

		current--;

		for (int i = 0; i < current; i++) {
			helper[i] = runes[i];
		}
		delete[] runes;

		runes = new Rune[capacity];

		for (int i = 0; i < current; i++) {
			runes[i] = helper[i];
		}
	}

	Inventory& operator=(Inventory const &other)
	{
		if (this != &other) {
			delete[] runes;
			copy(other);
		}
		return *this;
	}



	void print() {
		for (int i = 0; i < capacity; i++) {
			cout << "Runes are: " << runes << endl;
			runes[i].print();
		}
	}
};


class Student {
private:
	char *name;
	double grade;
public:
	Student() {
		name = NULL;
		grade = 4;
	}

	Student(char *name, double grade) {
		this->name = new char[strlen(name) + 1];
		strcpy_s(this->name, sizeof this->name, name);
		this->grade = grade;
	}

	~Student()
	{
		delete[] name;
	}

	Student(Student const& other) {
		this->name = new char[strlen(other.name) + 1];
		strcpy_s(this->name, sizeof this->name, other.name);
		this->grade = other.grade;
	}

	Student& operator=(Student const &other)
	{
		if (this != &other)
		{
			delete[] name;
			this->name = new char[strlen(other.name) + 1];
			strcpy_s(this->name, sizeof this->name, other.name);
			this->grade = other.grade;
		}
		return *this;
	}

	~Student()
	{
		delete[] name;
	}
};


class Fraction {
private:
	int number;
	int denom;
public:
	Fraction() {
		number = 1;
		denom = 1;
	}

	Fraction(int _number, int _denom){
		number = _number;
		denom = _denom;
	}

	int gcd(Fraction result) {
		while (result.number != result.denom)
			if (result.number > result.denom)
				result.number -= result.denom;
			else
				result.denom -= result.number;
		return result.number;
	}

	Fraction& operator=(Fraction const &other) {
		if (this != &other)
		{
			this->number = other.number;
			this->denom = other.denom;
		}
		return *this;
	}

	Fraction operator+(Fraction const& other) {
		return Fraction((number*other.denom + denom * other.number), denom*other.denom);	
	}

	Fraction operator+(Fraction const& other) {
		return Fraction((number*other.denom - denom * other.number), denom*other.denom);
	}


	Fraction operator*(const Fraction& other) {
		int x, y;
		x = number * other.number;
		y = denom * other.denom;
		return Fraction(x, y);
	}

	Fraction operator/(const Fraction& other) {
		int x, y;
		x = number * other.denom;
		y = denom * other.number;
		return Fraction(x, y);
	}
	
	Fraction(Fraction const &other) {
		number = other.number;
		denom = other.denom;
	}
};





int main()
{
	Rune a(20, 30, 40);
	a.print();
	Fraction h;



	Rune b(a);
	b.print();

	return 0;
}
