---
title: "DTCTransaction 이벤트 클래스 | Microsoft 문서"
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
- DTCTransaction event class
ms.assetid: 9a2d358e-5b8f-4d0b-8b93-6705c009ad57
caps.latest.revision: 37
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a7832dce3ed058f5ddd599fd19abd9703b20ff06
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="dtctransaction-event-class"></a>DTCTransaction 이벤트 클래스
  **DTCTransaction** 이벤트 클래스를 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] DTC(Distributed Transaction Coordinator)를 통해 통합된 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 트랜잭션의 상태를 모니터링할 수 있습니다. 여기에는 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 동일 인스턴스에서 둘 이상의 데이터베이스와 관련된 트랜잭션 또는 둘 이상의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스와 관련된 분산 트랜잭션이 있습니다.  
  
## <a name="dtctransaction-event-class-data-columns"></a>DTCTransaction 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|**BinaryData**|**image**|DTC 내에서 이 트랜잭션을 고유하게 식별하는 UOW(Unit of Work) ID의 이진 표현입니다.|2|예|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|**EventClass**|**int**|이벤트 유형 = 19|27|아니요|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 0=주소 얻기<br /><br /> 1=트랜잭션 전파<br /><br /> 3=연결 닫기<br /><br /> 6=새 DTC 트랜잭션 만들기<br /><br /> 7=DTC 트랜잭션 참여<br /><br /> 9=내부 커밋<br /><br /> 10=내부 중단<br /><br /> 14=트랜잭션 준비 중<br /><br /> 15=트랜잭션 준비 완료<br /><br /> 16=트랜잭션 중단 중<br /><br /> 17=트랜잭션 커밋 중<br /><br /> 22=준비된 상태에서 TM 실패<br /><br /> 23=알 수 없음|21|예|  
|**GroupID**|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IntegerData**|**int**|트랜잭션의 격리 수준입니다.|25|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|사용 가능한 경우 이벤트가 시작된 시간입니다.|14|예|  
|**TextData**|**ntext**|DTC 내에서 이 트랜잭션을 고유하게 식별하는 UOW를 텍스트로 표시한 것입니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
