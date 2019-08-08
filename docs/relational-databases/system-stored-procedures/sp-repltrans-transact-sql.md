---
title: sp_repltrans (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40477973efebac9a484e89e7627f0996285b430b
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770858"
---
# <a name="sp_repltrans-transact-sql"></a>sp_repltrans(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  게시 데이터베이스 트랜잭션 로그에서 복제용으로 표시되어 있으나 배포용으로는 표시되어 있지 않은 모든 트랜잭션의 결과 집합을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>결과 집합  
 **sp_repltrans** 는 실행 되는 게시 데이터베이스에 대 한 정보를 반환 하 여 현재 배포 되지 않은 트랜잭션 (배포자에 전송 되지 않은 트랜잭션 로그에 남아 있는 트랜잭션)을 볼 수 있도록 합니다. 결과 집합에는 각 트랜잭션에 대한 처음 및 마지막 레코드의 로그 시퀀스 번호가 표시됩니다. **sp_repltrans** 는 [sp_replcmds &#40;transact-sql&#41; ](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 과 유사 하지만 트랜잭션에 대 한 명령을 반환 하지 않습니다.  
  
## <a name="remarks"></a>설명  
 **sp_repltrans** 은 트랜잭션 복제에 사용 됩니다.  
  
 이외[!INCLUDE[msCoName](../../includes/msconame-md.md)] 게시자에 대해서는 sp_repltrans이 지원 되지 않습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만이 **sp_repltrans**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_repldone &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
