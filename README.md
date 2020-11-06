# second-day
用链表创建银行账户
#include <iostream>
using namespace std;

int num;
class bank_count {
	friend int login(bank_count* persion);
	friend bank_count* create_bank(bank_count* head);
private:
	string name;
	int count;
	string password;
	double money;
public:
	void add(double ad);
	void fix(bank_count* persion);
	void inquire(bank_count* persion);
	void add_count(bank_count* persion);
	bank_count* next;
};

int login(bank_count* persion)
{
	bank_count a;
	cout << "请输入账户：" << endl;
	cin >> a.count;
	cout << "请输入密码：" << endl;
	cin >> a.password;
	if (persion->count == a.count && persion->password == a.password)
		return 1;
	return 0;
}

//查询用户信息 
void bank_count::inquire(bank_count* persion)
{
	cout << "用户姓名为：" << persion->name << endl;
	cout << "账户为：" << persion->count << endl;
	cout << "余额为：" << persion->money << endl;
}

//增加存款
void bank_count::add(double ad)
{
	money += ad;
}

//新加用户

void bank_count::add_count(bank_count* persion)
{
	bank_count* p1 = new bank_count;
	persion->next = p1;
	num += 1;
	p1->count = num;
	cout << "请输入账户" << p1->count << "的姓名。" << endl;
	cin >> p1->name;
	cout << "请输入账户" << p1->count << "第一次存入的钱。" << endl;
	cin >> p1->money;
	cout << "请输入账户" << p1->count << "的密码。" << endl;
	cin >> p1->password;
}

//账户修改信息
void bank_count::fix(bank_count* persion)
{
	int chioce;
	cout << "修改密码请输入0\n修改姓名请输入1\n都修改请输入2" << endl;
	cout << "请选择你想修改的信息：" << endl;
	cin >> chioce;
	if (chioce)
	{
		string n;
		cout << "请输入你想修改成的信息：" << endl;
		cin >> n;
		persion->name = n;
	}
	else if (chioce == 0)
	{
		string p;
		cout << "请输入你想修改成的密码：" << endl;
		cin >> p;
		persion->password = p;
	}
	else
	{
		string n;
		cout << "请输入你想修改成的信息:" << endl;
		cin >> n;
		persion->name = n;
		string p;
		cout << "请输入你想修改成的密码:" << endl;
		cin >> p;
		persion->password = p;
	}
}

//银行创建；
bank_count* create_bank(bank_count* head)
{
	bank_count* p1, * p2;
	p1 = p2 = new bank_count;
	head = p1;
	num = 1;
	p1->count = num;
	cout << "请输入账户" << p1->count << "的姓名。"<<endl;
	cin >> p1->name;
	cout << "请输入账户" << p1->count << "第一次存入的钱。" << endl;
	cin >> p1->money;
	cout << "请输入账户" << p1->count << "的密码。" << endl;
	cin >> p1->password;
	int circle = 1;
	cout << "如果想继续输入请输入1，否则请输入0." << endl;
	cin >> circle;

	while (circle==1)
	{
		p2 = new bank_count;
		p1->next = p2;
		p1 = p2;
		num += 1;
		p1->count = num;
		cout << "请输入账户" << p1->count << "的姓名。" << endl;
		cin >> p1->name;
		cout << "请输入账户" << p1->count << "第一次存入的钱。" << endl;
		cin >> p1->money;
		cout << "请输入账户" << p1->count << "的密码。" << endl;
		cin >> p1->password;
		cout << "如果想继续输入请输入1，否则请输入0." << endl;
		cin >> circle;
	}

	return head;
}

int main()
{
	cout << "-------------------------------------------欢迎来到银行创建系统！！！----------------------------------------------------" << endl;
	cout << "----------------------------------------------请先初始化系统！！---------------------------------------------------------" << endl;
	bank_count* c = new bank_count, * persion, * head;
	persion = create_bank(c);
	head = persion;
	cout << "-----------------------------------------------恭喜您创建成功!-----------------------------------------------------------" << endl;
	cout << "-----------------------------------------------请登录一个账户!-----------------------------------------------------------" << endl;
	for (int i = 0;i < num;i++)
	{
		if (login(persion))
		{
			int chioce;
			cout << "请输入一个整数表示您将进行的操作：" << endl;
			cout << "输入0表示注销用户\n输入1表示新建一个用户\n输入2表示修改用户信息\n输入3表示存款\n输入4表示查询用户信息" << endl;
			cin >> chioce;
			if (chioce == 0)
			{
				//账户注销
				for (int j = 1;j < num;j++)
					head = head->next;
				head->next = persion->next;
				num -= 1;
				delete persion;
			}
			else if (chioce == 1)
			{
				for (int j = 1;j < num;j++)
					persion = persion->next;
				persion->add_count(persion);
			}
			else if (chioce == 2)
			{
				persion->fix(persion);
			}
			else if (chioce == 3)
			{
				double ad;
				cout << "请输入你将存入的钱数：" << endl;
				cin >> ad;
				persion->add(ad);
				cout << "感谢你的信任！！" << endl;
			}
			else if (chioce == 4)
			{
				persion->inquire(persion);
			}
			else
				cout << "输入错误！！" << endl;
		}
		else if(i==num-1&&login(persion)==0)
			cout << "-------------------------------------------密码错误！！---------------------------------------------------------" << endl;
		persion = persion->next;
	}
	return 0;
}
