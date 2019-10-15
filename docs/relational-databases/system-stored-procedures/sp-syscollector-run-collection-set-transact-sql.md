---
title: sp_syscollector_run_collection_set (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3807a53921572bbe20b4c459bff34958cbb42001
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304999"
---
# <a name="sp_syscollector_run_collection_set-transact-sql"></a>sp_syscollector_run_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  수집기가 이미 활성화되어 있고 컬렉션 집합이 캐시되지 않는 컬렉션 모드로 구성된 경우 컬렉션 집합을 시작합니다.  
  
> [!NOTE]  
>  이 프로시저는 캐시되는 컬렉션 모드로 구성된 컬렉션 집합에 대해 실행하면 실패하게 됩니다.  
  
 사용자는 sp_syscollector_run_collection_set을 사용하여 요청 시 데이터 스냅샷을 만들 수 있습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @collection_set_id = ] collection_set_id`은 컬렉션 집합의 고유한 로컬 식별자입니다. *collection_set_id* 은 **int** 이며 *name* 이 NULL 인 경우에는 값이 있어야 합니다.  
  
`[ @name = ] 'name'`은 컬렉션 집합의 이름입니다. *name* 은 **sysname** 이며 *collection_set_id* 가 NULL 인 경우 값이 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 *Collection_set_id* 또는 *name* 에는 값이 있어야 하며 둘 다 NULL 일 수 없습니다.  
  
 이 프로시저는 지정 된 컬렉션 집합에 대 한 컬렉션 및 업로드 작업을 시작 하 고, 컬렉션 집합의 **\@collection_mode** 가 캐시 안 됨 (1)으로 설정 된 경우 컬렉션 에이전트 작업을 즉시 시작 합니다. 자세한 내용은 [sp_syscollector_create_collection_set &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)을 참조 하세요.  
  
 sp_sycollector_run_collection_set는 또한 일정이 없는 컬렉션 집합을 실행하는 데도 사용할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행 하려면 **dc_operator** (EXECUTE 권한 포함) 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="example"></a>예제  
 식별자를 사용하여 컬렉션 집합을 시작합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>관련 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)  
  
  
