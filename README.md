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


***爱奇艺笔试题***  
   
**幸运ID**  
六位数字，求操作几次能使前三位数字和与后三位数字和相同  
***思路：求出前三位的和，后三位的和，将两个三位与数字9的差值放入数组，并分别排序，判断两个和谁大，对应再去判断差值与几个临界值的关系，输出次数***  
>#include<iostream>  
#include<algorithm>  
using namespace std;  
bool cmp(int a,int b)  
{  
    return a>b;  
}  
int main()  
{  
	char c[6];  
	int a[6];  
	int cha1[3];  
	int cha2[3];  
	int sum1 = 0,sum2 = 0;  
	for(int i = 0;i<3;i++){  
		cin>>c[i];  
		a[i] = c[i]-'0';  
		sum1 += a[i];   
		cha1[i] = 9 -a[i];  
	}  
	for(int i = 3;i<6;i++){  
		cin>>c[i];  
		a[i] = c[i]-'0';  
		sum2 += a[i];   
		cha2[i-3] = 9 -a[i];  
	}  
	if(sum1<=sum2){  
	int chazhi = sum2 - sum1;  
	sort(cha1,cha1+3,cmp);  //降序  
	if(chazhi == 0)cout<<"0";  
	else if(chazhi<=cha1[0]) cout<<"1";  
	else if(chazhi<=cha1[0]+cha1[1])cout<<"2";  
	else if(chazhi<=cha1[0]+cha1[1]+cha1[2])cout<<"3";  
	}  
	else{  
	int chazhi = sum1 - sum2;  
	sort(cha2,cha2+3,cmp);  //降序  
	if(chazhi == 0)cout<<"0";  
	else if(chazhi<=cha2[0]) cout<<"1";  
	else if(chazhi<=cha2[0]+cha2[1])cout<<"2";  
	else if(chazhi<=cha2[0]+cha2[1]+cha2[2])cout<<"3";	  
	}  
	return 0;  
}
						       
						       
**局长的实物**  
  
局长有个实物仓储表，每天吃或者买某份食物，求某一天某份实物容量在剩余中排第几  
***思路：将读入时的序号num，读入的容量count,预备成员变量paiming,全定义在food结构体中再放如冰vector，读入字符和数字去找到对应食物对应count进行操作，根据count值排序后更新vector中的paiming成员变量值***  
>#include<iostream>  
#include<vector>  
#include<algorithm>  
using namespace std;  
//用结构体做  
struct food  
{  
	int num;//序号，最后查找用  
	int count;//食物数量  
	int paiming;   
};   
bool cmp(food a, food b)  
{  
	return a.count>b.count;  
}  
vector<food> v(1000);  //预先申请内存！！！   
int main()  
{  
	int n,m,p;  
	cin>>n>>m>>p;  
	for(int i = 0; i <n; i++){  
		cin>>v[i].count;  
		v[i].num = i+1;  
	}  
	for(int j = 0; j<m;j++){  
		char c;  
		int temp;  
		scanf("%c %d\n",&c,&temp);  
//	    cin>>c>>temp;  
		if(c == 'A'){//count++  
		    v[temp-1].count++;  
		}  
		else if(c == 'B'){  
			 v[temp-1].count--;  
		}  
	}  
	sort(v.begin(),v.end(),cmp);  
	v[0].paiming = 1;  
	int k =1;  
	for(int i = 1; i< v.size(); i++){  
		if(v[i].count != v[i-1].count){  
			k++;  
			v[i].paiming = k;  
		}  
		else if(v[i].count == v[i-1].count){  
			v[i].paiming = v[i-1].paiming;  
			k++;  
		}  
	}   
	for(int i = 0;i<v.size();i++){  
		if(v[i].num == p){  
			cout<<v[i].paiming;  
			break;   
		}  
	}  
	return 0;  
}   
***注意：这道题在编写完成后编译没问题，但是读不进去后面增减那些语句，报错的也看不懂，后面将初始化的vector定义了一个大小后，AC，反过头揣测可能是我多次对vector成员不同成员变量操作，需要预先申请内存***
	
	
/*  
百词斩笔试题  给定坐标值，求多边形面积  

>#include<iostream>  
#include<cmath>   
using namespace std;  
int main()  
{  
	int n;  
	cin>>n;  
	double a[n] = {0.0};  
	double b[n] = {0.0};  
	for(int i = 0 ; i < n ; i++){  
		cin>>a[i]>>b[i];  
	}  
	double s = 0;  
	for (int i=0;i<n;i++){  
		s+=((double)a[i]*b[(i+1)%n]-(double)a[(i+1)%n]*b[i])/2;  
		s=fabs(s);  
	}   
	int ss;  
	ss = (int)s;  
	cout<<ss<<endl;   
	return 0;   
}  
*/  



