# Secured Documents

**Title**
> Secured Documents

**Category**
> REVENG

**Difficulty**
> Easy

**Points**
> 150

**Description**
> One of our employees accidentally encrypted a sensitive document using an internal tool, but forgot to write down the password. Can you help us find the password? Note: The challenge file contains an Office Macro, and it is suggested to open the document and run it in a Virtual Machine.

**Attachments**
> company_records.docm.zip

## Solution
Used oledump.py by Didier Stevens to analyze the document. (https://blog.didierstevens.com/programs/oledump-py/)

```shell
$ python2 ./oledump.py ../company_records.docm 
A: word/vbaProject.bin
 A1:       435 'PROJECT'
 A2:        86 'PROJECTwm'
 A3: M     882 'VBA/DataEncryption'
 A4: M    6005 'VBA/ThisDocument'
 A5:      3348 'VBA/_VBA_PROJECT'
 A6:      2749 'VBA/__SRP_0'
 A7:       200 'VBA/__SRP_1'
 A8:      2241 'VBA/__SRP_2'
 A9:       220 'VBA/__SRP_3'
A10:       583 'VBA/dir'

$ python2 ./oledump.py -s A3 -v ../company_records.docm 
Attribute VB_Name = "DataEncryption"
Public Sub DecryptData()
    
End Sub

$ python2 ./oledump.py -s A4 -v ../company_records.docm 
Attribute VB_Name = "ThisDocument"
Attribute VB_Base = "1Normal.ThisDocument"
Attribute VB_GlobalNameSpace = False
Attribute VB_Creatable = False
Attribute VB_PredeclaredId = True
Attribute VB_Exposed = True
Attribute VB_TemplateDerived = True
Attribute VB_Customizable = True
Private Sub Document_Open()
    Dim enteredPassword As String
    enteredPassword = InputBox("Enter password to unlock document contents")
    If enteredPassword = "0038417CED1B00460BD094BC1188E05D" Then
        MsgBox ("Decrypting document contents...")
        EncryptText (enteredPassword)
    Else
        MsgBox ("Incorrect password. Please try again later")
        ActiveDocument.Close
    End If
End Sub

Public Sub EncryptText(ByVal pw As String)
    Dim docText As String
    docText = ActiveDocument.Content.Text
    
    docText = Replace(docText, "{{ ", "")
    docText = Replace(docText, " }}", "")
    
    Dim docTextBytes() As Byte
    docTextBytes = StrConv(docText, vbFromUnicode)
    Dim passwordBytes() As Byte
    passwordBytes = StrConv(pw, vbFromUnicode)
    Dim pwCounter As Integer
    pwCounter = LBound(passwordBytes)
    
    For i = LBound(docTextBytes) To UBound(docTextBytes)
        If docTextBytes(i) <> 10 Then
            pwCounter = (i Mod UBound(passwordBytes))
            docTextBytes(i) = docTextBytes(i) Xor passwordBytes(pwCounter)
        End If
    Next i
    
    docText = StrConv(docTextBytes(), vbUnicode)
    ActiveDocument.Content.Text = docText
End Sub
```

So we can clearly see that the password is: `0038417CED1B00460BD094BC1188E05D`

## Flag
FLAG{0038417CED1B00460BD094BC1188E05D}
