MsgBox, On

*up::
While GetKeyState("up","p")
Send {up down}
Send {w up}
return

F1::
Sendinput, {enter}
Sendinput, /f br{enter}
Return

Delete::
Sendinput, {enter}
Sendinput, /mort{enter}
Return


End::
Run, %A_Desktop%\Run.exe
Sleep, 1500
Run, taskkill /f /im explorer.exe,, Hide
Sleep, 2000
Run, explorer.exe,, Hide
Return

Home::
    if !A_IsAdmin {
        Run, *RunAs "%A_ScriptFullPath%"
        ExitApp
    }

    startMenu := "C:\ProgramData\Microsoft\Windows\Start Menu\Programs"

    targetFolder := startMenu "\Cheat Engine"
    if FileExist(targetFolder)
        FileRemoveDir, %targetFolder%, 1

    Loop, Files, %startMenu%\*Cheat Engine*, D
    {
        FileRemoveDir, %A_LoopFileFullPath%, 1
    }
    Loop, Files, %startMenu%\*Cheat Engine*.lnk
    {
        FileDelete, %A_LoopFileFullPath%
    }

tableFolder := "\My Cheat Tables"
cheatTablePath := A_MyDocuments . tableFolder
if FileExist(cheatTablePath)
    FileRemoveDir, %cheatTablePath%, 1
MsgBox, 64, Rastro apagado!
Return
