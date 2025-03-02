

---

**24-12-22**

无感悟



### 构造函数

```cpp
class Array{
	private:
		int n;//数组大小 
		int *a;//数组 
	public:
    	// 默认构造函数
		Array(){
			cin>>n;
			a=new int [n];
			for (int i=0;i<n;i++) cin>>a[i];
		}
    	// 拷贝构造函数
        Array(const Array& other) {
            n = other.n;  // 拷贝数组的大小
            a = new int[n];  // 为新对象分配内存
            for (int i = 0; i < n; i++) {
                a[i] = other.a[i];  // 拷贝数组中的元素
            }
        }
    	// 移动构造
    	Array(Array&& other){
            n = other.n;  // 拷贝大小
            a = other.a;  // 移动指针（将资源所有权转移到当前对象）
            other.a = nullptr;  // 将原对象的指针设为 nullptr，防止析构时释放资源
            other.n = 0;  // 清空原对象的大小
        }

		~Array(){
			delete []a;
		}
		int getlen(){
			return n;
		}
		int get(int i){
			return a[i];
		}
		// write your code here......

        Array& operator=(const Array& x);
		void show(){
			for (int i=0;i<n;i++) cout<<a[i]<<' ';
		}
};
int main(){
	Array a;
	Array b=a; 
	b.show();
	return 0;
}
```





### 友元函数

- 可以对类私有和保护对象的访问

- 对封装的妥协，类与类之间紧密协作和性能优化。

- 比起反射，友元机制是静态的（编译时确定），类设计者要明确指定哪些类或函数为“友元”

```cpp
class A {
private:
    int x;
public:
    A() : x(10) {}
    friend void printX(A& obj);  // 函数 printX 是 A 的友元函数
};

void printX(A& obj) {
    cout << obj.x << endl;  // 友元函数可以访问私有成员
}
```



```cpp
// classes_as_friends2.cpp
// compile with: /EHsc
#include <iostream>

using namespace std;
class YourClass {
friend class YourOtherClass;  // Declare a friend class
public:
   YourClass() : topSecret(0){}
   void printMember() { cout << topSecret << endl; }
private:
   int topSecret;
};

class YourOtherClass {
public:
   void change( YourClass& yc, int x ){yc.topSecret = x;}
};

int main() {
   YourClass yc1;
   YourOtherClass yoc1;
   yc1.printMember();
   yoc1.change( yc1, 5 );
   yc1.printMember();
}
```

声明指定函数友元，声明指定类友元，声明指定类的方法友元

- a声明b友元，b就可以访问a的人员数据
- 友元关系不会继承





### 运算符重载

```cpp
#include <iostream>
using namespace std;

class Time {

    public:
        int hours;      // 小时
        int minutes;    // 分钟

        Time() {
            hours = 0;
            minutes = 0;
        }

        Time(int h, int m) {
            this->hours = h;
            this->minutes = m;
        }
        Time operator+(const Time& other){
            Time res(hours+other.hours,minutes+other.minutes);
            res.hours+=res.minutes/60;
            res.minutes=res.minutes%60;
            return res;
        } 
        void show() {
            cout << hours << " " << minutes << endl;
        }

        // write your code here......
        

};

int main() {

    int h, m;
    cin >> h;
    cin >> m;

    Time t1(h, m);
    Time t2(2, 20);

    Time t3 = t1 + t2;
    t3.show();
    
    return 0;
}
```

---

### 指针

指针的3个隐患

- 没有初始化
- 没有释放
- 释放后没有置空，多指针指向一个内存结果被释放，另一个不知道



强指针：强技术到0，不管弱技术多少都释放（解决死锁）

弱指针：只有转换成强指针时才可访问（解决野指针）



智能指针指向对象的父类是RefBase



---

## NULL的二义性

```cpp
void myfun(float *);
void myfun(int);

//调用方时想传float指针类型的参数，但是可能出现	把空指针传入这个函数
myfun(NULL);    // 二义性，0也是int类型，系统不知道调用哪个方法
```

