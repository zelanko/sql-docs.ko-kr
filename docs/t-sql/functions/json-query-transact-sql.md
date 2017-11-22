---
title: JSON_QUERY (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: "19"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 310d85e26226cd54eff5d1c99e94b235348a90f7
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 JSON 문자열에서 개체 또는 배열을 추출합니다.  
  
 배열 또는 개체 대신 JSON 문자열에서 스칼라 값을 추출 하려면 참조 [JSON_VALUE &#40; Transact SQL &#41; ](../../t-sql/functions/json-value-transact-sql.md). 간의 차이점에 대 한 정보에 대 한 **JSON_VALUE** 및 **JSON_QUERY**, 참조 [비교 JSON_VALUE 및 JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 식입니다. 일반적으로 JSON 텍스트를 포함 하는 열 또는 변수 이름입니다.  
  
 경우 **JSON_QUERY** JSON에 유효 하지 않은 찾습니다 *식* 로 식별 되는 값을 찾기 전에 *경로*, 함수는 오류를 반환 합니다. 경우 **JSON_QUERY** 로 식별 되는 값을 찾지 못하면 *경로*, 전체 텍스트 검색 및 반환 하는 JSON 발견 되 면 오류가 아무 곳 이나 유효 하지 않습니다. *식*합니다.  
  
 *경로*  
 개체 또는 배열 추출 하려면 지정 하는 JSON 경로가 있습니다.

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]의 값으로 변수를 제공할 수 있습니다 *경로*합니다.

JSON 경로 구문 분석을 위한 lax 또는 strict 모드를 지정할 수 있습니다. 구문 분석 모드를 지정 하지 않으면, lax 모드는 기본값입니다. 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  

에 대 한 기본값 *경로* '$'가 있습니다. 에 대 한 값을 제공 하지 않으면 결과적으로 *경로*, **JSON_QUERY** 입력 반환 *식*합니다.

경우 형식의 *경로* 유효 하지 **JSON_QUERY** 에서 오류를 반환 합니다.  
  
## <a name="return-value"></a>반환 값  
 JSON 조각 형식 nvarchar (max)를 반환합니다. 반환된 된 값의 데이터 정렬은 입력된 식의 데이터 정렬과 동일 합니다.  
  
 값이 개체 또는 배열을 아닙니다.  
  
-   Lax 모드로 **JSON_QUERY** null을 반환 합니다.  
  
-   Strict 모드에서는 **JSON_QUERY** 에서 오류를 반환 합니다.  
  
## <a name="remarks"></a>주의  

### <a name="lax-mode-and-strict-mode"></a>Lax 모드와 strict 모드

 다음 JSON 텍스트를 살펴보십시오.  
  
```json  
{
    "info": {
        "type": 1,
        "address": {
            "town": "Bristol",
            "county": "Avon",
            "country": "England"
        },
        "tags": ["Sport", "Water polo"]
    },
    "type": "Basic"
} 
```  
  
 다음 표에서 비교의 동작 **JSON_QUERY** lax 모드와 strict 모드에서. 선택적인 path 모드 사양 (lax 또는 strict)에 대 한 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|경로|Lax 모드에서 값을 반환 합니다.|Strict 모드에서는 반환 값|추가 정보|  
|----------|------------------------------|---------------------------------|---------------|  
|$|전체 JSON 텍스트를 반환합니다.|전체 JSON 텍스트를 반환합니다.|해당 사항 없음|  
|$. info.type|NULL|오류|개체 또는 배열 되지 않습니다.<br /><br /> 사용 하 여 **JSON_VALUE** 대신 합니다.|  
|$. info.address.town|NULL|오류|개체 또는 배열 되지 않습니다.<br /><br /> 사용 하 여 **JSON_VALUE** 대신 합니다.|  
|$.info입니다. " address "|N'{"동": "로마", "군": "Avon", "국가": "England"을 (를) '|N'{"동": "로마", "군": "Avon", "국가": "England"을 (를) '|해당 사항 없음|  
|$. info.tags|N '["스포츠", "물 polo"]'|N '["스포츠", "물 polo"]'|해당 사항 없음|  
|$. info.type[0]|NULL|오류|배열 되지 않습니다.|  
|$. info.none|NULL|오류|속성이 존재 하지 않습니다.|  

### <a name="using-jsonquery-with-for-json"></a>FOR JSON JSON_QUERY 사용

**JSON_QUERY** 유효한 JSON 조각을 반환 합니다. 결과적으로, **FOR JSON** 의 특수 문자를 이스케이프 하지 않습니다는 **JSON_QUERY** 값을 반환 합니다.

FOR json 결과 반환 하는 JSON 형식 (열에서 또는 식의 결과로)에 이미 있는 데이터를 포함 하는 경우 사용 하 여 JSON 데이터를 래핑할 **JSON_QUERY** 없이 *경로* 매개 변수입니다.

## <a name="examples"></a>예  
  
### <a name="example-1"></a>예제 1  
 JSON 조각을 반환 하는 방법을 보여 주는 다음 예제는 `CustomFields` 쿼리 결과 열에에서 있습니다.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>예제 2  
다음 예에서는 FOR JSON 절의 출력에 JSON 조각을 포함 하는 방법을 보여 줍니다.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>관련 항목:  
 [JSON 경로 식 &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터 &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
