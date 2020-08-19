---
description: Status 속성 예제(필드)(VB)
title: Status 속성 예제 (필드) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: rothja
ms.author: jroth
ms.openlocfilehash: 66fab5cee49adf89bffee79f5b51b13780d5d982
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441945"
---
# <a name="status-property-example-field-vb"></a>Status 속성 예제(필드)(VB)
다음 예제에서는 [인터넷 게시 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)를 사용 하 여 읽기/쓰기 폴더에서 문서를 엽니다. [레코드](../../../ado/reference/ado-api/record-object-ado.md) 에 대 한 [Field](../../../ado/reference/ado-api/field-object.md) 개체의 [Status](../../../ado/reference/ado-api/status-property-ado-field.md) 속성은 먼저 **adfieldpendinginsert**로 설정 된 다음 **adFieldOk**로 업데이트 됩니다.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 다음 예에서는 문서에서 연 **레코드** 에서 알려진 **필드** 를 삭제 합니다. **Status** 속성은 먼저 **adFieldOK**로 설정 된 다음 **adfieldpendingunknown**으로 설정 됩니다.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 다음 코드는 읽기 전용 문서에서 열린 **레코드** 에서 **필드** 를 삭제 합니다. **상태** 는 **adfieldpendingdelete**로 설정 됩니다. [업데이트](../../../ado/reference/ado-api/update-method.md)시에는 삭제 작업이 실패 하 고 **상태** 는 **Adfieldpendingdelete** plus **adfieldpendingdelete 거부**합니다. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 보류 중 **상태** 설정을 지웁니다.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>참고 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status 속성(ADO 필드)](../../../ado/reference/ado-api/status-property-ado-field.md)
