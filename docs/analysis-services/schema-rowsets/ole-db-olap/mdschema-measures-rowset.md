---
title: "MDSCHEMA_MEASURES 행 집합 | Microsoft Docs"
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
- MDSCHEMA_MEASURES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- MDSCHEMA_MEASURES rowset
ms.assetid: 6ff5bd1a-aad0-49b8-9f8d-7df2637caacf
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c77b91b179e360f539549cda05d0a17f0697ee56
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="mdschemameasures-rowset"></a>MDSCHEMA_MEASURES 행 집합
  큐브 내의 각 측정값을 설명합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **MDSCHEMA_MEASURES** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**||이 측정값이 속한 카탈로그의 이름입니다. 공급자가 카탈로그를 지원하지 않는 경우**NULL** 입니다.|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**||이 측정값이 속한 스키마의 이름입니다. **NULL** 공급자 스키마를 지원 하지 않는 경우.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||이 측정값이 속한 큐브의 이름입니다.|  
|**MEASURE_NAME**|**DBTYPE_WSTR**||측정값 이름입니다.|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**||측정값의 고유한 이름입니다. 자격에 따라 고유한 이름을 생성하는 공급자의 경우 이 이름의 각 구성 요소는 구분 기호로 분리됩니다.|  
|**MEASURE_CAPTION**|**DBTYPE_WSTR**||측정값과 연결된 레이블 또는 캡션입니다. 주로 표시 목적으로 사용됩니다. 캡션이 없는 경우 **MEASURE_NAME** 반환 됩니다.|  
|**MEASURE_GUID**|**DBTYPE_GUID**||지원되지 않습니다.|  
|**MEASURE_AGGREGATOR**|**DBTYPE_I4**||측정값이 파생된 방식을 식별하는 열거형입니다. 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **MDMEASURE_AGGR_SUM** (**1**)에서 측정값이 집계 됨을 식별 **SUM**합니다.<br /><br /> **MDMEASURE_AGGR_COUNT** (**2**)에서 측정값이 집계 됨을 식별 **COUNT**합니다.<br /><br /> **MDMEASURE_AGGR_MIN** (**3**)에서 측정값이 집계 됨을 식별 **MIN**합니다.<br /><br /> **MDMEASURE_AGGR_MAX** (**4**)에서 측정값이 집계 됨을 식별 **최대**합니다.<br /><br /> **MDMEASURE_AGGR_AVG** (**5**)에서 측정값이 집계 됨을 식별 **AVG**합니다.<br /><br /> **MDMEASURE_AGGR_VAR** (**6**)에서 측정값이 집계 됨을 식별 **VAR**합니다.<br /><br /> **MDMEASURE_AGGR_STD** (**7**)에서 측정값이 집계 됨을 식별 **STDEV**합니다.<br /><br /> **MDMEASURE_AGGR_DST** (**8**)에서 측정값이 집계 됨을 식별 **고유 카운트**합니다.<br /><br /> **MDMEASURE_AGGR_NONE** (**9**)에서 측정값이 집계 됨을 식별 **NONE**합니다.<br /><br /> **MDMEASURE_AGGR_AVGCHILDREN** (**10**)에서 측정값이 집계 됨을 식별 **AVERAGEOFCHILDREN**합니다.<br /><br /> **MDMEASURE_AGGR_FIRSTCHILD** (**11**)에서 측정값이 집계 됨을 식별 **FIRSTCHILD**합니다.<br /><br /> **MDMEASURE_AGGR_LASTCHILD** (**12**)에서 측정값이 집계 됨을 식별 **LASTCHILD**합니다.<br /><br /> **MDMEASURE_AGGR_FIRSTNONEMPTY** (**13**)에서 측정값이 집계 됨을 식별 **FIRSTNONEMPTY**,<br /><br /> **MDMEASURE_AGGR_LASTNONEMPTY** (**14**)에서 측정값이 집계 됨을 식별 **LASTNONEMPTY**합니다.<br /><br /> **MDMEASURE_AGGR_BYACCOUNT** (**15**)에서 측정값이 집계 됨을 식별 **BYACCOUNT**합니다.<br /><br /> **MDMEASURE_AGGR_CALCULATED** (**127**) 측정값이 위의 단일 함수가 아닌 한 수식에서 파생 되었음을 식별 합니다.<br /><br /> **MDMEASURE_AGGR_UNKNOWN** (**0**) 측정값이 알 수 없는 집계 함수나 수식에서 파생 되었음을 식별 합니다.|  
|**DATA_TYPE**|**DBTYPE_UI2**||측정값의 데이터 형식입니다.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||측정값 개체의 데이터 형식이 정확한 숫자인 경우 속성의 최대 전체 자릿수입니다. **NULL** 다른 모든 속성 유형에 대해 합니다.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||측정값 개체의 유형 표시기가 있는 경우 소수점 오른쪽 자릿수 **DBTYPE_NUMERIC** 또는 **DBTYPE_DECIMAL**합니다. 그렇지 않으면이 값은 **NULL**합니다.|  
|**MEASURE_UNITS**|**DBTYPE_WSTR**||지원되지 않음|  
|**DESCRIPTION**|**DBTYPE_WSTR**||측정값에 대한 사람이 읽을 수 있는 설명입니다. **NULL** 설명이 없는 경우.|  
|**식**|**DBTYPE_WSTR**||멤버에 대한 식입니다.|  
|**MEASURE_IS_VISIBLE**|**DBTYPE_BOOL**||항상 True를 반환하는 부울입니다. 측정값을 볼 수 없으면 스키마 행 집합에 포함되지 않습니다.|  
|**LEVELS_LIST**|**DBTYPE_WSTR**||항상 반환 하는 문자열 **NULL**합니다.|  
|**MEASURE_NAME_SQL_COLUMN_NAME**|**DBTYPE_WSTR**||측정값의 이름에 해당하는 SQL 쿼리의 열 이름입니다.|  
|**MEASURE_UNQUALIFIED_CAPTION**|**DBTYPE_WSTR**||측정값 그룹 이름으로 한정되지 않은 측정값의 이름입니다.|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**||측정값이 속한 측정값 그룹의 이름입니다.|  
|**MEASURE_DISPLAY_FOLDER**|**DBTYPE_WSTR**||사용자 인터페이스에 측정값을 표시할 때 사용할 경로입니다. 폴더 이름은 세미콜론으로 구분됩니다. 중첩 된 폴더에 백슬래시가 표시 됩니다 (\\).|  
|**DEFAULT_FORMAT_STRING**|**DBTYPE_WSTR**||측정값의 기본 형식 문자열입니다.|  
  
 에 행 집합은 정렬 **CATALOG_NAME**, **SCHEMA_NAME**, **CUBE_NAME**, **MEASURE_NAME**합니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **MDSCHEMA_MEASURES** 행 집합은 다음 표에 나열 된 열에 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**CATALOG_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**SCHEMA_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEASURE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEASURE_UNIQUE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**MEASUREGROUP_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**CUBE_SOURCE**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 CUBE<br /><br /> 2 DIMENSION|  
|**MEASURE_VISIBILITY**|**DBTYPE_UI2**|(선택 사항) 기본 제한 값 1은 합니다. 유효한 값 중 하나를 사용 하는 비트맵.<br /><br /> 1 Visible<br /><br /> 2 Not Visible|  
  
## <a name="see-also"></a>관련 항목:  
 [OLAP 스키마 행 집합 용 OLE DB](../../../analysis-services/schema-rowsets/ole-db-olap/ole-db-for-olap-schema-rowsets.md)  
  
  
