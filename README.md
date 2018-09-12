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



***美团笔试第一题***
**规定三个人一组，每个人分别擅长a,b技能，要求每组必须含有两种技能的人，求最大组数**

>#include<iostream>  
using namespace std;  
int main()  
{  
	int m,n;  
	cin>>m>>n;  
	int min = (m<n)?m:n;  
	int max = (m>n)?m:n;  
	int k = 0;  
	if(max > 2*min) k = min;  
	else{  
		int temp;  
		temp = min/3;  
		min = min-3*temp;  
		max = max-3*temp;  
		if(min == 0) k = 2*temp;  
		else if(min == 1) k = 2*temp+1;  
		else if(min == 2){  
			if(max>3) k = 2*temp+2;  
			else k = 2*temp+1;  
		}  
	}  
    cout<<k<<endl;  
	return 0;  
}   

***开始时只想到了找到较小数，然后余3，剩下的数再去判断跟较大数余3后剩下的数能够匹配几个队，后来突然思考到还有种较大数2倍甚至更多的情况，那种情况下组数就是较小数数值，而我开始思考的方法适用于较大数在较小数的1-2倍之间***

***美团笔试第二题***
**给定答题时间，给定每道题用的时间和能获得的分数，求出最大的分数**

/*  
#define N 9  
#define W 121   
int B[N][W] = {0};  
int t[N]={0,20,100,50,80,100,110,5,10};  //时间   
int score[N]={0,20,60,30,55,60,88,3,6};   //分数   
20 20 100 60  
50 30 80 55  
100 60 110 88  
5 3 10 6  
*/  

//探究二维数组初始化问题  memset(a,填充数，sizeof(a))	  
>#include<iostream>    
#include<cstring>  
using namespace std;  
int main()  
{  
	int n,N,W;  
	scanf("%d",&n);  
	N=2*n+1;  
	W=121;  
	int B[N][W];  
	for(int i = 0; i<N; i++){  
		for(int j = 0; j<W; j++){  
			B[i][j] = 0;  
		}  
	}  
//	memset(B,0,sizeof(B));   	
	int t[N]={0};  
	int score[N]={0};  
	for(int i=1;i<N;i++){  
		cin>>t[i]>>score[i];  
	}   
	for(int k=1;k<N;k++){  
		for(int c=1;c<W;c++){  
			if(t[k]>c)B[k][c]= B[k-1][c];  
			else{  
				int value1 = B[k-1][c-t[k]]+score[k];  
				int value2 = B[k-1][c];  
				B[k][c]=value1>value2?value1:value2;  
			}  
		}  
	}  
	cout<<B[8][120]<<endl;  
	cout<<B[N-1][W-1]<<endl;  
//    printf("%d",B[N-1][W-1]);  
    return 0;  
}  
	
***这是一道典型的0/1背包问题，但是每道题的花费时间和所得分数需要读入，而且我用二维数组存储初始化方法为B[N][W] = 0,发现每次答案会有随机答案出现，我调试时将初始化都为0的二维数组打开，发现在第一行取了很多随机数，于是改变了初始化方式，二维数组遍历取零或者用memset函数，成功AC***


**附带求路径的程序**
int x[N] = {0};    
int c = W-1;  
void trace()  
{  
	for(int i = N-1;i>1;i--){  
		if(B[i][c] != B[i-1][c]){//因为有i-1,所以i的范围要>1  后面单独讨论第一个选没有  
		    x[i]=1;  
		    c-=t[i];  
		}  	  
		else{  
			x[i]=0;  
		}   
	}  
	x[1]=(B[1][c]>0)?1:0;	  
}   

***戈尼斯堡七桥问题证明***
>#include<stdio.h>  
#include<stdlib.h>  
int main()  
{  
	//将四个顶点与七条边构造二维数组  没有通路为0   
	int way[4][4]={{0,1,1,1},{1,0,2,2},{1,2,0,0},{1,2,0,0}};   
	int shibai=0;  
    for(int i=0;i<4;i++)   
    {  
    	for(int j=0;j<4;j++)  
		{  
    	int hang=i;int lie=j;  
	loop:if(way[hang][lie]!=0)  
	{  
		way[hang][lie]--;  
		way[lie][hang]--;  
		if(way[4][4]={0})  
		printf("遍历完成\n");  
		else{   
		hang=lie;  
		for(int i=0;i<4;i++)  
		{  
			if(way[hang][i]!=0)  
			{  
			   hang=i;  
			   goto loop;	  
			}  
		}   
		printf("遍历失败\n");  
		shibai++;  
		}  
		}  
	else {  
	printf("遍历失败\n");  
	shibai++;  
	}  
	}   
	}  
	printf("%d",shibai);  
	//失败次数为16次，则无论起点选择哪里都无法走通   
	return 0;  
}  

***构造二维数组，用两个循环实现每个点开始出发，遍历所有情况，输出16次失败，证明无通路***

***中兴比较变态的笔试题***
**钻石存储问题**
>#include<iostream>  
using namespace std;  
int main()  
{  
	int cnt=0;  
	int count;  
	int cap;//总量  
	int sum;//总重   
	int carat[count+1] = {0};  
	int m[count+1][cap+1]={0};// 0/1背包二维图  
	cin>> count>>cap;  
	for(int i=1;i<count+1;i++){  
		cin>>carat[i];  
		sum+=carat[i];  //所有钻石的总重量   
	}  
    while(sum>0){  
	int x[count+1] = {1};//记录路径  
    	for(int i=1;i<=count;i++){  
    		for(int j=1;j<=cap;j++){  
    			if(j>=carat[i]){  
    				if(m[i-1][j]<m[i-1][j-carat[i]]+carat[i]){  
    					m[i][j] = m[i-1][j-carat[i]]+carat[i];  
					}  
					else m[i][j] = m[i-1][j];  
				}   
				else m[i][j] = m[i-1][j];  
			}  
		}   
		int c =  cap-1;  
		for(int i = count; i>1; i--){  
			if (m[i][c]!= m[i-1][c]){  
				x[i]=0;  
				c-=carat[i];  
			}  
		}  
		x[1] = (m[1][c]>0)?0:1;    
		cnt++;  
		for(int i=1;i<=count;i++){  
			carat[i]=carat[i]*x[i];  
			sum+=carat[i];  
		}  	
	}  
	return 0;  
}  

***类似0/1背包问题，问需要的容器数，但是钻石只有大小，所以将价值定为大小等价，每次最大收益就是装得最满的情况，所以是不停的循环做0/1背包，做的次数就是容器数，未调试，不知道运行时间是否足够
ps:有人排序后直接切割，正向排序逆向排序做两次，但是思路太过于投机***


