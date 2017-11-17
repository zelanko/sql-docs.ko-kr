---
title: APPLOCK_TEST (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a272abaccb41653c9b1b0569738b74905e93e5c9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="applocktest-transact-sql"></a>APPLOCK_TEST(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

지정된 잠금 소유자가 특정 응용 프로그램 리소스에 대한 잠금을 획득할 수 있는지에 대한 정보를 반환합니다. 실제로 잠금을 획득하지는 않습니다. APPLOCK_TEST는 응용 프로그램 잠금 함수 이며 현재 데이터베이스에서 작동 합니다. 응용 프로그램 잠금의 범위는 데이터베이스입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
APPLOCK_TEST ( 'database_principal' , 'resource_name' , 'lock_mode' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>인수  
**'** *데이터베이스 _ 보안 주체* **'**  
데이터베이스의 개체에 대한 사용 권한이 부여될 수 있는 사용자, 역할 또는 응용 프로그램 역할입니다. 함수의 호출자의 멤버 여야 합니다. *데이터베이스 _ 보안 주체*, **dbo**, 또는 **db_owner** 함수를 성공적으로 호출 하려면 고정된 데이터베이스 역할.
  
**'** *resource_name* **'**  
클라이언트 응용 프로그램이 지정한 잠금 리소스의 이름입니다. 응용 프로그램은 리소스가 고유한지 확인해야 합니다. 지정된 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 관리자에 저장할 수 있는 값으로 내부적으로 해시됩니다. *resource_name*은 **nvarchar (255)** 이며 기본값은 없습니다. *resource_name* 은 이진 비교는 현재 데이터베이스의 데이터 정렬 설정에 관계 없이 대 소문자를 구분 합니다.
  
**'** *lock_mode* **'**  
특정 리소스에 대해 획득할 잠금 모드입니다. *lock_mode* 은 **nvarchar (32)** 및 기본값은 없습니다. 값 중 하나일 수 있습니다: **Shared**, **업데이트**, **IntentShared**, **IntentExclusive**, **단독** .
  
**'** *lock_owner* **'**  
가 있는 잠금 소유자는 *lock_owner* 잠금이 요청 된 값입니다. *lock_owner* 은 **nvarchar (32)**합니다. 값일 수 **트랜잭션** (기본값) 또는 **세션**합니다. 하는 경우 기본 또는 **트랜잭션** 을 명시적으로 지정, APPLOCK_TEST는 트랜잭션 내에서 실행 되어야 합니다.
  
## <a name="return-types"></a>반환 형식
**smallint**
  
## <a name="return-value"></a>반환 값
지정된 소유자에게 잠금을 허용할 수 없는 경우 0, 잠금을 허용할 수 있는 경우 1을 반환합니다.
  
## <a name="function-properties"></a>함수 속성
**비결 정적**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>예  
다음 예제에서는 두 명의 사용자 (**사용자 A** 및 **사용자 B**)의 다음 순서를 실행 하는 별도 세션을 갖는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문.
  
**사용자 A** 실행:
  
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
  
**사용자 B** 다음 실행:
  
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
  
**사용자 A** 다음 실행:
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
**사용자 B** 다음 실행:
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
**사용자 A** 및 **사용자 B** 모두 실행 한 후:
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[APPLOCK_MODE &#40; Transact SQL &#41;](../../t-sql/functions/applock-mode-transact-sql.md)  
[sp_getapplock &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

