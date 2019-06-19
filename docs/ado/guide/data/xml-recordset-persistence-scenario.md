---
title: XML 레코드 집합 지 속성 시나리오 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 893921a7100ca22cae219f5a0e88d543499053b1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699698"
---
# <a name="xml-recordset-persistence-scenario"></a>XML 레코드 집합 지속성 시나리오
이 시나리오에서는 레코드 집합 개체의 내용을 ASP 응답 개체에 직접 저장 하는 ASP Active Server Pages () 응용 프로그램을 만듭니다.  
  
> [!NOTE]
>  이 시나리오에는 서버에 인터넷 정보 서버 (IIS) 5.0 했거나 이상이 설치 되어 필요 합니다.  
  
 Internet Explorer에서 반환 된 레코드 집합은 표시를 사용 하 여는 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)합니다.  
  
 이 시나리오를 만드는 데 필요한 다음과 같습니다.  
  
-   응용 프로그램 설정  
  
-   데이터 가져오기  
  
-   데이터 보내기  
  
-   수신 하 고 데이터를 표시 합니다.  
  
## <a name="step-1-set-up-the-application"></a>1단계: 응용 프로그램 설정  
 사용 권한 스크립팅 "XMLPersist" 이라는 IIS 가상 디렉터리를 만듭니다. 가상 디렉터리를 가리키는, 하나의 명명 된 "XMLResponse.asp,"는 다른 명명 된 "Default.htm." 폴더에 새 텍스트 파일을 두 개를 만듭니다.  
  
## <a name="step-2-get-the-data"></a>2단계: 데이터 가져오기  
 이 단계에서는 클라이언트에 보낼 준비를 ADO 레코드 집합을 열고 코드를 작성 합니다. 메모장과 같은 텍스트 편집기를 사용 하 여 XMLResponse.asp 파일을 열고 다음 코드를 삽입 합니다.  
  
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
  
 값을 변경 해야 합니다 `Data Source` 매개 변수에서 `strCon` Microsoft SQL Server 컴퓨터의 이름으로 합니다.  
  
 열기 및 다음 단계로 이동 파일을 유지 합니다.  
  
## <a name="step-3-send-the-data"></a>3단계: 데이터 보내기  
 레코드 집합 했으므로 ASP 응답 개체를 XML로 저장 하 여 클라이언트에 보낼 해야 있습니다. XMLResponse.asp 맨 아래에 다음 코드를 추가 합니다.  
  
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
  
 ASP 응답 개체에는 레코드 집합 대상으로 지정 됩니다 [Save 메서드](../../../ado/reference/ado-api/save-method.md)합니다. 대상의 Save 메서드를 ADO와 같은 IStream 인터페이스를 지 원하는 개체 수 [Stream 개체 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md), 또는 레코드 집합 저장 되는 전체 경로 포함 하는 파일 이름입니다.  
  
 저장 하 고 단계를 진행 하기 전에 XMLResponse.asp를 닫습니다. XMLResponse.asp 파일을 저장 하는 동일한 폴더에 기본 ADO 라이브러리 설치 폴더에서 adovbs.inc 파일을 복사할 수도 있습니다.  
  
## <a name="step-4-receive-and-display-the-data"></a>4단계: 수신 하 고 데이터를 표시 합니다.  
 이 단계에서 만들려는 HTML 파일을 사용 하 여 포함 된 [DataControl 개체 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md) 를 레코드 집합을 가져올 XMLResponse.asp 파일에서 가리키는 개체입니다. Default.htm 메모장과 같은 텍스트 편집기를 열고 다음 코드를 추가 합니다. URL에 "sqlserver를" 서버 이름으로 바꿉니다.  
  
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
  
 Default.htm 파일을 닫고 XMLResponse.asp 저장 한 같은 폴더에 저장 합니다. Internet Explorer 4.0을 사용 하 여 열거나 나중에 URL https://*sqlserver*/XMLPersist/default.htm 하 고 결과 관찰 합니다. 데이터 바인딩된 DHTML 테이블에 표시 됩니다. 이제 URL https://를 엽니다 *sqlserver* /XMLPersist/XMLResponse.asp 하 고 결과 관찰 합니다. XML이 표시 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)   
 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)
