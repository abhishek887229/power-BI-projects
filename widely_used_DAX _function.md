# widely Used DAX functions 

* CALCULATE: Evaluates an expression in a modified filter context.
>> syntex ``` calculate(<expression>,filter1,filter2)```
>>>example:- let we have sales[sales Amount], sales[Region],sales[year]
>>>we want max sales where region is india and year is 2014 then we canuse calculate
>>>it is similar to sQl's where
>>>
>>>example
>>>>  ```calculate(max(sales[sales_amount]),sales[Region]="india",sales[year]=2014)```

___

* CALCULATETABLE :- return a table wih modified filtr context
>> example :- let say we want a modified tablewhere year should be less then 2024 and month shold be `jan` only so we can make a subtable from exisiting table using calculate table formula.
>>> syntext --> ```CALCULATETABLE(TABLE,FILTER1,FILTER2,FILTER3...)```
>>> example:- ```calculatetable(sales_table,sales_table[year]>2012)```
___

* SELECTCOLUMNS :-  create a new Table by selecting specific column from an existing table and optionally renaming them
>> example :- let we have `sales` table with columns `SalesAmount`,`Regions`and `Date` we want only `SalesAmount` and `Regions`.
>>> syntex --> ```SELECTCOLUMNS(<table>, <new_column_name1>, <column_expression1>, <new_column_name2>, <column_expression2>, ...)```
>>> example --> ```Table = SELECTCOLUMNS(financials,"years",financials[Year],"sales",financials[Sale Price])```

* financials --> main table from where we want to extarct columns
* "year","sales" --> name of new table
* financials[Year],financials[Sale Price] --> expression of columns from previous table, to extract them at new table
___

* allselect --> Returns all the rows in a table, or all the values in a column, ignoring any filters that might have been applied inside the query, but keeping filters that come from outside.