**深信服笔试**  
   
***二进制数末尾的零，输出零的位数的二进制底的数***  
>#include<iostream>   
using namespace std;  
int main()   
{   int k = 0;  
	while(1){  
		int n;  
		cin>>n;  
		if(n == 0)return 0;  
		else{  
			while(n%2 == 0){  
				k++;  
				n/=2;  
			}  
			int sum = 1;  
				for(int i = 0 ; i < k ; i++){  
					sum = sum*2;  
				}  
				cout<<sum<<endl;  
				k=0;  
			}  
		}  
	return 0;  
}  

  
**统计单词输出单词与出现次数，与非法单词个数**  
***思路：单词分割，不区分是否非法，不去除最后的符号，置个标志位放入合法与非法的两个vector    部分正确***   
>#include<iostream>  
#include<vector>  
#include<map>  
using namespace std;  
int main()  
{     
vector<string> v1,v2;  
map<string,int> m;  
    string s,sout,ssout;  
    getline(cin,s);  
    int flag = 0;  
    int k = 0;  
    for(int i = 0 ; i< s.size();i++){  
    	char c;  
    	c = s[i];  
    	if(c == ' ' || c == '\n'){  
				if(flag == 0){  
					if(sout[sout.size()-1]=='!' || sout[sout.size()-1]==',' ||sout[sout.size()-1]=='.' ){  
					for(int j = 0 ; j < sout.size()-1; j++){  
				        ssout[j] = sout[j];  
					}   
					v1.push_back(ssout);  
					m[ssout]++;  
					sout = "";  
					}  
					else {  
						v1.push_back(sout);  
					    m[sout]++;  
					    sout = "";  
					}  
				}   
				else v2.push_back(sout);   
				sout = "";  
		}  
    	else if(c != ' ' || c!= '\n'){  
    		sout += c;  
    		if(c>= '0' && c<= '9') flag = 1; //此单词为非法单词   
			}  
		}   	
	for(int i = 0 ;i < v1.size() ; i++){  
		cout<<v1[i]<<" "<<m[v1[i]]<<endl;  
	}  
	cout<<v2.size()<<endl;  
	return 0;  
}   
  
  
  
***1010字符翻转k个0，求1的最长连续***  
  
>#include<iostream>  
using namespace std;  
int main()  
{  
	int n;  
	cin>>n;  
	int change;  
	cin>>change;  
	int count[n] = {0};  
	int shu = 0;  
	string s;    
	cin>>s;  
	for(int i = 0 ; i < n ; i++){  
		if(s[i] == '0'){  
			count[i]++;  
			shu++;  
		}	  
	}  
	int max = 0;  
	for(int qishi = 0 ; qishi < n-shu ; qishi++){  
		int k = change;  
		int lianxu = 0;  
                int i = qishi ;   
			while(k>0){  
				if(count[i]==0){  
					lianxu++;  
					i++;  
				}  
				else if(count[i]!=0){  
					k--;  
					lianxu++;  
					i++;  
				}  
				while(count[i]==0){  
					lianxu++;  
					i++;  
				}  
		}  
		if(lianxu>max) max = lianxu;  
	}   
	cout<<max;  
	return 0;  
}  
	
	
	
***让数组归零的次数，本数将q，其余数降p***  
>#include<iostream>  
#include<algorithm>  
using namespace std;  
int main()  
{  
	int n;  
	cin>>n;  
	int count[n] = {0};   
	int ccount[n] = {0};  
	int p,q;  
	cin>>p>>q;  
	for(int i = 0 ; i < n ; i++){  
		cin>>count[i];  
	}  
	sort(count,count+n);  
	int kk = 0;  
	for(int i = n-1 ; i >=0 ;i--){  //ccount降序   
		ccount[kk] = count[i];  
		kk++;  
	}  
	int k = 0;  
	int cs = 0;  
	while(ccount[k]>0){  
        int cishu = 0;   
	cishu = (ccount[k]+p-1)/p;   
	for(int i = k+1 ; i < n; i++){  
		ccount[i] = ccount[i] - cishu*q;  
	}  
	cs += cishu;  
	k++;  
    }  
    cout<<cs;  
	return 0;  
}  
	     
	     
***趣味题***     
  
**两个勺子一个舀9两，一个舀13两，客人要6两，量出的方法**  
思路：用大勺子舀n次，总数为13n，再去装小勺子，装m次，可以倒出9m，使得最后剩的为6两，即13n - 9m = 6  
两个的差分别为4 8 12 而超过9之后可以取余为3  
完整数列为：4 8 3 7 2 6  
  
  
***爱奇艺笔试***  
  
