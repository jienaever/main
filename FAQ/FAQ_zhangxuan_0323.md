## 讨论精华 第一期
----
张轩 2016-3-23

###OJ操作问题
----
- Q：我的编程作业总是0分，这个作业到底具体要求是什么呢，求同学给个有分的例子。 PS：这种计算机运行代码的检查方式难道不是太死板了么
- A：作为黑盒测试，作业会给出若干组测试数据，系统会将你的程序运行若干次，每次输入是不同的。如果你每次对应的输出都是正确的，就可以得到满分；得到0分一般是算法有比较明显的问题，或者程序本身编译无法通过。建议在本机进行调试。关于第二个问题，合理的测试数据可以充分检验该程序的正确性、高效性、稳定性等性能，也是所有程序设计比赛中通用的检查办法。尽管代码风格本身是重要的，但最重要的无疑是正确性。
- Q：话是这样说不错 但举个例子，这次作业的第三个编程题，要求输出菱形的那个 我有一句  cout << "输入菱形阶数" << endl; 电脑算错，因为按照要求我多输出了这句话，但这不是一个程序的正常提示么，我去掉这句话后就得满分了 Orz
- A：就人性化而言加一句提示是好的，但系统目前能做到的只能是比对你的输出是否完全和要求的输出一致，提示信息也算作输出的一部分。请谅解~

