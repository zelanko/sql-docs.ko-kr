---
title: DISCOVER_PARTITION_STAT 행 집합 | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d2dd86a1ab15fbe9bcf11c6a4891fce22091fe58
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT 행 집합
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  특정 파티션의 집계에 대한 통계를 반환합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_PARTITION_STAT** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|필수임|차원을 포함하는 데이터베이스 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|필수임|파티션을 포함하는 큐브 또는 테이블 형식 모델 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|필수임|차원에 있는 측정값 그룹 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|필수임|파티션의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|**AGGREGATION_NAME**|**DBTYPE_WSTR**||집계의 이름입니다.|  
|**AGGREGATION_SIZE**|**DBTYPE_I8**||집계의 크기입니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
