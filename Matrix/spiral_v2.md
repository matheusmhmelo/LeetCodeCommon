Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.

Example 1:

Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]

Example 2:

Input: n = 1
Output: [[1]]

####################

type point struct {
    x int
    y int
}

func generateMatrix(n int) [][]int {
    result := make([][]int, n)
    visited := map[point]bool{}

    totalLen := n * n
    count := 1

    movX, movY := getNextMovement(0, 0)
    var curX, curY int
    for count <= totalLen {
        if result[curX] == nil {
            result[curX] = make([]int, n)
        }
        result[curX][curY] = count

        curPoint := point{
            x: curX,
            y: curY,
        }
        nextPoint := point{
            x: curX + movX,
            y: curY + movY,
        }

        if (curX + movX < 0 || curX + 1 + movX > n) ||
        (curY + movY < 0 || curY + 1 + movY > n) {
            movX, movY = getNextMovement(movX, movY)
        }
        if visited[nextPoint] {
            movX, movY = getNextMovement(movX, movY)
        }

        visited[curPoint] = true
        curX, curY = curX + movX, curY + movY
        count++
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

