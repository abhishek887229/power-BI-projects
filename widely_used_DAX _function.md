# DAX functions topics and formulas

### calclated Column explaination 
it expands table by creating `new column`, Stores along with `tables` and `consumes memory` but have `less analytical` capability.

### measure explain 
it summarized data into `single value` and calculated at `runtime`,store in `memory on temporarily` and `Rich analyics` Capabilites.
* in measure we mostly use aggregator or Summarization functions
* try to use more measures instead direct columns
___
## filter and Row Context
#### row Context --> It Calculate Each Row while applying formula, with Value within Each row , for example doing sum of sales and cost will affect or calculated from each row of sales and cost.
>> Profit = sum(sales,[sales amount]-[cost amount])


#### filter context --> it is set of filter that applied before that table arrives for use
>> total_sales=Sum(sales[Sales Amount])
>> Applying filter from Filter pane/Visuals/Slicers (year=2017,country=India,City=Chennai)


## widely Used DAX functions 

* CALCULATE: Evaluates an expression in a modified filter context.
>> syntex ``` calculate(<expression>,filter1,filter2)```
>>>example:- let we have sales[sales Amount], sales[Region],sales[year]
>>>we want max sales where region is india and year is 2014 then we canuse calculate
>>>it is similar to sQl's `where`  

>>>example :- ```calculate(max(sales[sales_amount]),sales[Region]="india",sales[year]=2014)```
>>> we want sales from all region not only from india then we will use.
>>> sales_from_all_locations=Calculate(sum(sales),all(region))

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
* SUMX  --> When we Need to find out the Calculation Row by Row then we use SUMX
  >>sales_amount=SUMX(Sales,Sales[Unit Price]*Sales[QTY])

here is an exmaple to illustrate SUMX and SUM and how they are different.

<table border="1">
  <thead>
    <tr>
      <th>Sales</th>
      <th>Qty</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>500</td>
      <td>2</td>
    </tr>
    <tr>
      <td>400</td>
      <td>3</td>
    </tr>
    <tr>
      <td>800</td>
      <td>6</td>
    </tr>
    <tr>
      <td>785</td>
      <td>5</td>
    </tr>
  </tbody>
</table>

* Example --> Sum(sales)*sum(qty)
* explain --> sum(500+400+800+785)* sum(2+3+6+5)=39760 ` this is sum and multiplication

* eg2--> Sumx(sales*Qty)
* explain --> sumx will do following thing (500*2+400*3+800*6+785*5)=10925
* this one is correct way to get total 

