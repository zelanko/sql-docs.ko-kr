---
title: JSON 데이터 인덱싱 | Microsoft 문서
ms.custom: ''
ms.date: 06/01/2016
ms.prod: sql
ms.reviewer: genemi
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- JSON, indexing JSON data
- indexing JSON data
ms.assetid: ced241e1-ff09-4d6e-9f04-a594a9d2f25e
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d87675c4feb0ab784f0003143406b3784f7e8a83
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62716689"
---
# <a name="index-json-data"></a>JSON 데이터 인덱싱
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

SQL Server 및 SQL Database에서 JSON은 기본 제공 데이터 형식이 아니며 SQL Server에는 사용자 지정 JSON 인덱스가 없습니다. 그러나 표준 인덱스를 사용하여 JSON 문서에 대한 쿼리를 최적화할 수 있습니다. 

데이터베이스 인덱스는 필터 및 정렬 작업의 성능을 향상합니다. 인덱스를 사용하지 않으면 SQL Server는 데이터를 쿼리할 때마다 전체 테이블을 검색해야 합니다.  
  
## <a name="index-json-properties-by-using-computed-columns"></a>계산된 열을 사용하여 JSON 속성 인덱싱  
SQL Server에 JSON 데이터를 저장하는 경우 JSON 문서 *속성* 하나 이상을 기준으로 쿼리 결과를 필터링하거나 정렬하는 것이 일반적입니다.  

### <a name="example"></a>예제 
이 예제에서는 AdventureWorks `SalesOrderHeader` 테이블에 판매 주문에 대한 다양한 정보가 JSON 형식으로 포함되어 있는 `Info` 열이 있다고 가정합니다. 예를 들어 이 열은 고객, 영업 사원, 배송 및 대금 청구 주소 등에 대한 정보를 포함합니다. `Info` 열의 값을 사용하여 고객의 판매 주문을 필터링하려고 합니다.

### <a name="query-to-optimize"></a>최적화할 쿼리
다음은 인덱스를 사용하여 최적화할 쿼리 형식의 예제입니다.  
  
```sql  
SELECT SalesOrderNumber,
    OrderDate,
    JSON_VALUE(Info, '$.Customer.Name') AS CustomerName
FROM Sales.SalesOrderHeader
WHERE JSON_VALUE(Info, '$.Customer.Name') = N'Aaron Campbell' 
```  

### <a name="example-index"></a>예제 인덱스
JSON 문서에서 속성에 대한 `ORDER BY` 절 또는 필터링의 속도를 향상하려면 다른 열에서 이미 사용 중인 동일한 인덱스를 사용할 수 있습니다. 그러나 JSON 문서에서는 속성을 *직접* 참조할 수 없습니다.
    
1.  먼저 필터링에 사용할 값을 반환하는 “가상 열”을 만들어야 합니다.
2.  그런 다음 해당 가상 열에 인덱스를 만들어야 합니다.  
  
다음 예제에서는 인덱싱에 사용할 수 있는 계산 열을 만듭니다. 그런 다음 새 계산 열에서 인덱스를 만듭니다. 이 예제에서는 JSON 데이터의 `$.Customer.Name` 경로에 저장된 고객 이름을 표시하는 열을 만듭니다. 
  
```sql  
ALTER TABLE Sales.SalesOrderHeader
ADD vCustomerName AS JSON_VALUE(Info,'$.Customer.Name')

CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)  
```  
### <a name="more-info-about-the-computed-column"></a>계산 열에 대한 자세한 정보 
계산 열은 지속형이 아닙니다. 인덱스를 다시 작성해야 하는 경우에만 계산됩니다. 테이블에서 추가 공간을 차지하지 않습니다.   
  
쿼리에서 사용할 동일한 식으로 계산 열을 만드는 것이 중요합니다. 이 예제의 식은 `JSON_VALUE(Info, '$.Customer.Name')`입니다.  
  
쿼리를 다시 작성할 필요가 없습니다. 위 예제 쿼리와 같이 `JSON_VALUE` 함수가 포함된 식을 사용하는 경우 SQL Server는 같은 식을 사용하는 동일한 계산 열이 있는지 확인한 후 해당하는 경우 인덱스를 적용합니다.

### <a name="execution-plan-for-this-example"></a>이 예제에 대한 실행 계획
다음은 이 예제의 쿼리 실행 계획입니다.  
  
![실행 계획](../../relational-databases/json/media/jsonindexblog1.png "Execution plan")  
  
SQL Server는 전체 테이블을 검색하지 않고 비클러스터형 인덱스에서 인덱스 검색하여 지정된 조건을 충족하는 행을 찾습니다. 그런 다음 `SalesOrderHeader` 테이블에서 키 조회를 사용하여 쿼리에서 참조된 다른 열(이 예제에서는 `SalesOrderNumber` 및 `OrderDate`)을 가져옵니다.  
 