####问题点评
- 大家或许曾经没有接触过黑盒测试，对黑盒测试的一些性能有所不理解，希望大家在OJ上遇到任何问题时，首先查看我们的[lab FAQ](http://www.xuetangx.com/courses/course-v1:TsinghuaX+00740043X+2016_T1/45aaae55fff144c79706e971dee36b50/)，里面对很多问题都给了比较充分的解释。

###编程作业问题
----
- Q：请问将范围增大之后之所以算不出来是因为超出int值的范围了吗……如果是的话该怎么解决呢？

----
- A：（同学的解答）1.当n的数据范围扩大之后，会爆int，可以使用long long； 2.如果你的算法有问题的话，可能会导致TLE；

---

- A：（助教的解答）int是一个方面，需要用long long int支持更大的数据，更多的则是算法的问题。

	与此密切相关的问题是算法的复杂性。在本章习题中要求使用递归的方法编写斐波那契数列的求解，那么，我们可以根据递归算法考察一下n=5时程序是如何运行的。

	f(5) = f(4) + f(3)——①

	接下来根据递归，我们需要求解f(4)，f(4) = f(3) + f(2)

	好，这里我们发现又需要再次求解f(3)。但这个求解的结果能否被①式所利用呢？答案是不可以，我们并没有把这个计算的结果保存下来。

	可以想见，当n很大时，实际上这样的冗余计算是非常多的

	多到什么程度呢？数学上可以证明，它的计算量是n的指数型函数。“指数爆炸”这一概念，如果学过高中数学的话应该有所了解。也就意味着，当n并不是很大时，实际上计算量已经过大了

	计算机的计算能力也是有限的，当计算量过大时，所需的时间也会过长，导致无法在期望的时间内给出结果。

	初学者对此做简单了解即可，对此有兴趣可以参考“时间复杂度”概念

	至于解决方法，可以尝试使用“递推”的思路哦。

----

- A：（助教的解答）您说的应该是斐波那契那道题的选做版本吧！能找到做对它的思路，说明你在编程能力之上，也有着算法设计的能力。

	事实上，这两种做法的区别远不仅仅在于是否涉及到了函数递归，因而才有极大的运算速度的区别。

	例如使用简单的函数递归的话，想要计算f(5)，则要递归进行f(4)和f(3)；而为了计算f(4)，又要递归进行f(3)和f(2)……注意，f(3)单单在这么短的时间里就出现了两次。出现两次意味着什么？意味着有一个你明明知道是多少的数，却又从f(0)和f(1)一点点向上计算了至少两次。这就造成了时间的浪费。

	如果像你的最后一个做法一样，将它们的数值计算下来并递推，就不会有时间的浪费——每个数都只计算了一次。

	事实上，还可以在不抛弃递归的基础上做好这道题。大家可以这样试试：

	定义一个全局数组，将其初始化为所有的元素都为0。每次如果计算完一个f（x），就把f[x]的值保存为这个值。其实，这就是用一个数组帮你记住“是否已经算过了这个值”。这样的话，就可以在每次进入f(x)时，先检查自己是否算过这个值，如果算过就不需要进行冗余的递归啦！

	下面给一个这种思路的示例（非完全程序，请自行补充剩余部分）。

		long long f[100];
		
		long long fibonacci(int x) {
    		if (f[x] > 0) { // 计算过f(x)的值
        		return f[x];
    		}
    		return f[x] = fibonacci(x - 1) + fibonacci(x - 2);
		}
	
		int main() {
    		for (int i = 0; i < 100; i++)
        		f[i] = 0;
    		f[0] = 1;
    		f[1] = 1;

    		return 0;
		}

####问题点评
- 这道选作题目涉及到了时间复杂度的概念，可能也是第一次大家会频繁出现“TLE”的题目。它告诉我们，对一个算法的评价，仅靠正确性是不够的，足够的效率也是必须的。
- 对此有兴趣的同学可以参见时间复杂度的相关知识，这里提供一篇[Wikipedia的词条链接](https://en.wikipedia.org/wiki/Time_complexity)

###语法细节问题
---
- Q：例题3-2中，

		value+=static_cast（power（2，i））；
static_cast 是什么意思啊？
- A：表示将变量强制转换为int类型。int可以更换成其它的数据类型。注意power函数的返回值本应是double

---

- Q：std::ends和' '有什么区别？为什么我在第二章编程作业里用std::ends代替' '，反馈结果是错误的？
- A：ends输出的是'\0'，相当于字符串的终止符；' '则相当于字符串中的一个空格，二者区别很大。
	
	不同的系统对二者的输出显示是不同的，windows输出ends时会带一个空格，但linux不会。
	
	一般oj采用linux环境的比较多。建议需要输出空格时还是直接输出' '吧。
	
---

- Q：换行操作endl与\n有什么差别，为什么有两个，用哪一个比较好？"\n"和'\n'有什么差别，仅仅只是"\n"的后面多了一个’\0‘的字符？
- A：
	
	**1 endl和'\n'的差别**

	std::endl可以看作是只能和cout配合使用的一个东西——实际上它是一个函数，其作用是在其对应的位置添加一个换行符'\n'。例如：
	
		cout << "hello world!" << endl;
	实际上和
	
		cout << "hello world!\n";
	在结果上没有差别。
	
	不过，硬要说的话其实是有一点不同的：在std::endl的实现中，它做了一次“刷新输出缓冲区”的工作。不清楚这个工作是做什么的并不要紧——实际上我也不清楚——不过频繁地采用std::endl代替'\n'可能会由于这额外的工作而浪费一些时间。大家可以分别用两种方法输出大量（非常大量）的换行，看看运行的时间是不是真的有差距。
	
	你有一个用词非常好：换行操作。可以试试这样的一行语句：
	
		std::endl(cout);
	猜猜它的功能，然后去试试看猜的对不对吧！不过要理解这个语句的原理可能就稍显复杂了，感兴趣的同学可以自己查阅一下相关的资料。这里是[一篇博客文章](http://soft.zdnet.com.cn/software_zone/2008/0118/710903.shtml)，感兴趣的话可以阅读一下，相信可以加深你对cout“输出语句”的认识。
	
	**2 "\n"和'\n'的区别**
	
	这个区别可就大了——前者用""包裹起来，说明它是一个字符串，一般情况下可以说它是一个char数组。而后者则用''包裹，这代表着它是一个字符，也就是char。如果要说它们之间有什么差别的话，不如说它们只是碰巧长得比较像一样——前者是一句话，可惜它只有一个字“好”；而后者则是单一个‘好’字。程序世界对于“话”和‘字’的区分（实际上是C++对“类型”的区分）可是相当严格的，绝对不要弄混。该用一句话的地方就不能用‘字’，而如果有人只要一个字，你也不能塞给他一句“话”——即使这句话只有一个字也不行。
	
	举个例子：头文件中有这样一个函数strcmp(const char* str1, const char* str2)，它的功能是接受两个字符串，如果它们相等则返回0，否则返回非0的值。此时可绝对不能
	
		cout << strcmp('\n', "\n"); // ERROR!!
		
	这就是那个该用一句话的地方——只给一个字是不可以的。
	
	说的有点绕了，可能把简单的问题搞复杂了。当然了，你说的差别其实也很对，前者实际上要多一个标志char数组（或许也可以直接称之为字符串）结束的标志'\0'。
	
