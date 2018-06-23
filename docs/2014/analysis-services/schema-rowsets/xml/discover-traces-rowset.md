---
title: DISCOVER_TRACES 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 1be6a035-ffc9-489e-9d4d-7391b3e384e2
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7b3c8428b34a72f16986044db1652b9907384b07
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36180598"
---
# <a name="discovertraces-rowset"></a>DISCOVER_TRACES 행 집합
  서버에서 현재 활성 상태인 추적에 대한 정보를 제공합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_TRACES` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|`TraceID`|`DBTYPE_WSTR`|추적 ID입니다.|  
|`TraceName`|`DBTYPE_WSTR`|추적 이름입니다.|  
|`LogFileName`|`DBTYPE_WSTR`|추적 로그 파일 이름입니다.|  
|`LogFileSize`|`DBTYPE_I4`|추적 로그 파일 크기입니다.|  
|`LogFileRollover`|`DBTYPE_BOOL`|true이면 로그 파일이 롤오버되어야 함을 나타내고, 그렇지 않으면 false입니다.|  
|`AutoRestart`|`DBTYPE_BOOL`|true이면 자동 다시 시작 옵션을 사용할 수 있음을 나타내고, 그렇지 않으면 false입니다.|  
|`CreationTime`|`DBTYPE_TIME`|추적을 만든 날짜와 시간입니다.|  
|`StopTime`|`DBTYPE_TIME`|추적 중지 시간입니다.|  
|`Type`|`PF_DBTYPE_WSTR`|추적의 유형입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `DISCOVER_TRACES` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**TraceId**|`DBTYPE_I4`|(선택 사항)|  
|`Type`|WSTR|(선택 사항)|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd1a-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRACES|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  