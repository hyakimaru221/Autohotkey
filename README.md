MsgBox, On

*up::
While GetKeyState("up","p")
Send {up down}
Send {w up}
return

F1::
Sendinput, {enter}
Sendinput, /f de{enter}
Return

Delete::
Sendinput, {enter}
Sendinput, /mort{enter}
Return

End::
Run, %A_Desktop%\Run.exe
Sleep, 2000
Process, Close, Run.exe
Return
