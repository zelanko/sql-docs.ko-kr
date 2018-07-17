---
title: CONTEXT_INFO(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f3d572bee6b06ef8cb1573759ec12e68f9e6ec9
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/04/2018
ms.locfileid: "37792194"
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

이 함수는 현재 세션 또는 일괄 처리에 대해 설정되거나 [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) 문을 사용하여 파생된 **context_info** 값을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>반환 값
**context_info** 값입니다.
  
**context_info**가 설정되지 않은 경우:
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 null을 반환합니다.  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 고유한 세션별 GUID를 반환합니다.  
  
## <a name="remarks"></a>Remarks  
MARS(Multiple Active Result Sets) 기능을 사용하면 응용 프로그램이 같은 시간에 같은 연결에서 여러 일괄 처리 또는 요청을 실행할 수 있습니다. MARS 연결 일괄 처리 중 하나가 SET CONTEXT_INFO를 실행하는 경우 `CONTEXT_INFO` 함수가 SET 문과 동일한 일괄 처리에서 실행하면 `CONTEXT_INFO` 함수는 새 컨텍스트 값을 반환합니다. `CONTEXT_INFO` 함수가 다른 연결 일괄 처리 중 하나 이상을 실행하는 경우 `CONTEXT_FUNCTION`은 SET 문을 실행한 일괄 처리를 완료한 후에 해당 일괄 처리가 시작되지 않으면 새 값을 반환하지 않습니다.
  
## <a name="permissions"></a>사용 권한  
특별한 권한이 필요하지 않습니다. 다음 시스템 보기는 컨텍스트 정보를 저장하지만 이러한 보기를 직접 쿼리하려면 SELECT 및 VIEW SERVER STATE 권한이 필요합니다.
- **sys.dm_exec_requests**
- **sys.dm_exec_sessions**
- **sys.sysprocesses**
  
## <a name="examples"></a>예  
이 간단한 예제에서는 **context_info** 값을 `0x1256698456`으로 설정한 다음, `CONTEXT_INFO` 함수를 사용하여 값을 검색합니다.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>관련 항목:
[SET CONTEXT_INFO&#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
