---
title: sp_script_synctran_commands (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 3705a28d85c7375aad701d77a517719778954c25
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  포함 하는 스크립트를 생성 된 **sp_addsynctrigger** 업데이트할 수 있는 구독에 대 한 구독자에서 적용에 대 한 호출입니다. 하나의 **sp_addsynctrigger** 게시의 각 아티클에 대해를 호출 합니다. 생성 된 스크립트에 포함 되어는 **sp_addqueued_artinfo** 만드는 호출은 **MSsubsciption_articles** 지연된 게시를 처리 하는 데 필요한 테이블입니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication** =] **'***게시***'**  
 스크립팅할 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@article** =] **'***문서***'**  
 스크립팅할 아티클의 이름입니다. *문서* 은 **sysname**, 기본값은 **모든**는 모든 아티클을 스크립팅 하도록 지정 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="results-set"></a>결과 집합  
 **sp_script_synctran_commands** 단일로 구성 된 결과 집합을 반환 **nvarchar (4000)** 열입니다. 결과 집합은 forms 전체 스크립트 모두 만드는 데 필요한는 **sp_addsynctrigger** 및 **sp_addqueued_artinfo** 구독자에서 적용에 대 한 호출입니다.  
  
## <a name="remarks"></a>주의  
 **sp_script_synctran_commands** 스냅숏 및 트랜잭션 복제에 사용 됩니다.  
  
 **sp_addqueued_artinfo** 업데이트할 수 있는 큐에 대기 중인된 구독에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_script_synctran_commands**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sp_addsynctriggers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
