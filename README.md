# Assignment-2-DAX
  Adding new tables,columns and measures in powerBI using DAX.

# 1 New tables

>A new table named "updated orders table" is created using "addcolumns" fuction so that this new table
contains all the columns of the existing "orders" table and 2 new created columns named "profit margin" 
and "sales category".
the DAX expression is:

updated order table = ADDCOLUMNS(Orders,"Profit margin",DIVIDE(Orders[Profit],Orders[Sales],0),"Sales category",IF(Orders[Sales]>400,"HIGH VALUE","LOW VALUE"))

>Another table named "discounted sales" is created using the "selectcolumns" fuction so that this new table
consists of individual columns from the chosen "orders" table and one new mathematically created 
"profit percentage" column.
the DAX expression is:

discounted sales = SELECTCOLUMNS(Orders,"Order id",Orders[Order ID],"sales",Orders[Sales],
"profit of orders",Orders[Profit],"discounted sales",Orders[Sales]*(1-Orders[Discount]))

>Both the above mentioned functions are combined and used to create the third column "profit summary table" 
where the individual columns from "orders" table are selected along with new mathematically created
 "profit margin" column from within the new table.
the DAX expression is:

profit summary table = ADDCOLUMNS(SELECTCOLUMNS(Orders,"Order id",Orders[Order ID],"sales",Orders[Sales],
"profit of orders",Orders[Profit]),"profit margin",DIVIDE([profit of orders],[sales],0))

# 2.New columns

>A new column named "sales categoy" is added to the independant "sales table" to classify the products into
 high valued and low valued according to their sales value and discount.
the DAX expression is:

salescategory = IF(AND('Orders'[Sales]>400,'Orders'[Discount]>0.2),"high value","low value")


>Another column named "days to ship" is added to the "order table" using the function "datediff" to 
calculate the number of days between order date and shipping date
the DAX expression is:


days to ship = DATEDIFF(Orders[Order Date],Orders[Ship Date],DAY)

>2 new columns to find the year of order and quarter of that year named "order year" and "order year
quarter" is added to the "ORDER  table" using the "year" and "quarter" functions respectively.
the DAX expression is:

Order year = YEAR(Orders[Order Date])

Order year quarter = QUARTER(Orders[Order Date])

>A column for calculating the sum of sales yet to date is created in "sales" table named "salesYTD"
 using "totalytd" function.
the DAXexpression is:

sales YTD = TOTALYTD(SUM(Orders[Sales]),Orders[Order Date])

>Another column for finding the rounded value of profit margin is created named "rounded profit margin" 
by using "round" function
the DAX expression is:

rounded profit margin = ROUND(DIVIDE(Orders[Profit],Orders[Sales],0),2)

# 3 New measure

>A new measure "total discount" is created to the "updated orders table" to calculate the sum of products 
of sales with its corresponding discount. the function "sumx" is used here.
the DAX expression is:

total discount = SUMX(Orders,Orders[Profit]*(1-Orders[Discount]))

>Another measure called "sales std_dev" is created to the "updated order table" to calculate the standard 
deviation of sales using "stdev.p" function.
the DAX expresson is:

sales std_dev = STDEV.P(Orders[Sales])

the measures created are visualized in the model view with the use of cards.



