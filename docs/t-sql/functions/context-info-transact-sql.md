---
title: CONTEXT_INFO(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 98a275622a809b3856b66d825cd48e2698fea51b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) 문을 사용하여 현재 세션 또는 일괄 처리에 대해 설정된 **context_info** 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>반환 값
**context_info**의 값입니다.
  
**context_info**가 설정되지 않은 경우:
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 null을 반환합니다.  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 고유한 세션별 GUID를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
MARS(Multiple Active Result Sets)를 사용하면 응용 프로그램이 같은 시간에 같은 연결에서 여러 일괄 처리 또는 요청을 실행할 수 있습니다. MARS 연결의 일괄 처리 중 하나에서 SET CONTEXT_INFO를 실행하는 경우 CONTEXT_INFO 함수를 SET 문과 동일한 일괄 처리에서 실행하면 새 컨텍스트 값이 반환됩니다. SET 문을 실행한 일괄 처리가 완료된 후에 연결에 있는 하나 이상의 다른 일괄 처리를 시작해야만 이러한 다른 일괄 처리에서 CONTEXT_INFO 함수에 의해 새 값이 반환됩니다.
  
## <a name="permissions"></a>사용 권한  
특별한 권한이 필요하지 않습니다. 컨텍스트 정보는 **sys.dm_exec_requests**, **sys.dm_exec_sessions** 및 **sys.sysprocesses** 시스템 뷰에도 저장되지만 뷰를 직접 쿼리하려면 SELECT 및 VIEW SERVER STATE 권한이 필요합니다.
  
## <a name="examples"></a>예  
다음 예에서는 **context_info** 값을 `0x1256698456`으로 설정한 다음, `CONTEXT_INFO` 함수를 사용하여 값을 검색합니다.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>관련 항목:
[SET CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
