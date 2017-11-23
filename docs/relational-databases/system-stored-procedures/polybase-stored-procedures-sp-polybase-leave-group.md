---
title: sp_polybase_leave_group (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine-polybase
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords: sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f86b26be75bfc5311714c969c9d965152a8acf5f
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="polybase-stored-procedures---sppolybaseleavegroup"></a>PolyBase 저장 프로시저-sp_polybase_leave_group
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server 인스턴스를 PolyBase 규모 확장 계산 그룹에서 제거합니다. 
 
 SQL Server 인스턴스에 있어야는 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md) 기능이 설치 되어 있습니다.  PolyBase는 Hadoop 및 Azure blob 저장소 등의 SQL Server 이외 데이터 원본에 통합할 수 있습니다. 참고 항목 [sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>Permissions  
 CONTROL SERVER 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 만 그룹에서 계산 노드를 제거할 수 있습니다.  
  
 저장된 프로시저를 실행 한 후 PolyBase 엔진 및 PolyBase 데이터 이동 서비스를 컴퓨터에서 다시 시작 합니다. 확인 하려면 다음 DMV는 헤드 노드에서 실행: **sys.dm_exec_compute_nodes**합니다.  
  
## <a name="example"></a>예제  
 이 예제에서는 PolyBase 그룹에서 현재 컴퓨터를 제거합니다.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [PolyBase 시작하기](../../relational-databases/polybase/get-started-with-polybase.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
