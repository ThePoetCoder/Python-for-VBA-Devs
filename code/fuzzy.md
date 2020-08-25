##### VBA Code
```vb
Option Explicit

Public Function fuzzy_comp(a As Variant, _
                           b As Variant, _
                  Optional match_case As Boolean = True) As Double
    
    Dim filepath As String
    Dim result As String
    Dim argument_string As String

    filepath = "C:\Full\Path\To\File.py"
    If match_case Then
        a = CStr(a)
        b = CStr(b)
    Else
        a = UCase(CStr(a))
        b = UCase(CStr(b))
    End If

    argument_string = "-a=" & a & " -b=" & b
    result = python_udf(file:=filepath, args:=argument_string)
    fuzzy_comp = CDbl(result)
End Function
```

##### Python Code
```py
import sys
import argparse
from difflib import SequenceMatcher

# Create parser
arg_parser = argparse.ArgumentParser()

# Add arguments you want to handle
arg_parser.add_argument("-a", type=str, required=True)
arg_parser.add_argument("-b", type=str, required=True)

if len(sys.argv) == 1:
    arg_parser.print_help()
    sys.exit(1)

# Parse sys.argv using parser
args = arg_parser.parse_args()

# Return value
result = SequenceMatcher(None, args.a, args.b).ratio()
print(result)
```
