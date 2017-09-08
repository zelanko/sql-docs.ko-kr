---
title: JSON_MODIFY (Transact SQL) | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 06/02/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-json
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 96bc8255-a037-4907-aec4-1a9c30814651
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 70f2c1456da6469c39389fada6a74ccf46383582
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="jsonmodify-transact-sql"></a>JSON_MODIFY (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  JSON 문자열에서 속성의 값을 업데이트 하 고 업데이트 된 JSON 문자열을 반환 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
JSON_MODIFY ( expression , path , newValue )  
```  
  
## <a name="arguments"></a>인수  
 *expression*  
 식입니다. 일반적으로 JSON 텍스트를 포함 하는 열 또는 변수 이름입니다.  
  
 **JSON_MODIFY** 경우 오류가 반환 *식* 유효한 JSON이 포함 되지 않습니다.  
  
 *경로*  
 업데이트할 속성을 지정 하는 JSON 경로 식입니다.

 *경로* 다음 구문을 가집니다.  
  
 `[append] [ lax | strict ] $.<json path>`  
  
-   *추가*  
    새 값에서 참조 하 여 배열에 연결할지를 지정 하는 선택적 한정자  *\<json 경로 >*합니다.  
  
-   *lax*  
    속성에서 참조 하도록 지정  *\<json 경로 >* 존재 필요는 없습니다. 속성이 없으면 JSON_MODIFY 지정된 된 경로에 새 값을 삽입 하려고 시도 합니다. 삽입 속성 경로에 삽입할 수 없을 경우에 실패할 수 있습니다. 지정 하지 않으면 *lax* 또는 *엄격한*, *lax* 기본 모드입니다.  
  
-   *엄격한*  
    속성에서 참조 하도록 지정  *\<json 경로 >* JSON 식에 있어야 합니다. 속성이 없으면 JSON_MODIFY 오류가 반환 됩니다.  
  
-   *\<json 경로 >*  
    업데이트할 속성에 대 한 경로 지정 합니다. 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
[!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)] 및 [!INCLUDE[ssSDSfull_md](../../includes/sssdsfull-md.md)]의 값으로 변수를 제공할 수 있습니다 *경로*합니다.

**JSON_MODIFY** 경우 오류가 반환 형식의 *경로* 유효 하지 않습니다.  
  
 *새 값*  
 지정한 속성에 대 한 새 값 *경로*합니다.  
  
 Lax 모드 JSON_MODIFY 새 값이 NULL이 지정된 된 키를 삭제 합니다.  
  
JSON_MODIFY 값의 형식이 VARCHAR 또는 NVARCHAR 경우 새 값의 모든 특수 문자를 이스케이프 합니다. 텍스트 값은 제대로 경우 이스케이프 되지 않으므로 FOR JSON, JSON_QUERY, 또는 JSON_MODIFY에 의해 생성 된 JSON 형식이 지정 합니다.  
  
## <a name="return-value"></a>반환 값  
 업데이트 된 값을 반환 *식* 제대로 표시 형식 JSON 텍스트입니다.  
  
## <a name="remarks"></a>주의  
 JSON_MODIFY 함수를 사용 하 여 기존 속성의 값을 업데이트, 새 키: 값 쌍을 삽입 또는 모드의 조합에 따라 및 값을 제공한 키를 삭제할 수 있습니다.  
  
 다음 표에서 비교의 동작 **JSON_MODIFY** lax 모드와 strict 모드에서. 선택적인 path 모드 사양 (lax 또는 strict)에 대 한 자세한 내용은 참조 하십시오. [JSON 경로 식 &#40; SQL Server &#41; ](../../relational-databases/json/json-path-expressions-sql-server.md).  
  
|기존 값|경로가 존재|Lax 모드|Strict 모드|  
|--------------------|-----------------|--------------|-----------------|  
|Not NULL|예|기존 값을 업데이트 합니다.|기존 값을 업데이트 합니다.|  
|Not NULL|아니요|지정된 된 경로에서 새 키: 값 쌍을 만들려고 시도 합니다.<br /><br /> 이 실패할 수 있습니다. 예를 들어, 경로 지정 하는 경우 `$.user.setting.theme`, JSON_MODIFY 키를 삽입 하지 않습니다 `theme` 경우는 `$.user` 또는 `$.user.settings` 개체가 존재 하지 않는 설정 또는 스칼라 값이 배열 인지 또는 합니다.|오류 – INVALID_PROPERTY|  
|NULL|예|기존 속성을 삭제 합니다.|기존 값을 null로 설정 합니다.|  
|NULL|아니요|작업이 없습니다. 첫 번째 인수는 결과로 반환 됩니다.|오류 – INVALID_PROPERTY|  
  
 Lax 모드로 JSON_MODIFY 새 키: 값 쌍을 만들 하려고 시도 하지만 일부 경우에 실패할 수 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="example---basic-operations"></a>예-기본 작업  
 다음 예제에서는 JSON 텍스트가 포함 수행할 수 있는 기본 작업을 보여 줍니다.  
  
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
  
### <a name="example---multiple-updates"></a>예-여러 업데이트  
 JSON_MODIFY 하나의 속성만을 업데이트할 수 있습니다. 여러 업데이트를 수행 해야 하는 경우에 여러 JSON_MODIFY 호출을 사용할 수 있습니다.  
  
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
  
### <a name="example---rename-a-key"></a>예-키 이름 바꾸기  
 다음 예제에서는 JSON_MODIFY 함수로 JSON 텍스트에서 속성 이름을 바꾸는 방법을 보여 줍니다. 먼저 기존 속성의 값을 사용할 수 있으며 새 키: 값 쌍으로 삽입할 수 있습니다. 그런 다음 이전 속성 값을 NULL로 설정 하 여 이전 키를 삭제할 수 있습니다.  
  
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
  
 숫자 형식으로 새 값을 캐스팅 하지 않는 경우 JSON_MODIFY는 텍스트로 처리 하 고 큰따옴표로 묶습니다.  
  
### <a name="example---increment-a-value"></a>예-증가 값  
 다음 예제에서는 JSON_MODIFY 함수로 JSON 텍스트에서 속성의 값이 증가 하는 방법을 보여 줍니다. 먼저 기존 속성의 값을 사용할 수 있으며 새 키: 값 쌍으로 삽입할 수 있습니다. 그런 다음 이전 속성 값을 NULL로 설정 하 여 이전 키를 삭제할 수 있습니다.  
  
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
  
### <a name="example---modify-a-json-object"></a>예-JSON 개체를 수정 합니다.  
 JSON_MODIFY 처리는 *newValue* 제대로 포함 된 경우에 일반 텍스트로 인수 형식이 JSON 텍스트를 지정 합니다. 결과적으로, 함수의 JSON 출력은 큰따옴표로 묶여 다음 예제에 나와 있는 것 처럼 모든 특수 문자는 이스케이프 합니다.  
  
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
  
 자동 이스케이프를 방지 하려면 제공 *newValue* JSON_QUERY 함수를 사용 하 여 합니다. JSON_MODIFY 임을 알고 JSON_MODIFY에서 반환한 값 올바르게 포맷 JSON 값을 이스케이프 하지 않습니다.  
  
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
  
### <a name="example---update-a-json-column"></a>예-JSON 열의 업데이트  
 다음 예제에서는 JSON이 포함 된 테이블 열에 속성의 값을 업데이트 합니다.  
  
```sql  
UPDATE Employee
SET jsonCol=JSON_MODIFY(jsonCol,"$.info.address.town",'London')
WHERE EmployeeID=17
 
```  
  
## <a name="see-also"></a>관련 항목:  
 [JSON 경로 식 &#40; SQL Server &#41;](../../relational-databases/json/json-path-expressions-sql-server.md)   
 [JSON 데이터 &#40; SQL Server &#41;](../../relational-databases/json/json-data-sql-server.md)  
  
  

