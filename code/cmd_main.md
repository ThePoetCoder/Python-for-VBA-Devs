##### VBA Code
```vb
Option Explicit

Public Function cmd(ByVal command As String, _
           Optional ByVal line_number As Variant = "ALL") As Variant
    '=============================================================================================
    ' This is an attempt to integrate using the command line in VBA.
    '
    ' The Command Prompt will hide itself/not open on the screen. The text that would have been
    ' printed in the Command Prompt as a result of your command will be redirected to a temporary
    ' file that is then accessed from VBA and the text extracted as the result of this function.
    ' If an error occurs in either the VBA or your command, a VBA error will be raised, and you
    ' are provided the opportunity to debug in the normal VBA fashion. If there is an error in
    ' your command, the text that would have printed to the Command Prompt (the Standard Error)
    ' is redirected to pop up as the description for a Err.Number 999 VBA error, and is also
    ' printed to the Immediate Window in case you are calling this function directly or
    ' indirectly from a worksheet, because a pop up window would not appear then.
    '
    ' I have combined knowledge & code found at the below links to create this function
    '     Original CommandLine function by "Aaron Bush (Oorang)"
    '         - http://www.vbaexpress.com/kb/getarticle.php?kb_id=971
    '     Textfile usage in the command line
    '         - https://stackoverflow.com/a/11529980
    '     WScript.Shell.Run vs WScript.Shell.Exec
    '         - https://stackoverflow.com/a/32298415
    '     More info on WScript.Shell.Run
    '         - http://www.informit.com/articles/article.aspx?p=1187429&seqNum=5
    '
    ' Parameters:
    '     command: Required String - The command you would like to send, packed into a string
    '
    '     line_number: Optional Variant - When "ALL": Function will return a String containing
    '                                                 the entire output of your command. Both
    '                                                 STDOUT (Standard Output) & STDERR (Standard
    '                                                 Error) are sent to the clipboard and
    '                                                 become the return value.
    '                                     When an Integer: a single line from the STDOUT or STDERR
    '                                                      is returned, specifically the
    '                                                      line number passed in. Zero-based, so
    '                                                      passing in 0 returns the first line,
    '                                                      1 returns the second line, etc.
    '                                     Default: "ALL"
    '                                     Note: To be used in conjunction with the all other
    '                                           parameters. If any of them are False, then it
    '                                           doesn't matter what is passed into `line_number`,
    '                                           as the line of code that handles this parameter
    '                                           will never be executed.
    '
    ' Return:
    '     String - The standard output (or a single line of it if an integer is passed to
    '              `line_number`) is returned as the result of this function. Errors in the VBA
    '              or Command will be printed in the Immediate Window and raised as a VBA Error
    '=============================================================================================
    Const MATCH As Long = 0
    Const CMD_EXE As String = "cmd.exe"
    Const COMSPEC As String = "COMSPEC"
    Const TERMINATE_COMMAND_WINDOW As String = " /c "
    Const SEND_STDOUT_TO_FILE As String = " >"
    Const SEND_STDERR_TO_FILE As String = " 2>"
    
    Dim cmd_exe_path As String
    Dim command_switch As String
    Dim final_command As String
    Dim out_filename As String
    Dim err_filename As String
    Dim err_string As String
    
    On Error GoTo Err_Hnd
    cmd_exe_path = VBA.Environ$(COMSPEC)
    If VBA.StrComp(VBA.Right$(cmd_exe_path, 7), CMD_EXE, vbTextCompare) <> MATCH Then
        command_switch = vbNullString
    Else
        command_switch = TERMINATE_COMMAND_WINDOW
    End If
    
    timestamp_filename_generator out_filename, err_filename
    final_command = cmd_exe_path & _
                    command_switch & _
                    command & _
                    SEND_STDOUT_TO_FILE & out_filename & _
                    SEND_STDERR_TO_FILE & err_filename
    'Debug.Print final_command ' un-comment if you want to print what command is getting sent
    
    ' Of the many possible way there are to run a command, I believe WScript.Shell.Run is
    ' the most useful. It can take 3 arguments: a string Command, an integer WindowStyle,
    ' and a boolean WaitOnReturn
    '     1.) The Command is built & concatenated into our final_command variable above
    '     2.) The WindowStyle I always input `vbHide` here; with the goal being to integrate
    '         command line processing into VBA as if it were built in, you don't want a
    '         Command Prompt to actually open, even a little bit.
    '     3.) The WaitOnReturn I always input `True` here; the functionality of the Command
    '         Prompt that I am most trying to emphasize is throwing an error when
    '         STDERR <> "" and returning STDOUT as the result of the function.
    '         Both of these features require that the command creates a temp file before VBA
    '         tries to read the temp file.
    CreateObject("WScript.Shell").Run final_command, vbHide, True
    
    ' check for errors in the command itself
    err_string = read_file(err_filename, False)
    If err_string <> "" Then
        err_string = "COMMAND LINE ERROR:" & err_string
        ' Print error as well, in case you are calling this from the worksheet
        ' or Python error is too long for error description
        Debug.Print err_string
        Err.Raise 999, , err_string
    End If

    cmd = read_file(out_filename, True)
    If cmd <> "" And UCase(CStr(line_number)) <> "ALL" Then
        ' strips out single line of output if desired
        cmd = Split(cmd, vbCrLf)(line_number)
    End If
    
    temp_file_cleanup out_filename, err_filename
    Exit Function
    
Err_Hnd:
    temp_file_cleanup out_filename, err_filename
    Err.Raise 999, , err_string
End Function

Private Sub timestamp_filename_generator(ByRef stdout As String, ByRef stderr As String)
    ' Finds a "temp" folder inside the AddIn folder, and creates 2 unique temporary
    ' text files to store the STDOUT & STDERR
    ' Arguments are passed ByRef to alter their values within this sub
    Dim filename As String
    Do
        filename = CStr(Now())
        filename = Replace(filename, "/", ".")
        filename = Replace(filename, " ", ".")
        filename = Replace(filename, ":", ".")
        filename = addin_temp_folder() & "\" & filename
        stdout = filename & ".out"
        stderr = filename & ".err"
    ' If the file already exists somehow, keep looping until Now() is different and
    ' returns a filename that is not being used already
    Loop While file_exists(stdout) Or file_exists(stderr)
End Sub

Private Function addin_temp_folder() As String
    ' Generate the AddIn folder path from Environ("AppData"), and if a
    ' folder titled "temp" does not yet exist there, create one
    addin_temp_folder = Replace(Environ("AppData"), "Roaming", "") & "Local\Temp\cmd4vba"
    
    ' check that "temp" folder exists inside AddIn folder
    If Dir(addin_temp_folder, vbDirectory) <> "cmd4vba" Then
        ' if it does not, create the folder
        With CreateObject("Scripting.FileSystemObject")
            .CreateFolder addin_temp_folder
        End With
    End If
End Function

Private Function read_file(filepath As String, crop As Boolean) As String
    ' reads a text file, with the option (crop=True) to remove the first vbCrLf
    Dim fso As Object
    Dim txtStream As Object
    Set fso = CreateObject("Scripting.FileSystemObject")
    Set txtStream = fso.OpenTextFile(filepath)
    
    Do While Not txtStream.AtEndOfStream
        read_file = read_file & vbCrLf & txtStream.ReadLine
    Loop
    If crop Then read_file = Mid(read_file, 3)
    Set fso = Nothing
    Set txtStream = Nothing
End Function

Private Sub temp_file_cleanup(out_filename As String, err_filename As String)
    ' deletes the temporary text files created during runtime
    If file_exists(out_filename) Then Kill out_filename
    If file_exists(err_filename) Then Kill err_filename
End Sub

Private Function file_exists(filepath As String) As Boolean
    file_exists = Mid(filepath, InStrRev(filepath, "\") + 1) = Dir(filepath, vbDirectory)
End Function
```
