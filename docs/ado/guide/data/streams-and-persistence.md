---
title: 스트림 및 지 속성 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 22fbf503196c467a7816bf4e9c76151276cc6d4a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924024"
---
# <a name="streams-and-persistence"></a>스트림 및 지속성
[레코드](../../../ado/reference/ado-api/recordset-object-ado.md) 집합 개체 [Save](../../../ado/reference/ado-api/save-method.md) 메서드는 파일에 **레코드 집합** 을 저장 하거나 *유지*하며, [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) 메서드는 해당 파일에서 **레코드 집합** 을 복원 합니다.  
  
 ADO 2.7 이상에서는 **Save** 및 **Open** 메서드가 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 개체에도 **레코드 집합** 을 유지할 수 있습니다. 이 기능은 RDS (원격 데이터 서비스) 및 ASP (Active Server 페이지)를 사용할 때 특히 유용 합니다.  
  
 ASP 페이지에서 지 속성을 단독으로 사용 하는 방법에 대 한 자세한 내용은 현재 ASP 설명서를 참조 하십시오.  
  
 다음은 **스트림** 개체 및 지 속성을 사용 하는 방법을 보여 주는 몇 가지 시나리오입니다.  
  
## <a name="scenario-1"></a>시나리오 1  
 이 시나리오에서는 단순히 **레코드 집합** 을 파일에 저장 한 다음 **스트림에**저장 합니다. 그런 다음 지속형 스트림을 다른 **레코드 집합**으로 엽니다.  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>시나리오 2  
 이 시나리오에서는 **레코드 집합** 을 XML 형식의 **스트림으로** 유지 합니다. 그런 다음 **스트림을** 검사 하거나 조작 하거나 표시할 수 있는 문자열로 읽습니다.  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>시나리오 3  
 이 예제 코드에서는 **레코드 집합** 을 XML로 **응답** 개체에 직접 유지 하는 ASP 코드를 보여 줍니다.  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>시나리오 4  
 이 시나리오에서 ASP 코드는 ADTG 형식의 **레코드 집합** 내용을 클라이언트에 기록 합니다. [OLE DB에 대 한 Microsoft Cursor Service](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 는이 데이터를 사용 하 여 연결 되지 않은 **레코드 집합**을 만들 수 있습니다.  
  
 RDS [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md) [URL](../../../ado/reference/rds-api/url-property-rds.md)의 새 속성은 **레코드 집합**을 생성 하는 .asp 페이지를 가리킵니다. 즉, 서버 쪽 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체 또는 비즈니스 개체를 작성 하는 사용자를 사용 하 여 RDS 없이 **레코드 집합** 개체를 가져올 수 있습니다. 이렇게 하면 RDS 프로그래밍 모델을 크게 간소화할 것입니다.  
  
 서버 쪽 코드, 명명 된https://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 클라이언트 쪽 코드:  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="https://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 또한 개발자는 클라이언트에서 **레코드 집합** 개체를 사용 하는 옵션도 있습니다.  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "https://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>참고 항목  
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)
