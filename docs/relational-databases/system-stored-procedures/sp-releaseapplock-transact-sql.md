---
title: sp_releaseapplock (TRANSACT-SQL) | Microsoft 문서
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
- sp_releaseapplock_TSQL
- sp_releaseapplock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_releaseapplock
ms.assetid: 51b03c2f-0d54-40f5-9172-e747942d4a46
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 7a3a9707be98ec3524a1d1d52c833b3ceb52f9c2
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39547913"
---
# <a name="spreleaseapplock-transact-sql"></a>sp_releaseapplock(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  응용 프로그램 리소스에서 잠금을 해제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_releaseapplock [ @Resource = ] 'resource_name'   
     [ , [ @LockOwner = ] 'lock_owner' ]  
     [ , [ @DbPrincipal = ] 'database_principal' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>인수  
 [ @Resource=] '*resource_name*'  
 클라이언트 응용 프로그램이 지정한 잠금 리소스의 이름입니다. 응용 프로그램은 리소스가 고유한지 확인해야 합니다. 지정된 이름은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 잠금 관리자에 저장할 수 있는 값으로 내부적으로 해시됩니다. *resource_name* 됩니다 **nvarchar(255)** 기본값은 없습니다. *resource_name* 은 이진 비교 되므로 현재 데이터베이스의 데이터 정렬 설정과 관계 없이 대/소문자 구분 됩니다.  
  
 [ @LockOwner=] '*lock_owner*'  
 잠금의 소유자이며 잠금이 요청되었을 때의 *lock_owner* 값입니다. *lock_owner*은 **nvarchar(32)** 입니다. 값은 **Transaction**(기본값) 또는 **Session**일 수 있습니다. 경우는 *lock_owner* 값이 **트랜잭션**, 기본 또는 명시적으로 지정 sp_getapplock에서 실행 되어야 합니다 트랜잭션 내에서.  
  
 [ @DbPrincipal=] '*database_principal*'  
 데이터베이스의 개체에 대한 사용 권한이 있는 사용자, 역할 또는 응용 프로그램 역할입니다. 함수를 성공적으로 호출하려면 이 함수의 호출자가 *database_principal*, dbo 또는 db_owner 고정 데이터베이스 역할의 멤버여야 합니다. 기본값은 public입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 \>= 0 (성공) 또는 < 0 (실패)  
  
|값|결과|  
|-----------|------------|  
|0|잠금이 성공적으로 해제되었습니다.|  
|-999|매개 변수 유효성 검사 또는 다른 호출에서 오류가 발생했음을 나타냅니다.|  
  
## <a name="remarks"></a>Remarks  
 응용 프로그램이 동일한 잠금 리소스에 대해 sp_getapplock을 여러 번 호출한 경우에는 잠금을 해제하는 데도 동일한 횟수만큼 sp_releaseapplock을 호출해야 합니다.  
  
 어떤 이유로든 서버가 종료되면 잠금은 해제됩니다.  
  
## <a name="permissions"></a>사용 권한  
 public 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `Form1` 데이터베이스의 `AdventureWorks2012` 리소스에 대해 현재 트랜잭션과 연관된 잠금을 해제합니다.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_getapplock @DbPrincipal = 'dbo', @Resource = 'Form1',   
     @LockMode = 'Shared';  
EXEC sp_releaseapplock @DbPrincipal = 'dbo', @Resource = 'Form1';  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [APPLOCK_MODE &#40;TRANSACT-SQL&#41;](../../t-sql/functions/applock-mode-transact-sql.md)   
 [APPLOCK_TEST &#40;TRANSACT-SQL&#41;](../../t-sql/functions/applock-test-transact-sql.md)   
 [sp_getapplock&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-getapplock-transact-sql.md)  
  
  
