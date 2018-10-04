---
title: DISCOVER_DATASOURCES 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DISCOVER_DATASOURCES
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_DATASOURCES rowset
ms.assetid: f3ff26ab-a447-416b-ba54-1716df2283de
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 070fcc80266169753d98a8ca0673e748250556ae
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174413"
---
# <a name="discoverdatasources-rowset"></a>DISCOVER_DATASOURCES 행 집합
  서버 또는 웹 서비스에서 사용할 수 있는 XMLA(XML for Analysis) 공급자 데이터 원본의 목록을 반환합니다. 게시된 데이터 원본은 응용 프로그램 웹 서버의 URL에서 반환됩니다. 이 목록의 데이터 원본 중 하나에 클라이언트를 연결할 수 있습니다.  
  
 호출 하는 경우는 [검색](../../xmla/xml-elements-methods-discover.md) 메서드를 `DISCOVER_DATASOURCES` 열거 값을 [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) 요소를 `Discover` 메서드가 반환 되는 `DISCOVER_DATASOURCES` 행 집합입니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 클라이언트 설정 하 여 데이터 원본을 선택 합니다 `DataSourceInfo` 속성에는 [속성](../../xmla/xml-elements-properties/properties-element-xmla.md) 요소와 함께 전송 되는 [명령](../../xmla/xml-elements-properties/command-element-xmla.md) 요소를 [Execute](../../xmla/xml-elements-methods-execute.md) 메서드입니다. 클라이언트는 서버로 보낼 `DataSourceInfo` 속성의 내용을 구성하지 않아야 합니다. 대신 클라이언트는 `Discover` 메서드를 사용하여 공급자에서 지원되는 데이터 원본을 찾아야 합니다. 그런 다음 클라이언트는 `DataSourceInfo` 행 집합에서 가져온 `DISCOVER_DATASOURCES` 속성에 대해 같은 값을 다시 보냅니다.  
  
 `DISCOVER_DATASOURCES` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DataSourceName`|`DBTYPE_WSTR`|사용자 계정 컨트롤|`Adventure Works`와 같은 데이터 원본 이름입니다.|  
|`DataSourceDescription`|`DBTYPE_WSTR`||게시자가 입력한 데이터 원본에 대한 설명입니다.<br /><br /> `NULL`을 반환할 수 있습니다.|  
|`URL`|`DBTYPE_WSTR`|사용자 계정 컨트롤|해당 데이터 원본에 대해 XMLA(XML for Analysis) 메서드를 호출할 위치를 보여 주는 고유 경로입니다.<br /><br /> `NULL`을 반환할 수 있습니다.|  
|`DataSourceInfo`|`DBTYPE_WSTR`||데이터 원본에 연결하는 데 필요한 추가 정보가 들어 있는 문자열입니다.<br /><br /> `NULL`을 반환할 수 있습니다.|  
|`ProviderName`|`DBTYPE_WSTR`|사용자 계정 컨트롤|데이터 원본의 공급자 이름입니다.<br /><br /> 예: `"MSOLAP"`<br /><br /> `NULL`을 반환할 수 있습니다.|  
|`ProviderType`|`DBTYPE_WSTR`|사용자 계정 컨트롤|공급자에서 지원되는 데이터 형식입니다. 이 배열에는 다음 형식 중 하나 이상이 포함될 수 있습니다.<br /><br /> `MDP`: 다차원 데이터 공급자입니다.<br /><br /> `TDP`: 테이블 형식의 데이터 공급자입니다.<br /><br /> `DMP`: 데이터 마이닝 공급자 (구현 된 OLE db for Data Mining 사양).|  
|`AuthenticationMode`|`DBTYPE_WSTR`|사용자 계정 컨트롤|데이터 원본에서 사용되는 보안 모드 형식의 사양입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> `Unauthenticated`없습니다 사용자 ID 또는 암호를 전송 해야 합니다.<br /><br /> `Authenticated`: 사용자 ID와 암호가 데이터 원본에 연결 하는 데 필요한 정보에 포함 되어야 합니다.<br /><br /> `Integrated`: 데이터 원본에서 제공 하는 통합 보안과 같은 권한 부여를 확인 하려면 기본 보안을 사용 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 인터넷 정보 서비스 (IIS).|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
> [!IMPORTANT]  
>  `DISCOVER_DATASOURCES` 행 집합은 DMV 쿼리와 SELECT 명령 구문을 사용하여 쿼리할 수 없습니다. 그러나 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.GetSchemaDataSet%2A>을 사용하여 `DISCOVER_DATASOURCES` 행 집합을 쿼리할 수 있습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|06c03d41-f66d-49f3-b1b8-987f7af4cf18|  
|ADOMDNAME|DataSources|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  
