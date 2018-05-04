---
title: Clone 메서드 예제 (VBScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
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
- Clone method [ADO], VBScript example
ms.assetid: 36b96e3d-8cb0-4b79-bd93-ea5e0eb5679f
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 831a70b6ecb6da6ac2f819b879c7befeedb8a8d9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="clone-method-example-vbscript"></a>Clone 메서드 예제 (VBScript)
사용 하 여이 예제는 [복제](../../../ado/reference/ado-api/clone-method-ado.md) 의 복사본을 만들고 메서드는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 다음 각 복사본의 레코드 포인터를 독립적으로 배치 하는 사용자 지정할 수 있도록 합니다.  
  
 다음 예제에는 페이지 ASP (Active Server)를 사용 합니다. 사용 하 여이 예제는 **Northwind** Microsoft Access와 함께 배포 하는 데이터베이스입니다. 잘라내기 메모장 이나 다른 텍스트 편집기에 다음 코드를 붙여 넣고 CloneVBS.asp로 저장 합니다. 모든 클라이언트 브라우저에서 결과 볼 수 있습니다.  
  
 예를 실습 하려면 줄을 변경 `RsCustomerList.Source = "Customers"` 를 `RsCustomerList.Source = "Products"` 를 큰 테이블을 계산 합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [Clone 메서드 (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
