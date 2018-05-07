---
title: sp_syscollector_delete_execution_log_tree (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_execution_log_tree_TSQL
- sp_syscollector_delete_execution_log_tree
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_delete_execution_log_tree
- data collector [SQL Server], stored procedures
ms.assetid: 0a9a7c5b-c3cc-40ca-b524-e948a8cce4e4
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3e2e7efc392e28b2dd8c3f1ee4fba3c8add8b5c6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spsyscollectordeleteexecutionlogtree-transact-sql"></a>sp_syscollector_delete_execution_log_tree(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나의 컬렉션 집합 실행에 대한 모든 로그 항목을 삭제합니다. 또한 이러한 실행에 대한 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 테이블의 로그 항목도 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_delete_execution_log_tree[ @log_id = ] log_id  
          , [ @from_collection_set = ] from_collection_set  
```  
  
## <a name="arguments"></a>인수  
 [ **@log_id =** ] *log_id*  
 컬렉션 집합 로그의 고유 식별자입니다. *log_id* 은 **int**합니다.  
  
 [ **@from_collection_set =** ] *from_collection_set*  
 컬렉션 집합의 식별자입니다. *from_collection_set* 은 **bit 1 =** 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **dc_operator** (EXECUTE 권한 있음)와이 프로시저를 실행 하는 고정된 데이터베이스 역할.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
