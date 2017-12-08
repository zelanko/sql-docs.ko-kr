---
title: "MDSCHEMA_MEASUREGROUP_DIMENSIONS 행 집합 | Microsoft Docs"
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
apiname: MDSCHEMA_MEASUREGROUP_DIMENSIONS
apitype: NA
applies_to: SQL Server 2016 Preview
helpviewer_keywords: MDSCHEMA_MEASUREGROUP_DIMENSIONS rowset
ms.assetid: c731c06a-7382-4e50-ba0e-d8cee3ab4f28
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d94779b19769a5ee5ac9d5d10f2804114911cde
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="mdschemameasuregroupdimensions-rowset"></a>MDSCHEMA_MEASUREGROUP_DIMENSIONS 행 집합
  측정값 그룹의 차원을 열거합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_MEASUREGROUP_DIMENSIONS** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||이 측정값 그룹이 속한 카탈로그의 이름입니다. 공급자가 카탈로그를 지원하지 않는 경우**NULL** 입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||이 측정값 그룹이 속한 큐브의 이름입니다.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||측정값 그룹의 이름입니다.|  
|**MEASUREGROUP_CARDINALITY**|**DBTYPE_WSTR**||단일 차원 멤버에 대해 측정값 그룹의 측정값이 가질 수 있는 인스턴스 수입니다. 가능한 값은 다음과 같습니다.<br /><br /> **하나**<br /><br /> **많은**|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**||차원의 고유한 이름입니다.|  
|**DIMENSION_CARDINALITY**|**DBTYPE_WSTR**||측정값 그룹의 단일 인스턴스에 대해 차원 멤버가 가질 수 있는 인스턴스 수입니다. 가능한 값은 다음과 같습니다.<br /><br /> **하나**<br /><br /> **많은**|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**||차원의 계층이 표시되는지 여부를 나타내는 부울입니다.<br /><br /> 차원에서 계층을 하나 이상 볼 수 있으면 **TRUE** 를 반환하고, 그렇지 않으면 **FALSE**입니다.|  
|**DIMENSION_IS_FACT_DIMENSION**|**DBTYPE_BOOL**||차원이 팩트 차원인지 여부를 나타내는 부울입니다.<br /><br /> 차원이 팩트 차원이면 **TRUE** 를 반환하고, 그렇지 않으면 **FALSE**입니다.|  
|**DIMENSION_PATH**|**DBTYPE_HCHAPTER**||참조 차원에 대한 차원 목록입니다.|  
|**DIMENSION_GRANULARITY**|**DBTYPE_WSTR**||세분성 계층의 고유한 이름입니다.|  
  
 행 집합은 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **MEASUREGROUP_NAME**, **DIMENSION_UNIQUE_NAME**기준의 정렬을 지원합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_MEASUREGROUP_DIMENSIONS** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> 1 Visible<br /><br /> 2 Not visible<br /><br /> 기본 제한 값은 1입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP용 OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
