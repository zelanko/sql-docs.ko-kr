---
title: "JSON 경로 식(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 01/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: json
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 8562b8dd2ab6ef2bea5edc5e5a3f751589bd9237
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="json-path-expressions-sql-server"></a>JSON 경로 식(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 JSON 경로 식을 사용하여 JSON 개체의 속성을 참조합니다.  
  
 다음 함수를 호출하는 경우 경로 식을 제공해야 합니다.  
  
-   JSON 데이터의 관계형 뷰를 만들기 위해 **OPENJSON** 을(를) 호출하는 경우. 자세한 내용은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
-   JSON 텍스트에서 값을 추출하기 위해 **JSON_VALUE** 를 호출하는 경우. 자세한 내용은 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)을 참조하세요.  
  
-   JSON 개체 또는 배열을 추출하기 위해 **JSON_QUERY** 를 호출하는 경우. 자세한 내용은 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)을 참조하세요.  
  
-   JSON 문자열에서 속성의 값을 업데이트하기 위해 **JSON_MODIFY**를 호출하는 경우. 자세한 내용은 [JSON_MODIFY&#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)을 참조하세요.  

## <a name="parts-of-a-path-expression"></a>경로 식의 요소
 경로 식에는 두 가지 구성 요소가 있습니다.  
  
1.  값이 **lax** 또는 **strict**인 선택적 [Path 모드](#PATHMODE)  
  
2.  [PATH](#PATH) 자체.  

##  <a name="PATHMODE"></a> Path mode  
 경로 식의 시작 부분에서 키워드 **lax** 또는 **strict**을(를) 지정하여 PATH 모드를 선택적으로 선언합니다. 기본값은 **lax**입니다.  
  
-   **lax** 모드에서 경로 식에 오류가 포함되어 있으면 함수는 빈 값을 반환합니다. 예를 들어 **$.name** 값을 요청했는데 JSON 텍스트에 **name** 키가 포함되어 있지 않으면 함수는 null을 반환하지만 오류를 발생시키지 않습니다.  
  
-   **strict** 모드에서 경로 식에 오류가 있으면 함수는 오류를 발생시킵니다.  

다음 쿼리는 경로 식에 `lax` 모드를 명시적으로 지정합니다.

```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{ ... }'

SELECT * FROM OPENJSON(@json, N'lax $.info')
```  
  
##  <a name="PATH"></a> Path  
 선택적인 PATH 모드 선언 후, PATH를 지정합니다.  
  
-   달러 기호(`$`)는 컨텍스트 항목을 나타냅니다.  
  
-   속성 경로는 경로 단계의 집합입니다. 경로 단계는 다음 요소와 연산자를 포함할 수 있습니다.  
  
    -   키 이름. 예를 들면 `$.name` 및 `$."first name"`입니다. 키 이름이 달러 기호로 시작되거나 공백과 같은 특수 기호를 포함하는 경우, 따옴표로 묶습니다.   
  
    -   배열 요소 `$.product[3]`)을 입력합니다. 배열은 0부터 시작됩니다.  
  
    -   점 연산자(`.`)는 개체의 멤버를 나타냅니다. 예를 들어 `$.people[1].surname`에서 `surname`은 `people`의 자식입니다.
  
## <a name="examples"></a>예  
 이 섹션의 예는 다음 JSON 텍스트를 참조합니다.  
  
```json  
{
    "people": [{
        "name": "John",
        "surname": "Doe"
    }, {
        "name": "Jane",
        "surname": null,
        "active": true
    }]
}
```  
  
 다음 테이블은 경로 식의 몇 가지 예를 보여줍니다.  
  
|경로 식|값|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## <a name="how-built-in-functions-handle-duplicate-paths"></a>기본 제공 함수에서 중복 경로를 처리하는 방법  
 JSON 텍스트에 중복된 속성(예: 수준과 이름이 같은 두 개의 키)이 포함되는 경우 **JSON_VALUE** 및 **JSON_QUERY** 함수는 경로와 일치하는 첫 번째 값만 반환합니다. 중복 키를 포함하는 JSON 개체의 구문을 분석하고 모든 값을 반환하려면 다음 예제와 같이 **OPENJSON**을 사용합니다.  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>SQL Server의 기본 제공 JSON 지원에 대한 자세한 정보  
많은 특정 솔루션, 사용 사례 및 권장 사항은 Microsoft 프로그램 관리자인 Jovan Popovic이 제공하는 SQL Server 및 Azure SQL Database의 [기본 제공 JSON 지원에 대한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.
  
## <a name="see-also"></a>관련 항목:  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  
