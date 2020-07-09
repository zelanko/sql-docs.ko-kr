---
title: Broker:Remote Message Ack 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Remote Message Ack event class
ms.assetid: 3d67efe1-74b4-4633-b029-c6e05b19f4dc
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb2e8f7fa1f39fffecf72a8eb51fac5bf9bcce51
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85763011"
---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack 이벤트 클래스

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **가 메시지 승인을 보내거나 받을 때** Broker:Remote Message Ack [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 생성합니다.  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Broker:Remote Message Ack 이벤트 클래스 데이터 열  
  
|데이터 열|Type|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**BigintData1**|**bigint**|승인이 포함된 메시지의 시퀀스 번호입니다.|52|예|  
|**BigintData2**|**bigint**|메시지의 시퀀스 번호를 인식하고 있습니다.|53|예|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|**DatabaseID**|**int**|USE *database* 문에서 지정된 데이터베이스의 ID입니다. 지정된 인스턴스에 대해 USE *database* 문이 실행되지 않은 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Broker:Message Ack** 의 경우 항상 **149**입니다.|27|예|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|예|  
|**EventSubClass**|**nvarchar**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **승인 포함 메시지 전송**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 일부로 승인을 보냈습니다.<br /><br /> **승인 전송**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 외부로 승인을 보냈습니다.<br /><br /> **승인 포함 메시지 수신**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 일부로 승인을 받았습니다.<br /><br /> **승인 수신**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 시퀀스 메시지의 외부로 승인을 받았습니다.|21|yes|  
|**GUID**|**uniqueidentifier**|대화 상자의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|예|  
|**HonorBrokerPriority**|**정수**|데이터베이스 HONOR_BROKER_PRIORITY 옵션의 현재 값은 0 = OFF, 1 = ON입니다.|32|yes|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|**IntegerData**|**int**|승인이 포함된 메시지의 조각 번호입니다.|25|예|  
|**IntegerData2**|**int**|승인되는 메시지의 조각 번호입니다.|55|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|yes|  
|**우선 순위**|**int**|대화의 우선 순위 수준입니다.|5|yes|  
|**RoleName**|**nvarchar**|메시지를 승인하는 인스턴스의 역할입니다. 이 역할은 **시작자** 또는 **대상**입니다.|38|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**StarvationElevation**|**int**|대화에 대해 구성된 우선 순위보다 우선 순위가 높은 메시지가 전송되었습니다. 0 = false, 1 = true입니다.|33|yes|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|예|  
  
  
