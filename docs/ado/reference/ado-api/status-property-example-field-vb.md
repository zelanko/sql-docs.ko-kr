---
title: 상태 속성 예제 (필드) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58c71c4f69cdd25de960eacba7370aa64b67bfb7
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35282042"
---
# <a name="status-property-example-field-vb"></a>상태 속성 예제 (필드) (VB)
다음 예제에서는 문서를 사용 하 여 읽기/쓰기 폴더에서 열고는 [인터넷 게시 공급자](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md)합니다. [상태](../../../ado/reference/ado-api/status-property-ado-field.md) 속성은 [필드](../../../ado/reference/ado-api/field-object.md) 의 개체는 [레코드](../../../ado/reference/ado-api/record-object-ado.md) 처음으로 설정 됩니다 **adFieldPendingInsert**, 로업데이트한다음**adFieldOk**합니다.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=http://MyServer/"  
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
  
 다음 예에서는 삭제 알려진 **필드** 에서 **레코드** 문서에서 열. **상태** 속성이 처음으로 설정 될 **adFieldOK**, 다음 **adFieldPendingUnknown**합니다.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 다음 코드 삭제는 **필드** 에서 **레코드** 읽기 전용 문서에서 열. **상태** 로 설정 됩니다 **adFieldPendingDelete**합니다. [업데이트](../../../ado/reference/ado-api/update-method.md), 삭제 되지 것입니다 및 **상태** 됩니다 **adFieldPendingDelete** 플러스 **adFieldPermissionDenied**합니다. [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) 지웁니다는 보류 중인 **상태** 설정 합니다.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>관련 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Status 속성(ADO 필드)](../../../ado/reference/ado-api/status-property-ado-field.md)
