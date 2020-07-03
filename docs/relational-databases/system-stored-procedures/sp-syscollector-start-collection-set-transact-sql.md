---
title: sp_syscollector_start_collection_set (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56fa6b114d58512f9cdec9c3da2575539af0d03b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892843"
---
# <a name="sp_syscollector_start_collection_set-transact-sql"></a>sp_syscollector_start_collection_set(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  수집기가 이미 활성화되어 있고 컬렉션 집합이 실행 중이 아니면 컬렉션 집합을 시작합니다. 수집기를 사용 하도록 설정 하지 않은 경우 [sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md) 를 실행 하 여 수집기를 사용 하도록 설정한 다음이 저장 프로시저를 사용 하 여 컬렉션 집합을 시작 합니다.  

  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @collection_set_id = ] collection_set_id`컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 이며 기본값은 NULL입니다. *name* 이 NULL 인 경우 *collection_set_id* 에 값이 있어야 합니다.  
  
`[ @name = ] 'name'`컬렉션 집합의 이름입니다. *name* 은 **sysname** 이며 기본값은 NULL입니다. *collection_set_id* 가 NULL 이면 *이름* 에 값이 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syscollector_create_collection_set는 SQL Server 에이전트가 활성화되어 있는 상태에서 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 이 프로시저는 일정이 없는 컬렉션 집합에 대해 실행하면 실패합니다. 컬렉션 집합이 일정을 포함 하지 않는 경우 (예: 해당 컬렉션 모드는 캐시 되지 않음으로 설정 되어 있기 때문에) [sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md) 저장 프로시저를 사용 하 여 컬렉션 집합을 시작 합니다.  
  
 이 프로시저는 지정된 컬렉션 집합에 대한 컬렉션 및 업로드 작업을 활성화하며 컬렉션 집합의 컬렉션 모드가 캐시된 모드(0)로 설정된 경우 즉시 컬렉션 에이전트 작업을 시작합니다. 자세한 내용은 [sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)를 참조 하세요.  
  
 컬렉션 집합에 컬렉션 항목이 포함되어 있지 않으면 이 작업은 효과가 없습니다. 이 경우 오류 14685가 경고로 반환됩니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_operator 고정 데이터베이스 역할의 멤버 자격이 필요합니다. 컬렉션 집합에 프록시 계정이 없는 경우에는 sysadmin 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 해당 식별자를 사용하여 컬렉션 집합을 시작합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;데이터 수집기 저장 프로시저](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 수집](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
