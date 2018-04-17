---
title: sys.fn_trace_gettable (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_trace_gettable
- fn_trace_gettable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_trace_gettable function
- sys.fn_trace_gettable function
ms.assetid: c2590159-6ec5-4510-81ab-e935cc4216cd
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 461807f1d79032c85316551adb5229d02aa67b06
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sysfntracegettable-transact-sql"></a>sys.fn_trace_gettable(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  하나 이상의 추적 파일의 내용을 테이블 형식으로 반환합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 확장 이벤트를 대신 사용하세요.  
   
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>인수  
 '*filename*'  
 읽을 초기 추적 파일을 지정합니다. *filename* 은 **nvarchar (256)**, 기본값은 없습니다.  
  
 *number_files*  
 읽을 롤오버 파일의 수를 지정합니다. 이 수에 지정 된 초기 파일이 포함 됩니다 *filename*합니다. *number_files* 는 **int**합니다.  
  
## <a name="remarks"></a>주의  
 경우 *number_files* 로 지정 된 **기본**, **fn_trace_gettable** 추적 끝에 도달할 때까지 모든 롤오버 파일을 읽습니다. **fn_trace_gettable** 지정된 된 추적에 대 한 유효한 모든 열이 있는 테이블을 반환 합니다. 자세한 내용은 참조 [sp_trace_setevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)합니다.  
  
 Fn_trace_gettable 함수 롤오버 파일 로드 되지 것입니다 수 (사용 하 여이 옵션을 지정 하는 경우는 *number_files* 인수)는 원래 추적 파일 이름이 밑줄과 숫자 값으로 끝나는 합니다. 이는 파일이 롤오버될 때 자동으로 추가된 밑줄과 숫자에는 적용되지 않습니다. 추적 파일의 이름을 변경하여 원래 파일 이름에서 밑줄을 제거하면 이 문제를 해결할 수 있습니다. 예를 들어 원래 파일 이름이 **Trace_Oct_5.trc** 롤오버 파일 이름이 고 **Trace_Oct_5_1.trc**, 파일 이름을 바꿀 수 있습니다 **TraceOct5.trc** 및  **TraceOct5_1.trc**합니다.  
  
 이 함수는 실행된 인스턴스에서 아직 활성 상태인 추적을 읽을 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 서버에 대한 ALTER TRACE 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-using-fntracegettable-to-import-rows-from-a-trace-file"></a>1. fn_trace_gettable을 사용하여 추적 파일에서 행 가져오기  
 다음 예에서는 `fn_trace_gettable` 문의 `FROM` 절에서 `SELECT...INTO`을 호출합니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fntracegettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>2. fn_trace_gettable을 사용하여 SQL Server 테이블로 로드할 수 있는 IDENTITY 열이 있는 테이블 반환  
 다음은 `SELECT...INTO` 문의 일부로 함수를 호출하고 `IDENTITY` 테이블로 로드할 수 있는 `temp_trc` 열이 있는 테이블을 반환하는 예입니다.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sp_trace_generateevent &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
