---
title: "Broker:Remote Message Ack 이벤트 클래스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Broker:Remote Message Ack 이벤트 클래스"
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
caps.latest.revision: 29
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 29
---
# Broker:Remote Message Ack 이벤트 클래스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **가 메시지 승인을 보내거나 받을 때** Broker:Remote Message Ack [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 생성합니다.  
  
## Broker:Remote Message Ack 이벤트 클래스 데이터 열  
  
|데이터 열|유형|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|**BigintData1**|**bigint**|승인이 포함된 메시지의 시퀀스 번호입니다.|52|아니요|  
|**BigintData2**|**bigint**|메시지의 시퀀스 번호를 인식하고 있습니다.|53|아니요|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정된 데이터베이스의 ID입니다. 지정된 인스턴스에 대해 USE *database* 문이 실행되지 않은 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Broker:Message Ack** 의 경우 항상 **149**입니다.|27|아니요|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니요|  
|**EventSubClass**|**nvarchar**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **승인 포함 메시지 전송**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 일부로 승인을 보냈습니다.<br /><br /> **승인 전송**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 외부로 승인을 보냈습니다.<br /><br /> **승인 포함 메시지 수신**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 일부로 승인을 받았습니다.<br /><br /> **승인 수신**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 시퀀스 메시지의 외부로 승인을 받았습니다.|21|예|  
|**GUID**|**uniqueidentifier**|대화 상자의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|아니요|  
|**HonorBrokerPriority**|**정수**|데이터베이스 HONOR_BROKER_PRIORITY 옵션의 현재 값은 0 = OFF, 1 = ON입니다.|32|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IntegerData**|**int**|승인이 포함된 메시지의 조각 번호입니다.|25|아니요|  
|**IntegerData2**|**int**|승인되는 메시지의 조각 번호입니다.|55|아니요|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|아니요|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|**Priority**|**int**|대화의 우선 순위 수준입니다.|5|예|  
|**RoleName**|**nvarchar**|메시지를 승인하는 인스턴스의 역할입니다. 이 역할은 **시작자** 또는 **대상**입니다.|38|아니요|  
|**ServerName**|**nvarchar**|추적되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**StarvationElevation**|**int**|대화에 대해 구성된 우선 순위보다 우선 순위가 높은 메시지가 전송되었습니다. 0 = false, 1 = true입니다.|33|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|아니요|  
  
  