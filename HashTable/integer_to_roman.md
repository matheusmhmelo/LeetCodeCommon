Seven different symbols represent Roman numerals with the following values:

Symbol	Value
I	1
V	5
X	10
L	50
C	100
D	500
M	1000
Roman numerals are formed by appending the conversions of decimal place values from highest to lowest. Converting a decimal place value into a Roman numeral has the following rules:

If the value does not start with 4 or 9, select the symbol of the maximal value that can be subtracted from the input, append that symbol to the result, subtract its value, and convert the remainder to a Roman numeral.
If the value starts with 4 or 9 use the subtractive form representing one symbol subtracted from the following symbol, for example, 4 is 1 (I) less than 5 (V): IV and 9 is 1 (I) less than 10 (X): IX. Only the following subtractive forms are used: 4 (IV), 9 (IX), 40 (XL), 90 (XC), 400 (CD) and 900 (CM).
Only powers of 10 (I, X, C, M) can be appended consecutively at most 3 times to represent multiples of 10. You cannot append 5 (V), 50 (L), or 500 (D) multiple times. If you need to append a symbol 4 times use the subtractive form.
Given an integer, convert it to a Roman numeral.

##############################

func intToRoman(num int) string {
    roman := getRoman(num, "")
    return roman
}

func getRoman(num int, roman string) string {
    if num == 0 {
        return roman
    }

    if num - 1000 >= 0 {
        return getRoman(num-1000, roman+"M")
    }
    if num - 900 >= 0 {
        return getRoman(num-900, roman+"CM")
    }
    if num - 500 >= 0 {
        return getRoman(num-500, roman+"D")
    }
    if num - 400 >= 0 {
        return getRoman(num-400, roman+"CM")
    }
    if num - 100 >= 0 {
        return getRoman(num-100, roman+"C")
    }
    if num - 90 >= 0 {
        return getRoman(num-90, roman+"XC")
    }
    if num - 50 >= 0 {
        return getRoman(num-50, roman+"L")
    }
    if num - 40 >= 0 {
        return getRoman(num-40, roman+"XL")
    }
    if num - 10 >= 0 {
        return getRoman(num-10, roman+"X")
    }
    if num - 9 >= 0 {
        return getRoman(num-9, roman+"IX")
    }
    if num - 5 >= 0 {
        return getRoman(num-5, roman+"V")
    }
    if num - 4 >= 0 {
        return getRoman(num-4, roman+"IV")
    }
    if num - 1 >= 0 {
        return getRoman(num-1, roman+"I")
    }
    return ""
}
