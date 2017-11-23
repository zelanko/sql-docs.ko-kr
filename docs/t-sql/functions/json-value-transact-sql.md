---
title: JSON_VALUE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/17/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
caps.latest.revision: "18"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 5762af5115dd65b819bc74c3585cfc8275a516b1
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="jsonvalue-transact-sql"></a>JSON_VALUE (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON 문자열에서 스칼라 값을 추출 합니다.  
  
 스칼라 값이 아닌 JSON 문자열에서 개체 또는 배열을 추출, 참조 [JSON_QUERY &#40; Transact SQL &#41; ](../../t-sql/functions/json-query-transact-sql.md). 간의 차이점에 대 한 정보에 대 한 **JSON_VALUE** 및 **JSON_QUERY**, 참조 [비교 JSON_VALUE 및 JSON_QUERY](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 식입니다. 일반적으로 JSON 텍스트를 포함 하는 열 또는 변수 이름입니다.  
 
 경우 **JSON_VALUE** JSON에 유효 하지 않은 찾습니다 *식* 로 식별 되는 값을 찾기 전에 *경로*, 함수는 오류를 반환 합니다. 하는 경우 **JSON_VALUE* 로 식별 되는 값을 찾지 못하면 *경로*, 전체 텍스트 검색 및 반환 하는 JSON 발견 되 면 오류가 아무 곳 이나 유효 하지 않습니다. *식*합니다.
  
 *경로*  
 추출할 속성을 지정 하는 JSON 경로가 있습니다. 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
 
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]의 값으로 변수를 제공할 수 있습니다 *경로*합니다.
  
 경우 형식의 *경로* 유효 하지 **JSON_VALUE** 에서 오류를 반환 합니다.  
  
## <a name="return-value"></a>반환 값  
 형식 nvarchar (4000)의 단일 텍스트 값을 반환 합니다. 반환된 된 값의 데이터 정렬은 입력된 식의 데이터 정렬과 동일 합니다.  
  
 값이 4000 자를 초과 합니다.  
  
-   Lax 모드로 **JSON_VALUE** null을 반환 합니다.  
  
-   Strict 모드에서는 **JSON_VALUE** 에서 오류를 반환 합니다.  
  
 4000 자 보다 큰 스칼라 값을 반환 해야 할 경우 사용 하 여 **OPENJSON** 대신 **JSON_VALUE**합니다. 자세한 내용은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
## <a name="remarks"></a>주의

### <a name="lax-mode-and-strict-mode"></a>Lax 모드와 strict 모드

 다음 JSON 텍스트를 살펴보십시오.  
  
```json  
DECLARE @jsonInfo NVARCHAR(MAX)

SET @jsonInfo=N'{  
     "info":{    
       "type":1,  
       "address":{    
         "town":"Bristol",  
         "county":"Avon",  
         "country":"England"  
       },  
       "tags":["Sport", "Water polo"]  
    },  
    "type":"Basic"  
 }'  
```  
  
 다음 표에서 비교의 동작 **JSON_VALUE** lax 모드와 strict 모드에서. 선택적인 path 모드 사양 (lax 또는 strict)에 대 한 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|경로|Lax 모드에서 값을 반환 합니다.|Strict 모드에서는 반환 값|추가 정보|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|오류|스칼라 된 값입니다.<br /><br /> 사용 하 여 **JSON_QUERY** 대신 합니다.|  
|$. info.type|N '1'|N '1'|해당 사항 없음|  
|$. info.address.town|N'Bristol'|N'Bristol'|해당 사항 없음|  
|$.info입니다. " address "|NULL|오류|스칼라 된 값입니다.<br /><br /> 사용 하 여 **JSON_QUERY** 대신 합니다.|  
|$. info.tags|NULL|오류|스칼라 된 값입니다.<br /><br /> 사용 하 여 **JSON_QUERY** 대신 합니다.|  
|$. info.type[0]|NULL|오류|배열 되지 않습니다.|  
|$. info.none|NULL|오류|속성이 존재 하지 않습니다.|  
  
## <a name="examples"></a>예  
  
### <a name="example-1"></a>예제 1  
 다음 예제에서는 JSON 속성의 값을 사용 하 여 `town` 및 `state` 쿼리 결과에 있습니다. 이후 **JSON_VALUE** 결과의 정렬 순서 원본의 데이터 정렬의 데이터 정렬에 의존 하는 전처리는 `jsonInfo` 열입니다.  
  
```sql  
SELECT FirstName,LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>예제 2  
 다음 예제에서는 JSON 속성의 값을 추출 `town` 지역 변수에 합니다.  
  
```sql  
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'<array of address info>'

SET @town=JSON_VALUE(@jsonInfo,'$.info.address.town')
```  
  
### <a name="example-3"></a>예 3  
 다음 예제에서는 JSON 속성의 값을 기반으로 하는 계산된 열을 만듭니다.  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(8000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>관련 항목:  
 [JSON 경로 식 &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터 &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
