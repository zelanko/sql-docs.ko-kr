---
title: FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.reviewer: douglasl
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR JSON
- JSON, exporting
- exporting JSON
ms.assetid: 15b56365-58c2-496c-9d4b-aa2600eab09a
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ed47af3378636e58e7fccccca3e5bcf7375255d
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52520895"
---
# <a name="format-query-results-as-json-with-for-json-sql-server"></a>FOR JSON을 사용하여 쿼리 결과를 JSON으로 서식 지정(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

**SELECT** 문에 **FOR JSON** 절을 추가하여 쿼리 결과를 JSON으로 서식 지정하거나 데이터를 SQL Server에서 JSON으로 내보냅니다. **FOR JSON** 절을 사용하면 JSON 출력 형식 지정을 앱에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 위임하여 클라이언트 응용 프로그램을 간소화할 수 있습니다.
  
 **FOR JSON** 절을 사용하는 경우 JSON 출력의 구조를 명시적으로 지정하거나 SELECT 문의 구조에 따라 출력이 결정되도록 할 수 있습니다.  
  
-   JSON 출력의 형식을 완전하게 제어하려면 **FOR JSON PATH**를 사용합니다. 래퍼 개체를 만들고 복잡한 속성을 중첩할 수 있습니다.  
  
-   SELECT 문의 구조에 따라 JSON 출력 형식을 자동으로 지정하려면 **FOR JSON AUTO**를 사용합니다.  
  
다음은 **FOR JSON** 절을 사용한 **SELECT** 문 및 해당 출력의 예입니다.
  
 ![FOR JSON](../../relational-databases/json/media/jsonslides2forjson.png)
  
## <a name="option-1---you-control-output-with-for-json-path"></a>옵션 1 - FOR JSON PATH로 출력 제어
**PATH** 모드에서는 점 구문(예: `'Item.Price'`)을 사용하여 중첩 출력을 서식 지정할 수 있습니다.  

다음은 **PATH** 모드를 **FOR JSON** 절과 함께 사용하는 예제입니다. 다음 예제에서는 **ROOT** 옵션을 사용하여 명명된 루트 요소를 지정합니다. 
  
 ![FOR JSON 출력의 흐름 다이어그램](../../relational-databases/json/media/forjson-example1.png) 

