# Table

## Utility
Some programs don't work well if we just copy paste a block of spreadsheet cells as their input.
This script converts two dimensional spreasheet cells into one dimensional list with a line holds only one cell each.

## Usage

We may directly run this script as an executable in Unix-like systems or pass it to python interpreter.
Run `table help` to get the list of available options.

This script operates on a concept of "table" and "list" with a text as the value contained within those.

- **Table**
> The format of table is each columns is separated by tab (`\t`) and each rows is separated by newline (`\n`).
> Each intersection of row and column is called cell that holds the value.
> The concept is similar to spreadsheet, and if we copy a block of cells from a spreadsheet editor into a text editor we'll notice this format describes the text that would get displayed on the text editor.
>
> ```
> value \t hello \t world \n
> 12345 \t 6 \t 7 \n
> ```
>
> The text above represents this table:
>
> ```
> +-------+-------+-------+
> | value | hello | world |
> +-------+-------+-------+
> | 12345 | 6     | 7     |
> +-------+-------+-------+
> ```

- **List**
> When we convert a table into a list there are some adjustments going to be made.
> 
> Take the previous table and convert it to list.
> - We always put the top-left-most cell (0,0) to the first line.
> - We choose either column-wise orientation or row-wise orientation.
> - If we hit the last cell of a row/column we add an empty line in the list then continue.
> - Each block separated by this empty line is called *batch* and corrensponds to either a whole row or column depending on the orientation.
>
> **Column-wise orientation**, continues to the right then bottom, batch is a whole row.
> ```
> value 
> hello
> world
>       ___
> 12345   |
> 6       | a batch (corresponds to the second row)
> 7     __|
> ```
>
> **Row-wise orientation**, continues to the bottom then right, batch is a whole column.
> ```
> value
> 12345
>       ___
> hello   | a batch
> 6     __| (corresponds to the second column)
>
> world
> 7
> ```
>
> If we convert a list into table we also have to specify the orientation.
> If we specify the same orientation as when we convert it from a table, the final table's cells would map to the previous table's cells perfectly.
>
> If we take the previous table and convert it to list column-wise and convert the list to table row-wise, we would get this.
> ```
> +-------+-------+
> | value | 12345 |
> +-------+-------+
> | hello | 6     |
> +-------+-------+
> | world | 7     |
> +-------+-------+
> ```

## Current Issues
- This script does not have a way to use pipe.
- This script cannot work with tables that have an empty cell.
> Empty cells are converted into empty lines in list, the problem is empty lines are used to separate batches with one another.
> If you get an error that a batch is not symmetrical with each other when converting into table, either the list doesn't correspond to valid table or the list have an empty cell which may resulted from converting a table with empty cell to a list.
