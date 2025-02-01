<details>
<summary>
  Sales and Budget in separate columns and Unpivot
</summary>

# Sales and Budget in separate columns and Unpivot
  
Have you ever received an excel file like the one below with two columns, one for actuals and another
for budget sales figures and you have to build the fact table with only one column for the amount and
one column for the scenario?

![figure1](https://github.com/user-attachments/assets/4730e09d-0b9b-41fa-a4f3-7b435fc9ebf8)

## The Bad way

If you are not sure how to handle this task, one way that I've seen people do is to duplicate the table
and select one where they keep the Sales actuals column and delete the Budget column, then add the Scenario
column and giving it a number, 1 for Actuals; and for the second table the opposite, delete the Sales actuals
column and keep the Budget column, add the Scenario column with a value of 2, and then appending both queries
afterwards to form the final Sales table.

>[!WARNING]
>This procedure could be very expensive if you have a Sales table with millions of records.


The DAX measures would then look like as follows:

Sales Actual = 
  CALCULATE(
    SUM( 'Sales table'[Amount] ),
    Sales table[Scenario] = 1
  )

Sales Budget =
  CALCULATE(
    SUM( 'Sales table'[Amount] ),
    Sales table[Scenario] = 2
  )


## The Good way

But the right way to handle this transformation is with the magic of Unpivot. 

https://learn.microsoft.com/en-us/power-query/unpivot-column

You just have to select the Sales actual and Sales Budget columns, right click and select Unpivot.

![figure1](https://github.com/user-attachments/assets/f120689f-4cc2-488e-a16b-9c0d2f99ee9f)

![figure1](https://github.com/user-attachments/assets/87a97ae3-7c11-481c-8eb3-4f907d5878b3)

After doing this the DAX formulas would be the same, but the process would have been much more efficient!

Here's the final report.

https://app.powerbi.com/view?r=eyJrIjoiOGJlNDE0YzQtMGE0Mi00Njc4LTk2MWEtMmQ3YzYwNGQxNzEyIiwidCI6ImFkODI0NDg1LWU0YzMtNGYzNS1iY2RjLTM4ZmY0OTlmNDQyYiJ9

</details>
