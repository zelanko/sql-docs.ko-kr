---
title: NumericScale 및 Precision 속성 예제 (VB) | Microsoft Docs
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
- NumericScale property [ADO], Visual Basic example
- Precision property [ADO], Visual Basic example
ms.assetid: 9c1e2322-c225-49d1-a120-a343f23cea73
author: rothja
ms.author: jroth
ms.openlocfilehash: fe33e513ebb5645952fcf1b57dc819e64af90315
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762346"
---
# <a name="numericscale-and-precision-properties-example-vb"></a>NumericScale 및 Precision 속성 예제(VB)
이 예에서는 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 및 [precision](../../../ado/reference/ado-api/precision-property-ado.md) 속성을 사용 하 여 ***Pubs*** 데이터베이스의 ***할인율*** 테이블에 있는 필드의 숫자 소수 자릿수와 전체 자릿수를 표시 합니다.  
  
```  
'BeginNumericScaleVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub NumericScaleX()  
  
    ' connection and recordset variables  
   Dim rstDiscounts As ADODB.Recordset  
   Dim Cnxn As ADODB.Connection  
   Dim fldTemp As ADODB.Field  
   Dim strCnxn As String  
   Dim strSQLDiscounts As String  
  
   ' Open connection  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "Provider='sqloledb';Data Source='MySqlServer';Initial Catalog='Pubs';Integrated Security='SSPI';"  
  
   Cnxn.Open strCnxn  
  
   ' Open recordset  
   Set rstDiscounts = New ADODB.Recordset  
   strSQLDiscounts = "Discounts"  
   rstDiscounts.Open strSQLDiscounts, Cnxn, adOpenStatic, adLockReadOnly, adCmdTable  
  
   ' Display numeric scale and precision of  
   ' numeric and small integer fields  
   For Each fldTemp In rstDiscounts.Fields  
      If fldTemp.Type = adNumeric Or fldTemp.Type = adSmallInt Then  
         MsgBox "Field: " & fldTemp.Name & vbCr & _  
            "Numeric scale: " & _  
               fldTemp.NumericScale & vbCr & _  
            "Precision: " & fldTemp.Precision  
      End If  
   Next fldTemp  
  
    ' clean up  
   rstDiscounts.Close  
   Cnxn.Close  
   Set rstDiscounts = Nothing  
   Set Cnxn = Nothing  
  
End Sub  
'EndNumericScaleVB  
```  
  
## <a name="see-also"></a>참고 항목  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [NumericScale 속성 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)   
 [Precision 속성(ADO)](../../../ado/reference/ado-api/precision-property-ado.md)
