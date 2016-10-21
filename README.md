# grammer_end
grammer_end,递归下降语法分析
#include<iostream>
#include<cstdio>
using namespace std;
#include<cstring> 
#include<math.h>
#include<fstream>
#include<stdlib.h>

string  key[14]={"program","const","var","procedure","begin","end",
               "if","else","then","call","while","do","read","write"};
string  Yunsuan[5]={"+","-","*","/","odd"};
string  JieFu[4]={",",";","(",")"};
string GuanxiFu[6]={"=","<","<=",">",">=","<>"};   
char ch;               
string str_get;      
string text="program id; d=15+3;";
int pt=0;       
int line=1,i;

int type;
int Error_num;
int choice();  
void Input();
bool Anlyze_Prog();
bool Anlyze_block();
bool Anlyze_condecl();
bool Anlyze_const();
bool Anlyze_vardecl();
bool Anlyze_proc();
bool Anlyze_body(); 
bool Anlyze_statement();
bool Anlyze_lexp();
bool Anlyze_exp();
bool Anlyze_term();

bool Anlyze_id(); 
bool Anlyze_interger();

int Is_FuZhi_sentence();
int Is_Case_sentence();
int Is_XunHuan_sentence();
int Is_Call_sentence();
int Is_read_sentence();
int Is_write_sentence(); 


int Is_lexp_expression();
int Is_exp_expression(); 
int Is_term_expression();
int Error_type[40];

int Find_type_key();
int Find_type_GuanXi();
int Find_type_Yunsuan();
int Find_type_JieFu(); 

