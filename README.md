#include <iostream>
#include <stack>
#include <vector>
using namespace std;

int main() {
  string str="(1+2)*(3+4)";
  stack  <int> sta;
  vector <int> ans;

  for(int i=0;i<str.length();i++){
    switch(str.at(i)){
      case '(' :
        sta.push( str.at(i) );
      break;
      case '+' :
      case '-' :
        if(sizeof(sta) == 0){
          sta.push( str.at(i) );
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
        
        int n=ans.size()-1;
        while(sta.top() != '('){
          ans.push_back( sta.top() );
          sta.pop();
        }
      
        sta.pop();

      break;
    }
    

  }

  return 0;

}
