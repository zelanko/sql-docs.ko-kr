---
title: sp_script_synctran_commands (Transact-sql) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 965fc3fe168ecd6027c2c1fc2ebad92bc334e383
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82816853"
---
# <a name="sp_script_synctran_commands-transact-sql"></a>sp_script_synctran_commands(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  업데이트할 수 있는 구독에 대해 구독자에 적용할 **sp_addsynctrigger** 호출을 포함 하는 스크립트를 생성 합니다. 게시의 각 아티클에 대해 하나의 **sp_addsynctrigger** 호출 합니다. 또한 생성 된 스크립트에는 대기 중인 게시를 처리 하는 데 필요한 **MSsubsciption_articles** 테이블을 만드는 **sp_addqueued_artinfo** 호출이 포함 되어 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`스크립팅할 게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @article = ] 'article'`스크립팅할 아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 모든 아티클을 스크립팅 하도록 지정 하는 **all**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="results-set"></a>결과 집합  
 **sp_script_synctran_commands** 는 단일 **nvarchar (4000)** 열로 구성 된 결과 집합을 반환 합니다. 결과 집합은 구독자에서 적용 될 **sp_addsynctrigger** 와 **sp_addqueued_artinfo** 호출을 만드는 데 필요한 전체 스크립트를 형성 합니다.  
  
## <a name="remarks"></a>설명  
 **sp_script_synctran_commands** 는 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_addqueued_artinfo** 는 지연 업데이트할 수 있는 구독에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_script_synctran_commands**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_addsynctriggers &#40;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [Transact-sql&#41;sp_addqueued_artinfo &#40;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
