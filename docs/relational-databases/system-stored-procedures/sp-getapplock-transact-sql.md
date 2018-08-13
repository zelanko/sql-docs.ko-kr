---
title: sp_getapplock (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_getapplock_TSQL
- sp_getapplock
dev_langs:
- TSQL
helpviewer_keywords:
- application locks
- sp_getapplock
ms.assetid: e1e85908-9f31-47cf-8af6-88c77e6f24c9
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: ce5a2f5350a16024dcefbdd3e162212a60d98059
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39555683"
---
# <a name="spgetapplock-transact-sql"></a>sp_getapplock(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  응용 프로그램 리소스에 잠금을 설정합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getapplock [ @Resource = ] 'resource_name' ,  
     [ @LockMode = ] 'lock_mode'   
     [ , [ @LockOwner = ] 'lock_owner' ]   
     [ , [ @LockTimeout = ] 'value' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 [ @Resource=] '*resource_name*'  
 잠금 리소스를 식별하는 이름을 지정하는 문자열입니다. 응용 프로그램은 리소스 이름이 고유한지 확인해야 합니다. 지정된 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 관리자에 저장할 수 있는 값으로 내부적으로 해시됩니다. *resource_name* 됩니다 **nvarchar(255)** 기본값은 없습니다. 리소스 문자열 보다 길면 **nvarchar(255)** 를 잘립니다 **nvarchar(255)** 합니다.  
  
 *resource_name* 은 이진 비교 되어 있으므로 현재 데이터베이스의 데이터 정렬 설정과 관계 없이 대/소문자를 구분 합니다.  
  
> [!NOTE]  
>  응용 프로그램 잠금을 획득한 후에는 처음 32자만 일반 텍스트로 검색되고 나머지는 해시됩니다.  
  
 [ @LockMode=] '*lock_mode*'  
 특정 리소스에 대해 획득할 잠금 모드입니다. *lock_mode*는 **nvarchar(32)** 이며 기본값은 없습니다. 값 중 하나일 수 있습니다: **공유**, **업데이트**, **IntentShared**, **IntentExclusive**, 또는 **전용** .  
  
 [ @LockOwner=] '*lock_owner*'  
 잠금의 소유자이며 잠금이 요청되었을 때의 *lock_owner* 값입니다. *lock_owner*은 **nvarchar(32)** 입니다. 값은 **Transaction**(기본값) 또는 **Session**일 수 있습니다. 경우는 *lock_owner* 값이 **트랜잭션**, 기본 또는 명시적으로 지정 sp_getapplock에서 실행 되어야 합니다 트랜잭션 내에서.  
  
 [ @LockTimeout=] '*값*'  
 잠금 제한 시간 값(밀리초)입니다. 기본값은 반환한 값과 동일 하 게@LOCK_TIMEOUT합니다. 즉시 허가할 수 없는 잠금 요청이 대기하지 않고 오류를 반환하도록 하려면 0을 지정하세요.  
  
 [ @DbPrincipal=] '*database_principal*'  
 데이터베이스의 개체에 대한 사용 권한이 있는 사용자, 역할 또는 응용 프로그램 역할입니다. 함수의 호출자의 멤버 여야 합니다 *database_principal*, dbo 또는 db_owner 고정 데이터베이스 역할을 성공적으로 함수를 호출 합니다. 기본값은 public입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 \>= 0 (성공) 또는 < 0 (실패)  
  
|값|결과|  
|-----------|------------|  
|0|동기식으로 잠금을 허가하는 데 성공했습니다.|  
|@shouldalert|호환되지 않는 다른 잠금이 해제되기를 기다린 다음 성공적으로 잠금을 허가하였습니다.|  
|-1|잠금 요청이 시간을 초과하였습니다.|  
|-2|잠금 요청이 취소되었습니다.|  
|-3|잠금 요청이 교착 상태에서 처리되지 않았습니다.|  
|-999|매개 변수 유효성 검사 또는 다른 호출에서 오류가 발생하였음을 나타냅니다.|  
  
## <a name="remarks"></a>Remarks  
 리소스에 설정된 잠금은 현재 트랜잭션 또는 현재 세션과 연관됩니다. 현재 트랜잭션과 연관된 잠금은 트랜잭션이 커밋되거나 롤백될 때 해제됩니다. 세션과 연관된 잠금은 세션이 로그 아웃될 때 해제됩니다. 서버가 종료되면 모든 잠금이 해제됩니다.  
  
 sp_getapplock에서 만든 잠금 리소스는 세션에 대한 현재 데이터베이스에서 만들어집니다. 각 잠금 리소스는 다음을 조합한 값으로 식별됩니다.  
  
-   해당 잠금 리소스를 포함하고 있는 데이터베이스의 ID  
  
-   @DbPrincipal 매개 변수에서 지정한 데이터베이스 보안 주체  
  
-   @Resource 매개 변수에서 지정한 잠금 이름  
  
 @DbPrincipal 매개 변수에 지정한 데이터베이스 보안 주체의 멤버만이 해당 보안 주체를 지정하는 응용 프로그램 잠금을 획득할 수 있습니다. dbo 및 db_owner 역할의 멤버는 암시적으로 모든 역할의 멤버로 간주됩니다.  
  
 sp_releaseapplock을 사용하여 명시적으로 잠금을 해제할 수 있습니다. 응용 프로그램이 동일한 잠금 리소스에 대해 sp_getapplock을 여러 번 호출한 경우에는 잠금을 해제하는 데도 동일한 횟수만큼 sp_releaseapplock을 호출해야 합니다.  
  
 동일 잠금 리소스에 대해 sp_getapplock을 여러 번 호출하되 요청 중 하나에서 기존 모드와 다른 잠금 모드를 지정한 경우 리소스에 두 잠금 모드를 합친 것만큼의 영향을 미칩니다. 즉, 대부분의 경우에 잠금 모드가 기존 모드 또는 새로 요청된 모드 중에서 보다 강력한 잠금 모드 수준으로 올라갑니다. 이 더욱 강력한 잠금 모드는 이전에 잠금 해제 호출이 발생한 경우에도 잠금이 궁극적으로 해제될 때까지 유지됩니다. 예를 들어 다음과 같은 호출 시퀀스에서 리소스는 `Exclusive` 모드가 아니라 `Shared` 모드에서 유지됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
EXEC @result = sp_releaseapplock @Resource = 'Form1';  
COMMIT TRANSACTION;  
GO  
```  
  
 응용 프로그램을 잠그는 교착 상태가 발생해도 응용 프로그램 잠금을 요청한 트랜잭션이 롤백되지 않습니다. 반환 값의 결과로 필요할 수 있는 롤백은 모두 직접 수행해야 합니다. 따라서 특정 값(예: -3)을 반환하는 경우 ROLLBACK TRANSACTION 또는 대체 동작을 시작하도록 코드에 오류 확인 작업을 포함시키는 것이 좋습니다.  
  
 다음 예를 참조하세요.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Exclusive';  
IF @result = -3  
BEGIN  
    ROLLBACK TRANSACTION;  
END  
ELSE  
BEGIN  
    EXEC @result = sp_releaseapplock @Resource = 'Form1';  
    COMMIT TRANSACTION;  
END;  
GO  
```  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 현재 데이터베이스 ID를 사용하여 리소스를 한정합니다. 따라서 sp_getapplock을 실행하면 다른 데이터베이스에서 동일한 매개 변수 값을 사용한 경우라도 별도의 리소스에 대해서는 별도의 잠금이 설정됩니다.  
  
 sys.dm_tran_locks 동적 관리 뷰나 sp_lock 시스템 저장 프로시저를 사용하여 잠금 정보를 검사하거나 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 잠금을 모니터링할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Form1` 데이터베이스의 `AdventureWorks2012` 리소스에 대해 현재 트랜잭션과 연관된 공유 잠금을 설정합니다.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRAN;  
DECLARE @result int;  
EXEC @result = sp_getapplock @Resource = 'Form1',   
               @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
 다음 예에서는 `dbo`를 데이터베이스 보안 주체로 지정합니다.  
  
```  
BEGIN TRAN;  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'AdventureWorks2012',   
     @LockMode = 'Shared';  
COMMIT TRAN;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [APPLOCK_MODE &#40;TRANSACT-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;TRANSACT-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_releaseapplock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-releaseapplock-transact-sql.md)  
  
  
