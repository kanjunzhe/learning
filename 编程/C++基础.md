# C++学习记录册
------

## 1000.入门：求两个数的和

* 输入样例：2 3
* 输出样例：5
* 代码实现：
```C++
#include <iostream>
int m000()
{
	int a, b;
	std::cin >> a >> b;
	std::cout << a + b;
	return 0;
}
```

## 1001.获取第二个整数

* 输入样例：100 135 322
* 输出样例：135
* 代码实现：
```c++
#include <iostream>
int m001()
{
	std::cin >> a >> b >> c;
	std::cout << b << std::endl;
	return 0;
}
```

## 1002.对齐输出(8字节)

* 输入样例：123456789 0 -1
* 输出样例：123456789        0       -1
* 代码实现：
```c++
#include <iostream>
int m002()
{
	int a, b, c;
	std::cin >> a >> b >> c;
	//printf() C的输出函数 => scanf()C的输入函数
	//%8d 8字节数字
	printf("%8d %8d %8d", a, b, c);
	return 0;
}
```

## 1003.字符三角形

* 输入样例：&
* 输出样例：
	    &
	  &&&
	&&&&&
* 代码实现：
```c++
#include <iostream>
int m003()
{
	char ch;
	std::cin >> ch;
    std::cout << " " << " " << ch << " " << " " << std::endl;
    std::cout << " " << ch << ch << ch << " " << std::endl;
    std::cout << ch << ch << ch << ch << ch << std::endl;
    return 0;
  }
```

## 1004.地球人口承载力估计

* 数据：1.地球资源按恒定速度增长
	 2.可供 x 亿人生活 a 年
	 3.可供 y 亿人生活 b 年
	 4.输出地球可持续发展所能承受最大人口(x > y,a < b)
* 输入样例：110 90 90 210 (x a y b)
* 输出样例：75.00 (小数点后两位)
* 代码实现：
```c++
#include <iosteram>
//四舍五入用头文件
#include <iomanip>
int m004()
{
	int x, y, a, b;
	std::cin >> x >> y >> a >> b;
	double z;
	z = (y * b - x * a) / (b - a);
	//四舍五入方式：cout << std::fixed << std::setprecision(保留位数) << 数据;
	std::cout << std::fixed << std::setprecision(2) << z << std::endl;
	return 0;
}
```

## 1005.计算 (a + b)  * 或 ÷  c 的值

* 输入样例：1 2 3
* 输出样例：9
* 代码实现：
```c++
#include <iosteram>
int m005()
{
	int a, b, c;
	std::cin >> a >> b >> c;
	std::cout << (a + b) * c << std::endl;
	std::cout << int(a + b) / c << std::endl;
	return 0;
}
```

## 1006.带余除法

* 输入样例：5 2
* 输出样例：2 1
* 代码实现：
```c++
#include <iosteram>
int m006()
{
	int a, b;
	std::cin >> a >> b;std::cout << a / b << " " << a % b;
	return 0;
}
```

## 1007.计算分数的浮点数值

* 输入样例：7 7
* 输出样例：1.0000000000
* 代码实现：
```c++
#include <iosteram>
int m007()
{
	int a, b;
	std::cin >> a >> b;
	//不能直接a/b，要对数据进行显式转换
	std::cout << std::fixed << std::setprecision(15) << (double)a / b << std::endl;
	return 0;
}
```

## 1008.计算几率

* 输入样例：10433 60
* 输出样例：0.575% (小数点后三位)
* 代码实现：
```c++
#include <iosteram>
int m008()
{
	int a, b;
	std::cin >> a >> b;
	std::cout << std::fixed << std::setprecision(3) << (double)b / a * 100 << "%" << std::endl;
	return 0;
}
```

## 1009.计算多项式f(x)
$$
f(x) = ax^3 + bx^2 + cx + d
$$
* 输入样例：2.31 1.2 2 2 3
* 输出样例：33.0838692 (小数点后7位)
* 代码实现：
```c++
#include <iosteram>
int m009()
{
	double x, a, b, c, d;
	std::cin >> x >> a >> b >> c >> d;
    //pow(num, row)函数用于计算num的row次方的值
	double f = a * pow(x, 3) + b * pow(x, 2) + c * x + d;
	std::cout << std::fixed << std::setprecision(7) << f << std::endl;
	return 0;
}
```

