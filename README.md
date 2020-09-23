<div align="center">

## Disable Form Close Button


</div>

### Description

This code is used to disable the "X" form button (that one top right) in a form
 
### More Info
 
The Handle of the form


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Claudio Di Flumeri](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/claudio-di-flumeri.md)
**Level**          |Beginner
**User Rating**    |4.8 (29 globes from 6 users)
**Compatibility**  |VB\.NET
**Category**       |[GUIs](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/guis__10-30.md)
**World**          |[\.Net \(C\#, VB\.net\)](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/net-c-vb-net.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/claudio-di-flumeri-disable-form-close-button__10-774/archive/master.zip)





### Source Code

```
Private Declare Function RemoveMenu Lib "user32" (ByVal hMenu As IntPtr, ByVal nPosition As Integer, ByVal wFlags As Long) As IntPtr
 Private Declare Function GetSystemMenu Lib "user32" (ByVal hWnd As IntPtr, ByVal bRevert As Boolean) As IntPtr
 Private Declare Function GetMenuItemCount Lib "user32" (ByVal hMenu As IntPtr) As Integer
 Private Declare Function DrawMenuBar Lib "user32" (ByVal hwnd As IntPtr) As Boolean
'
 Private Const MF_BYPOSITION = &H400
 Private Const MF_REMOVE = &H1000
 Private Const MF_DISABLED = &H2
'
 Public Sub DisableCloseButton(ByVal hwnd As IntPtr)
 Dim hMenu As IntPtr
 Dim menuItemCount As Integer
'
 'Obtain the handle to the form's system menu
 hMenu = GetSystemMenu(hwnd, False)
'
 'Obtain the number of items in the menu
 menuItemCount = GetMenuItemCount(hMenu)
'
 'Remove the system menu Close menu item.
 'The menu item is 0-based, so the last
 'item on the menu is menuItemCount - 1
 Call RemoveMenu(hMenu, menuItemCount - 1, _
  MF_DISABLED Or MF_BYPOSITION)
'
 'Remove the system menu separator line
 Call RemoveMenu(hMenu, menuItemCount - 2, _
  MF_DISABLED Or MF_BYPOSITION)
'
 'Force a redraw of the menu. This
 'refreshes the titlebar, dimming the X
 Call DrawMenuBar(hwnd)
 End Sub
'
'
'------------------- USAGE -------------------
 'Put this in the Load Event of a Form
'
 DisableCloseButton(Me.Handle)
```

