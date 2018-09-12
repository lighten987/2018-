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

//这道题的空在于两个while循环中等号右半部分，平时程序会用两三行写完，题目要求一行，当时没做出来，  
//后面思考能否用三目运算符，思考后代码如上，题目所给测试点能通过   
