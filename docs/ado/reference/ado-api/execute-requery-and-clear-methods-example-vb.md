---
title: "실행 하 고, Requery 메서드 예제 (VB)의 선택을 취소 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Requery method [ADO], Visual Basic example
- Clear method [ADO], Visual Basic example
- Execute method [ADO], Visual Basic example
ms.assetid: ed5e1b60-3769-4b26-a253-1d721e37941d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 97b0aebaa5450cf2dce7622c7771550dd7f77f2f
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="execute-requery-and-clear-methods-example-vb"></a>실행, Requery, 및 메서드 예제 (VB)를 지웁니다.
이 예제에서는 **Execute** 둘 다에서 실행 될 경우 메서드는 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 및 [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체입니다. 또한 사용 하 여는 [Requery](../../../ado/reference/ado-api/requery-method.md) 에 현재 데이터를 검색 하는 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md), 및 [지우기](../../../ado/reference/ado-api/clear-method-ado.md) 의 내용을 삭제 하는 메서드는 [오류](../../../ado/reference/ado-api/errors-collection-ado.md)컬렉션입니다. (의 **오류** 컬렉션을 통해 액세스 되는 **연결** 의 개체는 [ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) 속성은 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md).) ExecuteCommand 및 PrintOutput 절차는이 절차를 실행 하려면 필요 합니다.  
  
```  
'BeginExecuteVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo Err_Execute  
  
    ' connection, command, and recordset variables  
    Dim Cnxn As ADODB.Connection  
    Dim cmdChange As ADODB.Command  
    Dim rstTitles As ADODB.Recordset  
    Dim Err As ADODB.Error  
    Dim strSQLChange As String  
    Dim strSQLRestore As String  
    Dim strSQLTitles  
    Dim strCnxn As String  
  
     ' Define two SQL statements to execute as command text  
    strSQLChange = "UPDATE Titles SET Type = 'self_help' WHERE Type = 'psychology'"  
    strSQLRestore = "UPDATE Titles SET Type = 'psychology' WHERE Type = 'self_help'"  
  
     ' Open connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
     ' Create command object  
    Set cmdChange = New ADODB.Command  
    Set cmdChange.ActiveConnection = Cnxn  
    cmdChange.CommandText = strSQLChange  
  
     ' Open titles table  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "titles"  
    rstTitles.Open strSQLTitles, Cnxn, , , adCmdTable  
  
    ' Print report of original data  
    Debug.Print _  
       "Data in Titles table before executing the query"  
    PrintOutput rstTitles  
  
    ' Call the ExecuteCommand subroutine below to execute cmdChange command  
    ExecuteCommand cmdChange, rstTitles  
  
    ' Print report of new data  
    Debug.Print _  
       "Data in Titles table after executing the query"  
    PrintOutput rstTitles  
  
    ' Use the Connection object's execute method to  
    ' execute SQL statement to restore data and trap for  
    ' errors, checking the Errors collection if necessary  
    Cnxn.Execute strSQLRestore, , adExecuteNoRecords  
  
    ' Retrieve the current data by requerying the recordset  
    rstTitles.Requery  
  
    ' Print report of restored data using sub from below  
    Debug.Print "Data after executing the query to restore the original information "  
    PrintOutput rstTitles  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
Err_Execute:  
    ' Notify user of any errors that result from  
    ' executing the query  
    If rstTitles.ActiveConnection.Errors.Count >= 0 Then  
       For Each Err In rstTitles.ActiveConnection.Errors  
          MsgBox "Error number: " & Err.Number & vbCr & _  
             Err.Description  
       Next Err  
    End If  
  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
  
Public Sub ExecuteCommand(cmdTemp As ADODB.Command, rstTemp As ADODB.Recordset)  
  
   Dim Err As Error  
  
   ' Run the specified Command object and trap for  
   ' errors, checking the Errors collection  
   On Error GoTo Err_Execute  
   cmdTemp.Execute  
   On Error GoTo 0  
  
   ' Retrieve the current data by requerying the recordset  
   rstTemp.Requery  
  
   Exit Sub  
  
Err_Execute:  
  
   ' Notify user of any errors that result from  
   ' executing the query  
   If rstTemp.ActiveConnection.Errors.Count > 0 Then  
      For Each Err In rstTemp.ActiveConnection.Errors  
         MsgBox "Error number: " & Err.Number & vbCr & _  
            Err.Description  
      Next Err  
   End If  
  
   Resume Next  
  
End Sub  
  
Public Sub PrintOutput(rstTemp As ADODB.Recordset)  
  
   ' Enumerate Recordset  
   Do While Not rstTemp.EOF  
      Debug.Print "  " & rstTemp!Title & _  
         ", " & rstTemp!Type  
      rstTemp.MoveNext  
   Loop  
  
End Sub  
'EndExecuteVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Clear 메서드 (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Command 개체 (ADO)](../../../ado/reference/ado-api/command-object-ado.md)   
 [연결 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Error 개체](../../../ado/reference/ado-api/error-object.md)   
 [Execute 메서드 (ADO 명령)](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 메서드 (ADO 연결)](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Requery 메서드](../../../ado/reference/ado-api/requery-method.md)

