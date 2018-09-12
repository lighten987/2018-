# 2018-
一丢丢见过的尝试做的都扔到这里来了

***招商银行填空题***  

**26进制转换**  
// 0-25 对应 a-z 输入100 输出 dw  
//考点：一条语句完成对字符串和数据值的操作，思路用三目运算符，测试通过   

//若只有整数  
>#include<iostream>  
using namespace std;  
int main()  
{  
	string str = "abcdefghijklmnopqrstuvwxyz";  
	int n;  
	cin>>n;  
	string out = "";  
	while(n>0){  
		out = out+str[(n/26>0)? n/26 : n%26];  
		n = (n>26)? n-(n/26*26) : 0;  
	}  
	cout<<out<<endl;  
	return 0;  
}   

//若有分数部分  最多两位小数   
>#include<iostream>  
using namespace std;  
int main()  
{  
	string str = "abcdefghijklmnopqrstuvwxyz";  
	double n;  
	cin>>n;  
	int zheng,xiaoshu;  
	zheng = n/1;  
	xiaoshu = 100*(n-zheng);  
	string out1 = "";  
	string out2 = "";  
	while(zheng>0){  
		out1 = out1+str[(zheng/26>0)? zheng/26 : zheng%26];  
		zheng = (zheng>26)? zheng-(zheng/26*26) : 0;  
	}  
	while(xiaoshu>0){  
		out2 = out2+str[(xiaoshu/26>0)? xiaoshu/26 : xiaoshu%26];  
		xiaoshu = (xiaoshu>26)? xiaoshu-(xiaoshu/26*26) : 0;   
	}  
	cout<<out1<<"."<<out2<<endl;  
	return 0;  
}    

***这道题的空在于两个while循环中等号右半部分，平时程序会用两三行写完，题目要求一行，当时没做出来，  
后面思考能否用三目运算符，思考后代码如上，题目所给测试点能通过***  


***招商银行编程大题***  

**随机抢红包，使得红包刚好抢完，输出每个人的金额，并输出谁抢到最多，规定第一个人的金额为恒定的**

>#include<iostream>  
#include<stdlib.h>  
using namespace std;  
int main()  
{  
	double total,n,low,high;  
	cin>>total>>n>>low>>high;  
	total = total*100;  
	low = low*100;  
	high = high*100;  
	double a[100] = {0.0};  
	double b[100] = {0.0};  
	a[1] = 100;  
	b[1] = total-100;  
	int temp = high-low;  
	double max = 0.0;  
	int maxnum = 1;  
	int k=2;  
	while(1){	  
	while(k<=4){  
		int x = rand()%temp;  
		a[k] = x+low;   //抢到的钱   
		if((x+low)>max){  
			max = x+low;  
			maxnum = k;  
		}  
		total = total-(x+low);  
		b[k] = total;   //剩下的钱   
		k++;  
	}  
	if(total>=low && total<=high){  
		a[5] = total;  
		b[5] = 0;  
		if(a[5] > max)maxnum = 5;  
		for(int i = 1;i<=5;i++){  
			printf("第%d个人抢到的红包金额为%.2lf,红包剩余金额为%.2lf\n",i,a[i]/100,b[i]/100);  
		}  
		printf("\n抢到红包金额最多的是 %d 号",maxnum);  
		break;  
	}  
	else k=2;  
	}  
	return 0;  
}  
					
***因为金额涉及小数部分，所以将整体扩大100，处理小数点，最后输出时缩小100，对于金额分配的问题，随机数取值范围在0-最大金额与最小金额差之间，再加上最小金额底线，对于刚好抢完金额问题的处理，在while死循环中前面四个人抢完，判断第五个的余下金额是否满足条件，若满足，比较输出，并跳出死循环，若不满足，继续执行死循环***					
