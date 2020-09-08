#include <iostream>
#include <vector>
#include <stack>

using namespace std;

string infixToPostfix(string str , vector <int> postfix){
  stack <char> sta;
  int oper [4+1]={0};
  for(int i=0;i<str.length();i++){
    switch(str.at(i)){
      case '(' :
        sta.push( str.at(i) );
      break;
      case '+' :
      case '-' :
        if(sizeof(sta) == 0){
          sta.push( str.at(i) );
          oper[]
        }
        else{
          int n=sizeof(sta) / 4 - 1;
          while(str.at(n) == '('){
            n--;
          }
        }
      
      break;
      case '*' :
      case '/' :
        if(sizeof(sta) == 0){
          sta.push( str.at(i) );
        }
        //ans.push_back( str.at(i) );
      
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
        
        int n=sta.size()-1;
        while(sta.top() != '('){
          sta.push( sta.top() );
          sta.pop();
        }
      
        sta.pop();

      break;
    }
    

  }
  return str;
}

void postfixCalculate(string str){
  stack  <int> sta;
  for(int i=0;i<str.length();i++){
    int a,b;
    switch( str.at(i) ){
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

      case '+' :
        a=sta.top();
        sta.pop();
        b=sta.top();
        sta.pop();
        sta.push( a+b );
      break;

      case '-' :
        a=sta.top();
        sta.pop();
        b=sta.top();
        sta.pop();
        sta.push( a-b );
      break;

      case '*' :
        a=sta.top();
        sta.pop();
        b=sta.top();
        sta.pop();
        sta.push( a*b );
      break;

      case '/' :
        a=sta.top();
        sta.pop();
        b=sta.top();
        sta.pop();
        sta.push( a/b );
      break;      

    }
  }
  cout<<sta.top();
}

int main() {
  string str="(1+2)*(3+4)";
  vector <int> postfix;
  infixToPostfix(str,postfix);

  postfixCalculate(str);
  return 0;  
}
