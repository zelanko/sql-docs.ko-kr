---
title: OLEDB QueryInterface 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- OLEDB QueryInterface event class
ms.assetid: f54c9ef9-3add-497c-a09b-42c4ce3c623d
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 39059275021f1196b729af4f30f23a09fd95c197
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68050423"
---
# <a name="oledb-queryinterface-event-class"></a>OLEDB QueryInterface 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **OLEDB QueryInterface** 이벤트 클래스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 분산 쿼리 및 원격 저장 프로시저를 위해 OLE DB **QueryInterface** 를 호출할 때 발생합니다. 분산 쿼리 및 원격 저장 프로시저와 관련된 문제를 모니터링하는 추적에 이 이벤트 클래스를 포함시킵니다.  
  
 **OLEDB QueryInterface** 이벤트 클래스가 포함되면 오버헤드 양이 많아집니다. 이런 이벤트가 자주 발생할 경우 추적으로 인해 성능이 심각하게 저하될 수도 있습니다. 오버헤드 발생을 최소화하려면 단기간 동안 특정 문제를 모니터링하는 추적에서만 이 이벤트 클래스를 사용하십시오.  
  
## <a name="oledb-queryinterface-event-class-data-columns"></a>OLEDB QueryInterface 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|Duration|**bigint**|OLE DB QueryInterface 이벤트를 완료하는 데 소요되는 시간입니다.|13|예|  
|EndTime|**datetime**|이벤트가 종료된 시간입니다.|15|yes|  
|Error|**int**|지정된 이벤트의 오류 번호입니다. 종종 **sys.messages** 카탈로그 뷰에 저장된 오류 번호를 나타냅니다.|31|yes|  
|EventClass|**int**|이벤트 유형 = 120|27|예|  
|EventSequence|**int**|일괄 처리에서 OLE DB 이벤트 클래스의 순서입니다.|51|예|  
|EventSubClass|**int**|0=시작<br /><br /> 1=완료|21|예|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|LinkedServerName|**nvarchar**|연결된 서버의 이름입니다.|45|yes|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|yes|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|MethodName|**nvarchar**|호출 메서드의 이름입니다.|47|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|ProviderName|**nvarchar**|OLE DB Provider의 이름입니다.|46|yes|  
|RequestID|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TextData|**nvarchar**|OLE DB 호출에서 주고 받는 매개 변수입니다.|1|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Transact-SQL의 OLE 자동화 개체](../../relational-databases/stored-procedures/ole-automation-objects-in-transact-sql.md)  
  
  
