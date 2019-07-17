---
title: sp_replrestart (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replrestart_TSQL
- sp_replrestart
helpviewer_keywords:
- sp_replrestart
ms.assetid: 111b3dbf-92f8-4670-b156-1468c63e4fc1
author: stevestein
ms.author: sstein
ms.openlocfilehash: 482658872c069ff530484b6f5eaafd73cb0b3d74
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68113163"
---
# <a name="spreplrestart-transact-sql"></a>sp_replrestart(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  백업 및 복원 중에 트랜잭션 복제에서 사용되며 배포자의 복제된 데이터가 게시자의 데이터와 동기화되도록 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!IMPORTANT]  
>  **sp_replrestart** 내부 복제 저장 프로시저 및 항목에서 지시 된 대로 트랜잭션 복제 토폴로지에서 게시 데이터베이스를 복원 하는 경우에 사용 해야는 [Backing Up and Restoring 전략 스냅숏 및 트랜잭션 복제](../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replrestart  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_replrestart** 배포자에서 가장 높은 로그 시퀀스 번호 (LSN) 값에는 게시자에서 가장 높은 LSN 값을 일치 않을 때 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_replrestart**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
