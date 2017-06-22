---
title: "JSON 데이터 인덱싱 | Microsoft 문서"
ms.custom:
- SQL2016_New_Updated
ms.date: 06/01/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
caps.latest.revision: 9
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 439b568fb268cdc6e6a817f36ce38aeaeac11fab
ms.openlocfilehash: 3ed7a51b28d2b17b3239f971d0f4f684bec145cd
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="index-json-data"></a>JSON 데이터 인덱싱
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

SQL Server 2016에서 JSON은 기본 제공 데이터 형식이 아니며 및 SQL Server의 사용자 지정 JSON 인덱스가 없습니다. 그러나 사용자 쿼리를 최적화할 수 JSON 문서에 대해 표준 인덱스를 사용 하 여 합니다. 

데이터베이스 인덱싱은 필터 및 정렬 작업의 성능을 향상 시킵니다. 인덱스를 사용하지 않으면 SQL Server는 데이터를 쿼리할 때마다 전체 테이블을 검색해야 합니다.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>계산된 열을 사용하여 JSON 속성 인덱싱  
SQL Server에서 JSON 데이터를 저장 하는 경우 일반적으로 쿼리 결과 필터링 하거나 정렬 하 여 원하는 하나 이상의 *속성* JSON 문서입니다.  

### <a name="example"></a>예제 
이 예에서는 가정 AdventureWorks `SalesOrderHeader` 테이블에는 `Info` 판매 주문에 대 한 JSON 형식의 다양 한 정보가 포함 된 열입니다. 예를 들어 고객, 영업 사원, 배송 및 대금 청구 주소 등에 대 한 정보를 포함합니다. 값을 사용 하려는 `Info` 고객에 대 한 판매 주문을 필터링 할 열입니다.

### <a name="query-to-optimize"></a>쿼리 최적화를
인덱스를 사용 하 여 최적화 하려는 쿼리 유형의 예를 들면 다음과 같습니다.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>예제 인덱스
필터 속도 하려는 경우 또는 `ORDER BY` 속성 JSON 문서에 대 한 절을 다른 열에 이미 사용 중인 동일한 인덱스를 사용할 수 있습니다. 제한 사항이 있습니다. *직접* JSON 문서의 속성을 참조 합니다.
    
1.  "가상 열"을 만들어야 하는 경우 먼저 필터링에 사용 하려는 값을 반환 하는 합니다.
2.  그런 다음 해당 가상 열에 인덱스를 만들어야 합니다.  
  
다음 예제에서는 인덱싱에 사용할 수 있는 계산된 열을 만듭니다. 그런 다음 새 계산된 열에 인덱스를 만듭니다. 에 저장 된 사용자 이름을 표시 하는 열을 만드는이 예제는 `$.Customer.Name` JSON 데이터의 경로입니다. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>계산된 열에 대 한 자세한 정보 
계산 열은 지속형이 아닙니다. 인덱스를 다시 작성해야 하는 경우에만 계산됩니다. 테이블에서 추가 공간을 차지하지 않습니다.   
  
이 계산된 열 식으로 만드는 동일한 쿼리에서이 예제에서 사용 하려는 것이 식은 `JSON_VALUE(Info, '$.Customer.Name')`합니다.  
  
쿼리를 다시 작성할 필요가 없습니다. 사용 하 여 식을 사용 하는 경우는 `JSON_VALUE` 함수를 위의 예에서는 쿼리에 표시 된 것 처럼 SQL Server 있는지 확인은 같은 식 사용 하 여 해당 하는 계산된 열을 가능 하면 인덱스를 적용 합니다.

### <a name="execution-plan-for-this-example"></a>이 예제에 대 한 실행 계획
다음은이 예제의 쿼리 실행 계획입니다.  
  
![실행 계획](../../relational-databases/json/media/jsonindexblog1.png "Execution plan")  
  
SQL Server는 전체 테이블을 검색하지 않고 비클러스터형 인덱스에서 인덱스 검색하여 지정된 조건을 충족하는 행을 찾습니다. 키 조회를 사용 하 여는 `SalesOrderHeader` 이 예제에서는 쿼리에서 참조 되는 다른 열을 인출 하는 테이블 `SalesOrderNumber` 및 `OrderDate`합니다.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>포괄된 열이 있는 인덱스를 추가로 최적화
인덱스에 필요한 열을 추가 하는 경우이 추가 테이블 조회를 방지할 수 있습니다. 확장 하는 다음 예제와 같이 이러한 열을 표준형 포괄된 열으로 추가할 수 있습니다는 `CREATE INDEX` 위에 표시 된 예제입니다.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
SQL Server에서 추가 데이터를 읽을 수 없는 경우에 `SalesOrderHeader` 비클러스터형 JSON 인덱스에 포함 되어 필요한 모든 사항이 있기 때문에 테이블입니다. 이것은 쿼리에서 JSON과 열 데이터를에서 결합 하 고 작업에 대 한 최적의 인덱스를 만들 수는 좋은 방법입니다.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 인덱스는 데이터 정렬 인식 인덱스입니다.  
중요 한 JSON 데이터에 대해 인덱스 기능은 인덱스는 데이터 정렬 인식 됩니다. 결과 `JSON_VALUE` 계산된 열을 만들 때 사용 하는 함수는 입력된 된 식에서 해당 데이터 정렬을 상속 하는 텍스트 값입니다. 따라서 인덱스의 값은 원본 열에 정의 된 데이터 정렬 규칙을 사용 하 여 정렬 됩니다.  
  
