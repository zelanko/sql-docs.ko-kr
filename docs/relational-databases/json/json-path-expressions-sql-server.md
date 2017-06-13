---
title: "JSON 경로 식(SQL Server) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/23/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, path expressions
- path expressions (JSON)
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 44bfd54aa494dd52174eeed8479e14a99d810af3
ms.contentlocale: ko-kr
ms.lasthandoff: 06/09/2017

---
# <a name="json-path-expressions-sql-server"></a>JSON 경로 식(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

 JSON 경로 식을 사용 하 여 JSON 개체의 속성을 참조 합니다.  
  
 다음 함수를 호출하는 경우 경로 식을 제공해야 합니다.  
  
-   JSON 데이터의 관계형 뷰를 만들기 위해 **OPENJSON** 을(를) 호출하는 경우. 자세한 내용은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
-   JSON 텍스트에서 값을 추출하기 위해 **JSON_VALUE** 를 호출하는 경우. 자세한 내용은 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)을 참조하세요.  
  
-   JSON 개체 또는 배열을 추출하기 위해 **JSON_QUERY** 를 호출하는 경우. 자세한 내용은 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)을 참조하세요.  
  
-   JSON 문자열에서 속성의 값을 업데이트하기 위해 **JSON_MODIFY**를 호출하는 경우. 자세한 내용은 [JSON_MODIFY&#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)을 참조하세요.  

## <a name="parts-of-a-path-expression"></a>경로 식의 요소
 경로 식에는 두 가지 구성 요소가 있습니다.  
  
1.  선택적 [path 모드](#PATHMODE), 값이 **lax** 또는 **엄격한**합니다.  
  
2.  [PATH](#PATH) 자체.  

##  <a name="PATHMODE"></a> Path mode  
 경로 식의 시작 부분에서 키워드 **lax** 또는 **strict**을(를) 지정하여 PATH 모드를 선택적으로 선언합니다. 기본값은 **lax**입니다.  
  
-   **lax** 모드에서는 함수 반환 값이 비어 경로 식에 오류가 있습니다. 예를 들어, 값을 요청 하는 경우 **$.name**, JSON 텍스트가 포함 되어 있지는 **이름** 키, 함수가 null을 반환 되었지만 오류가 발생 하지 않습니다.  
  
-   **엄격한** 모드에서는 함수에서 오류가 발생 경로 식에 오류가 포함 되어 있습니다.  

다음 쿼리를 명시적으로 지정 `lax` 경로 식의 모드입니다.

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
  
    -   점 연산자(`.`)는 개체의 멤버를 나타냅니다. 예를 들어 `$.people[1].surname`, `surname` 의 자식인 `people`합니다.
  
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
 -동일한 수준에 같은 이름의 키 두는 예를 들어-JSON 텍스트에 중복 된 속성이 포함 하는 경우는 **JSON_VALUE** 및 **JSON_QUERY** 함수는 경로 일치 하는 첫 번째 값만 반환 합니다. 중복 키를 포함 하는 JSON 개체를 구문 분석 하 고 모든 값을 반환 하려면 사용 **OPENJSON**다음 예제에 나온 것 처럼 합니다.  
  
```sql  
DECLARE @json NVARCHAR(MAX)
SET @json=N'{"person":{"info":{"name":"John", "name":"Jack"}}}'

SELECT value
FROM OPENJSON(@json,'$.person.info') 
```  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.
  
## <a name="see-also"></a>관련 항목:  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  

