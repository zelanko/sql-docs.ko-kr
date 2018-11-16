---
title: SQL Server에서 JSON으로 일반적인 문제 해결 | Microsoft 문서
ms.custom: ''
ms.date: 07/07/2016
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, FAQ
ms.assetid: feae120b-55cc-4601-a811-278ef1c551f9
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8f6222c5829af5a63e4ab7fd079a405063f08ec5
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51661732"
---
# <a name="solve-common-issues-with-json-in-sql-server"></a>SQL Server에서 JSON으로 일반적인 문제 해결
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 JSON SQL Server에서 기본으로 제공되는 JSON 지원에 대한 일반적인 질문에 대한 대답을 여기에서 확인하십시오.  
 
## <a name="for-json-and-json-output"></a>FOR JSON 및 JSON 출력

### <a name="for-json-path-or-for-json-auto"></a>FOR JSON PATH 또는 FOR JSON AUTO?  
 **질문.** 단일 테이블에서 수행한 간단한 SQL 쿼리의 JSON 텍스트 결과를 만들려고 합니다. FOR JSON PATH 및 FOR JSON AUTO는 동일한 출력을 제공합니다. 이러한 두 옵션 중 어느 옵션을 사용해야 하나요?  
  
 **대답.** FOR JSON PATH 사용 JSON 출력에는 아무런 차이가 없지만 AUTO 모드에서는 열이 중첩되어야 하는지를 확인하는 일부 추가 논리를 적용합니다. PATH를 기본 옵션으로 고려합니다.  

### <a name="create-a-nested-json-structure"></a>중첩된 JSON 구조 만들기  
 **질문.** 동일한 수준에 여러 배열이 있는 복합 JSON을 작성하려고 합니다. FOR JSON PATH는 경로를 사용하여 중첩된 개체를 만들고 FOR JSON AUTO는 각 테이블에 대한 추가 중첩 수준을 만듭니다. 이러한 두 옵션 모두 원하는 출력을 생성할 수 없습니다. 기존 옵션에서 직접 지원되지 않는 사용자 지정 JSON 형식을 어떻게 만들 수 있나요?  
  
 **대답.** JSON 텍스트를 반환하는 FOR JSON 쿼리를 열 식으로 추가하여 데이터 구조를 만들 수 있습니다. JSON_QUERY 함수를 사용하여 JSON을 수동으로 만들 수도 있습니다. 다음 예제에서는 이러한 방법을 보여 줍니다.  
  
```sql  
SELECT col1, col2, col3,  
     (SELECT col11, col12, col13 FROM t11 WHERE t11.FK = t1.PK FOR JSON PATH) as t11,  
     (SELECT col21, col22, col23 FROM t21 WHERE t21.FK = t1.PK FOR JSON PATH) as t21,  
     (SELECT col31, col32, col33 FROM t31 WHERE t31.FK = t1.PK FOR JSON PATH) as t31,  
     JSON_QUERY('{"'+col4'":"'+col5+'"}' as t41  
FROM t1  
FOR JSON PATH  
```  
  
FOR JSON 쿼리의 모든 결과 및 열 식의 JSON_QUERY 함수는 별도의 중첩된 JSON 하위 개체로 형식이 지정되고 기본 결과에 포함됩니다.  

### <a name="prevent-double-escaped-json-in-for-json-output"></a>FOR JSON 출력에서 이중 이스케이프 JSON 방지  
 **질문.** 텍스트 열에 저장된 JSON 텍스트가 있습니다. 이것을 FOR JSON의 출력에 포함하려고 합니다. 하지만 다음 예제에서 보이는 것과 같이 FOR JSON은 JSON에서 모든 문자를 이스케이프하므로 중첩 개체 대신 JSON 문자열이 반환됩니다.  
  
```sql  
SELECT 'Text' AS myText, '{"day":23}' AS myJson  
FOR JSON PATH  
```  
  
 이 쿼리는 다음 출력을 생성합니다.  
  
```json  
[{"myText":"Text", "myJson":"{\"day\":23}"}]  
```  
  
 이 문제를 어떻게 방지할 수 있나요? `{"day":23}` 을(를) 이스케이프된 텍스트가 아닌 JSON 개체로 반환하고 싶습니다.  
  
 **대답.** 텍스트 열 또는 리터럴에 저장된 JSON은 텍스트로 처리됩니다. 즉, 큰따옴표로 묶여 이스케이프됩니다. 이스케이프되지 않은 JSON 개체를 반환하려는 경우 다음 예제에서 보이는 것과 같이 JSON 열을 JSON_QUERY 함수의 인수로 전달합니다.  
  
```sql  
SELECT col1, col2, col3, JSON_QUERY(jsoncol1) AS jsoncol1  
FROM tab1  
FOR JSON PATH  
```  
  
 선택적인 두 번째 매개 변수가 없는 JSON_QUERY는 첫 번째 인수만 결과로 반환합니다. JSON_QUERY는 항상 유효한 JSON을 반환하므로 FOR JSON은 이 결과가 이스케이프되지 않아야 한다는 것을 알고 있습니다.

### <a name="json-generated-with-the-withoutarraywrapper-clause-is-escaped-in-for-json-output"></a>WITHOUT_ARRAY_WRAPPER 절로 생성된 JSON은 FOR JSON 출력에서 이스케이프됨  
 **질문.** FOR JSON 및 WITHOUT_ARRAY_WRAPPER 옵션을 사용하여 열 식을 포맷하려고 합니다.  
  
