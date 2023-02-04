# FETCH REWARDS DATA ANALYTICS TASK

## <B> TASK 1: Review Existing Data and Diagram a New Structured Relational Data Model </B>

![alt text](https://github.com/vatsalchheda/FetchRewards-DataAnalytics/blob/main/Relational%20Model.png)

## <B> Task 2: Write a query that directly answers question(s) from a business stakeholder </B>

### 1. Which brand saw the most dollars spent in the month of June?

```
SELECT B.NAME
FROM brands B JOIN receipt_items Ri ON (B.BARCODE = Ri.BARCODE) JOIN receipts as R ON (Ri.REWARDS_RECEIPT_ID = R.ID)
WHERE MONTH(R.PURCHASE_DATE) = 6
GROUP BY B.NAME
ORDER BY SUM(Ri.TOTAL_FINAL_PRICE) DESC
LIMIT 1;

```

### 2. Which user spent the most money in the month of August?

```
SELECT u.ID
FROM users u JOIN receipts r ON (u.ID=r.USER_ID)
WHERE MONTH(R.PURCHASE_DATE) = 8
GROUP BY u.ID
ORDER BY SUM(r.TOTAL_SPENT) DESC
LIMIT 1;
```

### 3. What user bought the most expensive item?

```
SELECT u.ID
FROM users u JOIN receipts r ON (u.ID=r.USER_ID) JOIN receipt_items ri ON (r.ID=ri.REWARDS_RECEIPT_ID)
ORDER BY ri.TOTAL_FINAL_PRICE/ri.QUANTITY_PURCHASED DESC
LIMIT 1
```

### 4. What is the name of the most expensive item purchased?

```
SELECT ri.DESCRIPTION 
FROM receipt_items ri 
ORDER BY ri.TOTAL_FINAL_PRICE/ri.QUANTITY_PURCHASED DESC 
LIMIT 1;
```

### 5. How many users scanned in each month?

```
SELECT MONTH(r.DATE_SCANNED), COUNT( DISTINCT r.USER_ID) 
FROM receipts r 
GROUP BY MONTH(r.DATE_SCANNED);
```

## Task 3: Choose something noteworthy about the data and share with a non-technical stakeholder

### FINDINGS: To gain insights from the dataset, I utilized Tableau to create an interactive dashboard after removing all the null values. By doing this, I was able to uncover several interesting correlations:


#### 1. The "Category Type Receipt Count for Different Months" sheet, which uses a packed bubbles chart, displays the count of each category type for a selected month. By selecting all months, it becomes evident that the Beverages category consistently leads in terms of receipt count, while the Beauty & Personal Care category has the lowest number of receipts. This can be clearly seen through the color gradient, where dark blue represents the highest number of receipt counts, and the color gradually changes to light blue for the categories with the lowest number of receipt counts.


#### 2. The "States vs Users" map in the interactive dashboard provides insight into which state in the USA has the highest and lowest number of users for the selected month. The month can be easily changed to fit the needs of the analysis. Through the color gradient, which ranges from dark blue (representing the highest number of users) to light blue (representing the lowest number of users), we can see that the state of Florida has the largest number of users, closely followed by New York. On the other hand, states such as Washington, Nevada, and North Dakota have the least number of users.

![Tableau Dashboard](https://github.com/vatsalchheda/FetchRewards-DataAnalytics/blob/main/Findings.jpg)
