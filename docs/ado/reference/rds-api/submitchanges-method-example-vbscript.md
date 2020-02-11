---
title: SubmitChanges 메서드 예제 (VBScript) | Microsoft Docs
ms.prod: sql
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- SubmitChanges method [ADO], VBScript example
ms.assetid: 619bc7fd-ad0a-44ea-9678-ad40a662c258
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a74f69947d6d1a1d730d39875f32a0cfc7286705
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67963361"
---
# <a name="submitchanges-method-example-vbscript"></a>SubmitChanges 메서드 예제(VBScript)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565)로 마이그레이션해야 합니다.  
  
 다음 코드 조각에서는 RDS와 함께 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md) 메서드를 사용 하는 방법을 보여 줍니다 [. DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 개체입니다.  
  
 이 예를 테스트 하려면이 코드를 잘라내어 일반적인 ASP 문서에 붙여넣고 이름을 **SubmitChangesCtrlVBS**로 합니다. ASP 스크립트는 서버를 식별 합니다.  
  
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
    ' the Data Source value in the Connect property with identical values%>  
  
<HR>  
<OBJECT id="RDS" classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" HEIGHT="1" WIDTH="1"></OBJECT>  
<SCRIPT Language="VBScript">  
  
     'set RDS properties for control just created  
    RDS.Server = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    RDS.Connect = "Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind';"  
    RDS.SQL = "Select * from Employees"  
    RDS.Refresh  
</SCRIPT>  
  
<TABLE DATASRC="#RDS">  
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
   <TD> <INPUT DATAFLD="EmployeeID" size=4 id=text1 name=text1> </TD>  
   <TD> <INPUT DATAFLD="FirstName" size=10 id=text2 name=text2> </TD>  
   <TD> <INPUT DATAFLD="LastName" size=10 id=text3 name=text3> </TD>  
   <TD> <INPUT DATAFLD="Title" size=10 id=text4 name=text4> </TD>  
   <TD> <INPUT DATAFLD="HireDate" size=10 id=text5 name=text5> </TD>  
   <TD> <INPUT DATAFLD="BirthDate" size=10 id=text6 name=text6> </TD>  
   <TD> <INPUT DATAFLD="Extension" size=10 id=text7 name=text7> </TD>  
   <TD> <INPUT DATAFLD="HomePhone" size=8 id=text8 name=text8> </TD>  
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
</SCRIPT>  
  
</BODY>  
</HTML>  
<!-- EndCancelUpdateVBS -->  
```  
  
## <a name="see-also"></a>참고 항목  
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [SubmitChanges 메서드(RDS)](../../../ado/reference/rds-api/submitchanges-method-rds.md)


