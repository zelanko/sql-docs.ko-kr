---
title: "JSON 경로 식(SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/23/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "JSON, 경로 식"
  - "경로 식(JSON)"
ms.assetid: 25ea679c-84cc-4977-867c-2cbe9d192553
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 11
---
# JSON 경로 식(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON 경로를 사용하여 JSON 개체의 속성을 참조합니다. JSON 경로는 Javascript와 유사한 구문을 사용합니다.  
  
 다음 함수를 호출하는 경우 경로 식을 제공해야 합니다.  
  
-   JSON 데이터의 관계형 뷰를 만들기 위해 **OPENJSON** 을(를) 호출하는 경우. 자세한 내용은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
-   JSON 텍스트에서 값을 추출하기 위해 **JSON_VALUE**를 호출하는 경우. 자세한 내용은 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)를 참조하세요.  
  
-   JSON 개체 또는 배열을 추출하기 위해 **JSON_QUERY**를 호출하는 경우. 자세한 내용은 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)를 참조하세요.  
  
-   JSON 문자열에서 속성의 값을 업데이트하기 위해 **JSON_MODIFY**를 호출하는 경우. 자세한 내용은 [JSON_MODIFY&#40;Transact-SQL&#41;](../../t-sql/functions/json-modify-transact-sql.md)를 참조하세요.  
  
 경로 식에는 두 가지 구성 요소가 있습니다.  
  
1.  선택적인 [PATH 모드](#PATHMODE), lax 또는 strict.  
  
2.  [PATH](#PATH) 자체.  
  
##  <a name="PATHMODE"></a> PATH 모드  
 경로 식의 시작 부분에서 키워드 **lax** 또는 **strict**을(를) 지정하여 PATH 모드를 선택적으로 선언합니다. 기본값은 **lax**입니다.  
  
-   **lax** 모드에서, 경로 식에 오류가 포함되어 있으면 함수는 빈 값을 반환합니다. 예를 들어 **$.name**값을 요청했는데 JSON 텍스트에 **name** 키가 포함되어 있지 않으면 함수는 null을 반환합니다.  
  
-   **strict** 모드에서 경로 식에 오류가 있으면 함수는 오류를 발생시킵니다.  
  
##  <a name="PATH"></a> PATH  
 선택적인 PATH 모드 선언 후, PATH를 지정합니다.  
  
-   달러 기호($)는 컨텍스트 항목을 나타냅니다.  
  
-   속성 경로는 경로 단계의 집합입니다. 경로 단계는 다음 요소와 연산자를 포함할 수 있습니다.  
  
    -   키 이름. 키 이름이 달러 기호로 시작되거나 공백과 같은 특수 기호를 포함하는 경우, 따옴표로 묶습니다. 예를 들면 `$.name` 및 `$."first name"`입니다.  
  
    -   배열 요소 `$.product[3]`)을 입력합니다. 배열은 0부터 시작됩니다.  
  
    -   점 연산자(.)는 개체의 구성원을 나타냅니다.  
  
## 예  
 이 섹션의 예는 다음 JSON 텍스트를 참조합니다.  
  
```json  
{ "people":  
  [  
    { "name": "John", "surname": "Doe" },  
    { "name": "Jane", "surname": null, "active": true }  
  ]  
}  
```  
  
 다음 테이블은 경로 식의 몇 가지 예를 보여줍니다.  
  
|경로 식|값|  
|---------------------|-----------|  
|$.people[0].name|John|  
|$.people[1]|{ "name": "Jane",  "surname": null, "active": true }|  
|$.people[1].surname|null|  
|$|{ "people": [ { "name": "John",  "surname": "Doe" },<br />   { "name": "Jane",  "surname": null, "active": true } ] }|  
  
## 중복된 경로 처리 방식  
 JSON 텍스트에 중복된 속성(예를 들어, 수준과 이름이 같은 두 개의 키)이 포함되는 경우, JSON_VALUE 및 JSON_QUERY 함수는 경로와 일치하는 첫 번째 값을 반환합니다. 중복 키를 포함하는 JSON 개체의 구문을 분석하려면 다음 예제와 같이 OPENJSON을 사용합니다.  
  
```tsql  
DECLARE @json NVARCHAR(MAX) = N'{"person":{"info":{"name":"John", "name":"Jack"}}}'  
  
SELECT value FROM OPENJSON(@json, '$.person.info')  
```  
  
## 참고 항목  
 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)   
 [JSON_VALUE&#40;Transact-SQL&#41;](../../t-sql/functions/json-value-transact-sql.md)   
 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)  
  
  