## 1010.温度转化
$$
C = \frac{5}{9}(F - 32)
$$
* 输入样例：41
* 输出样例：5.00000 (小数点后5位)
* 代码实现：
```c++
#include <iosteram>
#include <iomanip>
int m013()
{
	double f;
	std::cin >> f;
	double c = (f - 32) * 5 / 9;
	std::cout << std::fixed << std::setprecision(5) << c << std::endl;
	return 0;
}
```

## 1011.计算圆的周长与面积
$$
C_圆 = 2\pi r ~~~~~~~~~~ S_圆 = \pi r^2
$$
* 输入样例：3.0
* 输出样例：18.8495 28.2743
* 代码实现：
```c++
#include <iosteram>
#include <iomanip>
int m011()
{
	double pi = 3.14159;
	double r, d, c, s;
	std::cin >> r;
	c = d * pi;
	s = pow(r, 2) * pi;
	std::cout << std::fixed << std::setprecision(5) << c << " ";
	std::cout << std::fixed << std::setprecision(5) << s << " ";
	std::cout << std::endl;
	return 0;
}
```

## 1012.计算并联电路中的总电阻大小
$$
R总 = \frac{1}{\frac{1}{r1} + \frac{1}{r2}}
$$
* 数据：支路电阻a, b
* 输入样例：1 2
* 输出样例：0.67
* 代码实现：
```c++
#include <iosteram>
#include <iomanip>
int m012()
{
	int r1, r2;
	std::cin >> r1 >> r2;
	double R = 1 / ((1 / r1) + (1 / r2));
	std::cout << std::fixed << std::setprecision(2) << R;
	return 0;
}
```

## 1013.计算float, double所占空间大小

* 输入样例：NULL
* 输出样例：4 8
* 代码实现：
```c++
#include <iosteram>
int m013()
{
	float f = 0;
	double d = 0;
	std::cout << sizeof(f) << " " << sizeof(d) << std::endl;
	return 0;
}
```

## 1014. int类型和boll类型的转换

* 输入样例：3
* 输出样例：1
* 代码实现：
```c++
#include <iosteram>
int m014()
{
	//隐式转换 =>非0就输出1
	int a;
	std::cin >> a;
	bool b = a;
	a = b;
	std::cout << a;
	return 0;
}
```

## 1015.保留12位小数的浮点数

* 输入样例：3.14159265357989323846
* 输出样例：3.141592653580
* 代码实现：
```c++
#include <iosteram>
int m015()
{
	double a;
	std::cin >> a;
	std::cout << std::fixed << std::setprecision(12) << a;
	return 0;
}
```

## 1016.计算两小数相除的余数

余数r定义: 
$$
a = kb + r
$$
其中a为被除数，k为商，b为除数
* 输入样例：73.263 0.9973
* 输出样例：0.4601
* 代码实现：
```c++
#include <iosteram>
//取绝对值使用包
#include <cmath>
int m016()
{
	double a, b;
	std::cin >> a >> b;
	int k = a / b;
	double r = a - k * b;
	if (a * b < 0)
	{
		//abs：取绝对值
		std::cout << abs(r + b) << std::endl;
	}
	else
	{
		std::cout << r << std::endl;
	}
	return 0;
}
```

## 1017.计算球的体积
$$
V_球 = \frac{4}{3}πr^3
$$
* 输入样例：4
* 输出样例：267.95
* 代码实现：
```c++
#include <iosteram>
#include <iomanip>
int m017()
{
	int r;
	int pi = 3.14;
	std::cin >> r;
	//不能按照公式顺序计算，不然4÷3会返回一个整数(4和3都是整数)
	double V = pi * pow(r,3) * 4 / 3;
	std::cout << std::fixed << std::setprecision(2) << V << std::endl;
	return 0;
}
```

## 1018.反向输出一个三位数

* 输入样例：358
* 输出样例：853
* 代码实现：
```c++
#include <iosteram>
int m018()
{
	int num;
	std::cin >> num;
    //程序构想
    //三位数个位的表示方法:	int(num / 100)
    //三位数十位的表示方法:	int(num % 100 / 10)
    //三位数百位的表示方法:	int(num % 10)
	std::cout << num % 10 << num % 100 / 10 << num / 100 << std::endl;
	return 0;
}
```

## 1019.大象喝水

* 数据：大象要喝 l 升水，现有深 h 厘米，底面半径 r 的装满水的小圆桶，求至少需要的桶的数量
* 输入样例：23 11
* 输出样例：3
* 代码实现：
```c++
#include <iosteram>
int m019()
{
	int l, h, r;
	double pi = 3.14;
	std::cin >> l >> h >> r;
	double t = pi * pow(r, 3) / 1000;
	std::cout << int(l / t) + 1;
	return 0;
}
```

