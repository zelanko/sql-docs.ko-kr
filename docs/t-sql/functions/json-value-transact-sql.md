---
title: JSON_VALUE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- JSON_VALUE
- JSON_VALUE_TSQL
helpviewer_keywords:
- JSON_VALUE function
- JSON, extracting
- JSON, querying
ms.assetid: cd016e14-11eb-4eaf-bf05-c7cfcc820a10
author: jovanpop-msft
ms.author: jovanpop
ms.reviewer: jroth
monikerRange: = azuresqldb-current||= azure-sqldw-latest||>= sql-server-2016||>= sql-server-linux-2017||= sqlallproducts-allversions
ms.openlocfilehash: 7201224aa89f4add1d618b976f8bff0b8857f5c9
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196802"
---
# <a name="json_value-transact-sql"></a>JSON_VALUE(Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

 JSON 문자열에서 스칼라 값을 추출합니다.  
  
 스칼라 값 대신 JSON 문자열에서 개체 또는 배열을 추출하려면 [JSON_QUERY&#40;Transact-SQL&#41;](../../t-sql/functions/json-query-transact-sql.md)를 참조하세요. **JSON_VALUE**와 **JSON_QUERY**의 차이점에 대한 정보는, [JSON_VALUE 및 JSON_QUERY 비교](../../relational-databases/json/validate-query-and-change-json-data-with-built-in-functions-sql-server.md#JSONCompare)를 참조하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
JSON_VALUE ( expression , path )  
```  
  
## <a name="arguments"></a>인수

 *expression*  
 식입니다. 일반적으로 JSON 텍스트를 포함하는 변수 또는 열의 이름입니다.  

 **JSON_VALUE**가 *path*로 식별된 값을 찾기 전에 *expression*에서 유효하지 않은 JSON을 찾으면 함수는 오류를 반환합니다. **JSON_VALUE**가 *path*에 의해 식별된 값을 찾지 못하면, 전체 텍스트를 검사하고 JSON이 유효하지 않고 *expression*에 있는 경우 오류를 반환합니다.
  
 *path*  
 추출할 속성을 지정하는 JSON 경로입니다. 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  

[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]에서 *path* 값으로 변수를 제공할 수 있습니다.
  
 *path*의 형식이 유효하지 않으면 **JSON_VALUE**가 오류를 반환합니다.  
  
## <a name="return-value"></a>반환 값

 nvarchar(4000) 형식의 단일 텍스트 값을 반환합니다. 반환된 값의 데이터 정렬은 입력된 식의 데이터 정렬과 동일합니다.  
  
 값이 4000자를 초과하는 경우:  
  
- lax 모드에서 **JSON_VALUE**는 null을 반환 합니다.  
  
- strict 모드에서 **JSON_VALUE**는 오류를 반환합니다.  
  
 4000자를 초과하는 스칼라 값을 반환해야 하는 경우 **JSON_VALUE** 대신 **OPENJSON**을 사용합니다. 자세한 내용은 [OPENJSON&#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)을 참조하세요.  
  
## <a name="remarks"></a>설명

### <a name="lax-mode-and-strict-mode"></a>lax 모드와 strict 모드

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
  
 다음 표에서는 lax 모드 및 strict 모드에서 **JSON_VALUE**의 동작을 비교합니다. 선택적 경로 모드 사양(lax 또는 strict)에 대한 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  
  
|경로|lax 모드에서 값을 반환합니다.|strict 모드에서 값을 반환합니다.|추가 정보|  
|----------|------------------------------|---------------------------------|---------------|  
|$|NULL|Error|스칼라 값이 아닙니다.<br /><br /> **JSON_QUERY**를 대신 사용합니다.|  
|$.info.type|N'1'|N'1'|해당 사항 없음|  
|$.info.address.town|N'Bristol'|N'Bristol'|해당 사항 없음|  
|$.info."address"|NULL|Error|스칼라 값이 아닙니다.<br /><br /> **JSON_QUERY**를 대신 사용합니다.|  
|$.info.tags|NULL|Error|스칼라 값이 아닙니다.<br /><br /> **JSON_QUERY**를 대신 사용합니다.|  
|$.info.type[0]|NULL|Error|배열이 아닙니다.|  
|$.info.none|NULL|Error|속성이 없습니다.|  
| &nbsp; | &nbsp; | &nbsp; | &nbsp; |
  
## <a name="examples"></a>예  
  
### <a name="example-1"></a>예 1
 다음 예에서는 쿼리 결과에서 JSON 속성 `town` 및 `state`의 값을 사용합니다. **JSON_VALUE**는 원본의 데이터 정렬을 유지하므로 결과의 정렬 순서는 `jsonInfo` 열의 데이터 정렬에 따라 다릅니다. 

> [!NOTE]
> (이 예에서는 `Person.Person` 테이블에 JSON 텍스트의 `jsonInfo` 열이 있고, 이 열의 구조는 이전에 lax 모드 및 strict 모드에 대한 설명에 표시된 구조라고 가정합니다. AdventureWorks 샘플 데이터베이스에서 `Person` 테이블에는 실제로 `jsonInfo`열이 없습니다.)
  
```sql  
SELECT FirstName, LastName,
 JSON_VALUE(jsonInfo,'$.info.address[0].town') AS Town
FROM Person.Person
WHERE JSON_VALUE(jsonInfo,'$.info.address[0].state') LIKE 'US%'
ORDER BY JSON_VALUE(jsonInfo,'$.info.address[0].town')
```  
  
### <a name="example-2"></a>예제 2
 다음 예에서는 JSON 속성 `town`의 값을 로컬 변수로 추출합니다.  
  
```sql
DECLARE @jsonInfo NVARCHAR(MAX)
DECLARE @town NVARCHAR(32)

SET @jsonInfo=N'{"info":{"address":[{"town":"Paris"},{"town":"London"}]}}';

SET @town=JSON_VALUE(@jsonInfo,'$.info.address[0].town'); -- Paris
SET @town=JSON_VALUE(@jsonInfo,'$.info.address[1].town'); -- London
```  
  
### <a name="example-3"></a>예제 3
 다음 예에서는 JSON 속성 값을 기반으로 계산된 열을 만듭니다.  
  
```sql  
CREATE TABLE dbo.Store
 (
  StoreID INT IDENTITY(1,1) NOT NULL,
  Address VARCHAR(500),
  jsonContent NVARCHAR(4000),
  Longitude AS JSON_VALUE(jsonContent, '$.address[0].longitude'),
  Latitude AS JSON_VALUE(jsonContent, '$.address[0].latitude')
 )
```  
  
## <a name="see-also"></a>참고 항목
 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터&#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
