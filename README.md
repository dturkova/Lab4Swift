1. На основі поданого нижче коду знайти потенційні проблеми.
2. Запустити приклад в середовищі Swift та проаналізувати його
роботу.
3. За допомогою інструментів по роботі з багатопоточністю на мові
Swift усунути знайдені проблеми. Перелік інструментів (приклад
повинен бути виправлений кожним із них почергово)
a. Dispatch Queue
b. Operation Queue
c. Semaphore (mutex, lock)

import Foundation

let concurrentQueue = DispatchQueue(label: "com.example.concurrentQueue", attributes: .concurrent)

var accountBalance = 1000

func withdraw(amount: Int) {

    concurrentQueue.async {

        if accountBalance >= amount {

            // Simulate delay for demonstration purposes
            Thread.sleep(forTimeInterval: 1)

            accountBalance -= amount

            print("Withdrawal successful. Remaining balance: \(accountBalance)")

        } else {
            print("Insufficient funds")
        }
    }
}

func refillBalance(amount: Int) {
    concurrentQueue.async {
        // Simulate delay for demonstration purposes
        Thread.sleep(forTimeInterval: 1)

        accountBalance += amount

        print("Refill successful. Remaining balance: \(accountBalance)")
    }
}

// Simulate multiple withdrawals happening concurrently
for _ in 1...5 {

    withdraw(amount: 150)
    refillBalance(amount: 200)
}
