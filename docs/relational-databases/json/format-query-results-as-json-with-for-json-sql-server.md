---
title: "FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정(SQL Server) | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 06095384c6f6ec876e0d103186b1269d19056987
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

**SELECT** 문에 **FOR JSON** 절을 추가하여 쿼리 결과를 JSON으로 서식 지정하거나 데이터를 SQL Server에서 JSON으로 내보냅니다. 사용 하 여는 **FOR JSON** 절을 클라이언트 응용 프로그램에서 JSON 출력의 서식을 위임 하 여 클라이언트 응용 프로그램을 단순화 하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.
  
 **FOR JSON** 절을 사용하는 경우 출력의 구조를 명시적으로 지정하거나 SELECT 문의 구조에 따라 출력이 결정되도록 할 수 있습니다.  
  
-   사용 하 여 **FOR JSON PATH** 를 JSON 출력의 형식에 대 한 모든 권한을 유지 관리 합니다. 래퍼 개체를 만들고 복잡한 속성을 중첩할 수 있습니다.  
  
-   사용 하 여 **FOR JSON AUTO** SELECT 문의 구조에 따라 JSON 출력을 자동으로 형식을 지정 합니다.  
  
다음은 **FOR JSON** 절을 사용한 **SELECT** 문 및 해당 출력의 예입니다.
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png "FOR JSON")  
  
## <a name="maintain-control-over-json-output-with-for-json-path"></a>FOR JSON PATH를 사용 하 여 JSON 출력에 대 한 제어 유지
**PATH** 모드에서는 점 구문(예: `'Item.Price'` )을 사용하여 중첩 출력을 서식 지정할 수 있습니다.  

다음은 **PATH** 모드를 **FOR JSON** 절과 함께 사용하는 예제입니다. 다음 예제에서는 **ROOT** 옵션을 사용하여 명명된 루트 요소를 지정합니다. 
  
 ![FOR JSON 출력의 흐름 다이어그램](../../relational-databases/json/media/forjson-example1.png "Diagram of flow of FOR JSON output")  

