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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3afbec77df9a80ab7e304d2e3101e795b939eef2
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763614"
---
# <a name="persisting-records-in-xml-format"></a>XML 형식으로 레코드 유지
ADTG 형식과 마찬가지로 XML 형식의 **레코드 집합** 지 속성은 Microsoft OLE DB 지 속성 공급자를 사용 하 여 구현 됩니다. 이 공급자는 ADO에서 생성 한 스키마 정보를 포함 하는 저장 된 XML 파일 또는 스트림에서 앞 으로만 이동 가능한 읽기 전용 행 집합을 생성 합니다. 마찬가지로, ADO **레코드 집합**을 사용 하 여 XML을 생성 하 고이를 파일 또는 COM **IStream** 인터페이스를 구현 하는 모든 개체에 저장할 수 있습니다. 실제로 파일은 **IStream**을 지 원하는 개체의 또 다른 예입니다. 2.5 이상 버전의 경우 ADO는 Microsoft XML 파서 (MSXML)를 사용 하 여 XML을 **레코드 집합**으로 로드 합니다. 따라서 msxml .dll이 필요 합니다.  
  
> [!NOTE]
>  계층적 **레코드 집합** (데이터 셰이프)을 XML 형식으로 저장할 때 몇 가지 제한 사항이 적용 됩니다. 계층 구조 **레코드 집합** 에 보류 중인 업데이트가 포함 되어 있고 매개 변수가 있는 계층적 **레코드 집합**을 저장할 수 없는 경우에는 XML에 저장할 수 없습니다. 자세한 내용은 [필터링 및 계층적 레코드 집합 유지](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)를 참조 하세요.  
  
 데이터를 XML로 유지 하 고 ADO를 통해 다시 로드 하는 가장 쉬운 방법은 각각 **Save** 및 **Open** 메서드를 사용 하는 것입니다. 다음 ADO 코드 예제에서는 **titles** 테이블의 데이터를 sav 라는 파일에 저장 하는 방법을 보여 줍니다.  
  
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
  
 ADO는 항상 전체 **레코드 집합** 개체를 유지 합니다. **Recordset** 개체의 행 하위 집합을 유지 하려면 **필터** 메서드를 사용 하 여 행의 범위를 좁히거나 선택 절을 변경 합니다. 그러나 필터 메서드를 사용 하 여 행의 하위 집합을 저장 하려면**CursorLocation**adUseClient (클라이언트 쪽 커서)를 사용 하 여 **레코드 집합** 개체를 열어야 합니다  =  **adUseClient**. **Filter** 예를 들어 문자 "b"로 시작 하는 제목을 검색 하려면 열려 있는 **레코드 집합** 개체에 필터를 적용 하면 됩니다.  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO는 항상 클라이언트 커서 엔진 행 집합을 사용 하 여 지 속성 공급자가 생성 하는 앞 으로만 이동 가능한 데이터를 기반으로 스크롤할 수 있는 책갈피 가능 **레코드 집합** 개체를 생성 합니다.  
  
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
