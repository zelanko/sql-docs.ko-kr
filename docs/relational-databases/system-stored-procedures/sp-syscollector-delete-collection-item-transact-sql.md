---
title: sp_syscollector_delete_collection_item (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
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
- sp_syscollector_delete_collection_item
- sp_syscollector_delete_collection_item_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_delete_collecton_item
- data collector [SQL Server], stored procedures
ms.assetid: 9c2b0990-1d3d-4a59-94a0-3cca6fef4681
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 587d7ca6d3610ac2d8950f73eb085b1f942f2e27
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2018
---
# <a name="spsyscollectordeletecollectionitem-transact-sql"></a>sp_syscollector_delete_collection_item(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  컬렉션 집합에서 컬렉션 항목을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_delete_collection_item [[ @collection_item_id = ] collection_item_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>인수  
 [ @collection_item_id = ] *collection_item_id*  
 컬렉션 항목의 고유 식별자입니다. *collection_item_id* 은 **int** 기본값은 NULL입니다. *collection_item_id* 경우 값이 있어야 *이름* 은 NULL입니다.  
  
 [ @name =] '*이름*'  
 컬렉션 항목의 이름입니다. *이름* 은 **sysname** 이며 기본값은 NULL입니다. *이름* 경우 값이 있어야 *collection_item_id* 은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 sp_syscollector_delete_collection_item은 msdb 시스템 데이터베이스의 컨텍스트 내에서 실행되어야 합니다. 시스템 컬렉션 집합에서는 컬렉션 항목을 삭제할 수 없습니다.  
  
 이 작업을 수행하는 동안에는 컬렉션 항목을 포함하는 컬렉션 집합이 중지되고 다시 시작됩니다.  
  
## <a name="permissions"></a>Permissions  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `MyCollectionItem1`이라는 컬렉션 항목을 삭제합니다.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_delete_collection_item @name = 'MyCollectionItem1';  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [sp_syscollector_create_collection_item &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-item-transact-sql.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_items&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-items-transact-sql.md)  
  
  
