---
title: Lock:Escalation 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Escalation event class
- lock escalation [SQL Server], event class
ms.assetid: d253b44c-7600-4afa-a3a7-03cc937c6a4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf72cd4c22003fef09805789b7ac9b70fbc42227
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48190873"
---
# <a name="lockescalation-event-class"></a>Lock:Escalation 이벤트 클래스
  **Lock:Escalation** 이벤트 클래스는 행 잠금이 개체 잠금으로 변환되는 것과 같이 미세 잠금이 성긴 잠금으로 변환되었음을 나타냅니다. 에스컬레이션 이벤트 클래스는 이벤트 ID 60입니다.  
  
## <a name="lockescalation-event-class-data-columns"></a>Lock:Escalation 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|**ClientProcessID**|`int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|**DatabaseID**|`int`|잠금을 획득한 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|**DatabaseName**|`nvarchar`|에스컬레이션이 발생한 데이터베이스의 이름입니다.|35|사용자 계정 컨트롤|  
|**EventClass**|`int`|이벤트 유형 = 60|27|아니요|  
|**EventSubClass**|`int`|잠금 에스컬레이션의 원인:<br /><br /> **0 - LOCK_THRESHOLD** 는 문이 잠금 임계값을 초과했음을 나타냅니다.<br /><br /> **1 - MEMORY_THRESHOLD** 는 문이 메모리 임계값을 초과했음을 나타냅니다.|21|사용자 계정 컨트롤|  
|**EventSequence**|`int`|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|**GroupID**|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|사용자 계정 컨트롤|  
|**HostName**|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|**IntegerData**|`int`|HoBT 잠금 카운트입니다. 잠금 에스컬레이션 시 HoBT의 잠금 수입니다.|25|사용자 계정 컨트롤|  
|**IntegerData2**|`int`|에스컬레이션된 잠금 카운트입니다. 변환된 총 잠금 수 입니다. 이러한 잠금 구조는 이미 에스컬레이션된 잠금으로 보호되므로 할당이 취소됩니다.|55|사용자 계정 컨트롤|  
|**IsSystem**|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|사용자 계정 컨트롤|  
|**LineNumber**|`int`|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 줄 수입니다.|5|사용자 계정 컨트롤|  
|**LoginName**|`nvarchar`|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|사용자 계정 컨트롤|  
|**LoginSid**|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|**모드**|`int`|에스컬레이션 후의 결과 잠금 모드:<br /><br /> 0=NULL - 모든 잠금 모드와 호환(LCK_M_NL)<br /><br /> 1=스키마 안정성 잠금(LCK_M_SCH_S)<br /><br /> 2=스키마 수정 잠금(LCK_M_SCH_M)<br /><br /> 3=공유 잠금(LCK_M_S)<br /><br /> 4=업데이트 잠금(LCK_M_U)<br /><br /> 5=배타 잠금(LCK_M_X)<br /><br /> 6=내재된 공유 잠금(LCK_M_IS)<br /><br /> 7=의도 업데이트 잠금(LCK_M_IU)<br /><br /> 8=의도 배타 잠금(LCK_M_IX)<br /><br /> 9=의도 업데이트 공유(LCK_M_SIU)<br /><br /> 10=의도 배타 공유(LCK_M_SIX)<br /><br /> 11=의도 배타 업데이트(LCK_M_UIX)<br /><br /> 12=대량 업데이트 잠금(LCK_M_BU)<br /><br /> 13=키 범위 공유/공유(LCK_M_RS_S)<br /><br /> 14=키 범위 공유/업데이트(LCK_M_RS_U)<br /><br /> 15=키 범위 삽입 NULL(LCK_M_RI_NL)<br /><br /> 16=키 범위 삽입 공유(LCK_M_RI_S)<br /><br /> 17=키 범위 삽입 업데이트(LCK_M_RI_U)<br /><br /> 18=키 범위 삽입 배타(LCK_M_RI_X)<br /><br /> 19=키 범위 배타 공유(LCK_M_RX_S)<br /><br /> 20=키 범위 배타 업데이트(LCK_M_RX_U)<br /><br /> 21=키 범위 배타 배타(LCK_M_RX_X)|32|사용자 계정 컨트롤|  
|**NTDomainName**|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|**NTUserName**|`nvarchar`|Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|**Exchange Spill**|`int`|잠금 에스컬레이션이 트리거된 테이블의 시스템 할당 ID입니다.|22|사용자 계정 컨트롤|  
|**ObjectID2**|`bigint`|관련 개체 또는 엔터티의 ID입니다. 즉, 잠금 에스컬레이션이 트리거된 HoBT ID입니다.|56|사용자 계정 컨트롤|  
|**Offset**|`int`|[!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 시작 오프셋입니다.|61|사용자 계정 컨트롤|  
|**OwnerID**|`int`|1=TRANSACTION<br /><br /> 2=CURSOR<br /><br /> 3=SESSION<br /><br /> 4=SHARED_TRANSACTION_WORKSPACE<br /><br /> 5=EXCLUSIVE_TRANSACTION_WORKSPACE<br /><br /> 6=WAITFOR_QUERY|58|사용자 계정 컨트롤|  
|**RequestID**|`int`|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SessionLoginName**|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|**SPID**|`int`|이벤트가 발생한 세션의 ID입니다.|12|사용자 계정 컨트롤|  
|**StartTime**|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|**TextData**|`ntext`|잠금 에스컬레이션을 발생시킨 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 텍스트입니다.|1|사용자 계정 컨트롤|  
|**TransactionID**|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
|**형식**|`int`|잠금 에스컬레이션 세분성:<br /><br /> 1=NULL_RESOURCE<br /><br /> 2=DATABASE<br /><br /> 3=FILE<br /><br /> 5=OBJECT(테이블 수준)<br /><br /> 6=PAGE<br /><br /> 7=KEY<br /><br /> 8=EXTENT<br /><br /> 9=RID<br /><br /> 10=APPLICATION<br /><br /> 11=METADATA<br /><br /> 12=HOBT<br /><br /> 13=ALLOCATION_UNIT|57|사용자 계정 컨트롤|  
  
## <a name="examples"></a>예  
 다음 예에서는 `sp_trace_create` 프로시저를 사용하여 추적을 만들고 `sp_trace_setevent` 를 사용하여 추적에 잠금 에스컬레이션 열을 추가한 다음 `sp_trace_setstatus` 를 추적을 시작합니다. `EXEC sp_trace_setevent @TraceID, 60, 22, 1`과 같은 문에서 숫자 `60` 은 에스컬레이션 이벤트 클래스를 나타내고, `22` 는 **ObjectID** 열을 나타내며, `1` 은 추적 이벤트를 ON으로 설정합니다.  
  
```  
DECLARE @RC int, @TraceID int;  
EXEC @rc = sp_trace_create @TraceID output, 0, N'C:\TraceResults';  
-- Set the events and data columns you need to capture.  
EXEC sp_trace_setevent @TraceID, 60,  1, 1; --  1 = TextData  
EXEC sp_trace_setevent @TraceID, 60, 12, 1; -- 12 = SPID  
EXEC sp_trace_setevent @TraceID, 60, 21, 1; -- 21 = EventSubClass  
EXEC sp_trace_setevent @TraceID, 60, 22, 1; -- 22 = ObjectID  
EXEC sp_trace_setevent @TraceID, 60, 25, 1; -- 25 = IntegerData  
EXEC sp_trace_setevent @TraceID, 60, 55, 1; -- 25 = IntegerData2  
EXEC sp_trace_setevent @TraceID, 60, 57, 1; -- 57 = Type  
-- Set any filter  byusing sp_trace_setfilter.  
-- Start the trace.  
EXEC sp_trace_setstatus @TraceID, 1;  
GO  
```  
  
 이제 추적이 실행되고 있으므로 추적할 문을 실행합니다. 문이 완료되면 다음 코드를 실행하여 추적을 중지한 다음 닫습니다. 이 예에서는 `fn_trace_getinfo` 함수를 사용하여 `traceid` 가 `sp_trace_setstatus` 문에 사용되도록 합니다.  
  
```  
-- After the trace is complete.  
DECLARE @TraceID int;  
-- Find the traceid of the current trace.  
SELECT @TraceID = traceid   
FROM ::fn_trace_getinfo(default)   
WHERE value = N'C:\TraceResults.trc';  
  
-- First stop the trace.   
EXEC sp_trace_setstatus @TraceID, 0;  
  
-- Close and then delete its definition from SQL Server.   
EXEC sp_trace_setstatus @TraceID, 2;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [sys.dm_tran_locks&#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql)  
  
  
