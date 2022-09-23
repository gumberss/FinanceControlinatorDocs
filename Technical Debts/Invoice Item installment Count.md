## What
It is not able to return the installment count in the [[Invoices Overview]], this is because the installment count is not setted in the invoce item, only in the expense.


<img src="https://user-images.githubusercontent.com/38296002/170798818-a015f654-f07f-44c1-b376-eda5c3142c29.png"/> 
## How to solve

When a invoice item is created, set the installment number and the installment count (new property) to know how much installments this item has.

Of course, when a expense is updated, need to update each item if the installment count change

