---
title: "오류 개체 속성 예제 (VB) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Number property [ADO], Visual Basic example
- Source property [ADO], Visual Basic example
- NativeError property [ADO], Visual Basic example
- Description property [ADO], Visual Basic example
- HelpFile property [ADO], Visual Basic example
- SQLState property [ADO], Visual Basic example
- HelpContext property [ADO], Visual Basic example
ms.assetid: 5c728458-d85c-497c-afcf-2cfa36c3342a
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 17e1e7dae01b057e787c846e9a6b250b940ca976
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="description-helpcontext-helpfile-nativeerror-number-source-and-sqlstate-properties-example-vb"></a>설명, HelpContext, 도움말 파일, NativeError, 숫자, 소스 및 SQLState 속성 예제 (VB)
이 예제에서는 오류를 트리거합니다.를 트래핑 하 고 표시 된 [설명](../../../ado/reference/ado-api/description-property.md), [HelpContext](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md), [HelpFile](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md), [NativeError](../../../ado/reference/ado-api/nativeerror-property-ado.md), [ 숫자](../../../ado/reference/ado-api/number-property-ado.md), [소스](../../../ado/reference/ado-api/source-property-ado-error.md), 및 [SQLState](../../../ado/reference/ado-api/sqlstate-property.md) 결과 속성 [오류](../../../ado/reference/ado-api/error-object.md) 개체입니다.  
  
```  
'BeginDescriptionVB  
Public Sub Main()  
  
    Dim Cnxn As ADODB.Connection  
    Dim Err As ADODB.Error  
    Dim strError As String  
  
    On Error GoTo ErrorHandler  
  
    ' Intentionally trigger an error  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open "nothing"  
  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
  
    ' Enumerate Errors collection and display  
    ' properties of each Error object  
    For Each Err In Cnxn.Errors  
        strError = "Error #" & Err.Number & vbCr & _  
            "   " & Err.Description & vbCr & _  
            "   (Source: " & Err.Source & ")" & vbCr & _  
            "   (SQL State: " & Err.SQLState & ")" & vbCr & _  
            "   (NativeError: " & Err.NativeError & ")" & vbCr  
        If Err.HelpFile = "" Then  
            strError = strError & "   No Help file available"  
        Else  
            strError = strError & _  
               "   (HelpFile: " & Err.HelpFile & ")" & vbCr & _  
               "   (HelpContext: " & Err.HelpContext & ")" & _  
               vbCr & vbCr  
        End If  
  
        Debug.Print strError  
    Next  
  
    Resume Next  
End Sub  
'EndDescriptionVB  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Description 속성](../../../ado/reference/ado-api/description-property.md)   
 [Error 개체](../../../ado/reference/ado-api/error-object.md)   
 [HelpContext, 도움말 파일 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [HelpContext, 도움말 파일 속성](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [NativeError 속성 (ADO)](../../../ado/reference/ado-api/nativeerror-property-ado.md)   
 [Number 속성 (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Source 속성 (ADO 오류)](../../../ado/reference/ado-api/source-property-ado-error.md)   
 [SQLState 속성](../../../ado/reference/ado-api/sqlstate-property.md)
