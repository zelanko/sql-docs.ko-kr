---
title: "MDSCHEMA_DIMENSIONS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MDSCHEMA_DIMENSIONS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d27f85dafc44caaeb4cf4f0f3b0ba613e717b962
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS 행 집합
  데이터베이스 내의 공유 차원과 전용 차원을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_DIMENSIONS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|데이터베이스의 이름입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|지원되지 않습니다.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|큐브의 이름입니다.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|차원의 이름입니다. 차원이 둘 이상의 큐브 또는 측정값 그룹의 일부인 경우 각 고유한 차원/측정값 그룹/큐브 조합마다 하나의 행이 있습니다.|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|차원의 고유한 이름입니다.|  
|**DIMENSION_GUID**|**DBTYPE_GUID**|지원되지 않습니다.|  
|**DIMENSION_CAPTION**|**DBTYPE_WSTR**|차원의 캡션입니다. 사용자 인터페이스 또는 보고서 등에서 사용자에게 차원 이름을 표시할 때 사용해야 합니다.|  
|**DIMENSION_ORDINAL**|**DBTYPE_UI4**|큐브 내 차원의 위치입니다.|  
|**DIMENSION_TYPE**|**DBTYPE_I2**|차원의 유형입니다. 유효한 값은 다음과 같습니다.<br /><br /> **MD_DIMTYPE_UNKNOWN** (**0**)<br /><br /> **MD_DIMTYPE_TIME** (**1**)<br /><br /> **MD_DIMTYPE_MEASURE** (**2**)<br /><br /> **MD_DIMTYPE_OTHER** (**3**)<br /><br /> **MD_DIMTYPE_QUANTITATIVE** (**5**)<br /><br /> **MD_DIMTYPE_ACCOUNTS** (**6**)<br /><br /> **MD_DIMTYPE_CUSTOMERS** (**7**)<br /><br /> **MD_DIMTYPE_PRODUCTS** (**8**)<br /><br /> **MD_DIMTYPE_SCENARIO** (**9**)<br /><br /> **MD_DIMTYPE_UTILIY** (**10**)<br /><br /> **MD_DIMTYPE_CURRENCY** (**11**)<br /><br /> **MD_DIMTYPE_RATES** (**12**)<br /><br /> **MD_DIMTYPE_CHANNEL** (**13**)<br /><br /> **MD_DIMTYPE_PROMOTION** (**14**)<br /><br /> **MD_DIMTYPE_ORGANIZATION** (**15**)<br /><br /> **MD_DIMTYPE_BILL_OF_MATERIALS** (**16**)<br /><br /> **MD_DIMTYPE_GEOGRAPHY** (**17**)|  
|**DIMENSION_CARDINALITY**|**DBTYPE_UI4**|키 특성의 멤버 수입니다.|  
|**DEFAULT_HIERARCHY**|**DBTYPE_WSTR**|차원의 계층입니다. 이전 버전과의 호환성을 위해 유지됩니다.|  
|**DESCRIPTION**|**DBTYPE_WSTR**|차원에 대한 알기 쉬운 설명입니다.|  
|**IS_VIRTUAL**|**DBTYPE_BOOL**|항상 **FALSE**합니다.|  
|**IS_READWRITE**|**DBTYPE_BOOL**|차원이 쓰기 가능한지 여부를 나타내는 부울입니다.<br /><br /> **True 이면** 차원이 쓰기 가능한 경우.|  
|**DIMENSION_UNIQUE_SETTINGS**|**DBTYPE_I4**|차원에 고유한 이름을 가진 멤버만 있는 경우 고유 값을 포함하는 열을 지정하는 비트맵입니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h에 정의됩니다.<br /><br /> **MDDIMENSIONS_MEMBER_KEY_UNIQUE**|  
|**DIMENSION_MASTER_UNIQUE_NAME**|**DBTYPE_WSTR**|항상 **NULL**합니다.|  
|**DIMENSION_IS_VISIBLE**|**DBTYPE_BOOL**|항상 **TRUE**합니다.<br /><br /> 참고: 차원에 하나 이상의 계층은 표시 하지 않는 한 차원이 표시 되지 않습니다.|  
  
 에 행 집합은 정렬 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **DIMENSION_NAME**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_DIMENSIONS** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**DIMENSION_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**DIMENSION_VISIBILITY**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 Visible<br /><br /> 2 Not visible|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  

