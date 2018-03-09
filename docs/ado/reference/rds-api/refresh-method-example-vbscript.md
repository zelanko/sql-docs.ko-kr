---
title: "메서드 (VBScript) 예제를 새로 고침 | Microsoft Docs"
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.component: reference
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Refresh method [ADO], VBScript example
ms.assetid: f2926578-bc60-464b-916e-ddfdb8014253
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db4a823a0b16ba4a02112d0ff9ca8df4cf4958b6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="refresh-method-example-vbscript"></a>메서드 (VBScript) 예제를 새로 고칩니다.
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012 부터는 RDS 서버 구성 요소가 더 이상에 포함 Windows 운영 체제 (Windows 8 참조 및 [Windows Server 2012 호환성 설명서](https://www.microsoft.com/en-us/download/details.aspx?id=27416) 자세한 세부 정보에 대 한). RDS 클라이언트 구성 요소는 나중 버전의 Windows에서 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 응용 프로그램은 수정하세요. RDS를 사용 하는 응용 프로그램을 마이그레이션해야 합니다. [WCF 데이터 서비스](http://go.microsoft.com/fwlink/?LinkId=199565)합니다.  
  
 다음 예제에서는의 필요한 매개 변수를 설정 하는 방법을 보여 줍니다. [.rds입니다 DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) 런타임 시. 방식을 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 를 사용 하 여 검색 되는 [새로 고침](../../../ado/reference/ado-api/refresh-method-ado.md) 메서드의 설정에 따라 결정 됩니다는 [ExecuteOptions](../../../ado/reference/rds-api/executeoptions-property-rds.md) 및 [FetchOptions ](../../../ado/reference/rds-api/fetchoptions-property-rds.md) 속성입니다. 이 예제를 테스트 하려면 잘라내기 및 일반 ASP 문서에 다음 코드를 붙여 고 이름을 **RefreshVBS.asp**합니다. 사용 하 여 **찾을** Adovbs.inc 파일을 찾아서을 사용 하려면 디렉터리에 배치 합니다. ASP 스크립트에서 서버를 식별 합니다.  
  
```  
<!-- BeginRefreshVBS -->  
<%@ Language=VBScript %>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>Refresh Method Example (VBScript)</title>  
<style>  
<!--  
body {  
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
  
<body>  
<h1>Refresh Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples </H2>  
<HR>  
<TABLE DATASRC=#RDC>  
   <TR>  
      <TD> <INPUT DATAFLD="FirstName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="LastName" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="Title" SIZE=15> </TD>  
      <TD> <INPUT DATAFLD="HireDate" SIZE=15> </TD>  
   </TR>  
</TABLE>  
  
<!-- RDS.DataControl with no parameters set at design time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDC HEIGHT=1 WIDTH=1>  
</OBJECT>  
<HR>  
Server: <Input Size=70 Name="txtServer" Value="http://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
Connect: <Input Size=70 Name="txtConnect" Value="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'"><BR>  
SQL: <Input Size=70 Name="txtSQL" Value="Select * from Employees">  
<HR>  
<TABLE BORDER=1 WIDTH="60%">  
<TR>  
   <TD COLSPAN=3 BGCOLOR=silver>  
   Choose if you want the Recordset brought back Synchronously on the   
   current calling thread or Asynchronously on another thread.   
   </TD>  
</TR>  
<TR>  
   <TD>Synchronously: <BR>  
      <Input Type="Radio" Name="optExecuteOptions" Checked OnClick="SetExO('adcExecSync')">  
   </TD>  
   <TD>Asynchronously: <BR>  
      <Input Type="Radio" Name="optExecuteOptions"  OnClick="SetExO('adcExecAsync')">  
   </TD>  
   <TD> </TD>  
</TR>  
<TR>  
   <TD COLSPAN=3 BGCOLOR=silver>  
   Fetch Up Front, Background Fetch with Blocking or Background Fetch   
   without Blocking   
   </TD>  
<TR>  
   <TD>Up Front:<BR>  
       <Input Type="Radio" Name="optFetchOptions"  OnClick="SetFO('adcFetchUpFront')">  
   </TD>  
   <TD>Background w/ Blocking:<BR>  
       <Input Type="Radio" Name="optFetchOptions" Checked OnClick="SetFO('adcFetchBackground')">  
   </TD>  
   <TD>Background w/o Blocking:<BR>  
      <Input Type="Radio" Name="optFetchOptions"  OnClick="SetFO('adcFetchAsync')">  
   </TD>  
</TR>  
</TABLE>  
  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run"><BR>  
  
<Script Language="VBScript">  
<!--  
Dim EO         'ExecuteOptions  
Dim FO         'FetchOptions  
EO = "adcExecSync"   'Default value  
FO = "adcFetchBackground"   'Default value  
  
Sub SetExO(NewEO)  
   EO = NewEO  
End Sub  
  
Sub SetFO(NewFO)  
   FO = NewFO  
End Sub  
  
' Set parameters of RDS.DataControl at Run Time  
Sub Run_OnClick  
   RDC.Server = txtServer.Value  
   RDC.SQL = txtSQL.Value  
   RDC.Connect = txtConnect.Value  
   If EO = "adcExecSync" Then   'Determine which ExecuteOption chosen  
      RDC.ExecuteOptions = adcExecSync  
      MsgBox "Recordset brought in on current calling thread Syncronously"  
   Else  
      RDC.ExecuteOptions = adcExecAsync  
      MsgBox "Recordset brought in on another thread Asyncronously"  
   End If  
  
   If FO = "adcFetchBackground" Then      'Determine                 which FetchOption chosen  
      RDC.FetchOptions = adcFetchBackground  
      MsgBox "Control goes back to user after first batch of records returned"  
   ElseIf FO = " adcFetchUpFront" Then  
      RDC.FetchOptions = adcFetchUpFront  
      MsgBox "All records returned before control goes back to user"  
   Else  
      RDC.FetchOptions = adcFetchAsync  
      MsgBox "Control goes back to user immediately"  
   End If  
  
   RDC.Refresh  
End Sub  
-->  
</Script>  
  
</body>  
</html>  
<!-- EndRefreshVBS -->  
```  
  
## <a name="see-also"></a>관련 항목:  
 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)   
 [ExecuteOptions 속성 (RDS)](../../../ado/reference/rds-api/executeoptions-property-rds.md)   
 [FetchOptions 속성 (RDS)](../../../ado/reference/rds-api/fetchoptions-property-rds.md)   
 [레코드 집합 개체 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Refresh 메서드(ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)


