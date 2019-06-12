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
manager: craigg
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7eb9cc127650d2fb6faacabcd30ce0ecb2ae3588
ms.sourcegitcommit: 02df4e7965b2a858030bb508eaf8daa9bc10b00b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265481"
---
# <a name="brokerremote-message-ack-event-class"></a>Broker:Remote Message Ack 이벤트 클래스

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **가 메시지 승인을 보내거나 받을 때** Broker:Remote Message Ack [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 생성합니다.  
  
## <a name="brokerremote-message-ack-event-class-data-columns"></a>Broker:Remote Message Ack 이벤트 클래스 데이터 열  
  
|데이터 열|형식|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|**BigintData1**|**bigint**|승인이 포함된 메시지의 시퀀스 번호입니다.|52|아니오|  
|**BigintData2**|**bigint**|메시지의 시퀀스 번호를 인식하고 있습니다.|53|아니오|  
|**ClientProcessID**|**ssNoversion**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**ssNoversion**|USE *database* 문에서 지정된 데이터베이스의 ID입니다. 지정된 인스턴스에 대해 USE *database* 문이 실행되지 않은 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**EventClass**|**ssNoversion**|캡처된 이벤트 클래스 유형입니다. **Broker:Message Ack** 의 경우 항상 **149**입니다.|27|아니오|  
|**EventSequence**|**ssNoversion**|이 이벤트의 시퀀스 번호입니다.|51|아니오|  
|**EventSubClass**|**nvarchar**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **승인 포함 메시지 전송**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 일부로 승인을 보냈습니다.<br /><br /> **승인 전송**:<br />                    [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 외부로 승인을 보냈습니다.<br /><br /> **승인 포함 메시지 수신**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 일반 시퀀스 메시지의 일부로 승인을 받았습니다.<br /><br /> **승인 수신**:<br />                  [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 시퀀스 메시지의 외부로 승인을 받았습니다.|21|예|  
|**GUID**|**uniqueidentifier**|대화 상자의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|아니오|  
|**HonorBrokerPriority**|**정수**|현재 데이터베이스 HONOR_BROKER_PRIORITY 옵션의 값: 0 = OFF, 1 = ON|32|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IntegerData**|**ssNoversion**|승인이 포함된 메시지의 조각 번호입니다.|25|아니오|  
|**IntegerData2**|**ssNoversion**|승인되는 메시지의 조각 번호입니다.|55|아니오|  
|**IsSystem**|**ssNoversion**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|아니오|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|**Priority**|**ssNoversion**|대화의 우선 순위 수준입니다.|5|예|  
|**RoleName**|**nvarchar**|메시지를 승인하는 인스턴스의 역할입니다. 이 역할은 **시작자** 또는 **대상**입니다.|38|아니오|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|**SPID**|**ssNoversion**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**StarvationElevation**|**ssNoversion**|대화에 대해 구성된 우선 순위보다 우선 순위가 높은 메시지가 전송되었습니다. 0 = false, 1 = true|33|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|아니오|  
  
  
