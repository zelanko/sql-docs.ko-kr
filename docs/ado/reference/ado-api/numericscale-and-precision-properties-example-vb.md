---
title: "NumericScale 및 전체 자릿수 속성 예제 (VB) | Microsoft Docs"
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
- NumericScale property [ADO], Visual Basic example
- Precision property [ADO], Visual Basic example
ms.assetid: 9c1e2322-c225-49d1-a120-a343f23cea73
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 51c7b958564503382a89c13b39545d4b6e3d0821
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="numericscale-and-precision-properties-example-vb"></a>NumericScale 및 전체 자릿수 속성 예제 (VB)
사용 하 여이 예제는 [NumericScale](../../../ado/reference/ado-api/numericscale-property-ado.md) 및 [정밀도](../../../ado/reference/ado-api/precision-property-ado.md) 소수 자릿수 및 필드에 전체 자릿수를 표시 하는 속성의 ***할인*** 목차는 *** Pubs*** 데이터베이스입니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Field 개체](../../../ado/reference/ado-api/field-object.md)   
 [NumericScale 속성 (ADO)](../../../ado/reference/ado-api/numericscale-property-ado.md)   
 [Parameter 개체](../../../ado/reference/ado-api/parameter-object.md)   
 [Precision 속성(ADO)](../../../ado/reference/ado-api/precision-property-ado.md)

