---
description: sp_syscollector_delete_execution_log_tree(Transact-SQL)
title: sp_syscollector_delete_execution_log_tree (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a2a4a1496bf7b46d3d816aad49cf402aef3ac4d4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89547397"
---
# <a name="sp_syscollector_delete_execution_log_tree-transact-sql"></a>sp_syscollector_delete_execution_log_tree(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  하나의 컬렉션 집합 실행에 대한 모든 로그 항목을 삭제합니다. 또한 이러한 실행에 대한 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 테이블의 로그 항목도 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_syscollector_delete_execution_log_tree[ @log_id = ] log_id  
          , [ @from_collection_set = ] from_collection_set  
```  
  
## <a name="arguments"></a>인수  
`[ @log_id = ] log_id` 컬렉션 집합 로그의 고유 식별자입니다. *log_id* 은 **int**입니다.  
  
`[ @from_collection_set = ] from_collection_set` 컬렉션 집합의 식별자입니다. *from_collection_set* 은 **bit = 1**입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="permissions"></a>사용 권한  
 이 프로시저를 실행 하려면 **dc_operator** (실행 권한 포함) 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
