---
title: PERMISSIONS(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- PERMISSIONS_TSQL
- PERMISSIONS
dev_langs:
- TSQL
helpviewer_keywords:
- permissions [SQL Server], verifying
- current permission status
- users [SQL Server], permissions status
- checking permission status
- security [SQL Server], permissions
- verifying permission status
- testing permissions
- PERMISSIONS function
ms.assetid: 81625a56-b160-4424-91c5-1ce8b259a8e6
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: fc38de8bffc09461dc69a24acf15ce143276422b
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "73843626"
---
# <a name="permissions-transact-sql"></a>PERMISSIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  현재 사용자의 문, 개체 또는 열 사용 권한을 나타내는 비트맵이 포함된 값을 반환합니다.  
  
 **중요** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 대신, [fn_my_permissions](../../relational-databases/system-functions/sys-fn-my-permissions-transact-sql.md) 및 [Has_Perms_By_Name](../../t-sql/functions/has-perms-by-name-transact-sql.md)을 사용합니다. PERMISSIONS 함수를 계속 사용하면 성능이 저하될 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
PERMISSIONS ( [ objectid [ , 'column' ] ] )  
```  
  
## <a name="arguments"></a>인수  
 *objectid*  
 보안 개체의 ID입니다. *objectid*를 지정하지 않으면 현재 사용자의 문 사용 권한이 비트맵 값에 포함됩니다. 이 값을 지정하면 현재 사용자의 해당 보안 개체에 대한 사용 권한이 비트맵 값에 포함됩니다. 지정한 보안 개체가 현재 데이터베이스에 있어야 합니다. [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md) 함수를 사용하여 *objectid* 값을 확인할 수 있습니다.  
  
 **'** *column* **'**  
 사용 권한 정보를 반환할 열의 선택적 이름입니다. 이 열은 *objectid*로 지정한 테이블에서 유효한 열 이름이어야 합니다.  
  
## <a name="return-types"></a>반환 형식  
 **int**  
  
## <a name="remarks"></a>설명  
 PERMISSIONS는 현재 사용자가 문을 실행하거나 다른 사용자에게 사용 권한을 부여할 수 있는 권한이 있는지 여부를 확인하는 데 사용할 수 있습니다.  
  
 사용 권한 정보는 32비트 비트맵으로 반환됩니다.  
  
 하위 16비트는 사용자에게 부여된 사용 권한 및 현재 사용자가 멤버로 속한 Windows 그룹 또는 고정 서버 역할에 적용되는 사용 권한을 나타냅니다. 예를 들어 *objectid*를 지정하지 않은 경우 반환 값 66(16진수 값 0x42)은 사용자에게 CREATE TABLE(10진수 값 2) 문과 BACKUP DATABASE(10진수 값 64) 문을 실행할 수 있는 권한이 있음을 나타냅니다.  
  
 상위 16비트는 사용자가 다른 사용자에게 부여할 수 있는 사용 권한을 나타냅니다. 상위 16비트는 65536으로 곱한 결과 왼쪽으로 16비트가 이동된다는 점을 제외하고 다음 표에 설명된 하위 16비트와 똑같이 해석됩니다. 예를 들어 *objectid*를 지정한 경우 0x8(10진수 값 8)은 INSERT 사용 권한을 나타내는 비트입니다. 반면 0x80000(십진수 값 524288)은 INSERT 권한을 부여할 수 있음을 나타냅니다. 524288 = 8 x 65536이기 때문입니다.  
  
 역할의 멤버로 속한 사용자는 문을 실행할 수 있는 권한이 없더라도 다른 사용자에게 사용 권한을 부여할 수는 있습니다.  
  
 다음 표에서는 *objectid*를 지정하지 않은 경우 명령문 사용 권한에 사용되는 비트를 보여 줍니다.  
  
|비트(10진수)|비트(16진수)|문 사용 권한|  
|-----------------|-----------------|--------------------------|  
|1|0x1|CREATE DATABASE(master 데이터베이스에만 해당)|  
|2|0x2|CREATE TABLE|  
|4|0x4|CREATE PROCEDURE|  
|8|0x8|CREATE VIEW|  
|16|0x10|CREATE RULE|  
|32|0x20|CREATE DEFAULT|  
|64|0x40|BACKUP DATABASE|  
|128|0x80|BACKUP LOG|  
|256|0x100|Reserved|  
  
 다음 표에서는 *objectid*만 지정한 경우 반환되는 개체 사용 권한에 사용되는 비트를 보여 줍니다.  
  
|비트(10진수)|비트(16진수)|문 사용 권한|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT ALL|  
|2|0x2|UPDATE ALL|  
|4|0x4|REFERENCES ALL|  
|8|0x8|INSERT|  
|16|0x10|Delete|  
|32|0x20|EXECUTE(프로시저에만 해당)|  
|4096|0x1000|SELECT ANY(하나 이상의 열)|  
|8192|0x2000|UPDATE ANY|  
|16384|0x4000|REFERENCES ANY|  
  
 다음 표에서는 *objectid*와 열을 모두 지정한 경우 반환되는 열 수준 개체 사용 권한에 사용되는 비트를 보여 줍니다.  
  
|비트(10진수)|비트(16진수)|문 사용 권한|  
|-----------------|-----------------|--------------------------|  
|1|0x1|SELECT|  
|2|0x2|UPDATE|  
|4|0x4|REFERENCES|  
  
 지정한 매개 변수가 NULL이거나 유효하지 않으면 NULL이 반환됩니다. 예를 들어 지정한 *objectid*나 열이 없는 경우가 해당합니다. 적용되지 않는 사용 권한에 대한 비트 값은 정의되지 않습니다. 테이블에 대한 EXECUTE 권한, 비트 0x20이 여기에 해당됩니다.  
  
 PERMISSIONS 함수에 의해 반환되는 비트맵의 각 비트를 확인하려면 비트 AND(&) 연산자를 사용하세요.  
  
 sp_helprotect 시스템 저장 프로시저를 사용하여 현재 데이터베이스의 사용자에 대한 사용 권한 목록을 반환할 수도 있습니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-the-permissions-function-with-statement-permissions"></a>A. 문 사용 권한과 함께 PERMISSIONS 함수 사용  
 다음 예는 현재 사용자가 `CREATE TABLE` 문을 실행할 수 있는지 여부를 확인합니다.  
  
```  
IF PERMISSIONS()&2=2  
   CREATE TABLE test_table (col1 INT)  
ELSE  
   PRINT 'ERROR: The current user cannot create a table.';  
```  
  
### <a name="b-using-the-permissions-function-with-object-permissions"></a>B. 개체 사용 권한과 함께 PERMISSIONS 함수 사용  
 다음 예에서는 현재 사용자가 `Address` 데이터베이스의 `AdventureWorks2012` 테이블에 데이터 행을 삽입할 수 있는지 여부를 확인합니다.  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&8=8   
   PRINT 'The current user can insert data into Person.Address.'  
ELSE  
   PRINT 'ERROR: The current user cannot insert data into Person.Address.';  
```  
  
### <a name="c-using-the-permissions-function-with-grantable-permissions"></a>C. 부여할 수 있는 권한과 함께 PERMISSIONS 함수 사용  
 다음 예에서는 현재 사용자가 `Address` 데이터베이스의 `AdventureWorks2012` 테이블에 대한 INSERT 권한을 다른 사용자에게 부여할 수 있는지 여부를 확인합니다.  
  
```  
IF PERMISSIONS(OBJECT_ID('AdventureWorks2012.Person.Address','U'))&0x80000=0x80000  
   PRINT 'INSERT on Person.Address is grantable.'  
ELSE  
   PRINT 'You may not GRANT INSERT permissions on Person.Address.';  
```  
  
## <a name="see-also"></a>참고 항목  
 [DENY&#40;Transact-SQL&#41;](../../t-sql/statements/deny-transact-sql.md)   
 [GRANT&#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)   
 [OBJECT_ID&#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)   
 [REVOKE&#40;Transact-SQL&#41;](../../t-sql/statements/revoke-transact-sql.md)   
 [sp_helprotect&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helprotect-transact-sql.md)   
 [시스템 함수&#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)  
  
  
