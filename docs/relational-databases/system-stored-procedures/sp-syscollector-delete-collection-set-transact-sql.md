---
title: sp_syscollector_delete_collection_set (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collection_set_TSQL
- sp_syscollector_delete_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collecton_set
ms.assetid: 29c63a74-4db4-4068-bd57-9fb519b0c598
author: stevestein
ms.author: sstein
ms.openlocfilehash: e60fb13244d6740b7d52c568835e54155eeb8c46
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68000879"
---
# <a name="sp_syscollector_delete_collection_set-transact-sql"></a>sp_syscollector_delete_collection_set(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  사용자 정의 컬렉션 집합과 이 집합의 모든 컬렉션 항목을 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_delete_collection_set [[ @collection_set_id = ] collection_set_id OUTPUT ]  
    , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>인수  
 [ @collection_set_id = ] *collection_set_id*  
 컬렉션 집합의 고유 식별자입니다. *collection_set_id* 은 **int** 이며 *name* 이 NULL 인 경우 값이 있어야 합니다.  
  
 [ @name = ] '*이름*'  
 컬렉션 집합의 이름입니다. *name* 은 **SYSNAME** 이며 *collection_set_id* NULL 인 경우 값이 있어야 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_syscollector_delete_collection_set은 msdb 시스템 데이터베이스의 컨텍스트에서 실행해야 합니다.  
  
 *Collection_set_id* 또는 *이름* 에는 값이 있어야 하며 둘 다 NULL 일 수 없습니다. 이러한 값을 확인하려면 syscollector_collection_set 시스템 뷰를 쿼리합니다.  
  
 시스템 정의 컬렉션 집합은 삭제할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행하려면 dc_admin(EXECUTE 권한 있음) 고정 데이터베이스 역할의 멤버 자격이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 *collection_set_id*를 지정 하는 사용자 정의 컬렉션 집합을 삭제 합니다.  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_delete_collection_set  
    @collection_set_id = 4;  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [데이터 컬렉션](../../relational-databases/data-collection/data-collection.md)   
 [Transact-sql&#41;syscollector_collection_sets &#40;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