### <a name="more-info-about-for-json-path"></a>FOR JSON PATH에 대한 추가 정보
자세한 내용과 예제는 [PATH 모드로 중첩 JSON 출력 형식 지정&#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md)을 참조하세요.

구문 및 사용법은 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  

## <a name="option-2---select-statement-controls-output-with-for-json-auto"></a>옵션 2 - FOR JSON AUTO를 사용하여 출력을 제어하는 SELECT 문
**AUTO** 모드에서는 SELECT 문의 구조가 JSON 출력의 서식을 결정합니다.

기본적으로 **null** 값은 출력에 포함되지 않습니다. **INCLUDE_NULL_VALUES** 를 사용하여 이 동작을 변경할 수 있습니다.  

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
 
### <a name="more-info-about-for-json-auto"></a>FOR JSON AUTO에 대한 추가 정보
자세한 내용과 예제는 [AUTO 모드를 사용하여 JSON 출력 형식 자동 지정&#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md)을 참조하세요.

구문 및 사용법은 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md).  
  
## <a name="control-other-json-output-options"></a>기타 JSON 출력 옵션 제어  
다음과 같은 추가 옵션을 사용하여 **FOR JSON** 절의 출력을 제어합니다.  
  
-   **ROOT**. 단일 최상위 요소를 JSON 출력에 추가하려면 **ROOT** 옵션을 사용합니다. 이 옵션을 지정하지 않으면 JSON 출력에 루트 요소가 포함되지 않습니다. 자세한 내용은 [ROOT 옵션을 사용하여 JSON 출력에 루트 노드 추가&#40;SQL Server&#41;](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
-   **INCLUDE_NULL_VALUES**. JSON 출력에 null 값을 포함하려면 **INCLUDE_NULL_VALUES** 옵션을 지정합니다. 이 옵션을 지정하지 않으면 쿼리 결과의 NULL 값에 대한 JSON 속성이 출력에 포함되지 않습니다. 자세한 내용은 [INCLUDE_NULL_VALUES 옵션을 사용하여 JSON 출력에 Null 값 포함&#40;SQL Server&#41;](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md)을 참조하세요.   

-   **WITHOUT_ARRAY_WRAPPER**. 기본적으로 **FOR JSON** 절의 JSON 출력을 둘러싸고 있는 대괄호를 제거하려면 **WITHOUT_ARRAY_WRAPPER** 옵션을 지정합니다. 이 옵션을 사용하면 단일 JSON 개체를 단일 행 결과의 출력으로 생성할 수 있습니다. 이 옵션을 지정하지 않으면 JSON 출력의 형식이 배열로 지정됩니다. 즉, 출력이 대괄호로 묶입니다. 자세한 내용은 [WITHOUT_ARRAY_WRAPPER 옵션을 사용하여 JSON 출력에서 대괄호 제거&#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md). 
   
## <a name="output-of-the-for-json-clause"></a>FOR JSON 절의 출력  
**FOR JSON** 절의 출력은 다음과 같은 특징이 있습니다.  
  
1.  결과 집합이 단일 열을 포함합니다.
    -   작은 결과 집합은 단일 행을 포함할 수 있습니다.
    -   결과 집합이 크면 긴 JSON 문자열이 여러 행으로 분할됩니다.
        -   기본적으로 SSMS(SQL Server Management Studio)는 출력 설정이 **표 형태로 결과 표시**인 경우 결과를 단일 행으로 연결합니다. SSMS 상태 표시줄에 실제 행 수가 표시됩니다.
        -   다른 클라이언트 응용 프로그램에는 여러 행의 내용을 연결하여 길이가 긴 결과를 하나의 유효한 JSON 문자열로 다시 결합하는 코드가 필요할 수 있습니다. C# 응용 프로그램에서 이 코드의 예는 [C# 클라이언트 앱에서 FOR JSON 출력 사용](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md#use-for-json-output-in-a-c-client-app)을 참조하세요.
  
     ![FOR JSON 출력의 예](../../relational-databases/json/media/forjson-example2.png)  
  
2.  결과는 JSON 개체의 배열로 서식 지정됩니다.  
  
    -   JSON 배열의 요소 수는 SELECT 문 결과(FOR JSON 절을 적용하기 전)의 행 수와 같습니다. 
  
    -   SELECT 문 결과(FOR JSON 절을 적용하기 전)의 각 행은 배열에서 별개의 JSON 개체가 됩니다.  
  
    -   SELECT 문 결과(FOR JSON 절을 적용하기 전)의 각 열은 JSON 개체의 속성이 됩니다.  
  
3.  JSON 구문에 따라 열과 해당 값의 이름이 모두 이스케이프됩니다. 자세한 내용은 [FOR JSON이 특수 문자 및 제어 문자를 이스케이프 처리하는 방법&#40;SQL Server&#41;](../../relational-databases/json/how-for-json-escapes-special-characters-and-control-characters-sql-server.md).
  
### <a name="example"></a>예제
다음은 **FOR JSON** 절에서 JSON 출력의 형식을 지정하는 방법을 보여 주는 예제입니다.  
  
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

## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-blog-posts"></a>Microsoft 블로그 게시물  
  
특정 솔루션, 사용 사례 및 권장 사항은 SQL Server 및 Azure SQL Database의 기본 제공 JSON 지원에 대한 [블로그 게시물](https://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)을 참조하세요.  

### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
  
## <a name="see-also"></a>참고 항목  
 [FOR 절&#40;Transact-SQL&#41;](../../t-sql/queries/select-for-clause-transact-sql.md)   
 [SQL Server 및 클라이언트 앱에서 FOR JSON 출력 사용&#40;SQL Server&#41;](../../relational-databases/json/use-for-json-output-in-sql-server-and-in-client-apps-sql-server.md)  
  
  
