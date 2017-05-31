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
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cf3c58c7d71a98bfaa1f27611762bf7fb3fe8725
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="index-json-data"></a>JSON 데이터 인덱싱
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  데이터베이스 인덱싱은 필터 및 정렬 작업의 성능을 향상시킵니다. 인덱스를 사용하지 않으면 SQL Server는 데이터를 쿼리할 때마다 전체 테이블을 검색해야 합니다.  
  
 JSON은 SQL Server 2016의 기본 제공 데이터 형식이 아니며 SQL Server 2016에는 사용자 지정 JSON 인덱스가 없습니다. 그러나 표준 인덱스를 사용하여 JSON 문서에 대한 쿼리를 최적화할 수 있습니다.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>계산된 열을 사용하여 JSON 속성 인덱싱  
 SQL Server에 JSON 데이터를 저장하는 경우 JSON 문서 속성을 기준으로 쿼리 결과를 필터링하거나 정렬하는 것이 일반적입니다.  
  
 이 예제에서 AdventureWorks SalesOrderHeader 테이블에는 판매 주문에 대한 다양한 정보(예: 고객, 영업 사원, 운송/청구 주소 등)를 포함하는 “Info” 열이 있습니다. Info 열의 값을 사용하여 고객에 대한 판매 주문을 필터링할 수 있습니다. 인덱스를 사용하여 최적화하는 쿼리의 예는 다음과 같습니다.  
  
```tsql  
SELECT SalesOrderNumber,OrderDate,JSON_VALUE(Info,'$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info,'$.Customer.Name')=N'Aaron Campbell' 
```  
  
 JSON 문서에서 속성에 대한 ORDER BY 절 또는 필터링 속도를 향상하려면 다른 열에서 사용 중인 동일한 인덱스를 사용할 수 있습니다. 그러나 JSON 문서에서는 속성을 직접 참조할 수 없습니다. 먼저 필터링에 사용할 값을 반환하는 "가상 열"을 만들어야 합니다. 그런 다음 해당 가상 열에 인덱스를 만들어야 합니다.  
  
 다음 예제에서는 인덱싱에 사용된 후 해당 열에 인덱스를 만드는 계산 열을 만듭니다. 이 예제에서는JSON 문서의 $.Customer.Name 경로에 저장된 사용자 이름을 표시하는 열을 만듭니다.  
  
```tsql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
  
 계산 열은 지속형이 아닙니다. 테이블에서 추가 공간을 차지하지 않습니다. 인덱스를 다시 작성해야 하는 경우에만 계산됩니다.  
  
 쿼리에서 사용할 동일한 식으로 계산 열을 만드는 것이 중요합니다. 이 예제에서는 `JSON_VALUE(Info, '$.Customer.Name')`입니다.  
  
 쿼리를 다시 작성할 필요가 없습니다. JSON_VALUE 함수 식을 사용하는 경우 SQL Server는 같은 식을 사용하는 동일한 계산 열이 있는지 확인한 후 해당하는 경우 인덱스를 적용합니다. 다음은 이 예제의 쿼리 실행 계획입니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog1.png "Execution plan")  
  
 SQL Server는 전체 테이블을 검색하지 않고 비클러스터형 인덱스에서 인덱스 검색하여 지정된 조건을 충족하는 행을 찾습니다. 그런 다음 SalesOrderHeader 테이블에서 키 조회를 사용하여 쿼리에서 참조된 다른 열을 가져옵니다. 이 예제에서는 SalesOrderNumber 및 OrderDate입니다.  
  
 JSON 인덱스에 필요한 열을 추가하는 경우 테이블에서 이러한 조회를 추가적으로 수행할 필요가 없습니다. 다음 예제에서와 같이 이러한 열을 표준형 포괄 열에 추가할 수 있습니다.  
  
```tsql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
 이 경우 비클러스터형 JSON 인덱스에 필요한 모든 사항이 있기 때문에 SQL Server는 SalesOrderHeader 테이블에서 정보를 추가로 읽지 않습니다. 이것은 쿼리에서 JSON과 열 데이터를 결합하고 작업에 대한 최적의 인덱스를 생성하기 위한 좋은 방법입니다.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 인덱스는 데이터 정렬 인식 인덱스입니다.  
 JSON 인덱스의 중요한 기능은 데이터 정렬을 인식한다는 것입니다. JSON_VALUE 함수의 결과는 입력된 식에서 해당 데이터 정렬을 상속하는 텍스트 값입니다. 따라서 인덱스의 값은 원본 열에 정의된 데이터 정렬 규칙을 사용하여 정렬됩니다.  
  
 이것을 보여주기 위해 다음 예제에서는 기본 키와 JSON 콘텐츠가 있는 단순한 컬렉션 테이블을 만듭니다.  
  
```tsql  
CREATE TABLE JsonCollection
 (
  id INT IDENTITY CONSTRAINT PK_JSON_ID PRIMARY KEY,
  json NVARCHAR(MAX) COLLATE SERBIAN_CYRILLIC_100_CI_AI
  CONSTRAINT [Content should be formatted as JSON]
  CHECK(ISJSON(json)>0)
 ) 
```  
  
 이전 명령은 JSON 열에 대하여 세르비아어 키릴 자모 데이터 정렬을 지정합니다. 다음 예제에서는 테이블을 자동으로 채우고 이름 속성에 대한 인덱스를 만듭니다.  
  
```tsql  
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
  
 이전 명령에는 계산 열 vName에 표준 인덱스를 만들고 그것은 JSON $.name 속성에서의 값을 나타냅니다. 세르비아어-키릴 자모 코드 페이지에서 문자 순서는 ‘А’,’Б’,’В’,’Г’,’Д’,’Ђ’,’Е’ 등의 순서입니다. JSON_VALUE 함수의 결과에는 원본 열의 컬렉션이 상속되므로 인덱스에서 항목의 순서는 세르비아어 키릴 자모 규칙을 따릅니다. 다음 예제에서는 이 컬렉션을 쿼리하고 이름을 기준으로 결과를 정렬합니다.  
  
```tsql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 실제 실행 계획을 보면 비클러스터형 인덱스에서 정렬된 값을 사용함을 확인할 수 있습니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog2.png "Execution plan")  
  
 쿼리에 ORDER BY 절이 있지만 실행 계획은 정렬 연산을 사용하지 않습니다. JSON 인덱스는 이미 세르비아어 키릴 자모 규칙에 따라 정렬됩니다. 따라서 SQL Server는 결과가 이미 정렬된 비클러스터형 인덱스를 사용합니다.  
  
 그러나 ORDER BY 식의 컬렉션을 변경하면(예: JSON_VALUE 함수 뒤에 `COLLATE French_100_CI_AS_SC` 입력) 다른 쿼리 실행 계획이 제공됩니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog3.png "Execution plan")  
  
 인덱스 값 순서는 프랑스어 데이터 정렬 규칙을 따르지 않으므로 SQL Server는 정렬 결과에 대한 인덱스를 사용할 수 없습니다. 따라서 프랑스어 데이터 정렬 규칙을 사용하여 결과를 정렬하는 정렬 연산자를 추가합니다.  
  
  

