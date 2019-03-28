---
title: sp_script_synctran_commands (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a9ee35eb4c5d67ff50f4f08c1cfa29596e27aec2
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536180"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  포함 된 스크립트를 생성 합니다 **sp_addsynctrigger** 업데이트할 수 있는 구독에 대 한 구독자에서 적용에 대 한 호출 합니다. 하나씩 있기 **sp_addsynctrigger** 게시의 각 아티클에 대해를 호출 합니다. 생성 된 스크립트에 포함 되어는 **sp_addqueued_artinfo** 만든 호출 합니다 **MSsubsciption_articles** 지연된 게시를 처리 하는 데 필요한 테이블입니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'` 스크립팅할 게시의 이름이입니다. *게시* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @article = ] 'article'` 스크립팅할 아티클의 이름이입니다. *문서* 됩니다 **sysname**, 기본값은 **모든**, 하는 모든 아티클을 스크립팅 하도록 지정 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="results-set"></a>결과 집합  
 **sp_script_synctran_commands** 반환 된 결과 집합을 단일 이루어져 **nvarchar(4000)** 열입니다. 결과 집합 forms 전체 스크립트를 모두 만드는 데 필요한 합니다 **sp_addsynctrigger** 하 고 **sp_addqueued_artinfo** 구독자에서 적용에 대 한 호출 합니다.  
  
## <a name="remarks"></a>Remarks  
 **sp_script_synctran_commands** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_addqueued_artinfo** 업데이트할 수 있는 큐에 대기 중인된 구독에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있습니다 **sp_script_synctran_commands**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sp_addsynctriggers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
