

## c11的语言特性

.h 头文件可以不加

```c
#include <vector>
#include <vector.h>
```



### varidic template

模版参数可变

```c++
void print(){}

template <typename T, typename... Types>
void print(const T& firstArg, const Types&... args) {
  cout << firstArg << endl;
  print(args...);// 当参数为0 的时候， 调用上面的空函数
}

print(1,"a");
```



### space in Template Expression, nullptr，auto

```c
vector<vector<int > >  // 旧版
vector<vector<int >>	// c11新版
  
void foo(int);
void foo(int*); 
foo(NULL) // foo1? foo2 ? 旧版有冲突
(NULL == 0) -> true
nullptr(void *) //c11 解决方案
        
auto i = NULL;
```



### Uniform Initiazation

初始化统一可以用大括号，在变量的后面直接用!!!  (强)

```c
int values[] {1,2,3};
vector<int> v {1,2,3};
vector<string> str{"df","df"};

```



#### initializer_list

```c
int i;
int p{};  //0
int *p;   //no
int *q{};	  //nullptr
    
void print(int i){cout << i << " ";}
void print(std::initializer_list<int> vals){
    for_each(vals.begin(), vals.end(), print);
}
print({1,2,3,45});
    
class P{
    P(int a){}
    P(initializer_list<int> intlist){}
    void operator=(initializer_list<int> il){}
};

P p(3); 		// 第一个构造函数
P p{3};			// 第二个
P P{3,4};
P P={3,4};		// 第三个

min({1,2,34,4})
max({string("dsf"),string("fsda")}); // 强
```



### explict for actors taking more than one argument

 ```c
class C{
	explict C(int a){}
};
C c = 1; //error  1 -> C not explict
 ```



### for

```c
int a[10] = {      1,      2,      3  };
  //* -----------------------------------
  printf("auto && foreach\n");
  for (auto& i : a) i = 2;  //取地址
  for (auto i : a) {        //取值
    cout << i << " ";
    if (i == 3) break;
  }
//! 尽量用 取值， 不然有拷贝会慢一点

  /*
  template<class InputIterator, class Function>
  Function for_each(InputIterator first, InputIterator last, Function fn){
      while (first!=last) {
        fn (*first);
        ++first;
      }
      return fn;      // or, since C++11: return move(fn);
  }
  */
  cout << endl;
  vector<int> foreach (a, a + 5);
  for_each(foreach.begin(), foreach.end(), [](int a) { cout << a << " "; });
  struct Sum {  //仿函数
    int sum;
    void operator()(int val) { sum += val; }
  };
```



### =defalut, =delete

```c
class B{
    B(int a) : a(a){} // 写了后没有构造函数
    B(const B&) = delete; //不给拷贝构造
    B& operator=(const B&) = delete; //不给拷贝构造
    private: 
    	int a;
}
// 也可以 放到private ，去friend中调用
```



### alias template

```c
template<typename T>
using vec = std::vector<T>;
typedef vector<int> vint // 无法带参数！！！！！
    
vec<int> arr;
vint arr;
    
    
```



### decltype

```c
auto t = [](){}

vector<decltype(t)> v(t);
```



```c
[]{ cou <<"heloo";} 	//函数
[]{cout << "world";}();	//
    
int x;
int y;
auto q = [x, &y]{};

```





## 左值和右值

#### 简单的定义

*左值 (lvalue, locator value)* 表示了一个占据内存中某个可识别的位置（也就是一个地址）的对象。

*右值 (rvalue)* 则使用排除法来定义。一个表达式不是 *左值* 就是 *右值* 。 那么，右值是一个 *不* 表示内存中某个可识别位置的对象的表达式。

```c
int globalvar = 20;

int& foo(){
    return globalvar;
}

int main(){
    foo() = 10;
    return 0;
}
```

##### 右值引用







## 标准库



### array

将数组封装成模版类， 没有构造函数和析构函数， 模拟出数组！



### tuple

```c
auto tu = make_tuple(22,44,"dsjfk");

tuple_size<>::value
 

```

