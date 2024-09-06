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
