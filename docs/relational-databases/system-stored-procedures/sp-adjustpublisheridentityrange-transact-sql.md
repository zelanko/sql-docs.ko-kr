---
title: sp_adjustpublisheridentityrange (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_adjustpublisheridentityrange_TSQL
- sp_adjustpublisheridentityrange
helpviewer_keywords:
- sp_adjustpublisheridentityrange
ms.assetid: 64f111fd-fb7d-4459-93f7-65f0f8dd7efe
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c2f0214309eb060bbc02c7c05bf5243444ed5796
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spadjustpublisheridentityrange-transact-sql"></a>sp_adjustpublisheridentityrange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  게시에 대한 ID 범위를 조정하고 게시의 임계값에 기반하여 새 범위를 다시 할당합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adjustpublisheridentityrange [ [ @publication = ] 'publication' ]  
    [ , [ @table_name = ] 'table_name' ]  
    [ , [ @table_owner= ] 'table_owner' ]  
```  
  
## <a name="arguments"></a>인수  
 [ ** @publication=**] **'***게시***'**  
 새 ID 범위가 다시 할당되는 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ ** @table_name=**] **'***table_name***'**  
 새 ID 범위가 다시 할당되는 테이블의 이름입니다. *table_name* 은 **sysname**, 기본값은 NULL입니다.  
  
 [ ** @table_owner=**] **'***table_owner***'**  
 게시자에서 테이블의 소유자입니다. *table_owner* 은 **sysname**, 기본값은 NULL입니다. 경우 *table_owner* 를 지정 하지 않으면 현재 사용자의 이름이 사용 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_adjustpublisheridentityrange** 모든 유형의 복제에 사용 됩니다.  
  
 자동 ID 범위를 사용할 수 있는 게시인 경우 배포 에이전트 또는 병합 에이전트는 해당 임계값에 기반하여 게시의 ID 범위를 자동으로 조정하는 역할을 합니다. 그러나 어떤 이유로 든에 대 한 배포 에이전트 또는 병합 에이전트가 실행 되지 않은 시간 기간에 대 한 id 범위 리소스 도달할 때까지 사용한 지점 임계값으로 하는 경우 사용자가 호출할 수 **sp_adjustpublisheridentityrange** 게시자에 대 한 값의 새 범위를 할당 합니다.  
  
 실행할 때 **sp_adjustpublisheridentityrange**, 어느 *게시* 또는 *table_name* 지정 해야 합니다. 두 가지 모두 지정하거나 둘 다 지정하지 않은 경우 오류가 반환됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_adjustpublisheridentityrange**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Id 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
