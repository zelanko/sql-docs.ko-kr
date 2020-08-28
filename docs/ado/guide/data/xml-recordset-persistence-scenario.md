---
description: XML 레코드 집합 지속성 시나리오
title: XML 레코드 집합 지 속성 시나리오 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: rothja
ms.author: jroth
ms.openlocfilehash: 91066d8dd42d1bcd4a11aab093661a9061a7d7d1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88978824"
---
# <a name="xml-recordset-persistence-scenario"></a>XML 레코드 집합 지속성 시나리오
이 시나리오에서는 레코드 집합 개체의 내용을 ASP 응답 개체에 직접 저장 하는 ASP (Active Server Pages) 응용 프로그램을 만듭니다.  
  
> [!NOTE]
>  이 시나리오에서는 서버에 IIS (인터넷 정보 서버 5.0) 이상이 설치 되어 있어야 합니다.  
  
 반환 된 레코드 집합은 [rds (DataControl 개체](../../reference/rds-api/datacontrol-object-rds.md))를 사용 하 여 Internet Explorer에 표시 됩니다.  
  
 이 시나리오를 만들려면 다음 단계를 수행 해야 합니다.  
  
-   응용 프로그램 설정  
  
-   데이터 가져오기  
  
-   데이터 보내기  
  
-   데이터 수신 및 표시  
  
## <a name="step-1-set-up-the-application"></a>1 단계: 응용 프로그램 설정  
 스크립트 사용 권한을 사용 하 여 "XMLPersist" 라는 IIS 가상 디렉터리를 만듭니다. 가상 디렉터리가 가리키는 폴더에 두 개의 새 텍스트 파일을 만듭니다. 하나는 이름이 "XMLResponse. .asp"이 고 다른 하나는 "Default.htm"입니다.  
  
## <a name="step-2-get-the-data"></a>2 단계: 데이터 가져오기  
 이 단계에서는 ADO 레코드 집합을 열고 클라이언트에 보낼 준비를 하는 코드를 작성 합니다. 메모장과 같은 텍스트 편집기를 사용 하 여 XMLResponse 파일을 열고 다음 코드를 삽입 합니다.  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 `Data Source`에서 매개 변수의 값을 `strCon` Microsoft SQL Server 컴퓨터 이름으로 변경 해야 합니다.  
  
 파일을 열어 두고 다음 단계로 이동 합니다.  
  
## <a name="step-3-send-the-data"></a>3 단계: 데이터 보내기  
 이제 레코드 집합이 있으므로 ASP 응답 개체에 XML로 저장 하 여 클라이언트에 전송 해야 합니다. XMLResponse의 맨 아래에 다음 코드를 추가 합니다.  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 그러면 ASP Response 개체가 레코드 집합 [저장 메서드의](../../reference/ado-api/save-method.md)대상으로 지정 됩니다. Save 메서드의 대상은 ado [Stream 개체 (ado)](../../reference/ado-api/stream-object-ado.md)와 같이 IStream 인터페이스를 지 원하는 개체 또는 레코드 집합을 저장할 전체 경로를 포함 하는 파일 이름일 수 있습니다.  
  
 다음 단계로 이동 하기 전에 XMLResponse .asp를 저장 하 고 닫습니다. 또한 기본 ADO 라이브러리 설치 폴더의 adovbs 파일을 XMLResponse 파일을 저장 한 폴더와 동일한 폴더에 복사 합니다.  
  
## <a name="step-4-receive-and-display-the-data"></a>4 단계: 데이터 받기 및 표시  
 이 단계에서는 XMLResponse 파일을 가리키는 RDS (포함 된 [DataControl 개체)](../../reference/rds-api/datacontrol-object-rds.md) 개체를 사용 하 여 레코드 집합을 가져오는 HTML 파일을 만듭니다. 메모장과 같은 텍스트 편집기를 사용 하 여 default.htm을 열고 다음 코드를 추가 합니다. URL의 "sqlserver"를 서버 이름으로 바꿉니다.  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 default.htm 파일을 닫고 XMLResponse .asp를 저장 한 폴더와 동일한 폴더에 저장 합니다. Internet Explorer 4.0 이상 버전을 사용 하 여 https://*sqlserver*/Xmlpersist/default.htm URL을 열고 결과를 관찰 합니다. 데이터는 바인딩된 DHTML 테이블에 표시 됩니다. 이제 URL https:// *sqlserver* /Xmlpersist/xmlresponse.xml을 열고 결과를 관찰 합니다. XML이 표시 됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Save 메서드](../../reference/ado-api/save-method.md)   
 [XML 형식으로 레코드 유지](./persisting-records-in-xml-format.md)