### <a name="optimize-the-index-further-with-included-columns"></a>포괄 열을 사용하여 추가로 인덱스 최적화
인덱스에 필요한 열을 추가하는 경우 테이블에서 이러한 조회를 추가로 수행할 필요가 없습니다. 위의 `CREATE INDEX` 예제를 확장하는 다음 예제처럼 이러한 열을 표준형 포괄 열로 추가할 수 있습니다.  
  
```sql  
CREATE INDEX idx_soh_json_CustomerName
ON Sales.SalesOrderHeader(vCustomerName)
INCLUDE(SalesOrderNumber,OrderDate)
```  
  
이 경우 비클러스터형 JSON 인덱스에 필요한 모든 사항이 있기 때문에 SQL Server는 `SalesOrderHeader` 테이블에서 데이터를 추가로 읽을 필요가 없습니다. 이러한 인덱스 유형은 쿼리에서 JSON과 열 데이터를 결합하고 작업에 대한 최적의 인덱스를 생성하기 위한 좋은 방법입니다.  
  
## <a name="json-indexes-are-collation-aware-indexes"></a>JSON 인덱스는 데이터 정렬 인식 인덱스입니다.  
JSON 데이터에 대한 중요한 인덱스 기능은 인덱스가 데이터 정렬 인식 인덱스라는 점입니다. 계산 열을 만들 때 사용하는 `JSON_VALUE` 함수의 결과는 입력 식에서 데이터 정렬을 상속하는 텍스트 값입니다. 따라서 인덱스의 값은 원본 열에 정의된 데이터 정렬 규칙을 사용하여 정렬됩니다.  
  
인덱스가 데이터 정렬을 인식한다는 것을 보여주기 위해 다음 예제에서는 기본 키와 JSON 콘텐츠가 있는 단순한 컬렉션 테이블을 만듭니다.  
  
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
  
앞의 명령은 JSON `$.name` 속성의 값을 나타내는 계산 열 `vName`에 표준 인덱스를 만듭니다. 세르비아어-키릴 자모 코드 페이지에서 문자 순서는 'А', 'Б', 'В', 'Г', 'Д', 'Ђ', 'Е' 등의 순서입니다. `JSON_VALUE` 함수의 결과는 원본 열에서 데이터 정렬을 상속하므로 인덱스에서 항목의 순서는 세르비아어 키릴 자모 규칙을 따릅니다. 다음 예제에서는 이 컬렉션을 쿼리하고 이름을 기준으로 결과를 정렬합니다.  
  
```sql  
SELECT JSON_VALUE(json,'$.name'),*
FROM JsonCollection
ORDER BY JSON_VALUE(json,'$.name')
```  
  
 실제 실행 계획을 보면 비클러스터형 인덱스에서 정렬된 값을 사용함을 확인할 수 있습니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog2.png "Execution plan")  
  
 쿼리에 `ORDER BY` 절이 있지만 실행 계획은 Sort 연산자를 사용하지 않습니다. JSON 인덱스는 이미 세르비아어 키릴 자모 규칙에 따라 정렬됩니다. 따라서 SQL Server는 결과가 이미 정렬된 비클러스터형 인덱스를 사용합니다.  
  
 그러나 `ORDER BY` 식의 데이터 정렬을 변경하면(예: `JSON_VALUE` 함수 뒤에 `COLLATE French_100_CI_AS_SC` 추가) 다른 쿼리 실행 계획이 제공됩니다.  
  
 ![실행 계획](../../relational-databases/json/media/jsonindexblog3.png "Execution plan")  
  
 인덱스 값 순서는 프랑스어 데이터 정렬 규칙을 따르지 않으므로 SQL Server는 정렬 결과에 대한 인덱스를 사용할 수 없습니다. 따라서 프랑스어 데이터 정렬 규칙을 사용하여 결과를 정렬하는 정렬 연산자를 추가합니다.  
 
## <a name="learn-more-about-json-in-sql-server-and-azure-sql-database"></a>SQL Server 및 Azure SQL Database에서 JSON에 대한 자세한 정보  
  
### <a name="microsoft-videos"></a>Microsoft 비디오

SQL Server 및 Azure SQL Database에서 기본 제공 JSON 지원에 대한 시각적 소개는 다음 비디오를 참조하세요.

-   [SQL Server 2016 및 JSON 지원](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

-   [SQL Server 2016 및 Azure SQL Database에서 JSON 사용](https://channel9.msdn.com/Shows/Data-Exposed/Using-JSON-in-SQL-Server-2016-and-Azure-SQL-Database)

-   [NoSQL과 관계형 간에 브리지인 JSON](https://channel9.msdn.com/events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds)
