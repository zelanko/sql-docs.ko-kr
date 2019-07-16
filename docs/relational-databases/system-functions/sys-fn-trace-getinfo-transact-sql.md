---
title: sys.fn_trace_getinfo (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_getinfo
- fn_trace_getinfo_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- traces [SQL Server], status information
- status information [SQL Server], traces
- sys.fn_trace_getinfo function
- fn_trace_getinfo function
ms.assetid: 04b140fe-110a-47b8-98b5-e4c161beb6c9
author: rothja
ms.author: jroth
ms.openlocfilehash: 041f651fb34c486cebc589f119f3e5f220314dd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68059229"
---
# <a name="sysfntracegetinfo-transact-sql"></a>sys.fn_trace_getinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  지정한 추적이나 모든 기존 추적에 대한 정보를 반환합니다.  
  
> **중요!** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.    
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.fn_trace_getinfo ( { trace_id | NULL | 0 | DEFAULT } )  
```  
  
## <a name="arguments"></a>인수  
 *trace_id*  
 추적의 ID입니다. *trace_id* 됩니다 **int**합니다.  유효한 입력은 NULL이 추적의 ID 번호를 0 또는 DEFAULT입니다. 이 컨텍스트에서 NULL, 0 및 DEFAULT는 동등한 값입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 모든 추적에 대한 정보를 반환하려면 NULL, 0 또는 DEFAULT를 지정합니다.  
  
## <a name="tables-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|traceid|**int**|추적의 ID입니다.|  
|속성|**int**|추적의 속성입니다.<br /><br /> 1= 추적 옵션. 자세한 내용은 @options 에 [sp_trace_create &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)합니다.<br /><br /> 2 = 파일 이름<br /><br /> 3 = 최대 크기<br /><br /> 4 = 중지 시간<br /><br /> 5 = 현재 추적 상태. 0 = 중지됨. 1 = 실행 중.|  
|value|**sql_variant**|지정된 추적의 속성에 대한 정보입니다.|  
  
## <a name="remarks"></a>설명  
 fn_trace_getinfo에 특정 추적의 ID를 전달하면 해당 추적에 대한 정보가 반환되고 잘못된 ID를 전달하면 빈 행 집합이 반환됩니다.  
  
 fn_trace_getinfo는 해당 결과 집합에 포함된 모든 추적 파일 이름에 .trc 확장명을 추가합니다. 추적 정의에 대 한 정보를 참조 하세요 [sp_trace_create &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)합니다. 추적 필터에 대 한 유사한 정보를 참조 하세요. [sys.fn_trace_getfilterinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)합니다.  
  
 추적 저장 프로시저를 사용 하는 전체 예제를 참조 하세요 [추적을 만들고 &#40;TRANSACT-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER TRACE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 모든 활성 추적에 대한 정보를 반환합니다.  
  
```  
SELECT * FROM sys.fn_trace_getinfo(0) ;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [추적 만들기&#40;Transact-SQL&#41;](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)   
 [sp_trace_create&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)   
 [sp_trace_generateevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)   
 [sys.fn_trace_getfilterinfo&#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)   
 [sys.fn_trace_geteventinfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)   
 [sys.fn_trace_gettable &#40;TRANSACT-SQL&#41;](../../relational-databases/system-functions/sys-fn-trace-gettable-transact-sql.md)  
  
  
