# RFM-Saved-Search <br>
![alt text](https://img.shields.io/github/last-commit/myatviz/RFM-Saved-Search)  ![alt text](https://img.shields.io/github/repo-size/myatviz/RFM-Saved-Search) <br><br>
**What is RFM?** 👀 <br> 

RFM segmentation allows marketers to target specific clusters of customers with communications that are much more relevant for their particular behavior.

![alt text](https://i.imgur.com/p6mmpcg.png)
Reports > Saved Searches > All Saved Searches > New

**Search Title = RFM Analysis** 

**Criteria** : Type = Invoice , Tax Line = false , Main Line = false

![alt text](https://i.imgur.com/FdMtYEc.png)

**Results:** <br><br>
Sort by = Amount <br><br>
![alt text](https://i.imgur.com/Nv1JuCC.png)
<br><br>

Field : Name , Summary Type = Group By , Label = Customer Name <br>

Field : Formula(Percent) , Summary Type = Sum , 
`PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC)`
, Label = %Recency
<br><br>
Field : Formula(Percent) , Summary Type = Sum , 
`PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)`
, Label = %Frequency
<br><br>
Field : Formula(Percent) , Summary Type = Sum , 
`PERCENT_RANK() OVER(ORDER BY SUM({amount}) ASC)`
, Label = %Monetary
<br><br>
Field : Formula(Text) , Summary Type = Maximum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)  BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END || CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END || CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = RFM
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)  BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = R
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({internalid}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = F
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`CASE WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.0 and 0.2 THEN 1 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.2 and 0.4 THEN 2 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.4 and 0.6 THEN 3 WHEN PERCENT_RANK() OVER(ORDER BY SUM({Amount}) ASC) BETWEEN 0.6 and 0.8 THEN 4 ELSE 5 END`
, Label = M
<br><br>
Field : Formula(Numeric) , Summary Type = Sum , 
`ROUND({today}-MAX({trandate}))`
, Label = Days from Last Purchased
<br><br>
Field : Document Number , Summary Type = Count , Label = Orders
<br><br>
Field : Amount , Summary Type = Sum , Label = Amount
<br><br>
###Remark
> I used 555 RFM value is the best instead of 111 RFM value. 

Thanks 🦄
