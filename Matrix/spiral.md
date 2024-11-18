Given an m x n matrix, return all elements of the matrix in spiral order.

Example 1:

Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]

Example 2:

Input: matrix = [[1,2,3,4],[5,6,7,8],[9,10,11,12]]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]

######################

type point struct {
    x int
    y int
}

func spiralOrder(matrix [][]int) []int {
    totalLen := len(matrix) * len(matrix[0])
    result := []int{}
    visited := map[point]bool{}

    movX, movY := getNextMovement(0, 0)
    var curX, curY int
    for len(result) < totalLen {
        result = append(result, matrix[curX][curY])
        curPoint := point{
            x: curX,
            y: curY,
        }
        nextPoint := point{
            x: curX + movX,
            y: curY + movY,
        }

        if (curX + movX < 0 || curX + 1 + movX > len(matrix)) ||
        (curY + movY < 0 || curY + 1 + movY > len(matrix[curX])) {
            movX, movY = getNextMovement(movX, movY)
        }
        if visited[nextPoint] {
            movX, movY = getNextMovement(movX, movY)
        }

        visited[curPoint] = true
        curX, curY = curX + movX, curY + movY
    }

    return result
}

func getNextMovement(x, y int) (int, int) {
    if x == 1 {
        return 0, -1
    }
    if x == -1 {
        return 0, 1
    }
    if y == 1 {
        return 1, 0
    }
    if y == -1 {
        return -1, 0
    }
    return 0, 1
}

