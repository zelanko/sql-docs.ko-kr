---
title: JSON_QUERY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- JSON_QUERY
- JSON_QUERY_TSQL
helpviewer_keywords:
- JSON, extracting
- JSON, querying
- JSON_QUERY function
ms.assetid: 1ab0d90f-19b6-4988-ab4f-22fdf28b7c79
caps.latest.revision: 19
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 82d4410de37601479b0f2140a709b64541578549
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="jsonquery-transact-sql"></a>JSON_QUERY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 JSON 문자열에서 개체 또는 배열을 추출합니다.  
  
 JSON 문자열에서 개체 또는 배열 대신 스칼라 값을 추출하려면 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)를 참조하세요. **JSON_VALUE**와 **JSON_QUERY**의 차이점에 대한 정보는, [JSON_VALUE 및 JSON_QUERY 비교](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
JSON_QUERY ( expression [ , path ] )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 식입니다. 일반적으로 JSON 텍스트를 포함하는 변수 또는 열의 이름입니다.  
  
 **JSON_QUERY**는 *path*로 식별된 값을 찾기 전에 *expression*에서 유효하지 않은 JSON을 찾으면 오류를 반환합니다. **JSON_QUERY**는 *path*로 식별된 값을 찾지 못할 경우 전체 텍스트를 검사한 후 *expression*에서 유효하지 않은 JSON을 찾으면 오류를 반환합니다.  
  
 *path*  
 추출할 개체 또는 배열을 지정하는 JSON 경로입니다.

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]에서 *path* 값으로 변수를 제공할 수 있습니다.

JSON 경로는 구문 분석을 위해 lax 또는 strict 모드를 지정할 수 있습니다. 구문 분석 모드를 지정하지 않으면 lax 모드가 기본값입니다. 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  

*path*의 기본값은 ‘$’입니다. 결과적으로 *path*에 값을 제공하지 않으면 **JSON_QUERY**가 입력된 *expression*을 반환합니다.

*path*의 형식이 유효하지 않으면 **JSON_QUERY**가 오류를 반환합니다.  
  
## <a name="return-value"></a>반환 값  
 nvarchar(max) 형식의 JSON 조각을 반환합니다. 반환된 값의 데이터 정렬은 입력된 식의 데이터 정렬과 동일합니다.  
  
 값이 개체 또는 배열이 아닌 경우:  
  
-   lax 모드에서 **JSON_QUERY**는 null을 반환합니다.  
  
-   strict 모드에서 **JSON_QUERY**는 오류를 반환합니다.  
  
## <a name="remarks"></a>Remarks  

### <a name="lax-mode-and-strict-mode"></a>lax 모드와 strict 모드

 다음 JSON 텍스트를 고려해 보세요.  
  
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
  
 다음 표는 lax 모드 및 strict 모드에서 **JSON_QUERY**의 동작을 비교합니다. 선택적 경로 모드 사양(lax 또는 strict)에 대한 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  
  
|경로|lax 모드에서 값을 반환합니다.|strict 모드에서 값을 반환합니다.|추가 정보|  
|----------|------------------------------|---------------------------------|---------------|  
|$|전체 JSON 텍스트를 반환합니다.|전체 JSON 텍스트를 반환합니다.|해당 사항 없음|  
|$.info.type|NULL|Error|개체 또는 배열이 아닙니다.<br /><br /> **JSON_VALUE**를 대신 사용하세요.|  
|$.info.address.town|NULL|Error|개체 또는 배열이 아닙니다.<br /><br /> **JSON_VALUE**를 대신 사용하세요.|  
|$.info."address"|N'{"town":"Bristol", "county":"Avon", "country":"England"}'|N'{"town":"Bristol", "county":"Avon", "country":"England"}'|해당 사항 없음|  
|$.info.tags|N’["Sport", "Water polo"]’|N’["Sport", "Water polo"]’|해당 사항 없음|  
|$.info.type[0]|NULL|Error|배열이 아닙니다.|  
|$.info.none|NULL|Error|속성이 없습니다.|  

### <a name="using-jsonquery-with-for-json"></a>FOR JSON과 함께 JSON_QUERY 사용

**JSON_QUERY**는 유효한 JSON 조각을 반환합니다. 결과적으로 **FOR JSON**은 **JSON_QUERY** 반환 값의 특수 문자를 이스케이프하지 않습니다.

FOR JSON을 사용하여 결과를 반환하고 이미 JSON 형식인 데이터(열 또는 식의 결과)를 포함하는 경우 *path* 매개 변수 없이 **JSON_QUERY**로 JSON 데이터를 래핑하세요.

## <a name="examples"></a>예  
  
### <a name="example-1"></a>예 1  
 다음 예에서는 쿼리 결과의 `CustomFields` 열에서 JSON 조각을 반환하는 방법을 보여줍니다.  
  
```sql  
SELECT PersonID,FullName,
 JSON_QUERY(CustomFields,'$.OtherLanguages') AS Languages
FROM Application.People
```  
  
### <a name="example-2"></a>예제 2  
다음 예에서는 FOR JSON 절의 출력에 JSON 조각을 포함하는 방법을 보여줍니다.  
  
```sql  
SELECT StockItemID, StockItemName,
         JSON_QUERY(Tags) as Tags,
         JSON_QUERY(CONCAT('["',ValidFrom,'","',ValidTo,'"]')) ValidityPeriod
FROM Warehouse.StockItems
FOR JSON PATH
```  
  
## <a name="see-also"></a>참고 항목  
 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터&#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
