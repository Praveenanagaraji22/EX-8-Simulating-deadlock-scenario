# EX 8: Simulating deadlock scenario
## Date: 21/9/23 
## AIM: 
To simulate a scenario of deadlock in concurrent execution of transactions.
## PROCEDURE:
1. Create a accounts table with the schema Accounts (account_id INT PRIMARY KEY,balance DECIMAL(10, 2)) and insert the values then create a transaction T1 and T2
2. T1 updates the balance by debiting 200 and simulate a delay and make T2 interferes T1
3. T2 updates balance by debiting 150 and simulate a delay and make T1 inteferes T2
4. Simulate a delay and make T1 inteferes T2
## QUERY
```sql
CREATE TABLE Accounts (account_id INT PRIMARY KEY,balance DECIMAL(10, 2));
INSERT INTO Accounts VALUES(1, 1000.00);
INSERT INTO Accounts VALUES(2, 2500.00);
```
## OUTPUT 
![image](https://github.com/dineshgl/EX-8-Simulating-deadlock-scenario/assets/143793356/2f35d3f2-474d-4366-ade6-d0a151da1d2c)
## Transaction T1
```sql
BEGIN TRANSACTION;
UPDATE Accounts
SET balance = balance - 200.00
WHERE account_id = 1;
WAITFOR DELAY '00:00:10'; -- This line introduces a delay
UPDATE Accounts
SET balance = balance + 200.00
WHERE account_id = 2;
COMMIT;
```
## Transaction T2
```sql
BEGIN TRANSACTION;
UPDATE Accounts
SET balance = balance - 150.00
WHERE account_id = 2;
WAITFOR DELAY '00:00:10'; -- This line introduces a delay
UPDATE Accounts
SET balance = balance + 150.00
WHERE account_id = 1;
COMMIT;
```
## OUTPUT:
```sql
Msg 1205, Level 13, State 51, Line 3
Transaction (Process ID) was deadlocked
on resourceswith anotherprocess and has been
chosen as the deadlock victim. Rerun the transaction.
```
## RESULT: 
Thus the program for the simulation of deadlock has been executed successfully.
