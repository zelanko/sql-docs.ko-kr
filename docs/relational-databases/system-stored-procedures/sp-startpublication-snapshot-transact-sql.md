---
title: sp_startpublication_snapshot (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_startpublication_snapshot
- sp_startpublication_snapshot_TSQL
helpviewer_keywords:
- sp_startpublication_snapshot
ms.assetid: 2cf568ee-0679-4d19-a394-27210bff61e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: ab1b3487c3a1affe7a0dc40f62d241d19b29186b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68032764"
---
# <a name="sp_startpublication_snapshot-transact-sql"></a>sp_startpublication_snapshot(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시를 위한 초기 스냅샷을 생성하는 스냅샷 에이전트 작업을 시작하는 데 사용됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_startpublication_snapshot [ @publication = ] 'publication'   
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @publisher = ] 'publisher'`이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 이름입니다. *publisher* 는 **sysname**이며 기본값은 NULL입니다. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자에 이 매개 변수를 지정하지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_startpublication_snapshot** 은 모든 유형의 복제에 사용 됩니다.  
  
 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 경우이 저장 프로시저는 배포 데이터베이스의 배포자에서 실행 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_startpublication_snapshot**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [초기 스냅샷 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [Transact-sql&#41;sp_addpublication_snapshot &#40;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)   
 [Transact-sql&#41;sp_changepublication_snapshot &#40;](../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md)  
  
  
