You are given a string s and an array of strings words. All the strings of words are of the same length.

A concatenated string is a string that exactly contains all the strings of any permutation of words concatenated.

For example, if words = ["ab","cd","ef"], then "abcdef", "abefcd", "cdabef", "cdefab", "efabcd", and "efcdab" are all concatenated strings. "acdbef" is not a concatenated string because it is not the concatenation of any permutation of words.
Return an array of the starting indices of all the concatenated substrings in s. You can return the answer in any order.

############################

func findSubstring(s string, words []string) []int {
    result := []int{}
    if len(words) == 0 {
        return result
    }

    wordLen := len(words[0])
    wordMap := map[string]int{}

    for _, w := range words {
        _, ok := wordMap[w]
        if ok {
            wordMap[w]++
            continue
        }
        wordMap[w] = 1
    }

    for i:=0; i<len(s); i++ {
        wordsUsed := map[string]int{}
        wordsUsedLen := 0

        checkingPos := i
        for {
            if wordsUsedLen == len(words) {
                result = append(result, i)
                break
            }
            if (checkingPos + wordLen) > len(s) {
                break
            }

            currentWord := s[checkingPos:checkingPos + wordLen]
            
            times, ok := wordMap[currentWord]
            if !ok {
                break
            } 
            timesUsed, used := wordsUsed[currentWord]
            if used && timesUsed+1 > times {
                break
            }

            if used {
                wordsUsed[currentWord]++
            } else {
                wordsUsed[currentWord] = 1
            }

            wordsUsedLen++
            checkingPos = checkingPos + wordLen
        }
    }

    return result
}
