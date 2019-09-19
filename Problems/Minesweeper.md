# 529. Minesweeper

## 思路
扫雷，思路也很直球，直接深搜就可以，但感觉自己代码写的又臭又长，下次得优化下代码的写法。。。

## 代码

```Java
class Solution {
    public char[][] updateBoard(char[][] board, int[] click) {
        int row = click[0];
        int col = click[1];
        int m = board.length;
        int n = board[0].length;
        int[][] neighbor = new int[m][n];
        for(int i = 0; i < m; i ++){
            for(int j = 0; j < n; j++){
                neighbor[i][j] = check(board, i-1, j-1) + check(board, i-1, j) + check(board, i-1, j+1) + check(board, i, j-1) + check(board, i+1, j+1) + check(board, i, j+1) + check(board, i+1, j-1) + check(board, i+1, j);
            }
        }
        if(board[row][col] == 'M'){
            board[row][col] = 'X';
            return board;
        }
        if(board[row][col] == 'E'){
            if(neighbor[row][col] > 0){
                board[row][col] = (char)('0' + neighbor[row][col]);
            }else{
                reveal(board, neighbor, row, col);
            }
        }
        return board;
    }
    
    public int check(char[][] board, int i, int j){
        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length)return 0;
        if(board[i][j] == 'M')return 1;
        return 0;
    }
    
    public void reveal(char[][] board, int[][] neighbor, int i, int j){
        if(i < 0 || j < 0 || i >= board.length || j >= board[0].length)return;
        if(neighbor[i][j] > 0){
            board[i][j] = (char)('0' + neighbor[i][j]);
            return;
        }else{
            if(board[i][j] =='B')return;
            board[i][j] = 'B';
            reveal(board, neighbor, i-1, j);
            reveal(board, neighbor, i-1, j+1);
            reveal(board, neighbor, i-1, j-1);
            reveal(board, neighbor, i, j+1);
            reveal(board, neighbor, i, j-1);
            reveal(board, neighbor, i+1, j+1);
            reveal(board, neighbor, i+1, j);
            reveal(board, neighbor, i+1, j-1);
        }
        return;
    }
}
```