### <a name="more-info"></a>추가 정보
자세한 내용과 예제를 참조 하십시오. [중첩 JSON 출력 형식으로 PATH 모드 &#40; SQL Server &#41; ](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md).

구문 및 사용법은 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="let-the-select-statement-control-json-output-with-for-json-auto"></a>FOR JSON AUTO를 사용 하 여 JSON 출력을 제어 하는 SELECT 문
**AUTO** 모드에서는 SELECT 문의 구조가 JSON 출력의 서식을 결정합니다. 기본적으로 **null** 값은 출력에 포함되지 않습니다. **INCLUDE_NULL_VALUES** 를 사용하여 이 동작을 변경할 수 있습니다.  

다음은 **AUTO** 모드를 **FOR JSON** 절과 함께 사용하는 샘플 쿼리입니다.
 
**쿼리:**  
  
```sql  
SELECT name, surname  
FROM emp  
FOR JSON AUTO  
```  
  
 **결과**  
  
```json  
[{
    "name": "John"
}, {
    "name": "Jane",
    "surname": "Doe"
}]
```  
### <a name="more-info"></a>추가 정보
자세한 내용과 예제를 참조 하십시오. [JSON 출력 형식 자동 AUTO 모드 &#40; SQL Server &#41; ](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).

구문 및 사용법은 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="control-other-json-output-options"></a>기타 JSON 출력 옵션 제어  
출력을 제어는 **FOR JSON** 다음과 같은 추가 옵션을 사용 하 여 절.  
  
-   **루트**합니다. 단일 최상위 요소를 JSON 출력에 추가하려면 **ROOT** 옵션을 사용합니다. 이 옵션을 지정 하지 않으면 JSON 출력에는 루트 요소가 되어 있지 않습니다. 자세한 내용은 [ROOT 옵션을 사용하여 JSON 출력에 루트 노드 추가&#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
-   **INCLUDE_NULL_VALUES**합니다. JSON 출력에 null 값을 포함하려면 **INCLUDE_NULL_VALUES** 옵션을 지정합니다. 이 옵션을 지정 하지 않는 경우 출력은 쿼리 결과에서 NULL 값에 대 한 JSON 속성 포함 되지 않습니다. 자세한 내용은 참조 하세요. [INCLUDE_NULL_VALUES 옵션 &#40;를 사용 하 여 JSON 출력에서 Null 값 포함 SQL Server &#41; ](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).   

-   **WITHOUT_ARRAY_WRAPPER**합니다. 기본적으로 **FOR JSON** 절의 JSON 출력을 둘러싸고 있는 대괄호를 제거하려면 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 단일 행 결과 출력으로 단일 JSON 개체를 생성 하려면이 옵션을 사용 합니다. 이 옵션을 지정 하지는 배열로 JSON 출력의 형식이-대괄호로 묶어야 즉, 합니다. 자세한 내용은 [WITHOUT_ARRAY_WRAPPER 옵션을 사용하여 JSON 출력에서 대괄호 제거&#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md). 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 절의 출력  
 **FOR JSON** 절의 출력은 다음과 같은 특징이 있습니다.  
  
1.  결과 집합이 단일 열을 포함합니다.
    -   작은 결과 집합은 단일 행을 포함할 수 있습니다.
    -   큰 결과 집합은 여러 행에서 긴 JSON 문자열을 분할합니다.
        -   기본적으로 SQL Server Management Studio (SSMS) 결과 연결 단일 행으로 출력 설정이 **표 형태로 결과**합니다. SSMS 상태 표시줄 실제 행 개수를 표시합니다.
        -   다른 클라이언트 응용 프로그램에는 여러 행의 내용을 결합 하 여 길이가 긴 결과 연결 하는 코드가 필요할 수 있습니다. C# 응용 프로그램에서이 코드 예제를 보려면 [C# 클라이언트 앱에서 사용 하 여 FOR JSON 출력](https://docs.microsoft.com/en-us/sql/relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server#use-for-json-output-in-a-c-client-app)합니다.
  
     ![FOR JSON 출력의 예](../../relational-databases/json/media/forjson-example2.png "Example of FOR JSON output")  
  
2.  결과는 JSON 개체의 배열로 서식 지정됩니다.  
  
    -   JSON 배열의 요소 수는 (FOR JSON 절을 적용 하기 전에) SELECT 문의 결과에서 행의 수와 같습니다. 
  
    -   SELECT 문의 (FOR JSON 절을 적용 하기 전에) 결과의 각 행은 배열의 별도 JSON 개체가 됩니다.  
  
    -   FOR JSON 절이 적용 됩니다) (이전 SELECT 문의 결과의 각 열에는 JSON 개체의 속성이 됩니다.  
  
3.  JSON 구문에 따라 열과 해당 값의 이름이 모두 이스케이프됩니다. 자세한 내용은 [FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법&#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md).
  
### <a name="example"></a>예제
다음은 보여 주는 예제는 방법을 **FOR JSON** 절의 JSON 출력의 형식을 지정 합니다.  
  
**쿼리 결과**  
  
|||||  
|-|-|-|-|  
|**변수를 잠그기 위한**|**B**|**C**|**D**|  
|10|11|12|X|  
|20|21|22|Y|  
|30|31|32|Z|  
  
 **JSON 출력**  
  
```json  
[{
    "A": 10,
    "B": 11,
    "C": 12,
    "D": "X"
}, {
    "A": 20,
    "B": 21,
    "C": 22,
    "D": "Y"
}, {
    "A": 30,
    "B": 31,
    "C": 32,
    "D": "Z"
}] 
```  
 **FOR JSON** 절의 출력에 나타나는 자세한 내용은 다음 항목을 참조하세요.  
-   [FOR JSON을 통해 SQL Server 데이터 형식을 JSON 데이터 형식으로 변환하는 방법&#40;SQL Server&#41;](../../relational-databases/json/how-for-json-converts-sql-server-data-types-to-json-data-types-sql-server.md)  
**FOR JSON** 절은 이 항목에서 설명하는 규칙을 사용하여 JSON 출력의 SQL 데이터 형식을 JSON 형식으로 변환합니다.  

-   [FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법&#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md)  
 **FOR JSON** 절은 특수 문자를 이스케이프하고 JSON 출력의 제어 문자를 이 항목에서 설명하는 대로 표시합니다.  

## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.
  
## <a name="see-also"></a>참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [SQL Server 및 클라이언트 앱에서 FOR JSON 출력 사용&#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  

