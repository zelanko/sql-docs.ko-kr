---
title: "SQL:StmtCompleted 이벤트 클래스 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL:StmtCompleted event class
ms.assetid: a55f005d-e020-423c-8940-c24ea1b20104
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 99a9d763386ecea12b12e9ddd6d597f00ff6b172
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="sqlstmtcompleted-event-class"></a>SQL:StmtCompleted 이벤트 클래스
  SQL:StmtCompleted 이벤트 클래스는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 완료되었음을 나타냅니다.  
  
## <a name="sqlstmtcompleted-event-class-data-columns"></a>SQL:StmtCompleted 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|CPU|**int**|이벤트에 의해 사용된 CPU 시간(밀리초)입니다.|18|예|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|기간|**bigint**|이벤트에 의해 사용된 시간(마이크로초)입니다.|13|예|  
|EndTime|**datetime**|이벤트가 종료된 시간입니다.|15|예|  
|EventClass|**int**|이벤트 유형 = 41|27|아니요|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IntegerData|**int**|문이 반환한 행의 수입니다.|25|예|  
|IntegerData2|**int**|실행 중인 문의 종료 오프셋(바이트)입니다.|55|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LineNumber|**int**|실행 중인 문의 줄 번호입니다.|5|예|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NestLevel|**int**|문이 저장 프로시저 내에서 실행된 경우 저장 프로시저의 중첩 수준입니다.|29|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|Offset|**int**|저장 프로시저나 일괄 처리 내에 있는 문의 시작 오프셋입니다.|61|예|  
|Reads|**bigint**|SQL 문에 의해 실행된 페이지 읽기 수입니다.|16|예|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|RowCounts|**bigint**|이벤트의 영향을 받은 행 수 입니다.|48|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**ntext**|실행된 문의 텍스트입니다.|1|예|  
|TransactionID|**bigint**|문이 트랜잭션 내에서 실행된 경우 트랜잭션의 ID입니다.|4|예|  
|Writes|**bigint**|SQL 문에 의해 실행된 페이지 쓰기 수입니다.|17|예|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
