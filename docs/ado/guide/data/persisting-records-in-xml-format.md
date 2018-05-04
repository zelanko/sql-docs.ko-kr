---
title: XML 형식으로 유지 레코드 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: 17
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 582e0a0fb3b757f9f9257ebaa199c819068cb2e4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="persisting-records-in-xml-format"></a>XML 형식으로 유지 레코드
ADTG 형식과 마찬가지로 **레코드 집합** Microsoft OLE DB 지 속성 공급자를 사용 하 여 지 속성 XML 형식으로 구현 됩니다. 이 공급자는 저장 된 XML 파일 또는 스트림에서 ADO에 의해 생성 된 스키마 정보를 포함 하는 읽기 전용, 정방향 전용 행 집합을 생성 합니다. 마찬가지로, ADO 지나야 **레코드 집합**XML을 생성 하 고 파일 또는 COM 구현 하는 개체에 저장할 **IStream** 인터페이스입니다. (실제로 파일은을 지 원하는 개체의 또 다른 예 **IStream**.) 2.5 이상 버전에서는 ADO 사용에 Microsoft XML (MSXML) 파서에 XML을 로드 하는 **레코드 집합**; 따라서 하면 msxml.dll이 필요 합니다.  
  
> [!NOTE]
>  계층 구조를 저장할 때 몇 가지 제한이 적용 **레코드 집합** (데이터 셰이프)를 XML 형식입니다. 경우에 XML로 저장할 수 없습니다 계층적 **레코드 집합** 보류 중인 업데이트가 포함 되어 매개 변수가 있는 저장할 수 없습니다 계층적 **레코드 집합**합니다. 자세한 내용은 참조 [계층적 레코드 집합 및 필터링 유지](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)합니다.  
  
 데이터를 XML로 유지 하 고 다시 로드 하는 가장 쉬운 방법은 다시 ADO를 통해 것으로 **저장** 및 **열려** 메서드를 각각. 다음 코드 예제 ADO에 데이터를 저장 하는 방법을 보여 줍니다는 **타이틀** titles.sav 라는 파일에는 테이블입니다.  
  
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
  
 ADO 항상 계속 되 면 전체 **레코드 집합** 개체입니다. 행의 하위 집합을 유지 하려는 경우는 **레코드 집합** 개체를 가져오려면는 **필터** 메서드 선택 절을 바꾸거나 행 범위를 좁힐 수 있습니다. 그러나 열어야는 **레코드 집합** 클라이언트 쪽 커서를 사용 하는 개체 (**앞** = **adUseClient**) 사용 하는 **필터링** 행의 하위 집합을 저장 방법입니다. 예를 들어 문자 "b"로 시작 하는 제목을 검색 하려면 있습니다 필터를 적용할 수는 열린 **레코드 집합** 개체:  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 항상를 사용 하 여 Client Cursor Engine 행 집합을 스크롤할 수 있는 책갈피를 설정할 **레코드 집합** 지 속성 공급자가 생성 되는 정방향 전용 데이터를 기반으로 하는 개체입니다.  
  
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
