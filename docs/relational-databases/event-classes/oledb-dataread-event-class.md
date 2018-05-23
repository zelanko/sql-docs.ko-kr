---
title: OLEDB DataRead 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- OLEDB DataRead event class
ms.assetid: fb6869ba-3199-4e32-a650-60a5dda2571e
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a026557c63e5db6c73a8c4544db2ea5c58ef4cec
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
---
# <a name="oledb-dataread-event-class"></a>OLEDB DataRead 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  OLEDB DataRead 이벤트 클래스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 분산 쿼리 및 원격 저장 프로시저 실행을 위해 OLE DB 공급자를 호출할 때 발생합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 언제 OLE DB 공급자에 데이터 요청 호출을 하는지 모니터링하는 추적에 이 이벤트 클래스를 포함시키십시오.  
  
 OLEDB DataRead 클래스가 추적에 포함되면 발생하는 오버헤드의 양이 늘어납니다. 따라서 짧은 시간 동안 특정 문제를 모니터링하는 추적에 대해 이 이벤트 클래스의 사용을 제한하는 것이 좋습니다.  
  
## <a name="oledb-dataread-event-class-data-columns"></a>OLEDB DataRead 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 USE *database*문이 발급되지 않은 경우에 사용되는 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|Duration|**bigint**|OLE DB Call 이벤트를 완료하는 데 소요되는 시간입니다.|13|아니요|  
|EndTime|**datetime**|이벤트가 종료된 시간입니다.|15|예|  
|Error|**int**|지정된 이벤트의 오류 번호입니다. 종종 sys.messages 카탈로그 뷰에 저장된 오류 번호를 나타냅니다.|31|예|  
|EventClass|**int**|이벤트 유형 = 121|27|아니요|  
|EventSequence|**int**|일괄 처리 내의 OLE DB 이벤트 클래스 시퀀스입니다.|51|아니요|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 0=시작<br /><br /> 1=완료|21|아니요|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LinkedServerName|**nvarchar**|연결된 서버의 이름입니다.|45|예|  
|LoginName|**nvarchar**|사용자 로그인 이름(DOMAIN\Username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|MethodName|**nvarchar**|호출 메서드의 이름입니다.|47|아니요|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|ProviderName|**nvarchar**|OLE DB Provider의 이름입니다.|46|예|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**정수**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**nvarchar**|OLE DB 호출에서 주고 받는 매개 변수입니다.|1|아니요|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Transact-SQL의 OLE 자동화 개체](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
