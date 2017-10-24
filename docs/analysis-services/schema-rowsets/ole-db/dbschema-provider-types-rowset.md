---
title: "DBSCHEMA_PROVIDER_TYPES 행 집합 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DBSCHEMA_PROVIDER_TYPES
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DBSCHEMA_PROVIDER_TYPES rowset
ms.assetid: 255e01ba-53a9-478d-9b86-45faba76710e
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6906aec1d1c1dd53b8c833d59483aa0453cf284b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="dbschemaprovidertypes-rowset"></a>DBSCHEMA_PROVIDER_TYPES 행 집합
  데이터 공급자가 지원하는 기본 데이터 형식을 식별합니다.  
  
## <a name="rowset-columns"></a>행 집합 열  
 **DBSCHEMA_PROVIDER_TYPES** 행 집합에는 다음 열이 포함되어 있습니다.  
  
|열 이름|유형 표시기|Description|  
|-----------------|--------------------|-----------------|  
|**TYPE_NAME**|**DBTYPE_WSTR**|공급자별 데이터 형식 이름입니다.|  
|**DATA_TYPE**|**DBTYPE_UI2**|데이터 형식의 표시기입니다.|  
|**COLUMN_SIZE**|**DBTYPE_UI4**|최대 길이 또는 공급자에서 이 형식에 정의한 길이를 참조하는 숫자가 아닌 열 또는 매개 변수의 길이입니다. 문자 데이터의 경우 문자 단위의 최대 길이 또는 정의된 길이입니다. DateTime 데이터 형식의 경우 문자열 표현의 길이입니다(소수 자릿수 초 구성 요소가 최대 허용 전체 자릿수라고 가정).<br /><br /> 데이터 형식이 숫자이면 이것은 데이터 형식의 최대 전체 자릿수에 대한 상한입니다.|  
|**LITERAL_PREFIX**|**DBTYPE_WSTR**|텍스트 명령에서 이 형식의 리터럴에 접두사로 사용할 문자(들)입니다.|  
|**LITERAL_SUFFIX**|**DBTYPE_WSTR**|텍스트 명령에서 이 형식의 리터럴에 접미사로 사용할 문자(들)입니다.|  
|**CREATE_PARAMS**|**DBTYPE_WSTR**|이 데이터 형식의 열을 만들 때 소비자가 지정한 생성 매개 변수입니다. 예를 들어, SQL 데이터 형식 **DECIMAL,** 에 전체 자릿수와 소수 자릿수가 필요합니다. 이 경우 생성 매개 변수는 "precision,scale" 문자열일 수 있습니다. 전체 자릿수 10, 소수 자릿수 2를 사용하여 **DECIMAL** 열을 만드는 텍스트 명령에서 **TYPE_NAME** 열의 값은 **DECIMAL()** 이 되고 완전한 유형 사양은 **DECIMAL(10,2)**입니다.<br /><br /> 생성 매개 변수는 쉼표로 구분된 값 목록으로 나타나며 매개 변수가 공급되는 순서대로 괄호 없이 표시됩니다. 생성 매개 변수가 길이, 최대 길이, 전체 자릿수, 소수 자릿수, 초기값, 증분인 경우 각각 "length", "max length", "precision", "scale", "seed", "increment"를 사용하십시오. 생성 매개 변수가 그 밖의 다른 값이면 공급자가 생성 매개 변수를 설명하는 데 사용할 텍스트를 결정합니다.<br /><br /> 데이터 형식에 생성 매개 변수가 필요하면 대개 형식 이름에 "()"가 나타납니다. 이는 생성 매개 변수를 삽입할 위치를 나타냅니다. 형식 이름에 "()"가 없으면 생성 매개 변수가 괄호로 묶여서 데이터 형식 이름에 첨부됩니다.|  
|**IS_NULLABLE**|**DBTYPE_BOOL**|데이터 형식이 null을 허용하는지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 null을 허용하는 데이터 형식임을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 null을 허용하지 않는 데이터 형식임을 나타냅니다.<br /><br /> **NULL**- 데이터 형식이 null을 허용하는지 여부를 알 수 없음을 나타냅니다.|  
|**CASE_SENSITIVE**|**DBTYPE_BOOL**|데이터 형식이 문자 유형이고 대/소문자를 구분하는지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 데이터 형식이 문자 유형이고 대/소문자를 구분함을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 데이터 형식이 문자 유형이 아니거나 대/소문자를 구분하지 않음을 나타냅니다.|  
|**검색 가능한**|**DBTYPE_UI4**|공급자가 **ICommandText**를 지원하는 경우 데이터 형식이 검색에 사용되는 방식을 나타내는 정수입니다. 그렇지 않으면 **NULL**입니다. 이 열에는 다음과 같은 값이 올 수 있습니다.<br /><br /> **DB_UNSEARCHABLE** 은 **WHERE** 절에서 데이터 형식을 사용할 수 없음을 나타냅니다.<br /><br /> **DB_LIKE_ONLY** 는 **WHERE** 조건자만 있는 **LIKE** 절에서 데이터 형식을 사용할 수 있음을 나타냅니다.<br /><br /> **DB_ALL_EXCEPT_LIKE** 는 **WHERE** 를 제외한 모든 비교 연산자가 있는 **LIKE**절에서 데이터 형식을 사용할 수 있음을 나타냅니다.<br /><br /> **DB_SEARCHABLE** 은 임의의 비교 연산자가 있는 **WHERE** 절에서 데이터 형식을 사용할 수 있음을 나타냅니다.|  
|**UNSIGNED_ATTRIBUTE**|**DBTYPE_BOOL**|데이터 형식이 부호 없는 형식인지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 데이터 형식이 부호 없는 형식임을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 데이터 형식이 부호 있는 형식임을 나타냅니다.<br /><br /> **NULL** 은 데이터 형식에 적용할 수 없음을 나타냅니다.|  
|**FIXED_PREC_SCALE**|**DBTYPE_BOOL**|데이터 형식이 고정 전체 자릿수 및 소수 자릿수를 갖는지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 데이터 형식이 고정 전체 자릿수 및 소수 자릿수를 가짐을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 데이터 형식이 고정 전체 자릿수 및 소수 자릿수를 갖지 않음을 나타냅니다.|  
|**AUTO_UNIQUE_VALUE**|**DBTYPE_BOOL**|데이터 형식이 자동 증가인지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 이 형식의 값이 자동 증가할 수 있음을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 이 형식의 값이 자동 증가할 수 없음을 나타냅니다.<br /><br /> 이 값이 **VARIANT_TRUE**이면 공급자의 **DBPROP_COL_AUTOINCREMENT** 열 속성에 따라 이 형식의 열이 항상 자동 증가되는지 여부가 결정됩니다. **DBPROP_COL_AUTOINCREMENT** 속성이 읽기/쓰기이면 **DBPROP_COL_AUTOINCREMENT** 속성의 설정에 따라 이 형식의 열이 자동 증가되는지 여부가 결정됩니다. **DBPROP_COL_AUTOINCREMENT** 가 읽기 전용 속성이면 이 형식의 열이 전부 자동 증가하거나 아무것도 자동 증가하지 않습니다.|  
|**LOCAL_TYPE_NAME**|**DBTYPE_WSTR**|**TYPE_NAME**의 지역화된 버전입니다. 데이터 공급자가 지역화된 이름을 지원하지 않는 경우에는**NULL** 이 반환됩니다.|  
|**MINIMUM_SCALE**|**DBTYPE_I2**|유형 표시기가 **DBTYPE_VARNUMERIC**, **DBTYPE_DECIMAL**또는 **DBTYPE_NUMERIC**인 경우 소수점 오른쪽에 허용되는 최소 자릿수입니다. 그렇지 않으면 **NULL**입니다.|  
|**MAXIMUM_SCALE**|**DBTYPE_I2**|유형 표시기가 **DBTYPE_VARNUMERIC**, **DBTYPE_DECIMAL**또는 **DBTYPE_NUMERIC**인 경우 소수점 오른쪽에 허용되는 최대 자릿수입니다. 그렇지 않으면**U**입니다.|  
|**GUID**|**DBTYPE_GUID**|(나중에 사용할 계획) 형식이 형식 라이브러리에 설명되어 있는 경우 형식의 **GUID** 입니다. 그렇지 않으면 **NULL**입니다.|  
|**형식 라이브러리**|**DBTYPE_WSTR**|(나중에 사용할 계획) 형식이 형식 라이브러리에 설명되어 있는 경우 형식 설명을 포함하는 형식 라이브러리입니다. 그렇지 않으면 NULL입니다.|  
|**버전**|**DBTYPE_WSTR**|(나중에 사용할 계획) 형식 정의의 버전입니다. 공급자가 형식 정의를 버전 지정할 수 있습니다. 공급자마다 타임스탬프나 숫자(integer 또는 float)와 같은 서로 다른 버전 지정 체계를 사용할 수 있습니다. 지원되지 않으면**NULL** 입니다.|  
|**있는 IS_LONG**|**DBTYPE_BOOL**|데이터 형식이 BLOB(binary large object)이고 매우 긴 데이터를 포함하는지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 데이터 형식이 매우 긴 데이터를 포함하는 **BLOB** 임을 나타냅니다. 매우 긴 데이터의 정의는 공급자별로 다릅니다.<br /><br /> **VARIANT_FALSE** 는 데이터 형식이 매우 긴 데이터를 포함하지 않는 **BLOB** 이거나, **BLOB**이 아님을 나타냅니다<br /><br /> 이 값에 따라 **DBCOLUMNFLAGS_ISLONG** 의 **GetColumnInfo** 와 **IColumnsInfo** 의 **GetParameterInfo** 에서 반환되는 **ICommandWithParameters**플래그의 설정이 결정됩니다.|  
|**BEST_MATCH**|**DBTYPE_BOOL**|데이터 형식이 가장 일치하는 항목인지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 해당 데이터 형식이 데이터 저장소에 있는 모든 데이터 형식과 **DATA_TYPE** 열의 값이 지시하는 OLE DB 데이터 형식 중에서 가장 일치하는 항목임을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 해당 데이터 형식이 가장 일치하는 항목이 아님을 나타냅니다.<br /><br /> **DATA_TYPE** 열 값이 같은 행 집합의 경우 **BEST_MATCH** 열이 행 하나에만 **VARIANT_TRUE** 로 설정되어 있습니다.|  
|**IS_FIXEDLENGTH**|**DBTYPE_BOOL**|열 길이가 고정되는지 여부를 나타내는 부울입니다.<br /><br /> **VARIANT_TRUE** 는 DDL(데이터 정의 언어)로 만든 이 형식의 열이 고정 길이임을 나타냅니다.<br /><br /> **VARIANT_FALSE** 는 DDL로 만든 이 형식의 열이 가변 길이임을 나타냅니다.<br /><br /> 필드가 **NULL**이면 공급자가 이 필드를 고정 길이 열로 매핑할지 가변 길이 열로 매핑할지 알 수 없습니다.|  
  
 행 집합은 **DATA_TYPE**을 기준으로 정렬됩니다.  
  
## <a name="restriction-columns"></a>제한 열  
 **DBSCHEMA_PROVIDER_TYPES** 행 집합은 다음 표의 열을 기준으로 제한될 수 있습니다.  
  
|열 이름|유형 표시기|  
|-----------------|--------------------|  
|**DATA_TYPE**|**DBTYPE_UI2**|  
|**BEST_MATCH**|**DBTYPE_BOOL**|  
  
## <a name="see-also"></a>관련 항목:  
 [OLE DB 스키마 행 집합](../../../analysis-services/schema-rowsets/ole-db/ole-db-schema-rowsets.md)  
  
  

