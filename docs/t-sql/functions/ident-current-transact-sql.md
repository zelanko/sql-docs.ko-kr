---
description: IDENT_CURRENT(Transact-SQL)
title: IDENT_CURRENT(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- IDENT_CURRENT
- IDENT_CURRENT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- last identity value generated for table
- identity values [SQL Server], last generated
- identity columns, current value
- IDENT_CURRENT function
ms.assetid: 21517ced-39f5-4cd8-8d9c-0a0b8aff554a
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: a4fe77504233fe2569a978c9f51c34e4e2236993
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91116335"
---
# <a name="ident_current-transact-sql"></a>IDENT_CURRENT(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

지정된 테이블 또는 뷰에 대해 생성된 마지막 ID 값을 반환합니다. 생성된 마지막 ID 값은 임의의 세션 및 범위에 대한 값일 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql  
IDENT_CURRENT( 'table_or_view' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
*table_or_view*  
ID 값을 반환할 테이블 또는 뷰의 이름입니다. *table_or_view*는 **varchar**이며 기본값은 없습니다.  
  
## <a name="return-types"></a>반환 형식  
**numeric**([@@MAXPRECISION](../../t-sql/functions/max-precision-transact-sql.md),0))  
  
## <a name="exceptions"></a>예외  
오류가 발생하거나 호출자가 개체를 볼 수 있는 권한을 갖고 있지 않으면 NULL을 반환합니다.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 사용자는 소유하고 있거나 사용 권한을 부여받은 보안 개체의 메타데이터만 볼 수 있습니다. 즉, 사용자가 개체에 대한 사용 권한이 없으면 IDENT_CURRENT와 같은 메타데이터 내보내기 기본 제공 함수가 NULL을 반환합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="remarks"></a>설명  
IDENT_CURRENT는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] IDENTITY 함수 SCOPE_IDENTITY 및 @@IDENTITY와 유사합니다. 이 세 함수는 모두 최근에 생성된 ID 값을 반환합니다. 그러나 각 함수에서 *last*가 정의하는 범위와 세션은 각기 다릅니다.  

-   IDENT_CURRENT는 임의의 세션과 범위에 있는 특정 테이블에 대해 최근 생성된 ID 값을 반환합니다.  
-   @@IDENTITY은 현재 세션의 전체 범위에 걸쳐 임의의 테이블에 대해 최근 생성된 ID 값을 반환합니다.  
-   SCOPE_IDENTITY는 현재 세션 및 현재 범위에 있는 임의의 테이블에 대해 최근 생성된 ID 값을 반환합니다.  
  
IDENT_CURRENT 값이 NULL인 경우(테이블에 행이 포함된 적이 없거나 테이블이 잘린 경우) IDENT_CURRENT 함수는 초기값을 반환합니다.  
  
문 및 트랜잭션이 실패해도 테이블의 현재 ID가 변경되고 ID 열 값 간에 간격이 생성될 수 있습니다. 테이블에 값을 삽입하려고 시도한 트랜잭션이 커밋되지 않아도 ID 값은 롤백되지 않습니다. 예를 들어 IGNORE_DUP_KEY 위반으로 인해 INSERT 문이 실패해도 테이블의 현재 ID 값은 계속 증가합니다.  

조인이 포함된 뷰에서 IDENT_CURRENT를 사용하는 경우 NULL이 반환됩니다. 이러한 결과는 ID 열이 단지 하나의 조인된 테이블에만 있는지 또는 둘 이상의 조인된 테이블에 있는지에 관계 없이 발생합니다. 
  
> [!IMPORTANT]
> IDENT_CURRENT를 사용하여 다음에 생성되는 ID 값을 예측할 때는 유의하세요. 다른 세션에서 삽입 작업을 수행하므로 실제로 생성된 값은 IDENT_CURRENT에 IDENT_INCR을 더한 값과 다를 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-returning-the-last-identity-value-generated-for-a-specified-table"></a>A. 지정된 테이블에 대해 마지막으로 생성된 ID 값 반환  
 다음 예에서는 `Person.Address` 데이터베이스의 `AdventureWorks2012` 테이블에 대해 마지막으로 생성된 ID 값을 반환합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT IDENT_CURRENT ('Person.Address') AS Current_Identity;  
GO  
```  
  
### <a name="b-comparing-identity-values-returned-by-ident_current-identity-and-scope_identity"></a>B. IDENT_CURRENT, @@IDENTITY 및 SCOPE_IDENTITY에서 반환된 ID 값 비교  
 다음 예에서는 `IDENT_CURRENT`, `@@IDENTITY` 및 `SCOPE_IDENTITY`가 반환하는 서로 다른 ID 값을 보여 줍니다.  
  
```sql 
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N't6', N'U') IS NOT NULL   
    DROP TABLE t6;  
GO  
IF OBJECT_ID(N't7', N'U') IS NOT NULL   
    DROP TABLE t7;  
GO  
CREATE TABLE t6(id INT IDENTITY);  
CREATE TABLE t7(id INT IDENTITY(100,1));  
GO  
CREATE TRIGGER t6ins ON t6 FOR INSERT   
AS  
BEGIN  
   INSERT t7 DEFAULT VALUES  
END;  
GO  
--End of trigger definition  
  
SELECT id FROM t6;  
--IDs empty.  
  
SELECT id FROM t7;  
--ID is empty.  
  
--Do the following in Session 1  
INSERT t6 DEFAULT VALUES;  
SELECT @@IDENTITY;  
/*Returns the value 100. This was inserted by the trigger.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns the value 1. This was inserted by the   
INSERT statement two statements before this query.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns value inserted into t7, that is in the trigger.*/  
  
SELECT IDENT_CURRENT('t6');  
/* Returns value inserted into t6. This was the INSERT statement four statements before this query.*/  
  
-- Do the following in Session 2.  
SELECT @@IDENTITY;  
/* Returns NULL because there has been no INSERT action   
up to this point in this session.*/  
  
SELECT SCOPE_IDENTITY();  
/* Returns NULL because there has been no INSERT action   
up to this point in this scope in this session.*/  
  
SELECT IDENT_CURRENT('t7');  
/* Returns the last value inserted into t7.*/  
```  
  
## <a name="see-also"></a>참고 항목  
 [@@IDENTITY&#40;Transact-SQL&#41;](../../t-sql/functions/identity-transact-sql.md)   
 [SCOPE_IDENTITY &#40;Transact-SQL&#41;](../../t-sql/functions/scope-identity-transact-sql.md)   
 [IDENT_INCR&#40;Transact-SQL&#41;](../../t-sql/functions/ident-incr-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [식&#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