int Find_ZhiBiaoFu();
int Find_ZhiBiaoFu()
{
	if(ch=='\t')
	Input();
}
int blingblingtt()
{
	Input();
	cout<<str_get<<"-----------"<<type<<endl;
	Input();
	cout<<str_get<<"============="<<type<<endl;
}
bool Anlyze_Prog()
{    
    Input();
    if(type==0)  
    {
		//cout<<type<<endl;
		 //
		 cout<<"---program进入成功!"<<endl;
	Input();
    if(type==-1)     //if(Anlyze_id())
        {

		 Input();
		   
	}
	else  
	  {    cout<<"program后缺少标识符"<<endl;
 cout<<"此时的type为:"<<type<<":"<<str_get<<endl;
}
    if(type!=20)
    {
    	cout<<"缺少;"<<endl;
    	//return false;
	}
    else cout<<"program语句成功----"<<endl;
}
    if(Anlyze_block())          //这个block块里可以有多个proc语句 
         return true;
else     return false;
}
 bool Anlyze_block()
 {  
   
 	Input();
 	cout<<"=======《block块》========="<<endl;
 
 if(type==1)      //逻辑矛盾????????? 
 {
 	if(Anlyze_condecl())
 	Input();
	 if(type==2)
	 {
	 if(Anlyze_vardecl())
	 Input();
	  if(type==3)
	 {
	  if(Anlyze_proc())
	  Input();
	  cout<<"<<block块语句群分析结束>>"<<endl;//1,2,3 
}
}
  else if(type==3)
      { if(Anlyze_proc())
	   cout<<"<<block块语句群分析结束>>"<<endl;//1,3 
}
 }
 else if(type==2)
 {

  if(Anlyze_vardecl());
 	Input();
 	if(type==3)
 	{
 	 if(Anlyze_proc())  //2,3
    Input();
    cout<<"<<block块语句群分析结束>>"<<endl;
 	}
	 cout<<"<<block块语句群分析结束>>"<<endl; 
 }
 else if(type==3)
 {
 if(Anlyze_proc())
 Input();
}  
if(type==4)
{

	if(Anlyze_body())
{     
		return true;
	}
	else 
	{
    cout<<"************退出body块:************"<<endl;
	    cout<<"此为非法语句"<<endl;
		 return false;
	}
}

 }
 //}
 bool Anlyze_condecl()
 {
  	//Input();
  	if(type==1)
 	while(type==1)
 	{
 		cout<<"------进入condecl块-------"<<endl;
 	//Input();
 	if(Anlyze_const())
 	 //Error_num=1;
 	 Input();
 
}
	return  false; 	
	
}
bool Anlyze_const()
{
	 Input();
	 cout<<"=======进入const语句====="<<endl;
     if(type==-1)    //a
     {
     Input();
       if(str_get==":")   
        {
        	Input();
		if(type==23) //:=
       Input();
       	  if(type==-2)//num 
		   {
     Input(); 
       }
         if(type==20)   
		 {
	  cout<<"const语句正确"<<endl;   return true;
      }  else 
        {
      cout<<"第"<<line<<"行:"<<str_get<<"后缺少;---2"<<endl;
	  return false;    
}  
	 }
	 else if(type==-2)
                {
				cout<<"第"<<line<<"行:"<<"在"<<str_get<<"后缺少赋值号:"<<endl; 
	             return true;
			}
}
 else  
      {  
	  cout<<"第"<<line<<"行:"<<"=======Error const!===="<<endl;
	  cout<<"const后应该接标识符"<<endl; 
       return false;
      } 
      //Input();
}
bool Anlyze_vardecl()
{
	//Input();
	cout<<"========进入var语句========="<<endl; 
	if(type==2)
	Input();
	 if(type!=-1)
     {
	 cout<<"第"<<line<<"行:"<<"在关键字var后缺少标识符====="<<endl;
}

if(type==-1)
{
	Input();
	while(type==19)
	{
		Input();
		if(type==-1)
		Input();
	}
      if(type==20)
     { 
	  cout<<"=====var语句正确"<<endl;
	   return true;
}
     	else {
	   cout<<"第"<<line<<"行:"<<"缺少;";//缺少;
	 return false;
	  }
}
}
bool Anlyze_proc()
{
	//Input();
	cout<<"===========进入proc语句============="<<endl;
	if(type==3)
	Input();
	
	if(Anlyze_id())   
{ 	
  Input();
	if(type==21)     //p(a,b,c)
	{
	Input();
	 if(Anlyze_id())
{  
   Input();
	while(type==19)         //,b,
       {
	   Input();
	   if(Anlyze_id())
	   Input(); 
   }
   if(type==22)
     Input();
       if(type==20) 
	   { 
	      cout<<"=====produrce语句正确========="<<endl; 
		  return true;
		   }    
   	else {
	 cout<<"第"<<line<<"行:"<<"缺少;"<<endl;//缺少;
	  return false; 
	 }             
}
	else
	{
		cout<<"第"<<line<<"行:"<<"(后接的应当是标识符"<<endl;
		cout<<"=====produrce语句出错========="<<endl; 
		return false; 
	}
}
}		else 
	{
	     cout<<"第"<<line<<"行:"<<"procedure后应当接标识符"<<endl;
	   return false;
}
}
bool Anlyze_body()
{
	
	//Input();
	 cout<<"begin:----------------------------------------------------"<<endl;
	   cout<<"===========进入body块=========="<<endl;
	if(type==4)                 //begin
	{
	Input();
	Input();
  	if(Anlyze_statement())   
	{	
 Input();
	while(Anlyze_statement())
      { 
//               Input();
Input();
    cout<<"00000此时的str_Get("<<str_get<<")"<<endl;  
}
}
  else
      {   cout<<"第"<<line<<"行:"<<"body中缺少语句"<<endl; 
      Input();
  }
}
    if(type==5)                 //end
    {    
    cout<<"============body块正确==============="<<endl;
    cout<<"============body块结束================"<<endl;
    cout<<"end:----------------------------------------------------"<<endl;
         return true;
  } 
    else
   { 
     cout<<"第"<<line<<"行:"<<"没有与begin相匹配的end"<<endl; 
   cout<<"============body块出错================"<<endl; 
   cout<<"============body块结束================"<<endl;
    return false;
}
}
bool Anlyze_statement()
{
	cout<<"=====================进入statement语句==============="<<endl;
	
if(type==4)
	{   
	cout<<"!!!!!!!从语句进入body块>>>>>>>>>>>>>>>>>>>>>>>>>>>>"<<endl;
		if(Anlyze_body())  
		{
		    Input();
		}
		return true;
	}
 else if(type==5)
  {
  	cout<<"==============body块结束==============="<<endl;
  	 cout<<"end:----------------------------------------------------"<<endl;
  }
 else  if(type==-1)
   {
   if(Is_FuZhi_sentence())
   {
   Input(); 
}
cout<<"第一个赋值语句之后的str_get*("<<str_get<<")"<<endl; 
   return true;
}

else     if(type==6)
	{ 
    if(Is_Case_sentence())
    Input();
    return true;
}else   if(type==10)
{
    if(Is_XunHuan_sentence())
Input();
    return true;
}else   if(type==9)
{
    if(Is_Call_sentence())
   Input();
    return true;
}else  if(type==12)
{	if(Is_read_sentence()) 
	Input();
	return true;
}else   if(type==13)
{   
cout<<"对write进行了执行"<<endl;
	if(Is_write_sentence())
     {
	 cout<<"write语句之后的str_get值("<<str_get<<")"<<endl;
	 Input();
}

  
     return true;
 }
 else if(ch=='\n')
 {   
 if(ch=='\n')
 cout<<"---------------分析文件结束----------------------"<<endl;
  cout<<"---------------分析文件结束----------------------"<<endl;
 return 0;
 }
else
	{
	cout<<"*******************************"<<endl;
	cout<<"*******************************"<<endl; 
	cout<<"=========="<<str_get<<":为错误语句!!!!"<<endl; 
	    cout<<"=====================statement语句end============"<<endl;
	      Input();
	   return false;	
}
}
bool Anlyze_id()
{
	if(type==-1||type==-2)
    return true;
	else 
	return false;//
}
//-----------------------------------------------
int Is_FuZhi_sentence()
{
	cout<<"1>进入赋值语句================="<<endl;
	if(Anlyze_id())
{
	if(str_get==":")
	Input();
	if(type==23)    //:= 
	Input();
	if(Is_exp_expression())
	{
   if(type==20)
   {
   cout<<"==============赋值语句正确"<<endl;
   cout<<"=====================赋值语句结束===================="<<endl;
   return true;
   }
   else{ 
   cout<<"缺少;赋值语句出错====="<<endl;
   cout<<"=====================赋值语句结束===================="<<endl;
   return false;
}
}
    else
    {
    cout<<"赋值语句出错============"<<endl;
    cout<<"=====================赋值语句结束===================="<<endl;
    return false;
}
}
}
int Is_Case_sentence()
{
//Input();
cout<<"2>进入条件语句================="<<endl;
if(type==6)
{
Input();
if(Is_lexp_expression())
{
Input();
    if(type==8)
    {
	  Input();
        while(Anlyze_statement())	
        Input();
    }
    else
    {
    	cout<<"if后缺少执行语句关键字then"<<endl;
    	return false;
	}
}
else {
	cout<<"if后所所接条件不合语法"<<endl;
	return false; 
}

if(1)
{
if(str_get=="else")
Input();
while(Anlyze_statement())
{ cout<<"Case语句执行成功."<<endl;
return true;
}
}
return  true;  //.>>><<<
}
return false;
}

