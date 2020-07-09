---
title: MSSQLSERVER_10509 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3897e0a92083f292ba2edd062536ebdd6bda6c69
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781516"
---
# <a name="mssqlserver_10509"></a>MSSQLSERVER_10509
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>세부 정보  
  
| attribute | 값 |  
| :-------- | :---- |  
|제품 이름|SQL Server|  
|이벤트 ID|10509|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|PG_INVALID_STMT|  
|메시지 텍스트|**\@stmt** 또는 **\@statement_start_offset**으로 지정된 문에 구문 오류가 있거나 계획 지침으로 사용하기에 적합하지 않아 계획 지침 ‘%.\*ls’을(를) 만들 수 없습니다. 올바른 단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 안에 있는 문의 올바른 시작 위치를 지정하십시오. 올바른 시작 위치를 가져오려면 sys.dm_exec_query_stats 동적 관리 함수의 statement_start_offset 열을 쿼리하십시오.|  
  
## <a name="explanation"></a>설명  
**\@stmt** 또는 **\@statement_start_offset**으로 지정된 문에 구문 오류가 있거나 계획 지침으로 사용하기에 적합하지 않습니다.  
  
## <a name="user-action"></a>사용자 동작  
올바른 단일 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리 안에 있는 문의 올바른 시작 위치를 지정하십시오. 올바른 시작 위치를 가져오려면 sys.dm_exec_query_stats 동적 관리 함수의 statement_start_offset 열을 쿼리하십시오.  
  
## <a name="see-also"></a>참고 항목  
[sp_create_plan_guide&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[계획 지침](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle&#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
