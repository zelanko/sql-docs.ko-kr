---
title: sp_syscollector_start_collection_set (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 54381b4d9b0baab7d9b726fd209a3cfb598fb8e1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spsyscollectorstartcollectionset-transact-sql"></a>sp_syscollector_start_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  수집기가 이미 활성화되어 있고 컬렉션 집합이 실행 중이 아니면 컬렉션 집합을 시작합니다. 수집기를 사용 하지 않는 경우 실행 하 여 수집기를 활성화 [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) 다음이 저장된 프로시저를 사용 하 여 컬렉션 집합을 시작 합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>인수  
 [ **@collection_set_id =** ] *collection_set_id*  
 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 이며 기본값은 NULL입니다. *collection_set_id* 경우 값이 있어야 *이름* 은 NULL입니다.  
  
 [ **@name =** ] '*name*'  
 컬렉션 집합의 이름입니다. *이름* 은 **sysname** 이며 기본값은 NULL입니다. *이름* 경우 값이 있어야 *collection_set_id* 은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syscollector_create_collection_set는 SQL Server 에이전트가 활성화되어 있는 상태에서 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 이 프로시저는 일정이 없는 컬렉션 집합에 대해 실행하면 실패합니다. 경우는 컬렉션 집합 일정에 따라 (해당 컬렉션 모드가 설정 되어 있으므로 캐시 되지 않은, 예를 들어), 사용 하 여는 [sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) 저장 프로시저를 컬렉션 집합을 시작 합니다.  
  
 이 프로시저는 지정된 컬렉션 집합에 대한 컬렉션 및 업로드 작업을 활성화하며 컬렉션 집합의 컬렉션 모드가 캐시된 모드(0)로 설정된 경우 즉시 컬렉션 에이전트 작업을 시작합니다. 자세한 내용은 참조 [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)합니다.  
  
 컬렉션 집합에 컬렉션 항목이 포함되어 있지 않으면 이 작업은 효과가 없습니다. 이 경우 오류 14685가 경고로 반환됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행하려면 dc_operator 고정 데이터베이스 역할의 멤버 자격이 필요합니다. 컬렉션 집합에 프록시 계정이 없는 경우에는 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 해당 식별자를 사용하여 컬렉션 집합을 시작합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
