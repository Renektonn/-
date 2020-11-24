#include <iostream>
#include <vector>
#include <stack>

using namespace std;

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
    else//堆疊中運算子優先順序若大於等於讀入的運算子優先順序的話，直接輸出堆疊中的運算子，再將讀入的運算子置入堆疊
        
		if(priority(cha) >= priority(sta.top())){ //運算子在堆疊中只能優先序大的壓優先序小的
        	ans.push_back(cha);
		}
		else{
			while(sta.top()!='null' && priority(cha) < priority(sta.top())){
       			ans.push_back(sta.top());
       			sta.pop();
        	}
        	sta.push(cha);
		}
		
    
    
}

string infixToPostfix(string str){
  
  vector <char> ans;
  stack <char> sta;
  sta.push(NULL); //c++的null為NULL //還沒報錯 
  cout<<sta.top();
  
  
  for(int i=0;i<str.length();i++){
	switch(str.at(i)){
      
	  case '(' :
        sta.push( str.at(i) );
      break;
      
      case '+' :
      case '-' :
      case '*' :
      case '/' :
		  operators(str.at(i) , sta , ans);
      break;
      
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
int main(){
	string str=infixToPostfix("1+2*3");
	//cout<<str;
}
