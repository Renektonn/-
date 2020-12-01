//中序式轉後敘式
import java.util.Scanner;
import java.util.ArrayList;
import java.util.Stack;
public class infixToPostfix {
	// 運算子優先序 (先乘除後加減 有括號先算括號)
	static int priority(char cha){ //c++沒有return居然不會報錯? 
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
	static void backBracket(Stack <Character> sta , ArrayList <Character> ans){
	    
		while(sta.peek() != '('){
			ans.add( sta.peek() );
			sta.pop();
		}
			      
		sta.pop(); //the last is '('
	}
	
	static void operators(char cha , Stack <Character> sta , ArrayList <Character> ans){
		
		if(sta.peek()==null){ 
	        
	        sta.push(cha);
	        
	    }
	    else
	        //以下大的小的皆指運算子的優先序
	        //運算子在堆疊中只能大的壓小的
			if(priority(cha) >= priority(sta.peek())){
			    
	        	sta.push(cha);
	        	
			}
			//如遇(小的)想壓(大的) 只好輸出所有大於(小的) 讓(小的)去壓(更小的)
			else{ 
				while(sta.peek()!=null && 
				priority(cha) < priority( sta.peek() ) ){
	       			ans.add(sta.peek());
	       			sta.pop();
	        	}
	        	sta.push(cha);
			}
			
	}
	
	static String infixToPostfix(String str){
		ArrayList <Character> ans = new ArrayList <Character> ();
		Stack <Character> sta = new Stack <Character> ();
		sta.push(null); 
		  
		  
		for(int i=0;i<str.length();i++){
			switch(str.charAt(i)){
			    //優先序最小 直接推入堆疊
				case '(' :
					sta.push( str.charAt(i) );
			    break;
			   
			    case '+' :
			    case '-' :
			    case '*' :
			    case '/' :
			    	operators(str.charAt(i) , sta , ans);
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
			    	ans.add( str.charAt(i) );
			    break;
			      
			    case ')':
			    	backBracket(sta,ans);
			    break;
		    }
		}
		  
		  while(sta.peek()!=null){
		  	
			  ans.add(sta.pop() );
	
		  }
		  //Arraylist to String ???
		  StringBuilder sb = new StringBuilder(); 
		  // Appends characters one by one 
		  for (Character ch : ans) { 
	            sb.append(ch); 
	      } 
	      // convert in string 
	      String result = sb.toString(); 
		  return result;
	}
	
	public static void main(String[] args) {
		String str=infixToPostfix("1+2*3");
		System.out.println(str);
	}

}
