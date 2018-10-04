---
title: MDSCHEMA_DIMENSIONS 행 집합 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MDSCHEMA_DIMENSIONS
topic_type:
- apiref
helpviewer_keywords:
- MDSCHEMA_DIMENSIONS rowset
ms.assetid: a0fd94bb-359a-4df6-93a6-d60d50223944
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 49cd8f4f01840b67cde31d9031320ac276ec6faa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48152640"
---
# <a name="mdschemadimensions-rowset"></a>MDSCHEMA_DIMENSIONS 행 집합
  데이터베이스 내의 공유 차원과 전용 차원을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `MDSCHEMA_DIMENSIONS` 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`||데이터베이스의 이름입니다.|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`||지원되지 않습니다.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||큐브의 이름입니다.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||차원의 이름입니다. 차원이 둘 이상의 큐브 또는 측정값 그룹의 일부인 경우 각 고유한 차원/측정값 그룹/큐브 조합마다 하나의 행이 있습니다.|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`||차원의 고유한 이름입니다.|  
|`DIMENSION_GUID`|`DBTYPE_GUID`||지원되지 않습니다.|  
|`DIMENSION_CAPTION`|`DBTYPE_WSTR`||차원의 캡션입니다. 사용자 인터페이스 또는 보고서 등에서 사용자에게 차원 이름을 표시할 때 사용해야 합니다.|  
|`DIMENSION_ORDINAL`|`DBTYPE_UI4`||큐브 내 차원의 위치입니다.|  
|`DIMENSION_TYPE`|`DBTYPE_I2`||차원의 유형입니다. 유효한 값은 다음과 같습니다.<br /><br /> -   `MD_DIMTYPE_UNKNOWN` (`0`)<br />-   `MD_DIMTYPE_TIME` (`1`)<br />-   `MD_DIMTYPE_MEASURE` (`2`)<br />-   `MD_DIMTYPE_OTHER` (`3`)<br />-   `MD_DIMTYPE_QUANTITATIVE` (`5`)<br />-   `MD_DIMTYPE_ACCOUNTS` (`6`)<br />-   `MD_DIMTYPE_CUSTOMERS` (`7`)<br />-   `MD_DIMTYPE_PRODUCTS` (`8`)<br />-   `MD_DIMTYPE_SCENARIO` (`9`)<br />-   `MD_DIMTYPE_UTILIY` (`10`)<br />-   `MD_DIMTYPE_CURRENCY` (`11`)<br />-   `MD_DIMTYPE_RATES` (`12`)<br />-   `MD_DIMTYPE_CHANNEL` (`13`)<br />-   `MD_DIMTYPE_PROMOTION` (`14`)<br />-   `MD_DIMTYPE_ORGANIZATION` (`15`)<br />-   `MD_DIMTYPE_BILL_OF_MATERIALS` (`16`)<br />-   `MD_DIMTYPE_GEOGRAPHY` (`17`)|  
|`DIMENSION_CARDINALITY`|`DBTYPE_UI4`||키 특성의 멤버 수입니다.|  
|`DEFAULT_HIERARCHY`|`DBTYPE_WSTR`||차원의 계층입니다. 이전 버전과의 호환성을 위해 유지됩니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||차원에 대한 알기 쉬운 설명입니다.|  
|`IS_VIRTUAL`|`DBTYPE_BOOL`||항상 `FALSE`입니다.|  
|`IS_READWRITE`|`DBTYPE_BOOL`||차원이 쓰기 가능한지 여부를 나타내는 부울입니다.<br /><br /> 차원이 쓰기 가능하도록 설정된 경우 `TRUE`입니다.|  
|`DIMENSION_UNIQUE_SETTINGS`|`DBTYPE_I4`||차원에 고유한 이름을 가진 멤버만 있는 경우 고유 값을 포함하는 열을 지정하는 비트맵입니다. 이 비트맵에 대해 다음 비트 값 상수가 Msmd.h에 정의됩니다.<br /><br /> -   `MDDIMENSIONS_MEMBER_KEY_UNIQUE`|  
|`DIMENSION_MASTER_UNIQUE_NAME`|`DBTYPE_WSTR`||항상 `NULL`입니다.|  
|`DIMENSION_IS_VISIBLE`|`DBTYPE_BOOL`||항상 `TRUE`입니다. **참고:** 차원을 표시 되지 않는 차원에 하나 이상의 계층 구조를 표시 합니다.|  
  
 행 집합은 `CATALOG_NAME`, `SCHEMA_NAME`, `CUBE_NAME`, `DIMENSION_NAME`을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 `MDSCHEMA_DIMENSIONS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`CATALOG_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`SCHEMA_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`DIMENSION_UNIQUE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`CUBE_SOURCE`|`DBTYPE_UI2`|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> -1 큐브<br />-2 차원<br /><br /> 기본 제한 값은 1입니다.|  
|`DIMENSION_VISIBILITY`|`DBTYPE_UI2`|다음 유효 값 중 하나가 포함된 비트맵입니다(선택 사항).<br /><br /> -1 표시<br />-2 not 표시<br /><br /> 기본 제한 값은 1입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [OLAP용 OLE DB 스키마 행 집합](ole-db-for-olap-schema-rowsets.md)  
  
  
