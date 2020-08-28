---
description: Clone 메서드 예제(VBScript)
title: Clone 메서드 예제 (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Clone method [ADO], VBScript example
ms.assetid: 36b96e3d-8cb0-4b79-bd93-ea5e0eb5679f
author: rothja
ms.author: jroth
ms.openlocfilehash: af5f0a49c2bf126dbba4f0c40d88e15f0d71a187
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88975404"
---
# <a name="clone-method-example-vbscript"></a>Clone 메서드 예제(VBScript)
이 예제에서는 [Clone](./clone-method-ado.md) 메서드를 사용 하 여 [레코드 집합](./recordset-object-ado.md) 의 복사본을 만든 다음 사용자가 각 복사본의 레코드 포인터를 독립적으로 배치할 수 있도록 합니다.  
  
 Active Server 페이지 (ASP)에서 다음 예제를 사용 합니다. 이 예에서는 Microsoft Access와 함께 배포 된 **Northwind** 데이터베이스를 사용 합니다. 다음 코드를 잘라내어 메모장 또는 다른 텍스트 편집기에 붙여넣고 CloneVBS로 저장 합니다. 모든 클라이언트 브라우저에서 결과를 볼 수 있습니다.  
  
 예제를 실행 하려면 줄을로 변경 하 여 `RsCustomerList.Source = "Customers"` `RsCustomerList.Source = "Products"` 더 큰 테이블을 계산 합니다.  
  
```  
<!-- BeginCloneVBS -->  
<% Language = VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<TITLE>ADO Clone Method</TITLE>  
</HEAD>  
  
<BODY>  
  
<H1 align="center">ADO Clone Method</H1>  
<HR>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim rsFirst, rsLast, rsCount  
    Dim rsClone  
    Dim CloneFirst, CloneLast, CloneCount  
  
    ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Cnxn.Open strCnxn  
  
    ' create and open Recordset using object refs  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
  
    rsCustomers.ActiveConnection = Cnxn  
    rsCustomers.CursorLocation = adUseClient  
    rsCustomers.CursorType = adOpenKeyset  
    rsCustomers.LockType = adLockOptimistic  
    rsCustomers.Source = strSQLCustomers  
    rsCustomers.Open  
  
    rsCustomers.MoveFirst  
    rsCount = rsCustomers.RecordCount  
    rsFirst = rsCustomers("CompanyName")  
    rsCustomers.MoveLast  
    rsLast = rsCustomers("CompanyName")  
  
    ' create clone  
    Set rsClone = rsCustomers.Clone  
    rsClone.MoveFirst  
    CloneCount = rsClone.RecordCount  
    CloneFirst = rsClone("CompanyName")  
    rsClone.MoveLast  
    CloneLast = rsClone("CompanyName")  
%>  
  
<!-- Display Results -->  
<H3>There Are <%=rsCount%> Records in the original recordset</H3>  
<H3>The first record is <%=rsFirst%> and the last record is <%=rsLast%></H3>  
<BR><HR>  
<H3>There Are <%=CloneCount%> Records in the original recordset</H3>  
<H3>The first record is <%=CloneFirst%> and the last record is <%=CloneLast%></H3>  
<BR><HR>  
<H4>Location of OLEDB Database</H4>  
  
<%  
    ' Show location of DSN data source  
    Response.Write(Cnxn)  
  
    ' Clean up  
    If rsCustomers.State = adStateOpen then  
       rsCustomers.Close  
    End If  
    If rsClone.State = adStateOpen then  
       rsClone.Close  
    End If  
    If Cnxn.State = adStateOpen then  
       Cnxn.Close  
    End If  
    Set rsCustomers = Nothing  
    Set rsClone = Nothing  
    Set Cnxn = Nothing  
%>  
</BODY>  
</HTML>  
<!-- EndCloneVBS -->  
```  
  
## <a name="see-also"></a>참고 항목  
 [Clone 메서드 (ADO)](./clone-method-ado.md)   
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)