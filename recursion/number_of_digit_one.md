Given an integer n, count the total number of digit 1 appearing in all non-negative integers less than or equal to n.

Example 1:

Input: n = 13
Output: 6

Example 2:

Input: n = 0
Output: 0

##########################

func countDigitOne(n int) int {
    if n <= 0 {
        return 0
    }
    

    total := 0
    rest := n/10

    for n > 0 && n/10 == rest {
        strNum := strconv.Itoa(n)
        total += strings.Count(strNum, "1")
        n--
    } 

    total += countDigitOne(n)
    return total
}
