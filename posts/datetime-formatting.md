# Datetime Formatting

You are likely very familiar with formating datetimes in Excel, with format strings such as "MM-DD-YYYY". 
But Python has its own format strings that are, in my opinion, less intuitive. 
So I've built the below table to help you translate between your current knowledge and Python.

For all examples below I will use the datetime `6/3/2002 01:04:09`

| Excel Format | Python Format | Example |
| -------- | -------- | -------- |
| "M" | "%-m" | 6 |
| "MM" | "%m" | 06 |
| "MMM" | "%b" | Jun |
| "MMMM" | "%B" | June |
| "D" | "%-d" | 3 |
| "DD" | "%d" | 03 |
| "DDD" | "%a" | Fri |
| "DDDD" | "%A" | Friday |
| "YY" | "%y" | 02 |
| "YYYY" | "%Y" | 2002 |
| "H" | "%-H" | 1 |
| "HH" | "%H" | 01 |
| "M" | "%-M" | 4 |
| "MM" | "%M" | 04 |
| "S" | "%-S" | 9 |
| "SS" | "%S" | 09 |
