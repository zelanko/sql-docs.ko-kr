---
title: "스트림 및 지 속성 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: af1ecf7ed9f4702d986d6f1881b3264ab8171c87
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="streams-and-persistence"></a>스트림 및 지 속성
[레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md) 개체 [저장](../../../ado/reference/ado-api/save-method.md) 메서드 저장소 또는 *계속 되 면*, **레코드 집합** 파일인 및 [열고](../../../ado/reference/ado-api/open-method-ado-recordset.md)메서드 복원은 **레코드 집합** 파일에 해당 합니다.  
  
 2.7 이상을 ADO와는 **저장** 및 **열려** 메서드 유지할 수는 **레코드 집합** 에 [스트림](../../../ado/reference/ado-api/stream-object-ado.md) 도 개체입니다. 이 기능은 원격 데이터 서비스 (RDS) 및 ASP Active Server Pages () 사용 하 여 작업할 때 특히 유용 합니다.  
  
 지 속성 사용할 수 있는 방법을 자체적으로 ASP 페이지에 대 한 자세한 내용은 현재 ASP 설명서를 참조 합니다.  
  
 다음은 몇 가지 시나리오를 보여 주는 방법을 **스트림** 개체 및 지 속성을 사용할 수 있습니다.  
  
## <a name="scenario-1"></a>시나리오 1  
 이 시나리오는 단순히 저장 한 **레코드 집합** 파일을 이동한 다음에 **스트림**합니다. 다른 파티션으로 지속형된 스트림의 다음 열었을 **레코드 집합**합니다.  
  
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
 지속 되 면이 시나리오는 **레코드 집합** 에 **스트림** XML 형식에서입니다. 그런 다음 읽어는 **스트림** 검사, 조작 또는 표시할 수 있는 문자열에 있습니다.  
  
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
 ASP 코드 유지 보여 주는 예제 코드는 **레코드 집합** 에 직접 XML로는 **응답** 개체:  
  
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
 이 시나리오에서는 ASP 코드의 내용을 씁니다.는 **레코드 집합** ADTG 형태로 표시 클라이언트에 있습니다. [OLE DB에 대 한 Microsoft 커서 서비스](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md) 연결이 끊긴 만드는 데이 데이터를 사용할 수 **레코드 집합**합니다.  
  
 RDS에 새 속성 [DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md), [URL](../../../ado/reference/rds-api/url-property-rds.md)를 생성 하는.asp 페이지를 가리키는 **레코드 집합**합니다. 즉, 한 **레코드 집합** 개체 없이 얻을 수 RDS 서버 쪽을 사용 하 여 [DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) 개체나 비즈니스 개체를 작성 하는 사용자입니다. RDS 프로그래밍 모델을 훨씬 간단해 집니다.  
  
 http://server/directory/recordset.asp 명명 된 서버 쪽 코드:  
  
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
    <PARAM NAME="URL" VALUE="http://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 개발자는을 사용 하 여 사용할 수도 **레코드 집합** 클라이언트에서 개체:  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "http://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Open 메서드 (ADO 레코드 집합)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Record 개체 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save 메서드](../../../ado/reference/ado-api/save-method.md)

