---
title: sp_replcounters (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords:
- sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 62f4cf0f471a17c927d1eb8ad2801a378657b0cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006912"
---
# <a name="spreplcounters-transact-sql"></a>sp_replcounters(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시된 각 데이터베이스에 대한 대기 시간, 처리량 및 트랜잭션 수에 관한 복제 통계를 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_replcounters  
  
```  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**데이터베이스 백업**|**sysname**|데이터베이스의 이름입니다.|  
|**복제 된 트랜잭션**|**int**|배포 데이터베이스에 전달되기 위해 대기하고 있는 로그의 트랜잭션 수입니다.|  
|**복제 속도 trans/sec**|**float**|배포 데이터베이스로 전달된 초 당 평균 트랜잭션 수입니다.|  
|**복제 대기 시간**|**float**|트랜잭션이 배포되기 전에 로그 내에 머무는 평균 시간을 초 단위로 표시한 것입니다.|  
|**Replbeginlsn**|**binary(10)**|로그에서 현재 잘라낼 지점의 LSN(로그 시퀀스 번호)입니다.|  
|**Replnextlsn**|**binary(10)**|배포 데이터베이스로 전달되기 위해 대기하고 있는 다음 커밋 레코드의 LSN입니다.|  
  
## <a name="remarks"></a>설명  
 **sp_replcounters** 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 고정된 데이터베이스 역할 또는 **sysadmin** 고정된 서버 역할입니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_replcmds&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
