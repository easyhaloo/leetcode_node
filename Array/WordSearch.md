
- ### 代码

```java

package interview.array;
	
	public class WordSearch {
	
	
	    public static void main(String[] args){
	        char[][] board = new char[][]{
	                {'A','B','C','E'},
	        {'S','F','C','S'},
	            {'A','D','E','E'}
	        };
	        String word = "ABCB";
	        System.out.println(exist(board,word));
	    }
	
	
	
	    public static boolean exist(char[][] board,String word){
	        boolean[][] visited = new boolean[board.length][board[0].length];
	        for(int i=0;i<board.length;i++){
	            for(int j=0;j<board[0].length;j++){
	                if(board[i][j] == word.charAt(0) && search(board,i,j,word,0,visited)){
	                    return true;
	                }
	            }
	        }
	        return false;
	    }
	
	
	    private static boolean search(char[][] board,int i,int j,String word,int index,boolean[][] visited){
	        if(index == word.length()) return true;
	        if(i >= board.length || i< 0 || j>= board[0].length || j< 0 || board[i][j] != word.charAt(index) || visited[i][j]){
	            return false;
	        }
	        visited[i][j] = true;
	        boolean res = search(board,i+1,j,word,index+1,visited)
	                ||search(board,i,j+1,word,index+1,visited)
	                ||search(board,i-1,j,word,index+1,visited)
	                ||search(board,i,j-1,word,index+1,visited);
	        visited[i][j] = false;
	        return res;
	    }
	
	
	    private static boolean search(char[][] board,int i,int j,String word,int index){
	        if(index == word.length()) return true;
	        if(i >= board.length || i< 0 || j>= board[0].length || j< 0 || board[i][j] != word.charAt(index) ){
	            return false;
	        }
	        char c  = board[i][j];
	        board[i][j] = '#';
	
	        boolean res = search(board,i+1,j,word,index+1)
	                ||search(board,i,j+1,word,index+1)
	                ||search(board,i-1,j,word,index+1)
	                ||search(board,i,j-1,word,index+1);
	        board[i][j] = c;
	        return res;
	    }
	}
	

```