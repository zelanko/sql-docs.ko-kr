---
title: "Broker:Forwarded Message Dropped 이벤트 클래스 | Microsoft 문서"
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
- Broker:Forwarded Message Dropped event class
ms.assetid: ec242d0b-77b0-45f5-8b12-186a14b173a8
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8d63f05d5f476dcb03398872759b92e21d04c99c
ms.contentlocale: ko-kr
ms.lasthandoff: 04/11/2017

---
# <a name="brokerforwarded-message-dropped-event-class"></a>Broker:Forwarded Message Dropped 이벤트 클래스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Service Broker가 전달될 메시지를 삭제하면 Broker:Forwarded Message Dropped 이벤트를 생성합니다.  
  
## <a name="brokerforwarded-message-dropped-event-class-data-columns"></a>Broker:Forwarded Message Dropped 이벤트 클래스 데이터 열  
  
|데이터 열|유형|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|BigintData1|**bigint**|메시지 시퀀스 번호입니다.|52|아니요|  
|ClientProcessID|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database*문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|DBUserName|**nvarchar**|이 메시지를 보낸 Broker 인스턴스 식별자입니다.|40|아니요|  
|오류|**int**|이벤트의 텍스트에 대한 sys.messages의 메시지 ID 번호입니다.|31|아니요|  
|EventClass|**int**|캡처된 이벤트 클래스 유형입니다. Broker:Forwarded Message Dropped의 경우 항상 191입니다.|27|아니요|  
|EventSequence|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니요|  
|FileName|**nvarchar**|메시지가 전송되는 서비스의 이름입니다.|36|아니요|  
|GUID|**uniqueidentifier**|대화의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|아니요|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IndexID|**int**|전달된 메시지에 대해 남아 있는 홉 수입니다.|24|아니요|  
|IntegerData|**int**|전달된 메시지의 조각 번호입니다.|25|아니요|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|ObjectId|**int**|전달된 메시지의 시간 제한 값입니다.|22|아니요|  
|ObjectName|**nvarchar**|전달된 메시지의 메시지 ID입니다.|34|아니요|  
|OwnerName|**nvarchar**|메시지 대상의 Broker 인스턴스 식별자입니다.|37|아니요|  
|RoleName|**nvarchar**|대화 핸들의 역할입니다. 다음 중 하나입니다.<br /><br /> -Initiator. 대화를 시작한 Broker입니다.<br /><br /> -Target. 대화의 대상이 되는 Broker입니다.|38|아니요|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|Severity|**int**|이벤트 텍스트의 심각도 숫자입니다.|29|아니요|  
|SPID|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|State|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 코드 내에서 이벤트가 생성된 위치를 나타냅니다. 이 이벤트가 생성될 수 있는 각 위치의 상태 코드는 서로 다릅니다. Microsoft 지원 엔지니어는 이 상태 코드를 사용하여 이벤트가 생성된 위치를 찾을 수 있습니다.|30|아니요|  
|성공|**int**|메시지가 활성 상태인 시간입니다. 이 값이 시간 제한 값보다 크거나 같으면 메시지가 삭제됩니다.|23|아니요|  
|TargetLoginName|**nvarchar**|메시지가 전달된 네트워크 주소입니다.|42|아니요|  
|TargetUserName|**nvarchar**|메시지에 대한 시작 서비스의 이름입니다.|39|아니요|  
|TextData|**ntext**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 메시지를 삭제한 이유에 대한 설명입니다.|1|예|  
|Transaction ID|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|아니요|  
  
 이 이벤트의 TextData 열에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 메시지를 삭제한 이유에 대한 설명이 들어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
