---
title: sp_scriptsubconflicttable (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_scriptsubconflicttable
- sp_scriptsubconflicttable_TSQL
helpviewer_keywords:
- sp_scriptsubconflicttable
ms.assetid: 13867145-3dad-47a4-8d50-a65175418479
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 86a5b01b46aee8a08c0e490b0d59e3887211d51e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spscriptsubconflicttable-transact-sql"></a>sp_scriptsubconflicttable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정된 지연 구독 아티클에 대한 충돌 테이블을 구독자에 만들기 위한 스크립트를 생성합니다. 생성된 스크립트는 구독 데이터베이스의 구독자에서 실행됩니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_scriptsubconflicttable [@publication =] 'publication'    , [@article =] 'article'  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication=**] **'***publication***'**  
 아티클을 포함하는 게시의 이름입니다. 이 이름은 데이터베이스에서 고유해야 합니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@article=**] **'***문서***'**  
 구독 아티클 이름입니다. *문서* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**cmdtext**|**nvarchar(4000)**|지연 구독 아티클에 대한 충돌 테이블을 구독자에 만들기 위한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트를 반환합니다. 이 스크립트는 구독 데이터베이스의 구독자에서 실행됩니다.|  
  
## <a name="remarks"></a>주의  
 **sp_scriptsubconflicttable** 초기 스냅숏이 수동으로 적용은 구독이 있는 구독자에 사용 됩니다. 구독자에서 충돌 테이블은 선택 사항입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_scriptsubconflicttable**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [지연 업데이트 충돌 감지 및 해결](../../relational-databases/replication/transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
