---
description: CHANGETABLE(Transact-SQL)
title: CHANGETABLE (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGETABLE_TSQL
- CHANGETABLE
dev_langs:
- TSQL
helpviewer_keywords:
- CHANGETABLE
- change tracking [SQL Server], CHANGETABLE
ms.assetid: d405fb8d-3b02-4327-8d45-f643df7f501a
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4f142f5de6f5580e7b0e21658e4b3c276984cd88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474705"
---
# <a name="changetable-transact-sql"></a>CHANGETABLE(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  테이블에 대한 변경 내용 추적 정보를 반환합니다. 이 문을 사용하여 테이블에 대한 모든 변경 내용이나 특정 행에 대한 변경 내용 추적 정보를 반환할 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql
CHANGETABLE (  
    { CHANGES table , last_sync_version  
    | VERSION table , <primary_key_values> } )  
[AS] table_alias [ ( column_alias [ ,...n ] )  
  
<primary_key_values> ::=  
( column_name [ , ...n ] ) , ( value [ , ...n ] )  
```  
  
## <a name="arguments"></a>인수  
 변경 *테이블* , *last_sync_version*  
 *Last_sync_version*지정 된 버전 이후에 발생 한 테이블의 모든 변경 내용에 대 한 추적 정보를 반환 합니다.  
  
 *table*  
 추적된 변경 내용을 가져올 사용자 정의 테이블입니다. 테이블에서 변경 내용 추적을 사용할 수 있어야 합니다. 한 부분, 두 부분, 세 부분 또는 네 부분으로 이루어진 테이블 이름을 사용할 수 있습니다. 테이블 이름은 테이블에 대한 동의어가 될 수 있습니다.  
  
 *last_sync_version*  
 변경 내용을 가져올 때 호출 애플리케이션은 변경 내용이 필요한 지점을 지정해야 합니다. last_sync_version은 이러한 지점을 지정합니다. 이 함수는 해당 버전 이후 변경된 모든 행에 대한 정보를 반환합니다. 애플리케이션은 last_sync_version 이후 버전의 변경 내용을 쿼리하여 받습니다.  
  
 일반적으로 변경 내용을 가져오기 전에 응용 프로그램은 **CHANGE_TRACKING_CURRENT_VERSION ()** 를 호출 하 여 다음에 변경 해야 하는 경우 사용 될 버전을 가져옵니다. 따라서 애플리케이션은 실제 값을 해석하거나 이해할 필요가 없습니다.  
  
 호출 애플리케이션에서 last_sync_version을 가져오므로 애플리케이션은 값을 유지해야 합니다. 애플리케이션에서 이 값을 손실하면 데이터를 다시 초기화해야 합니다.  
  
 *last_sync_version* 는 **bigint**입니다. 값은 스칼라여야 합니다. 식은 구문 오류를 야기합니다.  
  
 값이 NULL이면 추적되는 모든 변경 내용이 반환됩니다.  
  
 일부 또는 모든 변경 정보가 데이터베이스에 대해 구성 된 보존 기간에 따라 정리 되었을 수 있기 때문에 *last_sync_version* 의 유효성을 검사 하 여 너무 오래 되지 않았는지 확인 해야 합니다. 자세한 내용은 [CHANGE_TRACKING_MIN_VALID_VERSION &#40;transact-sql&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md) 및 [ALTER database SET 옵션 &#40;transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조 하세요.  
  
 버전 *테이블*, {<primary_key_values>}  
 지정된 행에 대한 최신 변경 내용 추적 정보를 반환합니다. 기본 키 값은 행을 식별해야 합니다. <primary_key_values> 기본 키 열을 식별 하 고 값을 지정 합니다. 기본 키 열 이름은 지정되는 순서에 제한을 받지 않습니다.  
  
 *테이블*  
 변경 내용 추적 정보를 가져올 사용자 정의 테이블입니다. 테이블에서 변경 내용 추적을 사용할 수 있어야 합니다. 한 부분, 두 부분, 세 부분 또는 네 부분으로 이루어진 테이블 이름을 사용할 수 있습니다. 테이블 이름은 테이블에 대한 동의어가 될 수 있습니다.  
  
 *column_name*  
 기본 키 열의 이름을 지정합니다. 여러 열 이름은 지정되는 순서에 제한을 받지 않습니다.  
  
 *값*  
 기본 키의 값입니다. 기본 키 열이 여러 개 있는 경우 *column_name* 목록에 열이 표시 되는 순서 대로 값을 지정 해야 합니다.  
  
 는 *table_alias* [(*column_alias* [,... *n* ])]  
 CHANGETABLE에서 반환하는 결과의 이름을 제공합니다.  
  
 *table_alias*  
 CHANGETABLE에서 반환하는 테이블의 별칭 이름입니다. *table_alias* 필요 하며 유효한 [식별자](../../relational-databases/databases/database-identifiers.md)여야 합니다.  
  
 *column_alias*  
 CHANGETABLE에서 반환하는 열에 대한 선택적 열 별칭 또는 열 별칭의 목록입니다. 결과에 중복 이름이 있는 경우 열 이름을 사용자 지정할 수 있습니다.  
  
## <a name="return-types"></a>반환 형식  
 **table**  
  
## <a name="return-values"></a>반환 값  
  
### <a name="changetable-changes"></a>CHANGETABLE CHANGES  
 CHANGES를 지정하면 다음 열이 있는 0개 이상의 행이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|행의 마지막 변경 내용과 연관된 버전 값입니다.|  
|SYS_CHANGE_CREATION_VERSION|**bigint**|마지막 삽입 작업과 연관된 버전 값입니다.|  
|SYS_CHANGE_OPERATION|**nchar(1)**|다음과 같은 변경 형식을 지정합니다.<br /><br /> **U** = 업데이트<br /><br /> **I** = 삽입<br /><br /> **D** = 삭제|  
|SYS_CHANGE_COLUMNS|**varbinary(4100)**|last_sync_version(기준) 이후에 변경된 열을 나열합니다. 계산 열은 변경 된 것으로 표시 되지 않습니다.<br /><br /> 다음 조건 중 하나가 충족되는 경우 값은 NULL입니다.<br /><br /> 열 변경 내용 추적을 사용할 수 없는 경우<br /><br /> 작업이 삽입 또는 삭제 작업인 경우<br /><br /> 모든 비기본 키 열이 단일 작업에서 업데이트된 경우. 이 이진 값을 직접 해석하면 안 됩니다. 대신 [CHANGE_TRACKING_IS_COLUMN_IN_MASK ()](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)를 사용 합니다.|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|[WITH](../../relational-databases/system-functions/with-change-tracking-context-transact-sql.md) 절을 INSERT, UPDATE 또는 DELETE 문의 일부로 사용 하 여 선택적으로 지정할 수 있는 컨텍스트 정보를 변경 합니다.|  
|\<primary key column value>|사용자 테이블 열과 같음|추적된 테이블의 기본 키 값입니다. 이러한 값은 사용자 테이블의 각 행을 고유하게 식별합니다.|  
  
### <a name="changetable-version"></a>CHANGETABLE VERSION  
 VERSION을 지정하면 다음 열이 있는 하나의 행이 반환됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|SYS_CHANGE_VERSION|**bigint**|행과 연관된 현재 변경 버전 값입니다.<br /><br /> 변경 내용 추적 보존 기간보다 긴 기간 동안 변경된 내용이 없거나, 변경 내용 추적이 사용된 이후 변경된 행이 없을 경우 이 값은 NULL입니다.|  
|SYS_CHANGE_CONTEXT|**varbinary(128)**|WITH 절을 INSERT, UPDATE 또는 DELETE 문의 일부로 사용하여 선택적으로 지정할 수 있는 컨텍스트 정보를 변경합니다.|  
|\<primary key column value>|사용자 테이블 열과 같음|추적된 테이블의 기본 키 값입니다. 이러한 값은 사용자 테이블의 각 행을 고유하게 식별합니다.|  
  
## <a name="remarks"></a>설명  
 CHANGETABLE 함수는 일반적으로 쿼리의 FROM 절에서 테이블인 것처럼 사용할 수 있습니다.  
  
## <a name="changetablechanges"></a>CHANGETABLE(CHANGES...)  
 새 행이나 수정된 행의 행 데이터를 가져오려면 기본 키 열을 사용하여 사용자 테이블에 결과 세트를 조인합니다. 변경 된 사용자 테이블의 각 행에 대해 하나의 행만 반환 됩니다. *last_sync_version* 값 이후 동일한 행에 대 한 변경 내용이 여러 개 있는 경우에도 마찬가지입니다.  
  
 기본 키 열 변경 내용은 업데이트로 표시되지 않습니다. 기본 키 값이 변경되면 이전 값의 삭제 및 새 값의 삽입으로 간주됩니다.  
  
 행을 삭제한 다음 이전 기본 키가 있는 행을 삽입하면 변경 내용이 행의 모든 열에 대한 업데이트로 표시됩니다.  
  
 SYS_CHANGE_OPERATION 및 SYS_CHANGE_COLUMNS 열에 대해 반환 되는 값은 지정 된 기준 (last_sync_version)을 기준으로 합니다. 예를 들어 버전 10에서 삽입 작업이 수행 되 고 버전 15에서 업데이트 작업이 수행 되었으며 기준 *last_sync_version* 12 인 경우 업데이트가 보고 됩니다. *Last_sync_version* 값이 8 이면 삽입이 보고 됩니다. SYS_CHANGE_COLUMNS는 계산 열을 업데이트된 것으로 보고하지 않습니다.  
  
 일반적으로 MERGE 문을 비롯하여 사용자 테이블에서 데이터를 삽입, 업데이트 또는 삭제하는 모든 작업은 추적됩니다.  
  
 사용자 테이블 데이터에 영향을 미치는 다음 작업은 추적되지 않습니다.  
  
-   UPDATETEXT 문 실행  
  
     이 문은 더 이상 사용되지 않으며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 이후 버전에서는 제거될 예정입니다. 그러나 UPDATE 문의 .WRITE 절을 사용하여 적용된 변경 사항은 추적됩니다.  
  
-   TRUNCATE TABLE을 사용하여 행 삭제  
  
     테이블이 잘리면 변경 내용 추적이 테이블에 설정된 것처럼 이 테이블과 연관된 변경 내용 추적 버전 정보가 다시 설정됩니다. 클라이언트 애플리케이션에서는 항상 마지막으로 동기화된 버전의 유효성을 검사해야 합니다. 테이블이 잘린 경우 유효성 검사에 실패합니다.  
  
## <a name="changetableversion"></a>CHANGETABLE(VERSION...)  
 존재하지 않는 기본 키를 지정하면 빈 결과 집합이 반환됩니다.  
  
 보존 기간보다 긴 기간 동안, 정리 프로세스가 변경 정보를 제거하는 등의 변경된 내용이 없거나 테이블에 대해 변경 내용 추적을 설정한 이후 변경된 행이 없을 경우 SYS_CHANGE_VERSION 값은 NULL일 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 에는 변경 내용 추적 정보를 가져오기 위해 *테이블* 값으로 지정 된 테이블에 대 한 다음 권한이 필요 합니다.  
  
-   기본 키 열의 SELECT 권한  
  
-   VIEW CHANGE TRACKING  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-rows-for-an-initial-synchronization-of-data"></a>A. 데이터의 초기 동기화에 대한 행 반환  
 다음 예제에서는 테이블 데이터의 초기 동기화에 대한 데이터를 가져오는 방법을 보여 줍니다. 쿼리는 모든 행 데이터 및 연관된 버전을 반환합니다. 그러면 동기화된 데이터를 포함하는 시스템에 이 데이터를 추가하거나 삽입할 수 있습니다.  
  
```sql  
-- Get all current rows with associated version  
SELECT e.[Emp ID], e.SSN, e.FirstName, e.LastName,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_CONTEXT  
FROM Employees AS e  
CROSS APPLY CHANGETABLE   
    (VERSION Employees, ([Emp ID], SSN), (e.[Emp ID], e.SSN)) AS c;  
```  
  
### <a name="b-listing-all-changes-that-were-made-since-a-specific-version"></a>B. 특정 버전 이후의 모든 변경 내용 나열  
 다음 예에서는 지정된 버전(`@last_sync_version)` 이후에 테이블에서 변경된 내용을 모두 나열합니다. [Emp ID] 및 SSN은 복합 기본 키에 있는 열입니다.  
  
```sql  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT [Emp ID], SSN,  
    SYS_CHANGE_VERSION, SYS_CHANGE_OPERATION,  
    SYS_CHANGE_COLUMNS, SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS C;  
```  
  
### <a name="c-obtaining-all-changed-data-for-a-synchronization"></a>C. 동기화를 위해 변경된 모든 데이터 가져오기  
 다음 예에서는 변경된 모든 데이터를 가져오는 방법을 보여 줍니다. 이 쿼리는 변경 내용 추적 정보를 사용자 테이블과 조인하여 사용자 테이블 정보가 반환되게 합니다. 삭제된 행에 대해 하나의 행이 반환되도록 `LEFT OUTER JOIN`이 사용됩니다.  
  
```sql  
-- Get all changes (inserts, updates, deletes)  
DECLARE @last_sync_version bigint;  
SET @last_sync_version = <value obtained from query>;  
SELECT e.FirstName, e.LastName, c.[Emp ID], c.SSN,  
    c.SYS_CHANGE_VERSION, c.SYS_CHANGE_OPERATION,  
    c.SYS_CHANGE_COLUMNS, c.SYS_CHANGE_CONTEXT   
FROM CHANGETABLE (CHANGES Employees, @last_sync_version) AS c  
    LEFT OUTER JOIN Employees AS e  
        ON e.[Emp ID] = c.[Emp ID] AND e.SSN = c.SSN;  
```  
  
### <a name="d-detecting-conflicts-by-using-changetableversion"></a>D. CHANGETABLE(VERSION...)을 사용하여 충돌 검색  
 다음 예에서는 행에 마지막 동기화 이후의 변경 내용이 없는 경우에만 행을 업데이트하는 방법을 보여 줍니다. 특정 행의 버전 번호는 `CHANGETABLE`을 사용하여 얻습니다. 행이 업데이트되었으면 변경 내용이 적용되지 않으며 쿼리가 행의 최근 변경 내용에 대한 정보를 반환합니다.  
  
```sql  
-- @last_sync_version must be set to a valid value  
UPDATE  
    SalesLT.Product  
SET  
    ListPrice = @new_listprice  
FROM  
    SalesLT.Product AS P  
WHERE  
    ProductID = @product_id AND  
    @last_sync_version >= ISNULL (  
        (SELECT CT.SYS_CHANGE_VERSION FROM   
            CHANGETABLE(VERSION SalesLT.Product,  
            (ProductID), (P.ProductID)) AS CT),  
        0);  
```  
  
## <a name="see-also"></a>참고 항목  
 [변경 내용 추적 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [데이터 변경 내용 추적&#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)   
 [Transact-sql&#41;CHANGE_TRACKING_IS_COLUMN_IN_MASK &#40;](../../relational-databases/system-functions/change-tracking-is-column-in-mask-transact-sql.md)   
 [Transact-sql&#41;CHANGE_TRACKING_CURRENT_VERSION &#40;](../../relational-databases/system-functions/change-tracking-current-version-transact-sql.md)   
 [CHANGE_TRACKING_MIN_VALID_VERSION&#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)  
  
  
