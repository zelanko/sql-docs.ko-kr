---
title: DMSCHEMA_MINING_STRUCTURE_COLUMNS 행 집합 | Microsoft Docs
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
api_name:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DMSCHEMA_MINING_STRUCTURE_COLUMNS rowset
ms.assetid: 81f25502-ac90-42f1-8ddf-7b0f9752ebfd
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98c8ec286e12cfe6198c36900067a26eefd5e1ad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088478"
---
# <a name="dmschemaminingstructurecolumns-rowset"></a>DMSCHEMA_MINING_STRUCTURE_COLUMNS 행 집합
  실행 중인 서버에 배포 된 모든 마이닝 구조의 개별 열에 설명 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 `DMSCHEMA_MINING_STRUCTURE_COLUMNS` 행 집합에는 다음과 같은 열을 포함 합니다.  
  
|열 이름|유형 표시기|길이|Description|  
|-----------------|--------------------|------------|-----------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`||카탈로그 이름입니다.|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`||정규화되지 않은 스키마 이름입니다. [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 스키마를 지원하지 않으므로 이 열은 항상 `NULL`입니다.|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`||구조 이름입니다. 이 열에는 `NULL`이 포함될 수 없습니다.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||열 이름입니다. 같은 패턴을 공유하는 열 간에만 고유성이 보장됩니다. 예를 들어 두 중첩 열이 같은 구조 내의 다른 두 중첩 테이블에 속해 있으면 이 두 열의 이름이 같을 수 있습니다.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||열 GUID입니다. 열을 식별하는 데 GUID를 사용하지 않는 공급자는 이 열에 `NULL`을 반환해야 합니다.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||열 속성 ID입니다. 열에 속성 ID를 연결하지 않는 공급자는 이 열에 `NULL`을 반환해야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 반환 `NULL` 이 열에 대 한 합니다.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||열의 서수입니다. 열 번호는 1부터 시작됩니다. 열에 대한 안정적인 서수 값이 없으면 `NULL`입니다.|  
|`COLUMN_HASDEFAULT`|`DBTYPE_BOOL`||이 열에 기본값이 있는지 여부를 나타내는 부울입니다.<br /><br /> 열에 기본값이 있으면 `TRUE`입니다.<br /><br /> 열에 기본값이 없거나 기본값이 있는지 알 수 없으면 `FALSE`입니다.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||열의 기본값입니다. 공급자는 `DBCOLUMN_DEFAULTVALUE`에서 반환하는 행 집합의 `DBCOLUMN_HASDEFAULT`(ISO 테이블의 경우)가 아닌 `IColumnsRowset::GetColumnsRowset`를 표시할 수 있습니다.<br /><br /> 기본값이 `NULL`이면 `COLUMN_HASDEFAULT`는 `TRUE`이고 `COLUMN_DEFAULT` 열은 `NULL` 값입니다.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||-열 특징을 설명 하는 비트 마스크입니다. `DBCOLUMNFLAGS` 열거 형식은 비트 마스크의 비트를 지정합니다. 이 열은 `NULL` 값을 포함할 수 없습니다. 유효한 값은 다음과 같습니다.<br />-   **DBCOLUMNFLAGS_ISNULLABLE** (`0x20`)<br />-   **DBCOLUMNFLAGS_MAYBENULL** (`0x40`)<br />-   **DBCOLUMNFLAGS_ISLONG** (`0x80`)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||이 열에 기본값이 있는지 여부를 나타내는 부울입니다.<br /><br /> 열에 `TRUE`이 포함될 수 있으면 `NULL`이고, 그렇지 않으면 `FALSE`입니다.|  
|`DATA_TYPE`|`DBTYPE_UI2`||열 데이터 형식 표시기입니다. 예를 들어:<br /><br /> -   "`TABLE`" = `DBTYPE_HCHAPTER`<br />-   "`TEXT`" = `DBTYPE_WCHAR`<br />-   "`LONG`" = `DBTYPE_I8`<br />-   "`DOUBLE`" = `DBTYPE_R8`<br />-   "`DATE`" = `DBTYPE_DATE`|  
|`TYPE_GUID`|`DBTYPE_GUID`||열 데이터 형식의 GUID입니다. 데이터 형식을 식별하는 데 GUID를 사용하지 않는 공급자는 이 열에 `NULL`을 반환해야 합니다.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||열 값의 최대 길이로서 문자, 이진 또는 비트 열의 경우 이 값은 다음 중 하나입니다.<br /><br /> -에 있는 열의 최대 길이 문자, 바이트 또는 비트, 각각 길이가 정의 되어 있는 경우. 예를 들어 SQL 테이블에 있는 `CHAR(5)` 열의 최대 길이는 5입니다.<br />-데이터의 최대 길이를 문자, 바이트 또는 비트를 각각 입력, 열에 정의 된 길이가 없는 경우.<br />-영 (0)의 정의 된 최대 길이 열 또는 데이터 형식이 아닙니다.<br />-   `NULL` 다른 모든 형식의 열입니다.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||열 유형이 문자 또는 이진이면 옥텟(바이트) 단위의 최대 열 길이입니다. 0 값은 열에 최대 길이가 없음을 나타냅니다. 다른 모든 열 유형의 경우에는 `NULL`입니다.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||열의 데이터 형식이 `VARNUMERIC` 이외의 숫자 데이터 형식이면 열의 최대 전체 자릿수입니다. 열의 데이터 형식이 숫자가 아니거나 `NULL`이면 `VARNUMERIC`입니다.<br /><br /> 데이터 형식이 `DBTYPE_DECIMAL` 또는 `DBTYPE_NUM`ERIC인 열의 전체 자릿수는 열 정의에 따라 달라집니다.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||열 유형 표시기가 `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC` 또는 `DBTYPE_VARNUMERIC`이면 소수점 이하 자릿수입니다. 그렇지 않으면 `NULL`입니다.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||열이 datetime 또는 간격 유형이면 열의 DateTime 전체 자릿수(초 소수 부분 자릿수)입니다. 열 데이터 형식이 datetime이 아니면 `NULL`입니다.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||문자 집합이 정의된 카탈로그 이름입니다. 공급자가 카탈로그 또는 다른 문자 집합을 지원하지 않으면 `NULL`입니다.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||문자 집합이 정의된 정규화되지 않은 스키마 이름입니다. 공급자가 스키마 또는 다른 문자 집합을 지원하지 않으면 `NULL`입니다.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||문자 집합 이름입니다. 공급자가 다른 문자 집합을 지원하지 않으면 `NULL`입니다.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||데이터 정렬이 정의된 카탈로그 이름입니다. 공급자가 카탈로그 또는 다른 데이터 정렬을 지원하지 않으면 `NULL`입니다.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||데이터 정렬이 정의된 정규화되지 않은 스키마 이름입니다. 공급자가 스키마 또는 다른 데이터 정렬을 지원하지 않으면 `NULL`입니다.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||데이터 정렬 이름입니다 공급자가 다른 데이터 정렬을 지원하지 않으면 `NULL`입니다.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||도메인이 정의된 카탈로그 이름입니다. 공급자가 카탈로그 또는 도메인을 지원하지 않으면 `NULL`입니다.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||도메인이 정의된 정규화되지 않은 스키마 이름입니다. 공급자가 스키마 또는 도메인을 지원하지 않으면 `NULL`입니다.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||도메인 이름입니다. 공급자가 도메인을 지원하지 않을 경우 `NULL`입니다.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||사람이 읽을 수 있는 열 설명입니다. 열과 관련된 설명이 없으면 `NULL`입니다.|  
|`DISTRIBUTION_FLAG`|`DBTYPE_WSTR`||마이닝 구조 열의 분포입니다.<br /><br /> -   "`NORMAL`"<br />-"`LOG_NORM`AL"<br />-   "`UNIFORM`"|  
|`CONTENT_TYPE`|`DBTYPE_WSTR`||마이닝 구조 열의 내용 유형입니다.<br /><br /> -   "`KEY`"<br />-   "`DISCRETE`"<br />-   "`CONTINUOUS`"<br />-"`DISCRETIZED(`[args]`)`"<br />-   "`ORDERED`"<br />-   "`SEQUENCE_TIME`"<br />-   "`CYCLICAL`"<br />-   "`PROBABILITY`"<br />-   "`VARIANCE`"<br />-   "`STDEV`"<br />-   "`SUPPORT`"<br />-   "`PROBABILITY_VARIANCE`"<br />-   "`PROBABILITY_STDEV`"|  
|`MODELING_FLAG`|`DBTYPE_WSTR`||쉼표로 구분된 모델링 플래그 목록입니다. 구조 열에 대해서는 "`NOT NULL`" 플래그만 지원됩니다.|  
|`IS_RELATED_TO_KEY`|`DBTYPE_BOOL`||이 열이 키와 관련되어 있는지 여부를 나타내는 부울입니다.<br /><br /> 이 열이 키와 관련되어 있으면 `VARIANT_TRUE`이고, 그렇지 않으면 `VARIANT_FALSE`입니다. 키가 단일 열이면 `RELATED_ATTRIBUTE` 필드에 열 이름이 포함될 수도 있습니다.|  
|`RELATED_ATTRIBUTE`|`DBTYPE_WSTR`||현재 열이 관련되거나 특수 속성을 갖는 대상 열의 이름입니다.|  
|`CONTAINING_COLUMN`|`DBTYPE_WSTR`||이 열이 포함되어 있는 `TABLE` 열의 이름입니다. 테이블에 열이 없으면 `NULL`입니다.|  
|`IS_POPULATED`|`DBTYPE_BOOL`||이 열이 사용 가능한 값 집합을 알고 있는지 여부를 나타내는 부울입니다.<br /><br /> 이 열이 사용 가능한 값 집합을 알고 있으면 `TRUE`이고, 그렇지 않으면 `FALSE`입니다.|  
  
## <a name="restriction-columns"></a>제한 열  
 `DMSCHEMA_MINING_STRUCTURE_COLUMNS` 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|제한 상태|  
|-----------------|--------------------|-----------------------|  
|`STRUCTURE_CATALOG`|`DBTYPE_WSTR`|(선택 사항)|  
|`STRUCTURE_SCHEMA`|`DBTYPE_WSTR`|(선택 사항)|  
|`STRUCTURE_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|(선택 사항)|  
  
## <a name="see-also"></a>관련 항목  
 [데이터 마이닝 스키마 행 집합](../../schema-rowsets/data-mining/data-mining-schema-rowsets.md) 
  
  