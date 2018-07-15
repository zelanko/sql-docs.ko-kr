---
title: DISCOVER_PARTITION_DIMENSION_STAT 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: bf4626b3-4d6b-4795-bb01-df335fb9c09a
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f4dc209f985cafe804f81fa54fa68c56655d3e4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310743"
---
# <a name="discoverpartitiondimensionstat-rowset"></a>DISCOVER_PARTITION_DIMENSION_STAT 행 집합
  파티션과 연결된 차원에 대한 통계를 반환합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DISCOVER_PARTITION_DIMENSION_STAT` 행 집합에는 다음 열을 포함 합니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|필수|데이터베이스의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|필수|큐브 또는 테이블 형식 모델의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|필수|측정값 그룹의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|필수|파티션의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||차원의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||차원의 특성 이름입니다.|  
|`ATTRIBUTE_INDEXED`|`DBTYPE_BOOL`||True이면 특성이 인덱싱됨을 나타내고, 그렇지 않으면 false입니다.|  
|`ATTRIBUTE_COUNT_MIN`|`DBTYPE_I8`||최소 특성 개수입니다.|  
|`ATTRIBUTE_COUNT_MAX`|`DBTYPE_I8`||최대 특성 개수입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd8e-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>관련 항목  
 [XML for Analysis 스키마 행 집합](xml-for-analysis-schema-rowsets.md)  
  
  
