# RFM Analysis in Saved Search 📊

![Last Commit](https://img.shields.io/github/last-commit/myatviz/RFM-Saved-Search) ![Repo Size](https://img.shields.io/github/repo-size/myatviz/RFM-Saved-Search) 

## What's RFM? 👀

RFM segmentation helps marketers target customers more effectively. RFM stands for Recency, Frequency, and Monetary, a method that identifies valuable customers by analyzing their purchase history. It groups customers based on how recently they bought 📅, how often they buy 🔄, and how much they spend 💰.

This segmentation allows for tailored marketing strategies. For example, recent big spenders might get a "VIP customer" offer, while inactive customers could receive a "win-back" promotion.

RFM is a powerful tool for boosting customer engagement and sales. 🚀

### How to Create RFM in NetSuite Saved Search?

![Create RFM](https://i.imgur.com/p6mmpcg.png)

1. Go to **Reports > Saved Searches > All Saved Searches > New**

2. Set the **Search Title** to **RFM Analysis** 📈

3. **Criteria**:
   - Type = Invoice 💳
   - Tax Line = false ❌
   - Main Line = false ❌

![Criteria](https://i.imgur.com/FdMtYEc.png)

4. **In Results**:
   - Sort by = Amount 💰

![Sort by](https://i.imgur.com/Nv1JuCC.png)

5. Fields:
   - Field : Name , Summary Type = Group By , Label = Customer Name 🧑‍🤝‍🧑
   - Field : Formula(Percent) , Summary Type = Sum , Label = %Recency
     ```sql
     PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC)
     ```
   - Field : Formula(Percent) , Summary Type = Sum , Label = %Frequency
     ```sql
     PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC)
     ```
   - Field : Formula(Percent) , Summary Type = Sum , Label = %Monetary
     ```sql
     PERCENT_RANK() OVER (ORDER BY SUM({amount}) ASC)
     ```
   - Field : Formula(Text) , Summary Type = Maximum , Label = RFM 📊
     ```sql
     CASE 
         WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.0 AND 0.2 THEN 1 
         WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.2 AND 0.4 THEN 2 
         WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.4 AND 0.6 THEN 3 
         WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.6 AND 0.8 THEN 4 
         ELSE 5 
     END 
     ||
     CASE 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.0 AND 0.2 THEN 1 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.2 AND 0.4 THEN 2 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.4 AND 0.6 THEN 3 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.6 AND 0.8 THEN 4 
         ELSE 5 
     END 
     ||
     CASE 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.0 AND 0.2 THEN 1 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.2 AND 0.4 THEN 2 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.4 AND 0.6 THEN 3 
         WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.6 AND 0.8 THEN 4 
         ELSE 5 
     END
     ```

   - Field : Formula(Numeric) , Summary Type = Sum , Label = R
     ```sql
     CASE WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.0 and 0.2 THEN 1 
     WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.2 and 0.4 THEN 2 
     WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC)  BETWEEN 0.4 and 0.6 THEN 3 
     WHEN PERCENT_RANK() OVER (ORDER BY ROUND({today} - MAX({trandate})) DESC) BETWEEN 0.6 and 0.8 THEN 4 
     ELSE 5 
     END
     ```

   - Field : Formula(Numeric) , Summary Type = Sum , Label = F
     ```sql
     CASE WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.0 and 0.2 THEN 1 
     WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.2 and 0.4 THEN 2 
     WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.4 and 0.6 THEN 3 
     WHEN PERCENT_RANK() OVER (ORDER BY SUM({internalid}) ASC) BETWEEN 0.6 and 0.8 THEN 4 
     ELSE 5 
     END
     ```

   - Field : Formula(Numeric) , Summary Type = Sum , Label = M
     ```sql
     CASE WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.0 and 0.2 THEN 1 
     WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.2 and 0.4 THEN 2 
     WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.4 and 0.6 THEN 3 
     WHEN PERCENT_RANK() OVER (ORDER BY SUM({Amount}) ASC) BETWEEN 0.6 and 0.8 THEN 4 
     ELSE 5 
     END
     ```

   - Field : Formula(Numeric) , Summary Type = Sum , Label = Days from Last Purchased 📆
     ```sql
     ROUND({today}-MAX({trandate}))
     ```

   - Field : Document Number , Summary Type = Count , Label = Orders 📦

   - Field : Amount , Summary Type = Sum , Label = Amount 💲

### Remark 🎉

I had a blast opting for a superior RFM value of

 555 over the 111 RFM value! 🚀🌟 Have Fun! 🦄
```