int Is_XunHuan_sentence()
{
cout<<"3>进入循环语句================="<<endl;
cout<<"此时的str_get为"<<str_get<<endl; 
if(type==10)
{
Input();
if(Is_lexp_expression())
   if(type==11)
    {       Input();
	if(ch==' ') 
	  Input(); 
           if(Anlyze_statement())    
{   
cout<<"循环语句正确"<<endl;
return true;
}
else
{
cout<<"循环执行语句do后的语句出错"<<endl;
return false;
}
}
  else 
           cout<<"缺少与while匹配的关键字do"<<endl;

}
else
cout<<"第"<<line<<"行:"<<"=Error XunHuan_sentence!===="<<endl;
return false;
}
///-------------------------------------
int Is_Call_sentence()
{
Input();
cout<<"4>进入call语句================="<<endl;
if(type==9)
  Input();
  if(Anlyze_id())
  Input();
    if(type==21)
  Input();
  while(Is_exp_expression())
  {
 if(type==19)
 Input();
  else if(type==22)
  { cout<<"call语句正确Str_get为:("<<str_get<<")"<<endl; 
    Input(); 
  	   if(type==20)
   {
  		cout<<"=========call语句正确======="<<endl;
  		cout<<"=====================call语句结束===================="<<endl;
		  return true;
   }
   else{ cout<<"缺少;赋值语句出错====="<<endl;
   return false;
}
  return true;}
}
return false;
}
//------------------------------------------------
int Is_read_sentence()
{
	//Input();
	cout<<"5>进入read语句================="<<endl;   
	if(type==12)
	Input();
	if(type==21)
{	Input();
	if(Anlyze_id())    
	Input();
	if(type==22)         
	{   
		cout<<"此时的str_get为:"<<str_get<<endl;  
		Input();
	   if(type==20)
   {
  		cout<<"=========read语句正确======="<<endl;
		  cout<<"=====================read语句结束===================="<<endl;
		  return true;
   }
   else{ cout<<"=======缺少;read语句出错====="<<endl;
   cout<<"=====================read语句结束===================="<<endl;
   return false;
}
}  
     else
     {
     cout<<"======read语句中标识符后缺少与'('相匹配的')'"<<endl;
     return false;
 }
}
else cout<<"=====read后缺少("<<endl;
      return false;
}
int Is_write_sentence()
{
cout<<"6>进入write语句================="<<endl;     
cout<<"此时str_get的值为:"<<str_get<<endl;
if(type==13)
Input();
if(type==21)
{ Input();
if(Is_exp_expression())
{  
  if(type==22)
  {   if(type==22)
  //cout<<"==========write语句正确=="<<endl;	
  Input();
     if(type==20)
   {
   cout<<"=========write语句正确"<<endl;
   cout<<"=====================write语句结束===================="<<endl;
   return true;
   }
   else{  cout<<"缺少;write语句出错====="<<endl;
   cout<<"=====================write语句结束===================="<<endl;
   return false;
}
}
  else
     {
     cout<<"======write语句中标识符后缺少与'('相匹配的')'"<<endl;
     return false;
 }
}   else {cout<<"write语句后应当接("<<endl; 
       return false;
 }
}
}
int Is_exp_expression()
{
	cout<<"=========进入exp表达式========="<<endl;
	if(Is_term_expression())
{
     if(type==14||type==15)    //+,-
{	Input();
	if(Is_term_expression())
	{
	cout<<"======exp表达式正确========="<<endl;
	cout<<"=====exp表达式结束========="<<endl; 
	return true;
}  else
{   cout<<"=========exp表达式出错========"<<endl;
   cout<<"=====exp表达式结束========="<<endl; 
   return false;
}
}
}
else { cout<<"=======赋值语句后应接exp表达式======="<<endl;
        return false;
    } 	  
}
int Is_lexp_expression()
{
	if(Is_exp_expression())
	{
	// Input();
	if(type>=23&&type<=28)
	{
	 { 
	Input();
   
}
	if(Is_exp_expression())
    {
	cout<<"关系表达式正确"<<endl;
	//cout<<"str_get:"<<str_get<<endl; 
	return true;
}
  else{
  	cout<<"关系符后所接表达式出错"<<endl;
  }
}
else{ cout<<"缺少关系符"<<endl;
return false;
}
}
   else 
   return false;
    
}
int Is_term_expression()
{
	//Input();
	cout<<"======进入term表达式----"<<endl; 
	if(Anlyze_id())
	{
	Input();
	if(type==16||type==17)
{	Input();
	if(Anlyze_id())
	{
	cout<<"term表达式正确"<<endl;
	Input();
	return true;
}  else{
	cout<<"*,/缺少右因子"<<endl;
	return false;
}
}
else 	{cout<<"term表达式成功，单因子"<<endl;
		 return true;
} 
}
	 return false;
}
//========================================================================================

