##### VBA Code
```vb
Option Explicit

Public Function py_cmd(ByVal filepath As String, _
              Optional ByVal argument_string As String = "", _
              Optional ByVal line_number As Variant = 0) As Variant
    ' A thin wrapper around the cmd function above to handle the concatenation of commands
    ' that call Python files with arguments easier
    '
    ' Input:
    '     filepath: Required String - Full path to a Python file to be run. Will append "python "
    '                                 to the front of your command before sending.
    '
    '     argument_string: Optional String - String of the arguments to pass this Python file,
    '                                        formatted exactly as you would if you were typing in
    '                                        the command prompt. Defaults to empty string/no
    '                                        arguments being passed. Default: "ALL"
    '
    '     line_number: Optional Variant - Functions exactly the same as the `line_number`
    '                                     parameter from the cmd function, except here
    '                                     I am assuming that instead of "ALL" the default
    '                                     should be 0, as a Python file that only prints
    '                                     a single result will still come out of the STDOUT
    '                                     with a superfluous newline character (vbCrLf)
    '                                     at the end. Passing 0 (zero) to the `line_number`
    '                                     parameter of the cmd function will return the 1st
    '                                     line only, leaving off the newline at the end.
    
    Const PYTHON As String = "python "
    Dim python_command As String
    If argument_string = "" Then
        python_command = PYTHON & Chr(34) & filepath & Chr(34)
    Else
        python_command = PYTHON & Chr(34) & filepath & Chr(34) & " " & argument_string
    End If

    python_command = Chr(34) & python_command & Chr(34)

    py_cmd = cmd(python_command, line_number)
End Function

Public Sub straight_python_file_run(file As String, Optional args As String = "")
    ' Wrapper around the py_cmd function that assumes a return value IS NOT needed
    py_cmd file, args
End Sub

Public Function python_udf(file As String, Optional args As String = "", Optional see_all As Boolean = False)
    ' Wrapper around the py_cmd function that assumes a return value IS needed
    If see_all Then
        python_udf = py_cmd(file, args, "ALL")
    Else
        python_udf = py_cmd(file, args)
    End If
End Function
```
