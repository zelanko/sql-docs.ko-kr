---
title: OLEDB Call 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- OLEDB Call event class
ms.assetid: e1be1e90-98cc-47a3-addd-59d4aeca6547
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2250847ee35210c63a4ac9ed5e1e41bab33a08ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62956364"
---
# <a name="oledb-call-event-class"></a>OLEDB Call 이벤트 클래스
  **OLEDB Call** 이벤트 클래스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 분산 쿼리 및 원격 저장 프로시저를 위해 OLE DB 공급자를 호출할 때 발생합니다.  
  
 **OLEDB Call** 이벤트 클래스는 데이터를 요청하지 않는 호출이나 **QueryInterface** 메서드를 사용하지 않는 호출을 모니터링 할 때만 추적에 포함시키십시오. **OLEDB Call** 이벤트 클래스를 추적에 포함할 때 발생하는 오버헤드의 정도는 추적 중 데이터베이스에 대한 OLE DB 호출의 빈도에 따라 달라집니다. 호출이 자주 발생할 경우 추적으로 인해 성능이 심각하게 저하될 수도 있습니다.  
  
## <a name="oledb-call-event-class-data-columns"></a>OLEDB Call 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|ClientProcessID|`Int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|DatabaseID|`Int`|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|DatabaseName|`nvarchar`|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|사용자 계정 컨트롤|  
|Duration|`Bigint`|OLE DB Call 이벤트를 완료하는 데 소요되는 시간입니다.|13|아니요|  
|EndTime|`Datetime`|이벤트가 종료된 시간입니다.|15|사용자 계정 컨트롤|  
|Error|`int`|지정된 이벤트의 오류 번호입니다. 종종 sys.messages 카탈로그 뷰에 저장된 오류 번호를 나타냅니다.|31|사용자 계정 컨트롤|  
|EventClass|`Int`|이벤트 유형 = 119|27|아니요|  
|EventSequence|`Int`|일괄 처리 내의 OLE DB 이벤트 클래스 시퀀스입니다.|51|아니요|  
|EventSubClass|`Int`|0=시작<br /><br /> 1=완료|21|아니요|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|사용자 계정 컨트롤|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|사용자 계정 컨트롤|  
|LinkedServerName|`nvarchar`|연결된 서버의 이름입니다.|45|사용자 계정 컨트롤|  
|LoginName|`nvarchar`|사용자 로그인 이름(DOMAIN\Username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|사용자 계정 컨트롤|  
|LoginSid|`Image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|MethodName|`nvarchar`|OLE DB 메서드의 이름입니다.|47|사용자 계정 컨트롤|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|ProviderName|`nvarchar`|OLE DB Provider의 이름입니다.|46|사용자 계정 컨트롤|  
|RequestID|`Int`|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하고 Login2로 문을 실행할 경우 `SessionLoginName`은 Login1을 표시하고 `LoginName`은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|SPID|`Int`|이벤트가 발생한 세션의 ID입니다.|12|사용자 계정 컨트롤|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|TextData|`nvarchar`|OLE DB 호출에서 주고 받는 매개 변수입니다.|1|아니요|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>관련 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [Transact-SQL의 OLE 자동화 개체](../stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