## 1020.计算线段的长度
$$
勾股定理:a^2 + b^2 = c^2
$$
* 数据：线段两端点A(X a, X b),B(Y a, Y b)
* 输入样例：1 1 2 2
* 输出样例：1.414
* 代码实现：
```c++
#include <iosteram>
//开方使用包
#include <cmath>
int m020()
{
	int xa, xb, ya, yb;
	std::cin >> xa >> xb >> ya >> yb;
	double ans = sqrt(pow(xa - xb, 2) + pow(ya - yb, 2));
	std::cout << std::fixed << std::setprecision(3) << ans << std::endl;
	return 0;
}
```

## 1021.计算三角形的面积

三角形面积计算海伦公式：
$$
S = \sqrt{p(p - a)(p - b)(p - c)}~~~~~~~~~~~~~~~~~~
p = \frac{a + b + c}{2}
$$
* 数据：三角形端点A(x a,y a),B(x b,y b),C(x c, y c)
* 输入样例：0 0 4 0 0 3
* 输出样例：6.00
* 代码实现：
```c++
#include <iosteram>
#include <iomanip>
#include <cmath>
int m021()
{
	int xa, xb, ya, yb, xc, yc;
	std::cin >> xa >> xb >> ya >> yb >> xc >>yc;
	double a = sqrt(pow(xa - xb, 2) + pow(ya - yb, 2));
	double b = sqrt(pow(xa - xc, 2) + pow(ya - yc, 2));
	double c = sqrt(pow(xb - xc, 2) + pow(yb - yc, 2));
	double p = (a + b + c) / 2;
	double S = sqrt(p * (p - a) * (p - b) * (p - c))
	std::cout << std::fixed << std::setprecision(3) << S << std::endl;
	return 0;
}
```

## 1022.计算等差数列的末项
$$
a_n = a_1 + (n - 1)(a_2 - a_1)
$$
其中n为项数，a 1为首项，a 2为第二项，a n为末项
* 数据：等差数列首项,第二项和项数
* 输入样例：1 4 100
* 输出样例：198
* 代码实现：
```c++
#include <iosteram>
int m023()
{
	int a, b, n, ans;
	std::cin >> a >> b >> n;
	ans = a + (n - 1) * (b - a);
	std::cout << ans << std::endl;
	return 0;
}
```

## 1023.计算大数A x B
$$
int类型数据大小：~~~~~~~~~~1 * 10 ^ 9
$$
$$
long long类型数据大小：1 * 10^{19}
$$

数据：两个数，A >= 1, B <= 50000(数据过大，无法使用int)
* 输入样例：3 4
* 输出样例：12
* 代码实现：
```c++
#include <iosteram>
int m023()
{
	long long a, b;
	std::cin >> a >> b;
	std::cout << a * b;
	return 0;
}
```

## 1024.计算2的幂

* 数据：一个数，2的n次方
* 输入样例：2
* 输出样例：4
* 代码实现：
```c++
#include <iosteram>
#include <cmath>
int m024()
{
	int n;
	std::cin >> n;
	std::cout << int(pow(2, n)) << std::endl;
	return 0;
}
```

## 1025.虫子吃苹果

* 数据：你一箱n个苹果，箱子里有b条虫子。虫子每x小时能吃掉一个苹果，假设虫子在吃完一个苹果之前不会吃另一 个，那么经过y小时还有多少个完整的苹果？
* 输入样例：10 1 4 9
* 输出样例：7
* 代码实现：
```c++
#include <iosteram>
int m025()
{
	int n, b, x, y;
	std::cin >> n >> b >> x >> y;
	int n_now;
	if (y % (x * b) == 0)
	{
		n_now = n - y / x;
	}
	else
	{
		n_now = n - y / x - 1;
	}
	if (n <= 0)
	{
		std::cout << 0 << std::endl;
	}
	else
	{
		xtd::cout << n_now  << std::endl;
	}
	return 0;
}
```

## 1026.判断正负数

