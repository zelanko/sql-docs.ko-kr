---
title: JSON_MODIFY(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: douglasl
ms.suite: sql
ms.technology:
- dbe-json
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: c9fcc143dcb154af9faabff556c5f9a23749498c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON 문자열의 속성 값을 업데이트하고 업데이트된 JSON 문자열을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 식입니다. 일반적으로 JSON 텍스트를 포함하는 변수 또는 열의 이름입니다.  
  
 **JSON_MODIFY**는 *expression*에 유효한 JSON이 포함되지 않은 경우 오류를 반환합니다.  
  
 *path*  
 업데이트할 속성을 지정하는 JSON 경로 식입니다.

 *path*에는 다음 구문이 있습니다.  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *append*  
    *\<json path>* 가 참조하는 배열에 새 값을 추가하도록 지정하는 선택적 한정자입니다.  
  
-   *lax*  
    *\<json path>* 가 참조하는 속성이 존재하지 않아도 된다는 것을 지정합니다. 속성이 없으면 JSON_MODIFY가 지정된 경로에 새 값을 삽입하려고 시도합니다. 속성을 경로에 삽입할 수 없는 경우 삽입이 실패할 수 있습니다. *lax* 또는 *strict*를 지정하지 않으면 *lax*가 기본 모드입니다.  
  
-   *strict*  
    *\<json path>* 가 참조하는 속성이 JSON 식에 있어야 함을 지정합니다. 속성이 없으면 JSON_MODIFY가 오류를 반환합니다.  
  
-   *\<json path>*  
    업데이트할 속성에 대한 경로를 지정합니다. 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  
  
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]에서 *path* 값으로 변수를 제공할 수 있습니다.

*path*의 형식이 유효하지 않으면 **JSON_MODIFY**가 오류를 반환합니다.  
  
 *newValue*  
 *path*로 지정된 속성의 새 값입니다.  
  
 lax 모드에서 JSON_MODIFY는 새 값이 NULL일 경우 지정된 키를 삭제합니다.  
  
JSON_MODIFY는 값의 형식이 VARCHAR 또는 NVARCHAR인 경우 새 값의 모든 특수 문자를 이스케이프합니다. FOR JSON, JSON_QUERY 또는 JSON_MODIFY에 의해 생성된 JSON 형식이 올바르다면 텍스트 값은 이스케이프되지 않습니다.  
  
## <a name="return-value"></a>반환 값  
 올바른 형식의 JSON 텍스트로 *expression*의 업데이트된 값을 반환합니다.  
  
## <a name="remarks"></a>Remarks  
 JSON_MODIFY 함수를 사용하여 기존 속성의 값을 업데이트하거나, 새 키:값 쌍을 삽입하거나, 모드와 제공된 값의 조합을 기반으로 키를 삭제할 수 있습니다.  
  
 다음 표에서는 lax 모드 및 strict 모드에서 **JSON_MODIFY**의 동작을 비교합니다. 선택적 경로 모드 사양(lax 또는 strict)에 대한 자세한 내용은 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)을 참조하세요.  
  
|기존 값|경로가 존재|lax 모드|strict 모드|  
|--------------------|-----------------|--------------|-----------------|  
|NOT NULL|예|기존 값을 업데이트합니다.|기존 값을 업데이트합니다.|  
|NOT NULL|아니오|지정된 경로에서 새 키:값 쌍을 만들려고 시도합니다.<br /><br /> 이는 실패할 수 있습니다. 예를 들어 경로 `$.user.setting.theme`을 지정하면, JSON_MODIFY는 `$.user` 또는 `$.user.settings` 개체가 존재하지 않거나 설정이 배열 또는 스칼라 값인 경우 키 `theme`을 삽입하지 않습니다.|오류 – INVALID_PROPERTY|  
|NULL|예|기존 속성을 삭제합니다.|기존 값을 null로 설정합니다.|  
|NULL|아니오|동작이 없습니다. 첫 번째 인수가 결과로 반환됩니다.|오류 – INVALID_PROPERTY|  
  
 lax 모드에서 JSON_MODIFY는 새 키:값 쌍을 만들려고 시도하지만 일부 경우에는 실패할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="example---basic-operations"></a>예 - 기본 작업  
 다음 예제에서는 JSON 텍스트를 사용하여 수행할 수 있는 기본 작업을 보여줍니다.  
  
 **쿼리**  
  
