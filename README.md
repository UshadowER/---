#include <iostream>
#include <string.h>
#include <stddef.h>
using namespace std;

#define OK 1
#define ERROR -1
#define Status int

typedef struct
{
	string name;
	string number;
	int scores;
}student;

typedef struct LNode
{
	student data;
	struct LNode *next;
}LNode,*LinkList;

int InitList(LinkList &L)
{
	L=new LNode;
	L->next=NULL;
	return OK;
}

void CreateList_R(LinkList &L,int n)
{
	LinkList r,p;
	L=new LNode;
	L->next=NULL;
	r=L;
	cout<<"请依次输入学生的姓名，学号以及成绩"<<endl;
	for(int i=0;i<n;i++)
	{
		p=new LNode;
		cin>>p->data.name>>p->data.number>>p->data.scores;
		p->next=NULL;r->next=p;
		r=p;
	}
}

int GetElem(LinkList L,int i,student &e)//取值函数 
{
	
    int j;
    LNode *p;
	p=L->next;j=1;
	while(p&&j<i)
	{
		p=p->next;
		++j;
	}
	if(!p||j>i)return ERROR;
	e=p->data;
    //cout<<e.name<<e.number<<e.scores<<endl; //(这里有问题！！！) 
	return OK;
}

LNode *LocateElem(LinkList L, student e)
{
	int j;
	LNode *p;//这里LNode p与LNode *p，前者是定义一个类型为LNode的变量，后者是定义一个类型为LNode的指针 
	p=L->next;
	while(p&&p->data.name!=e.name) 
		p=p->next;
	cout<<p->data.number<<p->data.scores; 
	//return p;
	
}

Status ListInsert(LinkList &L,int i,student e)//单链表的插入 
{
	int j;
	LinkList p,s;
	p=L;j=0;
	while(p&&(j<i-1))
	{
		p=p->next;++j;
	}
	if(!p||j>i-1) return ERROR;
	s=new LNode;
	s->data=e;
	s->next=p->next; 
	p->next=s;
	return OK;
}

Status ListDelete(LinkList &L,int i)//单链表的删除 
{
	int j;
	LinkList p,q;
	p=L;j=0;
	while((p->next)&&(j<i-1))
	{
		p=p->next;++j;
	}
	if(!(p->next)||(j>i-1))return ERROR;
	q=p->next;
	p->next=q->next;
	delete q;
	return OK; 
}

Status ListLength_L(LinkList L)
{
	LNode *p;
	p=L->next;
	int i=0;
	while(p)
	{	
		i++;
		p=p->next;
	}
	return i;
}

int main()
{
	student G ; 
	LNode *R,*p;
	int choice;
	int o,N,j;
	string nn;
	cout<<"[1] 初始化一个空的学生信息表"<<endl;
	cout<<"[2] 输入学生信息"<<endl;
	cout<<"[3] 根据位置查找学生信息"<<endl;
	cout<<"[4] 插入学生信息"<<endl;
	cout<<"[5] 删除学生信息"<<endl;
	cout<<"[6] 根据姓名查找学生信息"<<endl;
	cout<<"[7] 输出全部的学生信息"<<endl;
	while(1)
	{
		cout<<"请输入你的选项"<<endl;
		cin>>choice;
		switch(choice)
		{
			case 1:
				if(InitList(R))
				cout<<"学生信息表创建成功！"<<endl;
				else
				cout<<"学生信息表创建失败！"<<endl;
				break;
			case 2:
				cout<<"请输入你要插入的学生信息的个数"<<endl;
				cin>>N;
				CreateList_R (R,N);
				break;
			case 3:
				cout<<"请输入你想要查找的学生的位置"<<endl;
				cin>>j;
				GetElem(R,j,G);
				cout<<G.name<<G.number<<G.scores<<endl; 
				break;
			case 4:
				{
				cout<<"请输入你要插入的位置"<<endl;
				int bo;
				string bu,bi;
				cin>>o;
				cout<<"请输入你要插入的学生的姓名，学号以及成绩"<<endl;
				cin>>bu>>bi>>bo;
				G.name=bu;
				G.number=bi;
				G.scores=bo; 
				if(ListInsert(R,o,G))
				cout<<"插入成功"<<endl;
				else
				cout<<"插入失败"<<endl;
				}break;
			case 5:
				cout<<"请输入你要删除的学生信息的位置"<<endl;
				cin>>o;
				if(ListDelete(R,o))
				cout<<"删除成功"<<endl;
				else
				cout<<"删除失败"<<endl;
				break;
			case 6:
			    cout<<"请输入你想要查找的学生的姓名"<<endl;
				cin>>nn;
				G.name=nn;
				LocateElem(R,G);
				break;
			case 7:
				
				int j;
				j=ListLength_L(R);
				p=R;
				for(int i=0;i<j;i++)
				{	p=p->next;
					cout<<p->data.name<<p->data.number<<p->data.scores<<endl;
				}
				//cout<<j<<endl;
				break;
		}
    } 
    return 0;
}













