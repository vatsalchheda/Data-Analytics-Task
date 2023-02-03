# FETCH REWARDS DATA ANALYTICS TASK

## <B> TASK 1: Review Existing Data and Diagram a New Structured Relational Data Model </B>

![alt text](https://github.com/vatsalchheda/FetchRewards-DataAnalytics/blob/main/Relational%20Model.png)

## <B> Task 2: Write a query that directly answers question(s) from a business stakeholder </B>

### 1. Which brand saw the most dollars spent in the month of June?

```
SELECT B.NAME
FROM Brands B JOIN Receipt_Items Ri ON (B.BARCODE = Ri.BARCODE) JOIN Receipts as R ON (Ri.Reward_Reciept_Id = R.ID)
WHERE MONTH(R.Purchase_Date) = 6
GROUP BY B.NAME
ORDER BY SUM(Ri.Total_Final_Price)
LIMIT 1

```

### 2. Which user spent the most money in the month of August?

```
SELECT u.ID
FROM USERS u JOIN RECIEPTS R r ON (u.ID=r.USER_ID)
WHERE MONTH(R.Purchase_Date) = 8
GROUP BY u.ID
ORDER BY SUM(r.TOTAL_SPENT) DESC
LIMIT 1
```

### 3. What user bought the most expensive item?

```
SELECT u.ID
FROM USERS u JOIN RECIEPTS r ON (u.ID=r.USER_ID) JOIN RECIEPT_ITEMS ri ON (r.ID=ri.REWARDS_RECEIPT_ID)
ORDER BY CAST((ri.TOTAL_SPENT/ri.QTY) as DECIMAL(7,2))
LIMIT 1
```

### 4. What is the name of the most expensive item purchased?

```
SELEC ri.DESCRIPTION
FROM reciept_items ri
ORDER BY CAST((ri.TOTAL_SPENT/ri.QTY) as DECIMAL(7,2)) DESC
LIMIT 1
```

### 5. How many users scanned in each month?

```
SELECT MONTH(r.PURCHASE_DATE), COUNT(r.USER_ID)
FROM reciepts r
GROUP BY MONTH(r.PURCHASE_DATE)
```

## Task 3: Choose something noteworthy about the data and share with a non-technical stakeholder

### FINDINGS

#### 1.

#### 2.
