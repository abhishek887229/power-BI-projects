# widely Used DAX functions 

* CALCULATE: Evaluates an expression in a modified filter context.
>> syntex ``` calculate(<expression>,filter1,filter2)```
>>>example:- let we have sales[sales Amount], sales[Region],sales[year]
>>>we want max sales where region is india and year is 2014 then we canuse calculate
>>>it is similar to sQl's where

>>>example :- ```calculate(max(sales[sales_amount]),sales[Region]="india",sales[year]=2014)```

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
* RANKX --> ranks item based on he values in one or more expressions
>> syntex -->```RANKX(<table>, <expression>[, <value>[, <order>[, <ties>]]])```
>>> let say we have table `Sales` with Column `Salesperson` and `TotalSales` and our task is to rank salesperson baesed on `TotalSales`

>>> ```sales_rank=RANKX(ALL(Sales[Salesperson]), Sum(sales[totalSales]),,DESC,Dense)```
>>> example 2 --> ```rank_sales = RANKX(financials,financials[ Sales])```
* financials --> table from where we want to rank
* financials[sales] --> this is individual column we want to rank, it couls be expression as well with SUM(),AVERAGE().


___
* allselect --> all select remove all `filters` from `visual level` but not from `slicer level` if you apply slicer the filter will apply over it.
>> syntex -->ALLSELECTED([TableNameOrColumnName], [ColumnName1], ...)

___
* all --> it is basic all function remove all the filters from `slicers` or `visuals` give the exact value (remove any filter)
>> syntex --> ```ALL([TableNameOrColumnName], [ColumnName1], ...)```

>>>eg data=calculate(all(sales))

___
* ALLEXCEPT --> this work as above function but it remove all filters except the filter passed to it.
>>syntex --> ALLEXCEPT(TableName, ColumnName1, ...)

>> eg -->ALLEXCEPT(financials,financials[Country])
* remove all filter except filter on country column.
___ 
