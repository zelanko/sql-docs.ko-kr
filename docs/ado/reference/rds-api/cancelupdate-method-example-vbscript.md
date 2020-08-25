---
description: CancelUpdate 메서드 예제(VBScript)
title: CancelUpdate 메서드 예제 (VBScript) | Microsoft Docs
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
- CancelUpdate method [ADO], VBScript example
ms.assetid: c23912f0-1288-4727-8fb4-f643b8811cf7
author: rothja
ms.author: jroth
ms.openlocfilehash: 08691f0ae8f707f79a1725dfb466266ca45efdcb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88768782"
---
# <a name="cancelupdate-method-example-vbscript"></a>CancelUpdate 메서드 예제(VBScript)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 이 예를 테스트 하려면 \<Body> \</Body> 일반 HTML 문서의 및 태그 사이에이 코드를 잘라내어 붙여넣고 **CancelUpdateVBS**로 이름을 다시 만듭니다. ASP 스크립트는 인터넷 서버를 식별 합니다. 사용자의 설정을 반영 하도록 서버 이름을 편집 해야 합니다. MyServer에서 연결 문자열의 값을 SQL Server 설치 이름으로 변경 하면 됩니다.  
  
```  
<!-- BeginCancelUpdateVBS -->  
<%@Language=VBScript%>  
  
<%'Option Explicit%>  
<% 'use the following META tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<TITLE></TITLE>  
</HEAD>  
<BODY>  
<CENTER>  
<H1>Remote Data Service</H1>  
<H2>SubmitChanges and CancelUpdate Methods</H2>  
  
<%  ' to integrate/test this code replace the Server property value and   
    ' the Data Source value in the Connect property with appropriate values%>  
  
<HR>  
<OBJECT ID=RDS classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" HEIGHT=1 WIDTH=1></OBJECT>  
<SCRIPT Language="VBScript">  
  
     'set RDS properties for control just created  
  
    RDS.Server = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    RDS.SQL = "Select * from Employees"  
    RDS.Connect = "Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';"  
    RDS.Refresh  
</SCRIPT>  
  
<TABLE DATASRC=#RDS>  
<THEAD>  
<TR ID="ColHeaders">  
   <TH>ID</TH>  
   <TH>FName</TH>  
   <TH>LName</TH>  
   <TH>Title</TH>  
   <TH>Hire Date</TH>  
   <TH>Birth Date</TH>  
   <TH>Extension</TH>  
   <TH>Home Phone</TH>  
</TR>  
</THEAD>  
<TBODY>  
<TR>  
   <TD> <INPUT DATAFLD="EmployeeID" size=4> </TD>  
   <TD> <INPUT DATAFLD="FirstName" size=10> </TD>  
   <TD> <INPUT DATAFLD="LastName" size=10> </TD>  
   <TD> <INPUT DATAFLD="Title" size=10> </TD>  
   <TD> <INPUT DATAFLD="HireDate" size=10> </TD>  
   <TD> <INPUT DATAFLD="BirthDate" size=10> </TD>  
   <TD> <INPUT DATAFLD="Extension" size=10> </TD>  
   <TD> <INPUT DATAFLD="HomePhone" size=8> </TD>  
</TR>  
</TBODY>  
</TABLE>  
<HR>  
<INPUT TYPE=button NAME="SubmitChange" VALUE="Submit Changes">  
<INPUT TYPE=button NAME="CancelChange" VALUE="Cancel Update">  
<BR>  
<H4>Alter a current entry on the grid. Move off that Row. <BR>  
Submit the Changes to your DBMS or cancel the updates. </H4>  
</CENTER>  
<SCRIPT Language="VBScript">  
  
Sub SubmitChange_OnClick  
  
    msgbox "Changes will be made"  
    RDS.SubmitChanges     
    RDS.Refresh  
  
End Sub  
  
Sub CancelChange_OnClick  
  
    msgbox "Changes will be cancelled"  
    RDS.CancelUpdate  
    RDS.Refresh  
  
End Sub  
-->  
</SCRIPT>  
  
</BODY>  
</HTML>  
<!-- EndCancelUpdateVBS -->  
```  
  
## <a name="see-also"></a>참고 항목  
 [CancelUpdate 메서드(ADO)](../ado-api/cancelupdate-method-ado.md)