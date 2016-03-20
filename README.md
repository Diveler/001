#include<iostream>
#include<ctime>
#include<cstdlib>
using namespace std;
void Out(int x,int x0,int y,int y0,int z,int z0,int &i,int n,int m0){
	switch(z0){//判断整数或分数
	case 0:{
		switch(z){//运算法则判断
		case 0:
			cout<<n<<"   ("<<x<<")"<<" + "<<"("<<y<<")"<<" ="<<endl;
			break;
		case 1:
	       	cout<<n<<"    ("<<x<<")"<<" - "<<"("<<y<<")"<<" ="<<endl;
			break;
		case 2:
	   		cout<<n<<"    ("<<x<<")"<<" * "<<"("<<y<<")"<<" ="<<endl;
	    	break;
		case 3:
			if(y!=0){//防止出现除数为零的情况
				if(m0==2){
					if(x%y==0)//余数判断（该操作可能会降低除法概率，，）
						cout<<n<<"    ("<<x<<")"<<" / "<<"("<<y<<")"<<" ="<<endl;
					else
						i--;
				}
				if(m0==1)
					cout<<n<<"    ("<<x<<")"<<" / "<<"("<<y<<")"<<" ="<<endl;
			}
			else
				i--;
			break;
		}
		break;
		   }
	case 1:{
		if(x0!=0&&y0!=0){
			switch(z){//运算法则判断
			case 0:
				cout<<n<<"    ("<<x<<"/"<<x0<<")"<<" + "<<"("<<y<<"/"<<y0<<")"<<" ="<<endl;
				break;
			case 1:
				cout<<n<<"    ("<<x<<"/"<<x0<<")"<<" - "<<"("<<y<<"/"<<y0<<")"<<" ="<<endl;
				break;
			case 2:
				cout<<n<<"    ("<<x<<"/"<<x0<<")"<<" * "<<"("<<y<<"/"<<y0<<")"<<" ="<<endl;
				break;
			case 3:
				if(y!=0)//防止出现除数为零的情况
					cout<<n<<"    ("<<x<<"/"<<x0<<")"<<" / "<<"("<<y<<"/"<<y0<<")"<<" ="<<endl;
				else
					i--;
				break;
			}
		}
		else
			i--;
		break;
		   }
	}
}
void Judje(int &x,int &x0,int &y,int &y0){//保证真分数以及最简分数
	int m,i1;
	if(x>x0){//保证x<x0即保证为真分数
		m=x;
		x=x0;
		x0=m;
	}
	for(i1=x0;i1>1;i1--){//保证为最简分数
		if(x%i1==0&&x0%i1==0){
			x=x/i1;
			x0=x0/i1;
		}
	}
	if(y>y0){//保证y<y0即保证为真分数
		m=y;
		y=y0;
		y0=m;
	}
	for(i1=y0;i1>1;i1--){//保证为最简分数
		if(y%i1==0&&y0%i1==0){
			y=y/i1;
			y0=y0/i1;
		}
	}
		
}
void main(){
	int x,x0,y,y0,z,z0,j,n,n0,m,m0=0;//定义变量
	int num,max,min;
	cout<<"请输入随机数范围（先最小值，后最大值）"<<endl;
	cin>>min;
	cin>>max;
	cout<<"请输入加减是否有负数：1、有；2、没有"<<endl;
	cin>>j;
	cout<<"请输入是否要有乘除法：1、有；2、没有"<<endl;
	cin>>m;
	if(m==1){
		cout<<"请输入除法是否有余数（分数不做区别）：1、有；2、没有"<<endl;
		cin>>m0;
	}
	cout<<"请输入需要打印的题目数量（大于等于1）："<<endl;
	cin>>num;
	int *a=new int[num*5];//定义数组存储运算
	srand(time(0));//定义时间种子
	int i=0;
	if(min<0&&j==2)
		min=0;
	x = rand()%(max-min+1)+min;//产生随机数
	x0 = rand()%(max-min+1)+min;
	y = rand()%(max-min+1)+min;
	y0 = rand()%(max-min+1)+min;
	if(m==1)
		z = rand()%(3-0+1)+0;
	if(m==2)
		z = rand()%(1-0+1)+0;
	z0 = rand()%(1-0+1)+0;//用于判断整数运算与分数运算}
	Judje(x,x0,y,y0);
	cout<<"序号"<<endl;
	n=1;
	Out(x,x0,y,y0,z,z0,i,n,m0);
	a[0]=x;
	a[1]=x0;
	a[2]=y;
	a[3]=y0;
	a[4]=z;
	for(i=1;i<num;i++){//利用FOR循环进行剩余输出
		n=i+1;
		n0=i*5;
		x = rand()%(max-min+1)+min;//产生随机数
		x0 = rand()%(max-min+1)+min;
		y = rand()%(max-min+1)+min;
		y0 = rand()%(max-min+1)+min;
		if(m==1)
			z = rand()%(3-0+1)+0;//运算符
		if(m==2)
			z = rand()%(1-0+1)+0;
		z0 = rand()%(1-0+1)+0;//用于判断整数运算与分数运算}
		Judje(x,x0,y,y0);
		a[n0]=x;
		a[n0+1]=x0;
		a[n0+2]=y;
		a[n0+3]=y0;
		a[n0+4]=z;
		if(x!=x0&&y!=y0&&x0!=1&&y0!=1){//防止出现在x=x0时输出依旧为x/x0格式以及分母为一的情况
			if(a[n0]!=a[n0-5]||a[n0]!=a[n0-4]||a[n0]!=a[i-3]||a[n0]!=a[n0-2]||a[n0]!=a[n0-1]){//题目避免重复
				Out(x,x0,y,y0,z,z0,i,n,m0);
			}
		}
		else
			i--;
	}
	delete []a;
}
