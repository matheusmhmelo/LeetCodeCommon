A transaction is possibly invalid if:

the amount exceeds $1000, or;
if it occurs within (and including) 60 minutes of another transaction with the same name in a different city.
You are given an array of strings transaction where transactions[i] consists of comma-separated values representing the name, time (in minutes), amount, and city of the transaction.

Return a list of transactions that are possibly invalid. You may return the answer in any order.

Example 1:

Input: transactions = ["alice,20,800,mtv","alice,50,100,beijing"]
Output: ["alice,20,800,mtv","alice,50,100,beijing"]
Explanation: The first transaction is invalid because the second transaction occurs within a difference of 60 minutes, have the same name and is in a different city. Similarly the second one is invalid too.

Example 2:

Input: transactions = ["alice,20,800,mtv","alice,50,1200,mtv"]
Output: ["alice,50,1200,mtv"]

Example 3:

Input: transactions = ["alice,20,800,mtv","bob,50,1200,mtv"]
Output: ["bob,50,1200,mtv"]

#########################

type transactionInfo struct {
    transaction string
    name string
    time int
    amount int
    city string
    invalid bool
}

func invalidTransactions(transactions []string) []string {
    invalid := []string{}
    pastTransactions := map[string][]*transactionInfo{}

    for _, t := range transactions {
        tInfo := getTransactionInfo(t)
        if tInfo == nil {
            invalid = append(invalid, t)
            continue
        }

        previous, ok := pastTransactions[tInfo.name]
        if ok {
            for _, tPrevious := range previous {
                if tPrevious.city != tInfo.city && (tInfo.time - tPrevious.time <= 60) && tInfo.time - tPrevious.time >= -60 {
                    tPrevious.invalid = true
                    tInfo.invalid = true
                }
            }
        }
        if tInfo.amount > 1000 {
            tInfo.invalid = true
        }
        pastTransactions[tInfo.name] = append(pastTransactions[tInfo.name], tInfo)
    }

    for _, transactionsByCity := range pastTransactions {
        for _, t := range transactionsByCity {
            if t.invalid {
                invalid = append(invalid, t.transaction)
            }
        }
    }

    return invalid
}

func getTransactionInfo(t string) *transactionInfo {
    tArr := strings.Split(t, ",")
    if len(tArr) != 4 {
        return nil
    }

    time, _ := strconv.Atoi(tArr[1])
    amount, _ := strconv.Atoi(tArr[2])
    return &transactionInfo{
        transaction: t,
        name: tArr[0],
        time: time,
        amount: amount,
        city: tArr[3],
    }
}
