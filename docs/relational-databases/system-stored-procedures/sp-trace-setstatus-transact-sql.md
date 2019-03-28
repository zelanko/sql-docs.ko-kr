---
title: sp_trace_setstatus (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_trace_setstatus_TSQL
- sp_trace_setstatus
dev_langs:
- TSQL
helpviewer_keywords:
- sp_trace_setstatus
ms.assetid: 29e7a7d7-b9c1-414a-968a-fc247769750d
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b71e79f28abb5932fc9a7a644bf466f848c1e6e7
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58534805"
---
# <a name="sptracesetstatus-transact-sql"></a>sp_trace_setstatus(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 추적의 현재 상태를 수정합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_trace_setstatus [ @traceid = ] trace_id , [ @status = ] status  
```  
  
## <a name="arguments"></a>인수  
`[ @traceid = ] trace_id` 수정할 추적의 ID입니다. *trace_id* 됩니다 **int**, 기본값은 없습니다. 사용자는이 *trace_id* 식별, 수정 및 추적을 제어 하는 값입니다. 검색에 대 한 자세한 합니다 *trace_id*를 참조 하세요 [sys.fn_trace_getinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md).  
  
`[ @status = ] status` 추적에서 구현할 동작을 지정 합니다. *상태* 됩니다 **int**, 기본값은 없습니다.  
  
 다음 표에서는 지정할 수 있는 상태를 보여 줍니다.  
  
|상태|Description|  
|------------|-----------------|  
|**0**|지정한 추적을 중지합니다.|  
|**1**|지정한 추적을 시작합니다.|  
|**2**|지정한 추적을 닫고 서버에서 해당 정의를 삭제합니다.|  
  
> [!NOTE]  
>  추적은 먼저 중지한 후 닫아야 합니다. 추적은 먼저 중지하고 닫은 후에 확인할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 아래 표에서는 저장 프로시저가 완료된 후 사용자가 얻을 수 있는 코드 값을 설명합니다.  
  
|반환 코드|Description|  
|-----------------|-----------------|  
|**0**|오류가 없습니다.|  
|**1**|알 수 없는 오류입니다.|  
|**8**|지정한 상태는 유효하지 않습니다.|  
|**9**|지정한 추적 핸들이 유효하지 않습니다.|  
|**13**|메모리가 부족합니다. 지정한 동작을 수행할 메모리가 충분하지 않으면 반환됩니다.|  
  
 추적을 이미 지정한 상태에 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 돌아갑니다 **0**합니다.  
  
## <a name="remarks"></a>Remarks  
 모든 SQL Trace 저장 프로시저(**sp_trace_xx**)의 매개 변수는 엄격하게 형식이 지정되어 있습니다. 이러한 매개 변수가 인수 설명에서 지정한대로 정확한 입력 매개 변수 데이터 형식으로 호출되지 않으면 저장 프로시저는 오류를 반환합니다.  
  
 추적 저장 프로시저 사용에 대한 예는 [추적 만들기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)를 참조하세요.  
  
## <a name="permissions"></a>사용 권한  
 사용자는 ALTER TRACE 권한이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [sys.fn_trace_geteventinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_getfilterinfo&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sp_trace_generateevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [SQL 추적](../../relational-databases/sql-trace/sql-trace.md)  
  
  