```sql  

DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update name  

SET @info=JSON_MODIFY(@info,'$.name','Mike')

PRINT @info

-- Insert surname  

SET @info=JSON_MODIFY(@info,'$.surname','Smith')

PRINT @info

-- Delete name  

SET @info=JSON_MODIFY(@info,'$.name',NULL)

PRINT @info

-- Add skill  

SET @info=JSON_MODIFY(@info,'append $.skills','Azure')

PRINT @info
```  
  
 **결과**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL"],
    "surname": "Smith"
} {
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---multiple-updates"></a>예 - 여러 개 업데이트  
 JSON_MODIFY를 사용하면 하나의 속성만 업데이트할 수 있습니다. 여러 개를 업데이트를 해야 하는 경우 여러 JSON_MODIFY 호출을 사용할 수 있습니다.  
  
 **쿼리**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Multiple updates  

SET @info=JSON_MODIFY(JSON_MODIFY(JSON_MODIFY(@info,'$.name','Mike'),'$.surname','Smith'),'append $.skills','Azure')

PRINT @info
```  
  
 **결과**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "Mike",
    "skills": ["C#", "SQL", "Azure"],
    "surname": "Smith"
}
```  
  
### <a name="example---rename-a-key"></a>예 - 키 이름 바꾸기  
 다음 예에서는 JSON_MODIFY 함수를 사용하여 JSON 텍스트의 속성 이름을 바꾸는 방법을 보여줍니다. 먼저 기존 속성의 값을 가져와 새 키:값 쌍으로 삽입할 수 있습니다. 그런 다음, 이전 속성 값을 NULL로 설정하여 이전 키를 삭제할 수 있습니다.  
  
 **쿼리**  
  
```sql  
DECLARE @product NVARCHAR(100)='{"price":49.99}'

PRINT @product

-- Rename property  

SET @product=
 JSON_MODIFY(
  JSON_MODIFY(@product,'$.Price',CAST(JSON_VALUE(@product,'$.price') AS NUMERIC(4,2))),
  '$.price',
  NULL
 )

PRINT @product
```  
  
 **결과**  
  
```json  
{
    "price": 49.99
} {
    "Price": 49.99
}
```  
  
 새 값을 숫자 형식으로 캐스팅하지 않는 경우 JSON_MODIFY가 이를 텍스트로 처리하고 큰따옴표로 묶습니다.  
  
### <a name="example---increment-a-value"></a>예 - 값 증분  
 다음 예에서는 JSON_MODIFY 함수를 사용하여 JSON 텍스트의 속성 값을 증분하는 방법을 보여줍니다. 먼저 기존 속성의 값을 가져와 새 키:값 쌍으로 삽입할 수 있습니다. 그런 다음, 이전 속성 값을 NULL로 설정하여 이전 키를 삭제할 수 있습니다.  
  
 **쿼리**  
  
```sql  
DECLARE @stats NVARCHAR(100)='{"click_count": 173}'

PRINT @stats

-- Increment value  

SET @stats=JSON_MODIFY(@stats,'$.click_count',
 CAST(JSON_VALUE(@stats,'$.click_count') AS INT)+1)

PRINT @stats
```  
  
 **결과**  
  
```json  
{
    "click_count": 173
} {
    "click_count": 174
}
```  
  
### <a name="example---modify-a-json-object"></a>예 - JSON 개체 수정  
 JSON_MODIFY는 올바른 형식의 JSON 텍스트가 포함되어 있어도 *newValue* 인수를 일반 텍스트로 취급합니다. 결과적으로, 다음 예와 같이 함수의 JSON 출력은 큰따옴표로 묶이고 모든 특수 문자는 이스케이프됩니다.  
  
 **쿼리**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array

SET @info=JSON_MODIFY(@info,'$.skills','["C#","T-SQL","Azure"]')

PRINT @info
```  
  
 **결과**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": "["C#","T-SQL","Azure"]"
}
```  
  
 자동 이스케이프를 방지하려면 JSON_QUERY 함수를 사용하여 *newValue*를 제공하세요. JSON_MODIFY는 JSON_MODIFY가 반환한 값이 올바른 형식의 JSON임을 알고 값을 이스케이프하지 않습니다.  
  
 **쿼리**  
  
```sql  
DECLARE @info NVARCHAR(100)='{"name":"John","skills":["C#","SQL"]}'

PRINT @info

-- Update skills array  

SET @info=JSON_MODIFY(@info,'$.skills',JSON_QUERY('["C#","T-SQL","Azure"]'))

PRINT @info
```  
  
 **결과**  
  
```json  
{
    "name": "John",
    "skills": ["C#", "SQL"]
} {
    "name": "John",
    "skills": ["C#", "T-SQL", "Azure"]
}
```  
  
### <a name="example---update-a-json-column"></a>예 - JSON 열 업데이트  
 다음 예에서는 JSON이 포함된 테이블 열에서 속성 값을 업데이트합니다.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>참고 항목  
 [JSON 경로 식&#40;SQL Server&#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터&#40;SQL Server&#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  
