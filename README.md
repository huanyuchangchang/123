任务一：
#include<iostream>
using namespace std;
//生成基类对象Base
class Base
{
public:
	int a;
protected:
	int b;
private:
	int c;
public:
	static int count;
public:
	Base(int,int,int);
	~Base();
	void print();
	static int statistic();//输出类的数据成员函数print（），统计类对象创建个数的函数 static int statistic（）
};
//定义基类对象Base的构造函数和析构函数
int Base::count = 0;
Base::Base(int m,int n,int k)
{
	a = m;
	b = n;
	c = k;
	count++;
	cout << "构造函数被调用" << endl;
}
Base::~Base()
{
	cout << "析构函数被调用" << endl;
	getchar();
}
//定义两个普通函数，输出类的数据成员函数print（），统计类对象创建个数的函数 static int statistic（）
void Base::print()
{
	cout << a <<" " << b <<" "<< c << endl;
}
int Base::statistic()
{
	return count;
}
//定义三种继承方式的子类对象derived1，derived2，derived3
class derived1:public Base
{
private:
	int l;
	//Base h1;
public:
	derived1(int z, int m, int n, int k) :Base(m, n, k)
	{
		l = z;
		count++;
		cout << l << endl;
		print();
		cout << l << a << endl;
	}
	~derived1();

};
class derived2 :private Base
{
private:
	int l;
	Base h2;
public:
	derived2(int z, int m, int n, int k);
	~derived2();
};
class derived3 :protected Base
{
private:
	int l;
	Base h3;
public:
	derived3(int z, int m, int n, int k);
	~derived3();
};
//定义derived1的构造和析构函数
/*derived1::derived1(int z, int m, int n, int k):Base(m,n,k)
{
	l = z;
	count++;
	cout << l << endl;
	h1.print();
	cout << l << h1.a  << endl;
}*/
derived1::~derived1()
{
	cout << "析构函数被调用" << endl;
	getchar();
}
//定义derived2的构造和析构函数
derived2::derived2(int z, int m, int n, int k) : Base(m, n, k),h2(m, n, k)
{
	l = z;
	count++;
	cout << l << endl;
	h2.print();
	
}
derived2::~derived2()
{
	cout << "析构函数被调用" << endl;
	getchar();
}
//定义derived3的构造和析构函数
derived3::derived3(int z, int m, int n, int k) : Base(m, n, k), h3(m, n, k)
{
	l = z;
	count++;
	cout << l << endl;
	h3.print();
	
}
derived3::~derived3()
{
	cout << "析构函数被调用" << endl;
	getchar();
}
int main()
{
	int b;
	Base hy(0,0,0);//统计对象个数的一个对象
	derived1 D(1,2,3,4);
	derived2 E(1,2,3,4);
	derived3 F(1,2,3,4);
	cout <<hy.statistic() << endl;//全局变量的输出有问题
	return 0;
}
任务二：
#include<iostream>
using namespace std;
/*定义基类一个二维空间点类Location*/
class Location
{
public:
	float x;
	float y;
public:
	Location(float a, float b);
	~Location();
	void move(float ch1, float ch2);//ch1为x改变量，ch2为y改变量
	void show();
	
};
/*完成类内函数的定义*/
Location::Location(float a,float b)
{
	x = a;
	y = b;
}
Location::~Location()
{
	cout << "析构函数被调用" << endl;
}
void Location::move(float ch1, float ch2)
{
	x += ch1;
	y += ch2;
}
void Location::show()
{
	cout << '(' << x << ',' << y << ')' << endl;
}
/*以Location派生出三维空间坐标点类Point*/
class Point :public Location
{
public:
	float z;
public:
	Point(float a, float b, float c):Location(a,b)
	{
		z = c;
	}
	~Point()
	{

	}
	void move(float ch1, float ch2, float ch3)//ch1为x改变量，ch2为y改变量,ch3为z改变量
	{
		x += ch1;
		y += ch2;
		z += ch3;
	}
	void show()
	{
		cout << '(' << x <<','<<y <<','<< z << ')' << endl;
	}

};
/*以Pofloat派生处一个三维空间下的球体类Sphere*/
class Sphere :public Point
{
public:
	float r;
	
public:
	Sphere(float v1,float v2,float v3,float v4):Point(v1,v2,v3)
	{
		r = v4;
		
	}
	~Sphere()
	{

	}
	void move(float v5, float v6, float v7, float v8)//c1为k1改变量，c2为k2改变量
	{
		x += v5;
		y += v6;
		z += v7;
		r += v8;
	}
	void show()
	{
		cout << "球心为" << '(' << x << ',' << y << ',' << z <<')' << endl;
		cout << "半径为" << r << endl;
	}
};
int main()
{
	Location L1(1.1,1.2);
	L1.show();
	L1.move(2.7, 8.5);
	L1.show();
	
	Point P1(1.1, 1.2, 1.3);
	P1.show();
	P1.move(1.3, 4.2, 5.4);
	P1.show();

	Sphere S1(1.1, 1.2, 1.3, 4.3);
	S1.show();
	S1.move(1.1, 1.2, 1.3, 4.3);
	S1.show();

	system("pause");
	return 0;
}