```sql  
SELECT 'Text' as myText,  
   (SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER) as myJson  
FOR JSON PATH   
```  
  
 FOR JSON 쿼리에서 반환된 텍스트가 일반 텍스트로 이스케이프된 것 같습니다. 이 문제는 WITHOUT_ARRAY_WRAPPER가 지정된 경우에만 발생합니다. 왜 JSON 개체로 처리되지 않고 결과에서 이스케이프되지 않나요?  
  
 **대답.** 내부 `FOR JSON`에 `WITHOUT_ARRAY_WRAPPER` 옵션을 지정하는 경우 결과 JSON 텍스트가 유효한 JSON이 아닐 수 있습니다. 따라서 외부 `FOR JSON`은 이것을 일반 텍스트로 간주하고 문자열을 이스케이프합니다. 다음 예제에서 보이는 것과 같이 JSON 출력이 유효한 경우 `JSON_QUERY` 함수로 래핑하여 적절한 형식의 JSON으로 수준을 올립니다.  
  
```sql  
SELECT 'Text' as myText,  
      JSON_QUERY((SELECT 12 day, 8 mon FOR JSON PATH, WITHOUT_ARRAY_WRAPPER)) as myJson  
FOR JSON PATH    
```  

## <a name="openjson-and-json-input"></a>OPENJSON 및 JSON 입력

### <a name="return-a-nested-json-sub-object-from-json-text-with-openjson"></a>OPENJSON로 JSON 텍스트에서 중첩된 JSON 하위 개체 반환  
 **질문.** 명시적 스키마가 있는 OPENJSON을 사용하여 두 스칼라 값, 개체 및 배열을 포함하는 복합 JSON 개체 배열을 열 수 없습니다. WITH 절에서 키를 참조하는 경우 스칼라 값만 반환됩니다. 개체와 배열이 NULL 값으로 반환됩니다. 개체 또는 배열을 JSON 개체로 어떻게 추출하나요?  
  
 **대답.** 개체 또는 배열을 열로 반환하려면 다음 예제에서 보이는 것과 같이 열 정의에서 AS JSON 옵션을 사용합니다.  
  
```sql  
SELECT scalar1, scalar2, obj1, obj2, arr1  
FROM OPENJSON(@json)  
    WITH ( scalar1 int,  
        scalar2 datetime2,  
        obj1 NVARCHAR(MAX) AS JSON,  
        obj2 NVARCHAR(MAX) AS JSON,  
        arr1 NVARCHAR(MAX) AS JSON)  
```  

### <a name="return-long-text-value-with-openjson-instead-of-jsonvalue"></a>JSON_VALUE 대신 OPENJSON을 사용하여 긴 텍스트 값 반환
 **질문.** 긴 텍스트를 포함하는 JSON 텍스트에 설명 키가 있습니다. `JSON_VALUE(@json, '$.description')` 이(가) 값 대신 NULL을 반환합니다.  
  
 **대답.** JSON_VALUE는 작은 스칼라 값을 반환하도록 설계되었습니다. 일반적으로 함수는 오버플로 오류가 아닌 NULL을 반환합니다. 긴 값을 반환하려면 다음 예제에서와 같이 NVARCHAR(MAX) 값을 지원하는 OPENJSON을 사용하십시오.  
  
```sql  
SELECT myText FROM OPENJSON(@json) WITH (myText NVARCHAR(MAX) '$.description')  
```  

### <a name="handle-duplicate-keys-with-openjson-instead-of-jsonvalue"></a>JSON_VALUE 대신 OPENJSON을 사용하여 중복 키 처리
 **질문.** JSON 텍스트에 중복 키가 있습니다. JSON_VALUE는 경로에서 발견된 첫 번째 키만 반환합니다. 동일한 이름을 가진 모든 키를 어떻게 반환해야 하나요?  
  
 **대답.** 기본 제공 JSON 스칼라 함수는 참조된 개체의 첫 번째 일치 항목만 반환합니다. 다음 예제에서 보이는 것과 같이 둘 이상의 키가 필요한 경우 OPENJSON 테이블 반환 함수를 사용하십시오.  
  
```sql  
SELECT value FROM OPENJSON(@json, '$.info.settings')  
WHERE [key] = 'color'  
```  

### <a name="openjson-requires-compatibility-level-130"></a>OPENJSON은 호환성 수준 130을 필요로 함  
 **질문.** SQL Server 2016에서 OPENJSON을 실행하려는 데 다음 오류가 발생했습니다.  
  
 `Msg 208, Level 16, State 1 ‘Invalid object name OPENJSON’`  
  
 **대답.** OPENJSON 함수는 호환성 수준 130에서만 사용할 수 있습니다. DB 호환성 수준이 130보다 낮은 경우 OPENJSON은 숨겨집니다. 다른 JSON 함수는 모든 호환성 수준에서 사용할 수 있습니다.  
 
## <a name="other-questions"></a>기타 질문

### <a name="reference-keys-that-contain-non-alphanumeric-characters-in-json-text"></a>JSON 텍스트에 영숫자가 아닌 문자가 포함된 참조 키  
 **질문.** JSON 텍스트의 키에 영숫자가 아닌 문자가 포함되었습니다. 이러한 속성을 어떻게 참조할 수 있나요?  
  
 **대답.** JSON 경로에서 따옴표로 묶어야 합니다. `JSON_VALUE(@json, '$."$info"."First Name".value')`)을 입력합니다.
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](https://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