이것을 보여주기 위해 다음 예제에서는 기본 키와 JSON 콘텐츠가 있는 단순한 컬렉션 테이블을 만듭니다.  
  
```sql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
이전 명령은 JSON 열에 대하여 세르비아어 키릴 자모 데이터 정렬을 지정합니다. 다음 예제에서는 테이블을 자동으로 채우고 이름 속성에 대한 인덱스를 만듭니다.  
  
```sql  
INSERT INTO JsonCollection
VALUES
(N'{"name":"Иво","surname":"Андрић"}'),
(N'{"name":"Андрија","surname":"Герић"}'),
(N'{"name":"Владе","surname":"Дивац"}'),
(N'{"name":"Новак","surname":"Ђоковић"}'),
(N'{"name":"Предраг","surname":"Стојаковић"}'),
(N'{"name":"Михајло","surname":"Пупин"}'),
(N'{"name":"Борислав","surname":"Станковић"}'),
(N'{"name":"Владимир","surname":"Грбић"}'),
(N'{"name":"Жарко","surname":"Паспаљ"}'),
(N'{"name":"Дејан","surname":"Бодирога"}'),
(N'{"name":"Ђорђе","surname":"Вајферт"}'),
(N'{"name":"Горан","surname":"Бреговић"}'),
(N'{"name":"Милутин","surname":"Миланковић"}'),
(N'{"name":"Никола","surname":"Тесла"}')
GO
  
ALTER TABLE JsonCollection
ADD vName AS JSON_VALUE(json,'$.name')

CREATE INDEX idx_name
ON JsonCollection(vName)
```  
  
이전 명령 계산된 된 열에 표준 인덱스를 만들고 `vName`, JSON에서 값을 나타내는 `$.name` 속성입니다. 세르비아어-키릴 자모 코드 페이지에서 문자 순서는 ‘А’,’Б’,’В’,’Г’,’Д’,’Ђ’,’Е’ 등의 순서입니다. 인덱스에 있는 항목의 순서는 세르비아어 키릴 자모 규칙을 준수 하기 때문에 결과 `JSON_VALUE` 함수 원본 열에서 해당 데이터 정렬을 상속 합니다. 다음 예제에서는 이 컬렉션을 쿼리하고 이름을 기준으로 결과를 정렬합니다.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 실제 실행 계획을 보면 비클러스터형 인덱스에서 정렬된 값을 사용함을 확인할 수 있습니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog2.png "Execution plan")  
  
 쿼리에 있지만 `ORDER BY` 절, 실행 계획은 정렬 연산을 사용 하지 않습니다. JSON 인덱스는 이미 세르비아어 키릴 자모 규칙에 따라 정렬됩니다. 따라서 SQL Server는 결과가 이미 정렬된 비클러스터형 인덱스를 사용합니다.  
  
 그러나의 데이터 정렬을 변경 하면는 `ORDER BY` 포함 하는 경우 등의 식- `COLLATE French_100_CI_AS_SC` 후의 `JSON_VALUE` 함수-얻을 수 있는 다른 쿼리 실행 계획 합니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog3.png "Execution plan")  
  
 인덱스 값 순서는 프랑스어 데이터 정렬 규칙을 따르지 않으므로 SQL Server는 정렬 결과에 대한 인덱스를 사용할 수 없습니다. 따라서 프랑스어 데이터 정렬 규칙을 사용하여 결과를 정렬하는 정렬 연산자를 추가합니다.  
 
## <a name="learn-more-about-the-built-in-json-support-in-sql-server"></a>기본 제공 SQL Server에서 JSON 지원에 대 한 자세한 정보  
특정 솔루션에 많이 사용 사례 및 권장 사항, 참조는 [기본 제공 JSON 지원에 대 한 블로그 게시물](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/) SQL Server와 Microsoft 프로그램 관리자 인 Jovan popovic의 Azure SQL 데이터베이스에 있습니다.

