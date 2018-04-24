---
title: 필터 및 RecordCount 속성 예제 (JScript) | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- JScript
helpviewer_keywords:
- RecordCount property [ADO], JScript example
- Filter property [ADO], JScript example
ms.assetid: 677fa67e-9cb9-4d7d-a786-beeb5bee5236
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eefb5a795be9a94e5ea0c174423eebf885e7d240
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/18/2018
---
# <a name="filter-and-recordcount-properties-example-jscript"></a>필터 및 RecordCount 속성 예제 (JScript)
이 예제는 **레코드 집합** Northwind 데이터베이스 및 다음 사용 하 여 회사 테이블에는 [필터](../../../ado/reference/ado-api/filter-property.md) 문자로 시작 CompanyName 필드에는 표시 되는 레코드를 제한 하는 속성 4. 잘라내기, 메모장 이나 다른 텍스트 편집기에 다음 코드를 붙여 넣고로 저장 **붙여 넣고 FilterJS.asp**합니다.  
  
```  
<!-- BeginFilterJS -->  
<%@  Language=JavaScript %>  
<%// use this meta tag instead of adojavas.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
  
<html>  
  
<head>  
<title>ADO Recordset.Filter Example</title>  
<style>  
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
</style>  
</head>  
  
<body bgcolor="White">  
  
<h1>ADO Recordset.Filter Example</h1>  
<!-- Page text goes here -->  
<%  
    // connection and recordset variables  
    var Cnxn = Server.CreateObject("ADODB.Connection")  
    var strCnxn = "Provider='sqloledb';Data Source=" + Request.ServerVariables("SERVER_NAME") + ";" +  
            "Initial Catalog='Northwind';Integrated Security='SSPI';";  
    var rsCustomers = Server.CreateObject("ADODB.Recordset");  
    var SQLCustomers = "select * from Customers;";  
    // record variables  
    var fld, filter  
    var showBlank = " ";  
    var showNull = "-NULL-";  
  
    try  
    {  
        //open connection   
        Cnxn.Open(strCnxn);  
  
        // create recordset client-side using object refs  
        rsCustomers.ActiveConnection = Cnxn;  
        rsCustomers.CursorLocation = adUseClient;  
        rsCustomers.CursorType = adOpenKeyset;  
        rsCustomers.LockType = adLockOptimistic;  
        rsCustomers.Source = SQLCustomers;  
        rsCustomers.Open();  
  
        rsCustomers.MoveFirst();  
  
        //set filter  
        filter = "CompanyName LIKE 'b*'";  
        rsCustomers.Filter = filter  
  
        if (rsCustomers.RecordCount == 0) {  
            Response.Write("No records matched ");  
            Response.Write (SQLCustomers + "So cannot make table...");  
            Cnxn.Close();  
            Response.End  
        }  
        else {  
        // show the data  
            Response.Write('<table width="100%" border="2">');      
            while(!rsCustomers.EOF) {  
                Response.Write('<tr class="tbody">');  
                for (var thisField = 0; thisField < rsCustomers.Fields.Count; thisField++) {  
                    fld = rsCustomers(thisField);  
                    fldValue = fld.Value;  
                    if (fldValue == null)  
                        fldValue = showNull;  
                    if (fldValue == "")  
                        thisField=showBlank;  
                    Response.Write("<td>" + fldValue + "</td>")  
                }  
                rsCustomers.MoveNext();  
                Response.Write("</tr>");  
            }  
            // close the table  
            Response.Write("</table>");  
        }  
    }      
    catch (e)  
    {  
        Response.Write(e.message);  
    }  
    finally  
    {  
        // clean up  
        if (rsCustomers.State == adStateOpen)  
            rsCustomers.Close;  
        if (Cnxn.State == adStateOpen)  
            Cnxn.Close;  
        rsCustomers = null;  
        Cnxn = null;  
    }  
%>  
  
</body>  
  
</html>  
<!-- EndFilterJS -->  
```  
  
## <a name="see-also"></a>관련 항목:  
 [필터 속성](../../../ado/reference/ado-api/filter-property.md)   
 [RecordCount 속성 (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)   
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
