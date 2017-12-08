---
title: "DISCOVER_DIMENSION_STAT 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ed2707a9ee417f8e019137034e90f1a9132948e2
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="discoverdimensionstat-rowset"></a>DISCOVER_DIMENSION_STAT 행 집합
  차원이 포함된 데이터베이스 이름, 차원 이름, 해당 특성 및 각 특성의 멤버 수를 비롯한 차원에 대한 정보를 제공합니다. 테이블 형식 모델에서 이 항목은 테이블에 있는 열과 각 열에 있는 값의 수에 해당합니다.  
  
 **적용 대상:** 테이블 형식 모델, 다차원 모델  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DISCOVER_DIMENSION_STAT** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|제한|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**A S E _**|**DBTYPE_WSTR**|필수임|차원을 포함하는 데이터베이스 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|필수임|차원의 이름입니다.<br /><br /> 제한 목록에 이 열이 필요합니다.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||차원의 특성 이름입니다.|  
|**ATTRIBUTE_COUNT**|**DBTYPE_I8**||명명된 특성에 있는 값의 수입니다. 테이블 형식 모델의 경우 값은 항상 테이블의 행 수와 같습니다.|  
  
 이 스키마 행 집합은 정렬되지 않습니다.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>ADOMD.NET을 사용하여 행 집합 반환  
 ADOMD.NET 및 스키마 행 집합을 사용하여 메타데이터를 검색할 때 GUID 또는 문자열을 사용하여 GetSchemaDataSet 메서드의 스키마 행 집합 개체를 참조할 수 있습니다. 자세한 내용은 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)을 참조하세요.  
  
 다음 표에서는 이 행 집합을 식별하는 GUID와 문자열 값을 제공합니다.  
  
|인수|값|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>관련 항목:  
 [XML for Analysis 스키마 행 집합](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
