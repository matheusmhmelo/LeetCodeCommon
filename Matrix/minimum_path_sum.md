Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example 1:

Input: grid = [[1,3,1],[1,5,1],[4,2,1]]
Output: 7
Explanation: Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.

Example 2:

Input: grid = [[1,2,3],[4,5,6]]
Output: 12

#######################################

func minPathSum(grid [][]int) int {
    for x := range grid {
        for y := range grid[x] {
            if x - 1 >= 0 && y - 1 >= 0 {
                up := grid[x-1][y]
                left := grid[x][y-1]

                grid[x][y] += min(left, up)
            } else if x - 1 >= 0 {
                grid[x][y] += grid[x-1][y]
            } else if y - 1 >= 0 {
                grid[x][y] += grid[x][y-1]
            }
        }
    }

    return grid[len(grid)-1][len(grid[0])-1]
}