* 数据：一个整数 N，判断其正负：如果 N > 0 ，输出 positive；如果 N = 0 ，输出zero；如果 N < 0，输出 negative。
* 输入样例：1
* 输出样例：positive
* 代码实现：
```c++
#include <iosteram>
int m026()
{
	int n;
	std::cin >> n;
	if (n > 0)
	{
		std::cout << "positive" << std::endl;
	}
	if (n < 0)
	{
		std::cout << "negative" << std::endl;
	}
	else
	{
		std::cout << "zero" << std::endl;
	}
	return 0;
}
```

## 1027.计算绝对值

* 输入样例：-3.14
* 输出样例：3.14(保留小数点后两位)
* 代码实现：
```c++
#include <iosteram>
#include <cmath>
int m027()
{
	int x;
	std::cin >> x;
	std::cout << std::fixed << setprecision(2) << abs(x) << std::endl;
	return 0;
}
```

## 1028.奇偶数判断

* 数据：如果n是奇数输出odd；如果n是偶数，输出even
* 输入样例：11
* 输出样例：even
* 代码实现：
```c++
#include <iosteram>
int m028()
{
	int n;
	std::cin >> n;
	if (n ％ 2 == 0)
	{
		std::cout << "even";
	}
	else
	{
		std::cout << "odd";
	}
	return 0;
}
```

## 1029. ASCII码奇偶数判断

* 数据：如果字符n的ASCII码是奇数输出odd；如果n的ASCII码是偶数，输出even
* 输入样例：A
* 输出样例：odd
* 代码实现：
```c++
#include <iosteram>
int m029()
{
	char n;
	std::cin >> n;
	//当字符类型数据直接参与四则运算时，它将以其对应的ASCII码的值进行运算，即不需要转码
	if (n ％ 2 == 0)
	{
		std::cout << "even";
	}
	else
	{
		std::cout << "odd";
	}
	return 0;
}
```

## 1030.整数大小比较
$$
0 <= x <= 2^{32}~~~~~~~~~2^{-31} <= y <= 2^{31}
$$
* 数据：如果x > y输出 >；如果x < y输出 <，如果x = y输出 =
* 输入样例：1000 10
* 输出样例：>
* 代码实现：
```c++
#include <iosteram>
int m033()
{
	long long x, y;
	std::cin >> x >> y;
	if (x == y)
	{
		std::cout << "=";
	}
	if (x > y)
	{
		std::cout << ">";
	}
	if (x < y)
	{
		std::cout << "<";
	}
	return 0 ；
}
```

## 1031.判断是否为两位数

* 数据：判断一个正整数是否是两位数。该正整数是两位数就输出1，否则输出0
* 输入样例：10
* 输出样例：1
* 代码实现：
```c++
#include <iosteram>
int m031()
{
	int n;
	std::cin>>n;
    //切记不能使用连等，不然他会把前一轮的答案(1或0)与后面的相比较
    //&&为与运算符
	if (n > = 10 && n < = 99)
    {
        std::cout<<1;
    }
	else
    {
        std::cout<<0;
    }
	return 0;
}
```

## 1032.收集瓶盖赢大奖

* 数据：如果你有10个“幸运”或20个鼓励的印章，就可以兑换一个神秘大奖。现有x个幸运和y个鼓励瓶盖数，能赢就输出1，否则输出0
* 输入样例：11 19
* 输出样例：1
* 代码实现：
```c++
#include <iosteram>
int m032()
{
	int x, y;
	std::cin >> x >> y;
	if(x >= 10 || y >= 20)
	{
		std::cout << 1;
	}
	else
	{
		std::cout << 0;
	}
	return 0;
}

```

## 1033.判断一个数能否同时帔 3 和 5 整除

* 题目描述：判断一个数n能否同时被3和5整除，如果能就输出YES，否则输出 NO
* 数据：-1,000,000 < n < 1,000,000 
* 输入样例：15
* 输出样例：YES
* 代码实现：
```c++
#include <iosteram>
int m033()
{
	int n;
	std::cin>>n;
	if(n % 3 == 0 && n % 5 == O)
    {
        std::cout<<"YES";
    }
	else{
        std::cout<<"NO";
    }
	return 0;
}
```

## 1034.判断能否被 3 , 5 , 7 整除

* 题目描述：给定一个整数 ， 判断它能否被3，5，7整除，并输出以下信息：
	1、同时被3，5，7（ 直接输出 3 5 7 ，每个数中间一个空格）
	2、只能被被其中两个数（输出两个数，小的在前，大的在后。如3 5或者3 7或者5 7，中间用空格分隔）
	3、只能被其中一个数整除（输出这个数）
	不能被任意一个整除，输出字符n
