---
description: Open 및 Close 메서드 예제(VBScript)
title: Open 및 Close 메서드 예제 (VBScript) | Microsoft Docs
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
- Close method [ADO], VBScript example
- Open method [ADO], VBScript example
ms.assetid: 66eca011-e258-4d8f-bd67-e017bcf0871b
author: rothja
ms.author: jroth
ms.openlocfilehash: bb26a778e3d484ba024a5a38564d9e3abc0a3ef0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443005"
---
# <a name="open-and-close-methods-example-vbscript"></a>Open 및 Close 메서드 예제(VBScript)
이 예에서는 열려 있는 [레코드 집합과](../../../ado/reference/ado-api/recordset-object-ado.md) [연결](../../../ado/reference/ado-api/connection-object-ado.md) 개체 모두에서 [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 및 [Close](../../../ado/reference/ado-api/close-method-ado.md) 메서드를 사용 합니다.  
  
 Active Server 페이지 (ASP)에서 다음 예제를 사용 합니다. **찾기** 를 사용 하 여 Adovbs 파일을 찾은 다음 사용 하려는 디렉터리에 배치 합니다. 다음 코드를 잘라내어 메모장 또는 다른 텍스트 편집기에 붙여 넣고 **Openvbs .asp**로 저장 합니다. 모든 브라우저에서 결과를 볼 수 있습니다.  
  
```  
<!-- BeginOpenVBS -->  
<%@ Language=VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>ADO Open Method</title>  
<STYLE>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
  
<BODY>  
<H3>ADO Open Method</H3>  
  
<TABLE WIDTH=600 BORDER=0>  
<TR>  
<TD VALIGN=TOP COLSPAN=3>  
<FONT SIZE=2>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim rsProducts, strSQLProducts  
  
    ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
  
    Cnxn.Open strCnxn  
  
    ' create and open first Recordset using Connection - execute  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "SELECT CompanyName, ContactName, City FROM Customers"  
    Set rsCustomers = Cnxn.Execute(strSQLCustomers)   
  
    ' create and open second Recordset using recordset - open  
    Set rsProducts = Server.CreateObject("ADODB.Recordset")  
    strSQLProducts = "SELECT ProductName, UnitPrice FROM Products"  
    rsProducts.Open strSQLProducts, Cnxn, adOpenDynamic, adLockPessimistic, adCmdText  
    %>  
  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
    <!-- BEGIN column header row for Customer Table-->  
    <TR CLASS=thead>  
       <TD>Company Name</TD>  
       <TD>Contact Name</TD>  
       <TD>City</TD>  
    </TR>  
  
    <!--Display ADO Data from Customer Table-->  
    <% Do Until rsCustomers.EOF %>  
    <TR CLASS=tbody>  
      <TD> <%=rsCustomers("CompanyName")%> </TD>  
      <TD> <%=rsCustomers("ContactName")%></TD>  
      <TD> <%=rsCustomers("City")%> </TD>  
    </TR>   
    <%rsCustomers.MoveNext   
    Loop   
    %>  
    </TABLE>  
  
    <HR>  
  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
    <!-- BEGIN column header row for Product List Table-->  
  
    <TR CLASS=thead2>  
       <TD>Product Name</TD>  
       <TD>Unit Price</TD>  
    </TR>  
    <!-- Display ADO Data Product List-->  
    <% Do Until rsProducts.EOF %>  
      <TR CLASS=tbody>    
      <TD> <%=rsProducts("ProductName")%> </TD>  
      <TD> <%=rsProducts("UnitPrice")%> </TD>  
      </TR>  
      <!--  Next Row = Record -->  
    <%rsProducts.MoveNext   
    Loop   
  
    ' clean up  
    If rsProducts.State = adStateOpen then  
        rsProducts.Close  
    End If  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
    Set rsProducts = Nothing  
    Set rsCustomers = Nothing  
    Set Cnxn = Nothing  
  
    %>  
    </TABLE>  
  
</BODY>  
</HTML>  
<!-- EndOpenVBS -->  
```  
  
## <a name="see-also"></a>참고 항목  
 [Close 메서드 (ADO)](../../../ado/reference/ado-api/close-method-ado.md)   
 [Connection 개체 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Open 메서드 (ADO 연결)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
