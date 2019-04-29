---
title: XML 형식으로 레코드 유지 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c15f4be9d452580cebd6b530f0703f249af17b36
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62913298"
---
# <a name="persisting-records-in-xml-format"></a>XML 형식으로 레코드 유지
ADTG 형식과 비슷한 **레코드 집합** Microsoft OLE DB 지 속성 공급자를 사용 하 여 지 속성 XML 형식으로 구현 됩니다. 이 공급자는 저장 된 XML 파일 또는 스트림에서 ADO에서 생성 된 스키마 정보를 포함 하는 읽기 전용, 정방향 전용 행 집합을 생성 합니다. 마찬가지로, ADO 되려면 **Recordset**, XML을 생성 하 고 파일 또는 COM 구현 하는 개체에 저장 **IStream** 인터페이스입니다. (실제로 파일은 지 원하는 개체의 또 다른 예제 **IStream**.) 2.5 이상 버전에서는 ADO 사용에 XML 파서가 MSXML (Microsoft)에 XML을 로드 하는 **레코드 집합**; 하면 msxml.dll 되므로 필요 합니다.  
  
> [!NOTE]
>  계층을 저장 하는 경우 일부 제한 사항이 적용 됩니다 **레코드 집합** (데이터 셰이프)를 XML 형식입니다. 경우 XML로 저장할 수 없습니다 계층적 **Recordset** 보류 중인 업데이트가 포함 매개 변수가 있는 저장할 수 없습니다 계층적 **레코드 집합**합니다. 자세한 내용은 [필터링 유지 및 계층적 레코드 집합](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)합니다.  
  
 XML로 데이터를 유지 하 고 다시 로드 하는 가장 쉬운 방법은 ADO를 통해 역시 사용 하 여는 **저장** 하 고 **열기** 메서드를 각각. 다음 ADO 코드 예제에서 데이터를 저장 하는 방법을 보여 줍니다 합니다 **타이틀** titles.sav 라는 파일에는 테이블입니다.  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 항상 지속 되 면 전체 ADO **레코드 집합** 개체입니다. 행의 하위 집합을 유지 하려는 경우는 **레코드 집합** 개체를 사용 합니다 **필터** 행 범위를 좁힐 프로그램 선택 절을 변경 하는 메서드. 그러나 열어야를 **레코드 집합** 클라이언트 쪽 커서를 사용 하 여 개체 (**CursorLocation** = **adUseClient**)를 사용 하는 **필터링** 행의 하위 집합을 저장 하는 메서드. 예를 들어 문자 "b"로 시작 하는 제목을 검색할 수는 필터를 적용할 수 열린 **레코드 집합** 개체:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 항상 사용 하 여 Client Cursor Engine 행 집합 생성을 스크롤할 수 있는 책갈피를 설정할 **레코드 집합** 개체 지 속성 공급자에서 생성 된 정방향 전용 데이터를 기반으로 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [XML 지속성 형식](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [네임스페이스](../../../ado/guide/data/namespaces.md)  
  
-   [스키마 섹션](../../../ado/guide/data/schema-section.md)  
  
-   [데이터 섹션](../../../ado/guide/data/data-section.md)  
  
-   [XML의 계층적 레코드 집합](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [XML의 레코드 집합 동적 속성](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT 변환](../../../ado/guide/data/xslt-transformations.md)  
  
-   [XML DOM 개체에 저장](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML 보안 고려 사항](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [XML 레코드 집합 지속성 시나리오](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
