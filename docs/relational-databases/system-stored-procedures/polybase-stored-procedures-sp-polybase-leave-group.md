---
title: sp_polybase_leave_group (Transact-sql) | Microsoft Docs
description: Sp_polybase_leave_group Transact-sql 명령은 스케일 아웃 계산을 위해 PolyBase 그룹에서 SQL Server 인스턴스를 제거 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
f1_keywords:
- sp_polybase_leave_group
- sp_polybase_leave_group_TSQL
helpviewer_keywords:
- sp_polybase_leave_group
ms.assetid: ef87a8f1-5407-47b5-b8bf-bd7d08c0f0fe
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 82bcad58a97fa41938f127c0a814c312c4e22ec9
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: ko-KR
ms.lasthandoff: 07/07/2020
ms.locfileid: "86052726"
---
# <a name="sp_polybase_leave_group-transact-sql"></a>sp_polybase_leave_group (Transact-sql)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  스케일 아웃 계산을 위해 PolyBase 그룹에서 SQL Server 인스턴스를 제거 합니다. 
 
 SQL Server 인스턴스에 [PolyBase 가이드](../../relational-databases/polybase/polybase-guide.md) 기능이 설치 되어 있어야 합니다.  PolyBase를 사용 하면 Hadoop 및 Azure blob storage와 같은 비 SQL Server 데이터 원본을 통합할 수 있습니다. [Sp_polybase_join_group](../../relational-databases/system-stored-procedures/polybase-stored-procedures-sp-polybase-join-group.md)도 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_polybase_leave_group;  
  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="permissions"></a>사용 권한  
 CONTROL SERVER 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 그룹에서 계산 노드만 제거할 수 있습니다.  
  
 저장 프로시저를 실행 한 후 PolyBase 엔진을 다시 시작 하 고 컴퓨터에서 서비스를 PolyBase 데이터 이동 합니다. 헤드 노드에서 실행 하는 다음 DMV를 확인 하려면 **dm_exec_compute_nodes**합니다.  
  
## <a name="example"></a>예제  
 이 예에서는 PolyBase 그룹에서 현재 컴퓨터를 제거 합니다.  
  
```sql  
EXEC sp_polybase_leave_group ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [PolyBase 시작](../../relational-databases/polybase/get-started-with-polybase.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
