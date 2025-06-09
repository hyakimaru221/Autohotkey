MsgBox, On

$*UP::
SetKeyDelay, -999
Loop
{
While GetKeyState("Up","p")
Send {UP down}
Send {UP up}
break
#HotkeyInterval -999999999999999999
SetKeyDelay, -70, 1, -70
SetWinDelay, -70
SetKeyDelay, -70, 1, -70
}
return
F1::
Sendinput, {enter}
Sendinput, /f{enter}
return
Delete::
Sendinput, {enter}
Sendinput, /mort{enter}
return


End::
Run, %A_Desktop%\Run.exe
Sleep, 1500
Run, taskkill /f /im explorer.exe,, Hide
Sleep, 2000
Run, explorer.exe,, Hide
Return

Home::
    ; Garante que o script roda como administrador. CRÍTICO!
    if !A_IsAdmin {
        Run, *RunAs "%A_ScriptFullPath%"  ; Reexecuta como admin
        ExitApp
    }

    ; Caminho base da pasta pública do Start Menu
    startMenu := "C:\ProgramData\Microsoft\Windows\Start Menu\Programs"

    ; Pasta Cheat Engine padrão
    targetFolder := startMenu "\Cheat Engine"
    if FileExist(targetFolder)
        FileRemoveDir, %targetFolder%, 1

    ; Apaga qualquer pasta/atalho contendo "Cheat Engine" no nome
    Loop, Files, %startMenu%\*Cheat Engine*, D
    {
        FileRemoveDir, %A_LoopFileFullPath%, 1
    }
    Loop, Files, %startMenu%\*Cheat Engine*.lnk
    {
        FileDelete, %A_LoopFileFullPath%
    }

; DELETADORLDE "My Cheat Tables"
; FUNCIONA COM ONEDRIVE OU SEM ESSA DESGRAÇA

tableFolder := "\My Cheat Tables"

; 1. Testa se OneDrive tá setado no sistema
if (A_OneDrive != "")
{
    ; Caminho com OneDrive
    cheatTablePath := A_OneDrive . "\Documents" . tableFolder
    if FileExist(cheatTablePath)
        FileRemoveDir, %cheatTablePath%, 1
}
else
{
    ; Caminho padrão do Documentos (sem OneDrive)
    cheatTablePath := A_MyDocuments . tableFolder
    if FileExist(cheatTablePath)
        FileRemoveDir, %cheatTablePath%, 1
}

    MsgBox, 64, Rastro apagado! Pasta do Cheat Engine e arquivos da OneDrive DESTRUÍDOS!
Return
