---
description: DataSpace 개체 및 CreateObject 메서드 예제(VBScript)
title: 스페이스 개체 및 CreateObject 메서드 예제 (VBScript) | Microsoft Docs
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
- DataSpace object [RDS], VBScript example
- CreateObject method [ADO], VBScript example
ms.assetid: 12b0e160-5e5c-441f-bed7-ac0bd061e003
author: rothja
ms.author: jroth
ms.openlocfilehash: cc2887f46996450dc9d809439226dbef6cf76e97
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91720964"
---
# <a name="dataspace-object-and-createobject-method-example-vbscript"></a>DataSpace 개체 및 CreateObject 메서드 예제(VBScript)
> [!IMPORTANT]
>  Windows 8 및 Windows Server 2012부터 RDS 서버 구성 요소는 더 이상 Windows 운영 체제에 포함 되지 않습니다 (자세한 내용은 Windows 8 및 [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) 참조). 이후 버전의 Windows에서는 RDS 클라이언트 구성 요소가 제거 됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. RDS를 사용 하는 응용 프로그램은 [WCF Data Service](/dotnet/framework/wcf/)로 마이그레이션해야 합니다.  
  
 다음 예제에서는 RDS의 [CreateObject](./createobject-method-rds.md) 메서드를 사용 하는 방법을 보여 줍니다 [. ](./dataspace-object-rds.md) 기본 비즈니스 개체인 [RDSServer. DataFactory](./datafactory-object-rdsserver.md)를 사용 하 여 공간을 사용 합니다. 이 예를 테스트 하려면 \<Body> \</Body> 일반 HTML 문서의 및 태그 사이에이 코드를 잘라내어 붙여넣고 **DataSpaceVBS**로 이름을 다시 만듭니다. ASP 스크립트는 서버를 식별 합니다.  
  
```  
<!-- BeginDataSpaceVBS -->  
<html>  
<head>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>DataSpace Object and CreateObject Method Example (VBScript)</title>  
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
<h1>DataSpace Object and CreateObject Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using Query Method of RDSServer.DataFactory</H3>  
  
<!-- RDS.DataSpace  ID rdsDS-->  
<OBJECT ID="rdsDS" WIDTH=1 HEIGHT=1  
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters set at run time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS WIDTH=1 HEIGHT=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
  
<H4>Click Run -  
The <i>CreateObject</i> Method of the RDS.DataSpace Object Creates an instance of the RDSServer.DataFactory.  
The <i>Query</i> Method of the RDSServer.DataFactory is used to bring back a Recordset.</H4>  
  
<Script Language="VBScript">  
  
    Dim rdsDF  
    Dim strServer  
    Dim strCnxn  
    Dim strSQL  
  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            "<%=Request.ServerVariables("SERVER_NAME")%>" & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    strSQL = "Select FirstName, LastName from Employees"  
  
    Sub Run_OnClick()  
  
       Dim rs        
        ' Create Data Factory  
       Set rdsDF = rdsDS.CreateObject("RDSServer.DataFactory", strServer)  
        'Get Recordset    
       Set rs = rdsDF.Query(strCnxn, strSQL)     
       ' Use  RDS.DataControl to bind Recordset to data-aware Table above  
       RDS.SourceRecordset = rs  
  
    End Sub  
</Script>  
  
</body>  
</html>  
<!-- EndDataSpaceVBS -->  
```  
  
 다음 예에서는 **CreateObject** 메서드를 사용 하 여 사용자 지정 비즈니스 개체의 인스턴스를 만드는 방법을 보여 줍니다. VbBusObj. 또한 Active Server 페이지 스크립팅을 사용 하 여 웹 서버 이름을 식별 합니다.  
  
 전체 예제를 보려면 샘플 응용 프로그램 선택기를 엽니다. **클라이언트 계층** 열의 **Internet Explorer에서 VBScript**를 선택 합니다. **중간 계층** 열에서 **사용자 지정 Visual Basic 비즈니스 개체**를 선택 합니다.  
  
> [!NOTE]
>  Windows 인증을 지 원하는 데이터 원본 공급자에 연결 하는 경우 연결 문자열에 사용자 ID 및 암호 정보 대신 **Trusted_Connection = yes** 또는 **INTEGRATED Security = SSPI** 를 지정 해야 합니다.  
  
```  
Sub Window_OnLoad()  
   strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
   Set BO = ADS1.CreateObject("VbBusObj.VbBusObjCls", strServer)  
   txtConnect.Value = "dsn=Pubs;uid=MyUserID;pwd=MyPassword;"  
   txtGetRecordset.Value = "Select * From authors for Browse"  
End Sub  
```  
  
## <a name="see-also"></a>참고 항목  
 [CreateObject 메서드 (RDS)](./createobject-method-rds.md)   
 [DataSpace 개체(RDS)](./dataspace-object-rds.md)