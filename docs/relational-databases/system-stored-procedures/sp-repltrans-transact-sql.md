---
title: sp_repltrans (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2123841f5819842df4a4833e1a243dbfbeddf7dc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sprepltrans-transact-sql"></a>sp_repltrans(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시 데이터베이스 트랜잭션 로그에서 복제용으로 표시되어 있으나 배포용으로는 표시되어 있지 않은 모든 트랜잭션의 결과 집합을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>결과 집합  
 **sp_repltrans** 올 실행 현재 배포 되지 않은 트랜잭션을 볼 수 있도록 게시 데이터베이스에 대 한 정보를 반환 합니다 (에 전송 되지 않은 트랜잭션 로그에서 복제 된는 배포자)입니다. 결과 집합에는 각 트랜잭션에 대한 처음 및 마지막 레코드의 로그 시퀀스 번호가 표시됩니다. **sp_repltrans** 비슷합니다 [sp_replcmds &#40; Transact SQL &#41; ](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 하지만 트랜잭션 명령을 반환 하지 않습니다.  
  
## <a name="remarks"></a>주의  
 **sp_repltrans** 트랜잭션 복제에 사용 됩니다.  
  
 **sp_repltrans** 에 지원 되지 않습니다 이외[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_repltrans**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_repldone &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
