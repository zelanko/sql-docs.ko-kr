---
title: "CacheSize 속성 예제 (VB) | Microsoft Docs"
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
- CacheSize property [ADO], Visual Basic example
ms.assetid: a237ffdb-6e5b-47c6-9901-d5cdbe8625f3
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6ba7ecf1d439f4a48aafbb9bc78a2ec80773782b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="cachesize-property-example-vb"></a>CacheSize 속성 예제 (VB)
사용 하 여이 예제는 [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) 작업에 대 한 성능 차이 표시 하는 속성 집합과 30 개의 레코드가 캐시 없는 수행 합니다.  
  
```  
'BeginCacheSizeVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstRoySched As ADODB.Recordset  
    Dim strSQLSched As String  
    Dim strCnxn As String  
     'record variables  
    Dim sngStart As Single  
    Dim sngEnd As Single  
    Dim sngNoCache As Single  
    Dim sngCache As Single  
    Dim intLoop As Integer  
    Dim strTemp As String  
  
    ' Open the connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
    ' Open the RoySched Table  
    Set rstRoySched = New ADODB.Recordset  
    strSQLSched = "roysched"  
    rstRoySched.Open strSQLSched, strCnxn, , , adCmdTable  
  
    ' Enumerate the Recordset object twice and  
    ' record the elapsed time  
    sngStart = Timer  
  
    For intLoop = 1 To 2  
        rstRoySched.MoveFirst  
  
        If Not rstRoySched.EOF Then  
            ' Execute a simple operation for the  
            ' performance test  
            Do  
                strTemp = rstRoySched!title_id  
                rstRoySched.MoveNext  
            Loop Until rstRoySched.EOF  
        End If  
    Next intLoop  
  
    sngEnd = Timer  
    sngNoCache = sngEnd - sngStart  
  
    ' Cache records in groups of 30 records.  
    rstRoySched.MoveFirst  
    rstRoySched.CacheSize = 30  
    sngStart = Timer  
  
    ' Enumerate the Recordset object twice and record  
    ' the elapsed time  
    For intLoop = 1 To 2  
        rstRoySched.MoveFirst  
        Do While Not rstRoySched.EOF  
            ' Execute a simple operation for the  
            ' performance test  
            strTemp = rstRoySched!title_id  
            rstRoySched.MoveNext  
        Loop  
    Next intLoop  
  
    sngEnd = Timer  
    sngCache = sngEnd - sngStart  
  
    ' Display performance results.  
    MsgBox "Caching Performance Results:" & vbCr & _  
        "   No cache: " & Format(sngNoCache, "##0.000") & " seconds" & vbCr & _  
        "   30-record cache: " & Format(sngCache, "##0.000") & " seconds"  
  
    ' clean up  
    rstRoySched.Close  
    Set rstRoySched = Nothing  
    Exit Sub  
  
ErrorHandler:  
   ' clean up  
    If Not rstRoySched Is Nothing Then  
        If rstRoySched.State = adStateOpen Then rstRoySched.Close  
    End If  
    Set rstRoySched = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndCacheSizeVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CacheSize 속성 (ADO)](../../../ado/reference/ado-api/cachesize-property-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)