* 输入样例：15
* 输出样例：3 5
* 代码实现：
```c++
#include <iosteram>
int m034()
{
    int n;
    std::cin >> n;
    if (n % 3 == 0 && n % 5 == 0 && n % 7 == 0)
    {
        std::cout << "3 5 7";
        return 0;
    }
    if (n % 3 == 0 && n % 5 == 0)
    {
       	std::cout << "3 5";
        return 0;
    }
    if (n % 7 == 0 && n % 5 == 0)
    {
    	std::cout << "5 7";
        return 0;
    }
    if (n % 3 == 0 && n % 7 == 0)
    {
		std::cout << "3 7";
         return 0;
    }
    if (n % 3 == 0)
    {
       	std::cout << "3";
        return 0;
    }
    if (n % 5 == 0)
    {
       	std::cout << "5";
        return 0;
    }
    if (n % 7 == 0)
    {
       	std::cout << "7";
        return 0;
    }
    std::cout << "0";
    return 0;
}
```

## 1035.有一门课不及格的学生

* 题目描述：给出一名学生的文和数学成绩，判断他是否恰好有一门课不及格（60分）若是输出1，否则输出0
* 输入样例：50 80
* 输出样例：1
* 代码实现：
```c++
#include <iosteram>
int m035()
{
    int chinese, math;
    std::cin >> chinese >> math;
    //逻辑运算同样有先后顺序，可以通过括号改变
    if ((chinese <= 60 && math > 60) || (chinese > 60 && math <= 60))
    {
        std::cout << 1;
    }
    else
    {
        std::cout << 0;
    }
    return 0;
}
```

## 1036.晶晶赴约会

* 题目描述：晶晶的朋友贝贝约下周一起去看展览，但晶晶每周135必须上课，问晶晶能否接受贝贝的邀请，若能输YES，否则NO
* 输入样例：2
* 输出样例：YES
* 代码实现：
```c++
#include <iostream>
int m036()
{
	int date;
    std::cin >> date;
    
    if (date % 2 == 1 && date != 7)
    {
        std::cout << "YES";
    }
    else
    {
        std::cout << "NO";
    }
    return 0;
}
```

## 1037.骑车与走路

* 题目描述：假设从找到自行车到上自行车的时间为27秒，停车锁车的时问为23秒，步行每秒行走1.2米，骑车每秒行走3米。请判断走不同的距离是骑车快还是走路快。如果车快输出Bike，如果走快输出Walk，如果一样输出All
* 输入样例：120
* 输出样例：Bike
* 代码实现：
```c++
#include <iostream>
int m037()
{
    int d;
    std::cin >> d;
    double walk = d / 1.2;
    double bike = d / 3.0 + 50;
    if (walk > bike)
    {
        std::cout << "Walk";
        return 0;
    }
    if (walk < bike)
    {
        std::cout << "Bike";
        return 0;
    }
    std::cout << "All";
    return 0;
}
```

## 1038.分段函数 y = f(x)
$$
y = -x + 2.5~~~~~~~~~~~~~(0 ≤ x < 5)
$$
$$
y = 2 - 1.5(x - 3)^2 ~(5 ≤ x < 10)
$$
$$
y = \frac{x}{2} - 1.5 ~~~~~~~~~~~~(10 ≤ x < 20)
$$
* 输入样例：1.0
* 输出样例：-1.500
* 代码实现：
```c++
#include <iostream>
#include <iomanip>
#include <cmath>
int m038()
{
    double x;
    std::cin >> x;
    if (0 <= x && x < 5)
    {
        double y = -x + 2.5;
    }
    if (5 <= x && x < 10)
    {
        double y = 2 - 1.5 * pow(x - 3, 2);
    }
    if (10 <= x && x < 20)
    {
        double y = x / 2 - 1.5;
    }
    std::cout << std::fixed << std::setprecision(3) << y;
    return 0;
}
```

## 1039.计篇邮资

* 题目描述：质量在1000克以内（包括1000克）基本费8元。超过1000克的部分，每500克加收4元，不足500克部分按500克计算，如果用户选择加急（y）多收5元
* 输入样例：1200 Y
* 输出样例：17
* 代码实现：
```c++
#include <iostream>
int m039()
{
    int w;
    char isfast;
    std::cin >> w >> isfast;
    if (w <= 1000)
    {
        w = 8;
    }
    else
    {
        w = 8 + ((w - 1000) / 500 + 1) * 4
    }
}
```
