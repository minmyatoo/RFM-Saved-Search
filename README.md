# RFM-Saved-Search

😉 **What is RFM?** <br>
RFM segmentation allows marketers to target specific clusters of customers with communications that are much more relevant for their particular behavior

![alt text](https://i.imgur.com/p6mmpcg.png)
Reports > Saved Searches > All Saved Searches > New


Search Title = RFM Analysis 

Criteria : Type = Invoice , Tax Line = false , Main Line = false

![alt text](https://i.imgur.com/FdMtYEc.png)

Results: <br>
Sort by = Amount
![alt text](https://i.imgur.com/Nv1JuCC.png)

Field : Name , Summary Type = Group By , Label = Customer Name <br>
Field : Formula(Percent) , Summary Type = Sum , 
`PERCENT_RANK() OVER(ORDER BY ROUND({today}-MAX({trandate})) DESC)`
, Label = %Recency
