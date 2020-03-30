---
title: APPLOCK_TEST(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- APPLOCK_TEST_TSQL
- APPLOCK_TEST
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- APPLOCK_TEST function
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- testing application locks
ms.assetid: 4ea33d04-f8e9-46ff-ae61-985bd3eaca2c
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f71a288994afb76d1237f303edfc926116f5962e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "68040334"
---
# <a name="applock_test-transact-sql"></a>APPLOCK_TEST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 기능은 지정된 잠금 소유자가 특정 애플리케이션 리소스에 대한 잠금을 획득할 수 있는지에 대한 정보를 반환합니다. 실제로 잠금을 획득하지는 않습니다. 애플리케이션 잠금 함수로 APPLOCK_TEST는 현재 데이터베이스에서 작동합니다. 데이터베이스는 애플리케이션 잠금의 범위입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>인수  
**'** *database_principal* **'**  
데이터베이스의 개체에 대한 사용 권한이 부여될 수 있는 사용자, 역할 또는 애플리케이션 역할입니다. 함수를 성공적으로 호출하려면 함수 호출자가 *database_principal*, dbo 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다.
  
**'** *resource_name* **'**  
클라이언트 애플리케이션이 지정한 잠금 리소스의 이름입니다. 애플리케이션은 고유한 리소스 이름인지 확인해야 합니다. 지정된 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 관리자가 내부적으로 저장할 수 있는 값으로 내부적으로 해시됩니다.  *resource_name*은 **nvarchar(255)** 이며 기본값은 없습니다. *resource_name*은 이진 비교되며 현재 데이터베이스의 데이터 정렬 설정에 관계없이 대/소문자를 구분합니다.
  
**'** *lock_mode* **'**  
특정 리소스를 얻기 위한 잠금 모드입니다. *lock_mode*는 **nvarchar(32)** 이며 기본값은 없습니다. *lock_mode*는 **Shared**, **Update**, **IntentShared**, **IntentExclusive**, **Exclusive** 중 하나일 수 있습니다.
  
**'** *lock_owner* **'**  
잠금의 소유자이며 잠금이 요청되었을 때의 *lock_owner* 값입니다. *lock_owner*는 **nvarchar (32)** 이고 값은 **Transaction**(기본값) 또는 **Session**이 될 수 있습니다. 기본값 또는 **Transaction**이 명시적으로 지정되면 APPLOCK_TEST는 트랜잭션 내에서 실행되어야 합니다.
  
## <a name="return-types"></a>반환 형식
**smallint**
  
## <a name="return-value"></a>반환 값
지정된 소유자에게 잠금을 허용할 수 없는 경우 0, 잠금을 허용할 수 있는 경우 1을 반환합니다.
  
## <a name="function-properties"></a>함수 속성
**Nondeterministic**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>예  
별도의 세션을 갖는 두 명의 사용자(**사용자 A**와 **사용자 B**)가 다음의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 명령문 시퀀스를 실행합니다.
  
**사용자 A**가 다음을 실행합니다.
  
```sql
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result=sp_getapplock  
    @DbPrincipal='public',  
    @Resource='Form1',  
    @LockMode='Shared',  
    @LockOwner='Transaction';  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
GO  
```  
  
**사용자 B**가 다음을 실행합니다.
  
```sql
Use AdventureWorks2012;  
GO  
BEGIN TRAN;  
SELECT APPLOCK_MODE('public', 'Form1', 'Transaction');  
--Result set: NoLock  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Shared', 'Transaction');  
--Result set: 1 (Lock is grantable.)  
  
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: 0 (Lock is not grantable.)  
GO  
```  
  
**사용자 A**가 다음을 실행합니다.
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
**사용자 B**가 다음을 실행합니다.
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**사용자 A**와 **사용자 B**가 모두 다음을 실행합니다.
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[APPLOCK_MODE&#40;Transact-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  