int Find_type_key(string str)
{
	for(i=0;i<14;i++)
	{
		if(str==key[i])
		 return i;
	}	
	return -1; 
} 
int Find_type_Yunsuan(string str)
{
	for(i=0;i<5;i++)
	if(str==Yunsuan[i])
	return i+14;
}
int Find_type_JieFu(string str)
{
	for(i=0;i<4;i++)
	if(str==JieFu[i])
	return i+19;
}
int Find_type_GuanxiFu(string str)
{
	for(i=0;i<6;i++)
	if(str==GuanxiFu[i])
	return i+23;
}
//===================================================================================
int  choice()
{
cout<<"===================================================="<<endl
    <<"词法分析器.1>从文件中输入;   2>字符串输入;"<<endl
    <<"===================================================="<<endl;
    int choice;
    while(1)
    {
    cin>>choice;
    if(choice==1)
    {
        fstream outfile;
        outfile.open("1.txt");
        text.clear();
        char temp;
        while(1)
        {
          if(outfile.eof()) break;
          outfile.get(temp);
          text+=temp;
        }
        cout<<"要分析的程序内容："<<endl;
        cout<<text<<endl;
        break;
    }
    else if(choice==2)
    {
        cout<<"要分析的程序内容："<<endl;
        cout<<text<<endl;
        break;
    }
    else if(choice==0)
        exit(0);
    }
    return 0;
}
int main()  
{
     choice();
/*
     while(pt<text.length())
    {
       //Input1();
	  Input();
    }
    cout<<str_get;   
*/
	  cout<<endl<<endl;
	  cout<<"---------------------"<<endl; 
                     Anlyze_Prog();
//blingblingtt();
      cout<<"----------------------..."<<endl;
}
