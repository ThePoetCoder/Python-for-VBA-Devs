##### VBA Code
```vb
Option Explicit

Public Function py_slice(str_input As String, _
                Optional ByVal int_start As Variant, _
                Optional ByVal int_end As Variant, _
                Optional ByVal int_skip As Variant)
    
    Dim filepath As String
    Dim argument_string As String
    
    filepath = "C:\Full\Path\To\File.py"
    argument_string = "-str=" & Chr(34) & str_input & Chr(34)
    If Not IsMissing(int_start) Then argument_string = argument_string & " -start=" & int_start
    If Not IsMissing(int_end) Then argument_string = argument_string & " -end=" & int_end
    If Not IsMissing(int_skip) Then argument_string = argument_string & " -skip=" & int_skip
                      
    py_slice = python_udf(file:=filepath, args:=argument_string)
End Function
```

##### Python Code
```py
import sys
import argparse

# Create parser
arg_parser = argparse.ArgumentParser()

# Add arguments you want to handle
arg_parser.add_argument("-str"  , type=str, required=True )
arg_parser.add_argument("-start", type=int, required=False, default=None)
arg_parser.add_argument("-end"  , type=int, required=False, default=None)
arg_parser.add_argument("-skip" , type=int, required=False, default=None)

if len(sys.argv) == 1:
    arg_parser.print_help()
    sys.exit(1)

# Parse sys.argv using parser
args = arg_parser.parse_args()

# Return value
result = args.str[args.start : args.end : args.skip]
print(result)

```
