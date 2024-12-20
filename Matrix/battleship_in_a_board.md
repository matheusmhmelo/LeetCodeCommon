Given an m x n matrix board where each cell is a battleship 'X' or empty '.', return the number of the battleships on board.

Battleships can only be placed horizontally or vertically on board. In other words, they can only be made of the shape 1 x k (1 row, k columns) or k x 1 (k rows, 1 column), where k can be of any size. At least one horizontal or vertical cell separates between two battleships (i.e., there are no adjacent battleships).

Example 1:

Input: board = [["X",".",".","X"],[".",".",".","X"],[".",".",".","X"]]
Output: 2

Example 2:

Input: board = [["."]]
Output: 0

#################################

func countBattleships(board [][]byte) int {
    count := 0
    for x, line := range board {
        for y := range line {
            if board[x][y] == 'X' {
                count++
                dfs(board, x, y)
            }     
        }
    }

    return count
}

func dfs(board [][]byte, x, y int) {
    if x < 0 || x >= len(board){
        return
    }
    if y < 0 || y >= len(board[x]){
        return
    }
    if board[x][y] != 'X' {
        return
    } 
    board[x][y] = '.'

    dfs(board, x-1, y)
    dfs(board, x+1, y)
    dfs(board, x, y-1)
    dfs(board, x, y+1)
}
