# explicit关键字
*  C++中的explicit关键字只能用于修饰只有一个参数的类构造函数, 它的作用是表明该构造函数是显示的, 而非隐式的，
跟它相对应的另一个关键字是implicit, 意思是隐藏的,类构造函数默认情况下即声明为implicit(隐式).<br>
explicit关键字的作用：禁止隐式调用类内的单参数构造函数，这主要包括如下三层意思: <br>
（1）该关键字只能用来修饰类内部的构造函数 <br>
（2）禁止隐式调用拷贝构造函数 <br>
（3）禁止类对象之间的隐式转换 <br>
# 隐式转换 
``` cpp
class CExplict
{
public:
	CExplict();
	CExplict( bool _explicit)
	{
		this->is_explict = _explicit;
	}
	CExplict(const CExplict& other)
	{
		this->is_explict = other.is_explict;
	}
	friend void printExplicit(const CExplict& cx);	
 
private:
	bool is_explict;
};
 
void printExplicit(const CExplict& cx)
{
	cout<<"is_explict="<<cx.is_explict<<endl;
}
 
int main( int argc, char* argv[])
{
	CExplict cx1 = true;
	CExplict cx2 = cx1;
	printExplicit(cx1);
	printExplicit(cx2);
	printExplicit(false);
	getchar();
	return 1;
}
```
在上面的代码中: <br>
``` cpp
	CExplict cx1 = true;
	CExplict cx2 = cx1;
	printExplicit(false);
```
隐式调用CExplict类的单参数构造函数.这种调用在C++语法中是允许的，但是诸如：CExplict cx1 = true和printExplicit(false)这种表达形式看着很别扭， <br>
也很让人费解，将一个bool型的值赋给一个CExplicit类的cx1，使代码的可读性变差. <br>
因此，为了禁止对类的单参数构造函数的隐式调用，C++引入了关键字explicit.在类的定义中，在任何一个单参数构造函数钱加explicit关键字，就可以禁止对该构造函数的隐式调用.如下: <br>
``` cpp
class CExplict
{
public:
	CExplict();
	explicit CExplict( bool _explicit)
	{
		this->is_explict = _explicit;
	}
	CExplict(const CExplict& other)
	{
		this->is_explict = other.is_explict;
	}
	friend void printExplicit(const CExplict& cx);	
 
private:
	bool is_explict;
};
 
void printExplicit(const CExplict& cx)
{
	cout<<"is_explict="<<cx.is_explict<<endl;
}
 
int main( int argc, char* argv[])
{
	CExplict cx1 = true;
	CExplict cx2 = cx1;
	printExplicit(cx1);
	printExplicit(cx2);
	printExplicit(false);
	getchar();
	return 1;
}
```
此时，再调用上面一段代码，则会报：error C2440: “初始化”: 无法从“bool”转换为“CExplict”的错误，为了使程序能正确运行，需要将main函数内的代码改为: <br>
``` cpp
int main( int argc, char* argv[])
{
	CExplict cx1(true);
	CExplict cx2(cx1);
	printExplicit(cx1);
	printExplicit(cx2);
	printExplicit(CExplict(false));
	getchar();
	return 1;	
}
```
至此，程序就可以正常运行，而且进一步增加了程序的可读性. <br>
总结: <br>
（1）explicit关键字只需用于类内的单参数构造函数前面。由于无参数的构造函数和多参数的构造函数总是显示调用，这种情况在构造函数前加explicit无意义. <br>
（2）如果想禁止类A对象被隐式转换为类B对象，可在类B中使用关键字explicit，即定义这样的转换构造函数 <br>
``` cpp
        explicit B(A a)
	{
 
	}
	explicit B(const A &a)
	{
 
	}
```


