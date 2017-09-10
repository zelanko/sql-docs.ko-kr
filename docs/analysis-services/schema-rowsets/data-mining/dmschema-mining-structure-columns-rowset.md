---
title: "DMSCHEMA_MINING_STRUCTURE_COLUMNS 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff811a339635f5ff914224a060e14a52e3f94d6c
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS 행 집합
  실행 중인 서버에 배포 된 모든 마이닝 구조의 개별 열에 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DMSCHEMA_MINING_STRUCTURE_COLUMNS** 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**||카탈로그 이름입니다.|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**||정규화되지 않은 스키마 이름입니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]스키마를 지원 하지 않으므로이 열은 항상 **NULL**합니다.|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**||구조 이름입니다. 이 열은 한 **NULL**합니다.|  
|**COLUMN_NAME**|**DBTYPE_WSTR**||열 이름입니다. 같은 패턴을 공유하는 열 간에만 고유성이 보장됩니다. 예를 들어 두 중첩 열이 같은 구조 내의 다른 두 중첩 테이블에 속해 있으면 이 두 열의 이름이 같을 수 있습니다.|  
|**COLUMN_GUID**|**DBTYPE_GUID**||열 GUID입니다. 열을 식별 하는 Guid를 사용 하지 않는 공급자를 반환 해야 **NULL** 이 열에 있습니다.|  
|**COLUMN_PROPID**|**DBTYPE_UI4**||열 속성 ID입니다. 열이 없는 속성 Id를 연결 하지 않는 공급자를 반환 해야 **NULL** 이 열에 있습니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 반환 **NULL** 이 열에 대 한 합니다.|  
|**ORDINAL_POSITION**|**DBTYPE_UI4**||열의 서수입니다. 열 번호는 1부터 시작됩니다. **NULL** 열에 대 한 안정적인 서 수 값이 없는 경우.|  
|**COLUMN_HASDEFAULT**|**DBTYPE_BOOL**||이 열에 기본값이 있는지 여부를 나타내는 부울입니다.<br /><br /> **True 이면** 열에는 기본값입니다.<br /><br /> **FALSE** 열에 기본값이 없는 경우 또는를 알 수 없으면 열에 기본값이 설정 여부입니다.|  
|**COLUMN_DEFAULT**|**DBTYPE_WSTR**||열의 기본값입니다. 공급자가 노출 될 수 있습니다 **DBCOLUMN_DEFAULTVALUE** 아닌 **DBCOLUMN_HASDEFAULT** (ISO 테이블)에 대 한 반환 된 행 집합에서 **icolumnsrowset:: Getcolumnsrowset**합니다.<br /><br /> 기본값은 경우 **NULL**, **COLUMN_HASDEFAULT** 은 **TRUE** 및 **COLUMN_DEFAULT** 열이는 **NULL** 값입니다.|  
|**COLUMN_FLAGS**|**DBTYPE_UI4**||열 특징을 설명하는 비트 마스크입니다. **DBCOLUMNFLAGS** 열거 형식은 비트 마스크의 비트를 지정합니다. 이 열은 한 **NULL** 값입니다. 유효한 값은 다음과 같습니다.<br /><br /> **DBCOLUMNFLAGS_ISNULLABLE** (**0x20**)<br /><br /> **DBCOLUMNFLAGS_MAYBENULL** (**0x40**)<br /><br /> **DBCOLUMNFLAGS_ISLONG** (**0x80**)|  
|**IS_NULLABLE**|**DBTYPE_BOOL**||이 열에 기본값이 있는지 여부를 나타내는 부울입니다.<br /><br /> **True 이면** 열을 포함할 수 있는 경우 **NULL**; **FALSE**, 그렇지 않으면입니다.|  
|**DATA_TYPE**|**DBTYPE_UI2**||열 데이터 형식 표시기입니다. 예를 들어<br /><br /> "**테이블**" = **DBTYPE_HCHAPTER**<br /><br /> "**텍스트**" = **DBTYPE_WCHAR**<br /><br /> "**긴**" = **DBTYPE_I8**<br /><br /> "**DOUBLE**" = **DBTYPE_R8**<br /><br /> "**날짜**" = **DBTYPE_DATE**|  
|**TYPE_GUID**|**DBTYPE_GUID**||열 데이터 형식의 GUID입니다. 데이터 형식을 식별 하는 Guid를 사용 하지 않는 공급자를 반환 해야 **NULL** 이 열에 있습니다.|  
|**때**|**DBTYPE_UI4**||열 값의 최대 길이로서 문자, 이진 또는 비트 열의 경우 이 값은 다음 중 하나입니다.<br /><br /> 열 길이가 정의되어 있으면 열의 최대 길이(문자, 바이트 또는 비트)입니다. 예를 들어 SQL 테이블에 있는 `CHAR(5)` 열의 최대 길이는 5입니다.<br /><br /> 열 길이가 정의되어 있지 않으면 데이터 형식의 최대 길이(문자, 바이트 또는 비트)입니다.<br /><br /> 열과 데이터 형식의 최대 길이가 모두 정의되어 있지 않으면 0입니다.<br /><br /> **NULL** 외 모든 유형의 열에 대 한 합니다.|  
|**CHARACTER_OCTET_LENGTH**|**DBTYPE_UI4**||열 유형이 문자 또는 이진이면 옥텟(바이트) 단위의 최대 열 길이입니다. 0 값은 열에 최대 길이가 없음을 나타냅니다. **NULL** 외 모든 유형의 열에 대 한 합니다.|  
|**NUMERIC_PRECISION**|**DBTYPE_UI2**||이외의 숫자 데이터 형식의 열의 데이터 형식이 면 열의 최대 전체 자릿수 **VARNUMERIC**; **NULL** 경우 열의 데이터 형식이 숫자가 아니거나이 **VARNUMERIC**합니다.<br /><br /> 데이터 형식과 열의 전체 자릿수 **DBTYPE_DECIMAL** 또는 **DBTYPE_NUM**ERIC 열 정의에 따라 달라 집니다.|  
|**NUMERIC_SCALE**|**DBTYPE_I2**||열 유형 표시기가 **DBTYPE_DECIMAL**, **DBTYPE_NUMERIC**또는 **DBTYPE_VARNUMERIC**이면 소수점 이하 자릿수입니다. 그렇지 않으면 이것이 **NULL**합니다.|  
|**DATETIME_PRECISION**|**DBTYPE_UI4**||열이 datetime 또는 간격 유형이면 열의 DateTime 전체 자릿수(초 소수 부분 자릿수)입니다. 이 날짜/시간 열의 데이터 형식이 아닌 경우 **NULL**합니다.|  
|**CHARACTER_SET_CATALOG**|**DBTYPE_WSTR**||문자 집합이 정의된 카탈로그 이름입니다. **NULL** 경우 공급자가 카탈로그 또는 다른 문자 집합을 지원 하지 않습니다.|  
|**CHARACTER_SET_SCHEMA**|**DBTYPE_WSTR**||문자 집합이 정의된 정규화되지 않은 스키마 이름입니다. **NULL** 공급자 스키마 또는 다른 문자 집합을 지원 하지 않는 경우.|  
|**CHARACTER_SET_NAME**|**DBTYPE_WSTR**||문자 집합 이름입니다. **NULL** 공급자는 서로 다른 문자 집합을 지원 하지 않는 경우.|  
|**COLLATION_CATALOG**|**DBTYPE_WSTR**||데이터 정렬이 정의된 카탈로그 이름입니다. **NULL** 경우 공급자가 카탈로그 또는 다른 데이터 정렬을 지원 하지 않습니다.|  
|**COLLATION_SCHEMA**|**DBTYPE_WSTR**||데이터 정렬이 정의된 정규화되지 않은 스키마 이름입니다. **NULL** 공급자 스키마 또는 다른 데이터 정렬을 지원 하지 않는 경우.|  
|**데이터 정렬 이름**|**DBTYPE_WSTR**||데이터 정렬 이름입니다 **NULL** 공급자 다른 데이터 정렬을 지원 하지 않는 경우.|  
|**DOMAIN_CATALOG**|**DBTYPE_WSTR**||도메인이 정의된 카탈로그 이름입니다. **NULL** 경우 공급자가 카탈로그 또는 도메인을 지원 하지 않습니다.|  
|**DOMAIN_SCHEMA**|**DBTYPE_WSTR**||도메인이 정의된 정규화되지 않은 스키마 이름입니다. **NULL** 공급자 스키마 또는 도메인을 지원 하지 않는 경우.|  
|**DOMAIN_NAME**|**DBTYPE_WSTR**||도메인 이름입니다. **NULL** 공급자 도메인을 지원 하지 않는 경우.|  
|**DESCRIPTION**|**DBTYPE_WSTR**||사람이 읽을 수 있는 열 설명입니다. **NULL** 는 열에 연결 된 설명이 없습니다.|  
|**DISTRIBUTION_FLAG**|**DBTYPE_WSTR**||마이닝 구조 열의 분포입니다.<br /><br /> "**보통**"<br /><br /> "**LOG_NORM**AL"<br /><br /> "**UNIFORM**"|  
|**CONTENT_TYPE**|**DBTYPE_WSTR**||마이닝 구조 열의 내용 유형입니다.<br /><br /> "**키**"<br /><br /> "**이산**"<br /><br /> "**CONTINUOUS**"<br /><br /> "**DISCRETIZED (**[args]**)**"<br /><br /> "**ORDERED**"<br /><br /> "**SEQUENCE_TIME**"<br /><br /> "**CYCLICAL**"<br /><br /> "**확률**"<br /><br /> "**분산**"<br /><br /> "**STDEV**"<br /><br /> "**지원**"<br /><br /> "**PROBABILITY_VARIANCE**"<br /><br /> "**PROBABILITY_STDEV**"|  
|**MODELING_FLAG**|**DBTYPE_WSTR**||쉼표로 구분된 모델링 플래그 목록입니다. 지원 되는 유일한 플래그는 구조 열에 대 한 "**NOT NULL**"입니다.|  
|**IS_RELATED_TO_KEY**|**DBTYPE_BOOL**||이 열이 키와 관련되어 있는지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 이 열; 키와 관련 된 경우 **VARIANT_FALSE** 그렇지 않은 경우. 키가 단일 열 이면는 **RELATED_ATTRIBUTE** 필드 필요에 따라 수에 열 이름이 포함 됩니다.|  
|**RELATED_ATTRIBUTE**|**DBTYPE_WSTR**||현재 열이 관련되거나 특수 속성을 갖는 대상 열의 이름입니다.|  
|**CONTAINING_COLUMN**|**DBTYPE_WSTR**||이름에서 **테이블** 이 열이 포함 된 열입니다. **NULL** 없는 테이블의 열이 포함 되어 있습니다.|  
|**IS_POPULATED**|**DBTYPE_BOOL**||이 열이 사용 가능한 값 집합을 알고 있는지 여부를 나타내는 부울입니다.<br /><br /> **True 이면** 열이; 가능한 값의 집합을 알고 있는 경우 **FALSE**, 그렇지 않으면입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 **DMSCHEMA_MINING_STRUCTURE_COLUMNS** 다음 테이블의 열에 행 집합으로 제한 될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|**STRUCTURE_CATALOG**|**DBTYPE_WSTR**|(선택 사항)|  
|**STRUCTURE_SCHEMA**|**DBTYPE_WSTR**|(선택 사항)|  
|**STRUCTURE_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
|**COLUMN_NAME**|**DBTYPE_WSTR**|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 마이닝 스키마 행 집합](../../../analysis-services/schema-rowsets/data-mining/data-mining-schema-rowsets.md)  
  
  
