---
title: "OLEDB Call 이벤트 클래스 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: event-classes
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- OLEDB Call event class
ms.assetid: e1be1e90-98cc-47a3-addd-59d4aeca6547
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a5eb28eace8c8aa1e5f37e952207b6cf18543251
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/12/2018
---
# <a name="oledb-call-event-class"></a>OLEDB Call 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
**OLEDB Call** 이벤트 클래스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 분산 쿼리 및 원격 저장 프로시저를 위해 OLE DB 공급자를 호출할 때 발생합니다.  
  
 **OLEDB Call** 이벤트 클래스는 데이터를 요청하지 않는 호출이나 **QueryInterface** 메서드를 사용하지 않는 호출을 모니터링 할 때만 추적에 포함시키십시오. **OLEDB Call** 이벤트 클래스를 추적에 포함할 때 발생하는 오버헤드의 정도는 추적 중 데이터베이스에 대한 OLE DB 호출의 빈도에 따라 달라집니다. 호출이 자주 발생할 경우 추적으로 인해 성능이 심각하게 저하될 수도 있습니다.  
  
## <a name="oledb-call-event-class-data-columns"></a>OLEDB Call 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|ClientProcessID|**정수**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**정수**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|Duration|**Bigint**|OLE DB Call 이벤트를 완료하는 데 소요되는 시간입니다.|13|아니오|  
|EndTime|**날짜/시간**|이벤트가 종료된 시간입니다.|15|예|  
|Error|**int**|지정된 이벤트의 오류 번호입니다. 종종 sys.messages 카탈로그 뷰에 저장된 오류 번호를 나타냅니다.|31|예|  
|EventClass|**정수**|이벤트 유형 = 119|27|아니오|  
|EventSequence|**정수**|일괄 처리 내의 OLE DB 이벤트 클래스 시퀀스입니다.|51|아니오|  
|EventSubClass|**정수**|0=시작<br /><br /> 1=완료|21|아니오|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LinkedServerName|**nvarchar**|연결된 서버의 이름입니다.|45|예|  
|LoginName|**nvarchar**|사용자 로그인 이름(DOMAIN\Username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|예|  
|LoginSid|**이미지**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|MethodName|**nvarchar**|OLE DB 메서드의 이름입니다.|47|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|ProviderName|**nvarchar**|OLE DB Provider의 이름입니다.|46|예|  
|RequestID|**정수**|문을 포함하는 요청의 ID입니다.|49|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|**정수**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TextData|**nvarchar**|OLE DB 호출에서 주고 받는 매개 변수입니다.|1|아니오|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Transact-SQL의 OLE 자동화 개체](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
