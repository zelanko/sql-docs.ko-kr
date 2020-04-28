---
title: sp_refreshsubscriptions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_refreshsubscriptions
- sp_refreshsubscriptions_TSQL
helpviewer_keywords:
- sp_refreshsubscriptions
ms.assetid: 6cb9b1ce-1ce7-43ab-9451-201f79ed1ffa
author: stevestein
ms.author: sstein
ms.openlocfilehash: 548285b08ceedab49674b35128216bed320c3e7c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771180"
---
# <a name="sp_refreshsubscriptions-transact-sql"></a>sp_refreshsubscriptions(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  모든 기존 구독자에 대 한 새 아티클에 대 한 구독을 즉시 업데이트 게시에 추가 합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_refreshsubscriptions [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`구독을 새로 고칠 게시입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
 None  
  
## <a name="remarks"></a>설명  
 **sp_refreshsubscriptions** 은 스냅숏, 트랜잭션 및 병합 복제에 사용 됩니다.  
  
 **sp_refreshsubscriptions** 는 즉시 업데이트 게시를 위해 **sp_addarticle** 에서 호출 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_refreshsubscriptions**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addarticle &#40;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
