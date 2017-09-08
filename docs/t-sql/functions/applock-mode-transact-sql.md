---
title: APPLOCK_MODE (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- APPLOCK_MODE_TSQL
- APPLOCK_MODE
dev_langs:
- TSQL
helpviewer_keywords:
- locking [SQL Server], applications
- applications [SQL Server], locks
- sessions [SQL Server], application locks
- APPLOCK_MODE function
ms.assetid: e43d4917-77f1-45cc-b231-68ba7fee3385
caps.latest.revision: 32
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ceec0a5465187e1b470bd9eb8b1039a5b3d60aae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="applockmode-transact-sql"></a>APPLOCK_MODE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

특정 응용 프로그램 리소스에 대해 잠금 소유자가 보유한 잠금 모드를 반환합니다. APPLOCK_MODE는 응용 프로그램 잠금 함수이며 현재 데이터베이스에서 작동합니다. 응용 프로그램 잠금의 범위는 데이터베이스입니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
APPLOCK_MODE( 'database_principal' , 'resource_name' , 'lock_owner' )  
```  
  
## <a name="arguments"></a>인수  
'*데이터베이스 _ 보안 주체*'  
데이터베이스의 개체에 대한 사용 권한이 부여될 수 있는 사용자, 역할 또는 응용 프로그램 역할입니다. 함수의 호출자의 멤버 여야 합니다. *데이터베이스 _ 보안 주체*, 함수를 성공적으로 호출 하려면 dbo 또는 db_owner 고정 데이터베이스 역할.
  
'*resource_name*'  
클라이언트 응용 프로그램이 지정한 잠금 리소스의 이름입니다. 응용 프로그램은 리소스 이름이 고유한지 확인해야 합니다. 지정된 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 관리자에 저장할 수 있는 값으로 내부적으로 해시됩니다. *resource_name*은 **nvarchar (255)** 이며 기본값은 없습니다. *resource_name* 은 이진 비교 되며 현재 데이터베이스의 데이터 정렬 설정에 관계 없이 대/소문자를 구분 합니다.
  
'*lock_owner*'  
가 있는 잠금 소유자는 *lock_owner* 잠금이 요청 된 값입니다. *lock_owner* 은 **nvarchar (32)**, 값일 수 및 **트랜잭션** (기본값) 또는 **세션**합니다.
  
## <a name="return-types"></a>반환 형식
**nvarchar (32)**
  
## <a name="return-value"></a>반환 값
특정 응용 프로그램 리소스에 대해 잠금 소유자가 보유한 잠금 모드를 반환합니다. 잠금 모드는 다음 값 중 하나일 수 있습니다.
  
||||  
|-|-|-|  
|**NoLock**|**Update**|**\*SharedIntentExclusive**|  
|**IntentShared**|**IntentExclusive**|**\*UpdateIntentExclusive**|  
|**공유**|**단독**||  
  
*이 잠금 모드는 다른 잠금 모드의 조합이며 sp_getapplock을 사용하여 명시적으로 설정될 수 없습니다.
  
## <a name="function-properties"></a>함수 속성
**비결 정적**
  
**Nonindexable**
  
**Nonparallelizable**
  
## <a name="examples"></a>예  
별도의 세션을 갖는 두 명의 사용자(사용자 A와 사용자 B)가 다음의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 시퀀스를 실행합니다.
  
사용자 A는 다음을 실행합니다.
  
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
  
그런 다음 사용자 B는 다음을 실행합니다.
  
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
  
사용자 A는 다음을 실행합니다.
  
```sql
EXEC sp_releaseapplock @Resource='Form1', @DbPrincipal='public';  
GO  
```  
  
그런 다음 사용자 B는 다음을 실행합니다.
  
```sql
SELECT APPLOCK_TEST('public', 'Form1', 'Exclusive', 'Transaction');  
--Result set: '1' (The lock is grantable.)  
GO  
```  
  
사용자 A와 사용자 B가 다음을 실행합니다.
  
```sql
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>참고 항목
[APPLOCK_TEST &#40; Transact SQL &#41;](../../t-sql/functions/applock-test-transact-sql.md)  
[sp_getapplock &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
[sp_releaseapplock &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)
  
  

