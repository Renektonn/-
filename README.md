#include <iostream>
#include <vector>
#include <stack>

using namespace std;

// 運算子優先序 (先乘除後加減 有括號先算括號)
int priority(char cha){ //c++沒有return居然不會報錯? 
	if(cha=='*' || cha=='/'){
		return 3;
	}
	else
		if(cha=='+' || cha=='-'){
			return 2;
		}
		else
			if(cha=='('){
				return 1;
			}	
	return 0;
}
//遇右括號輸出堆疊中的運算子至左括號
void backBracket(stack <char> &sta , vector <char> &ans){
    
	while(sta.top() != '('){
        ans.push_back( sta.top() );
        sta.pop();
    }
      
    sta.pop(); //the last is '('
}

void operators(char cha , stack <char> &sta , vector <char> &ans){
	
	if(sta.top()==NULL){ 
        
        sta.push(cha);
        
    }
    else
        //以下大的小的皆指運算子的優先序
        //運算子在堆疊中只能大的壓小的
		if(priority(cha) >= priority(sta.top())){
		    
        	sta.push(cha);
        	
		}
		//如遇(小的)想壓(大的) 只好輸出所有大於(小的) 讓(小的)去壓(更小的)
		else{ 
			while(sta.top()!=NULL && 
			priority(cha) < priority( sta.top() ) ){
       			ans.push_back(sta.top());
       			sta.pop();
        	}
        	sta.push(cha);
		}
		
    
    
}
//中序式轉後敘式
string infixToPostfix(string str){
  vector <char> ans;
  stack <char> sta;
  sta.push(NULL); //c++的null為NULL //還沒報錯 
  
  
  for(int i=0;i<str.length();i++){
	switch(str.at(i)){
      //優先序最小 直接推入堆疊
	  case '(' :
        sta.push( str.at(i) );
      break;
      
      case '+' :
      case '-' :
      case '*' :
      case '/' :
		  operators(str.at(i) , sta , ans);
      break;
      //運算元直接輸出
      case '0' :
      case '1' :
      case '2' :
      case '3' :
      case '4' :
      case '5' :
      case '6' :
      case '7' :
      case '8' :
      case '9' :
      	ans.push_back( str.at(i) );
      break;
      
      case ')':
      	backBracket(sta,ans);
      break;
    }
    
  }
  
  while(sta.top()!=NULL){
  	ans.push_back(sta.top());
  	sta.pop();
  }
  
  string result(ans.begin(), ans.end());//vector <char> to string
  return result;
}

int calculate(int a , int b , char op){
	switch(op){
		case '+' : return b+a;
		case '-' : return b-a;
		case '*' : return b*a;
		case '/' : return b/a;
	}
}

//後敘式運算
void postfixCalculate(string str){
  stack  <int> sta;
  
  for(int i=0;i<str.length();i++){
    int a,b;
    switch( str.at(i) ){
      //遇運算元直接推入堆疊
      case '0':
      case '1':
      case '2':
      case '3':
      case '4':
      case '5':
      case '6':
      case '7':
      case '8':
      case '9':
        sta.push( str.at(i) - '0');
      break;
      //遇運算子 推出堆疊上方兩個運算元做運算    
      case '+' :
      case '-' :
      case '*' :
      case '/' :
        a=sta.top();
        sta.pop();
        b=sta.top();
        sta.pop();
        sta.push( calculate(a , b , str.at(i) ) );
	  break;	        
    }
  }
  cout<<sta.top();
}

int main(){
	string str=infixToPostfix("1+2*3");
	postfixCalculate(str);
}
