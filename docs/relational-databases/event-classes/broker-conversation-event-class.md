---
title: Broker:Conversation 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Conversation event class
ms.assetid: 784707b5-cc67-46a3-8ae6-8f8ecf4b27c0
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3330b9b44f2794daf8e9cd45e9806991a6a815de
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "67999763"
---
# <a name="brokerconversation-event-class"></a>Broker:Conversation 이벤트 클래스

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **Broker:Conversation** 이벤트를 생성하여 Service Broker 대화의 진행을 보고합니다.  
  
## <a name="brokerconversation-event-class-data-columns"></a>Broker:Conversation 이벤트 클래스 데이터 열  
  
|데이터 열|Type|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|**DatabaseID**|**int**|USE *database* 문에서 지정된 데이터베이스의 ID입니다. 실행된 USE *database*문이 없는 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. **DB_ID** 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Broker:Conversation** 의 경우 항상 **124**입니다.|27|예|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|예|  
|**EventSubClass**|**nvarchar**|이벤트 하위 클래스의 유형입니다. 각 이벤트 클래스에 대한 자세한 정보를 제공합니다.|21|yes|  
|**GUID**|**uniqueidentifier**|대화 상자의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 **HOST_NAME** 함수를 사용합니다.|8|yes|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**MethodName**|**nvarchar**|대화가 속한 대화 그룹입니다.|47|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|yes|  
|**ObjectName**|**nvarchar**|대화 상자의 대화 핸들입니다.|34|예|  
|**우선 순위**|**int**|대화의 우선 순위 수준입니다.|5|yes|  
|**RoleName**|**nvarchar**|대화 핸들의 역할입니다. 이 역할은 **시작자** 또는 **대상**입니다.|38|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**Severity**|**int**|이 이벤트에서 오류를 보고하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 심각도입니다.|29|예|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**TextData**|**ntext**|대화의 현재 상태입니다. 다음 값 중 하나가 될 수 있습니다.|1|yes|  
|||**SO**. 아웃바운드가 시작되었습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 이 대화에 대해 BEGIN CONVERSATION을 처리했지만 메시지가 전송되지 않았습니다.|||  
|||**SI**. 인바운드가 시작되었습니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 의 다른 인스턴스에서 현재 인스턴스와 새 대화를 시작했지만 현재 인스턴스가 첫 번째 메시지를 완전히 받지 못했습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 순서가 잘못된 메시지를 받는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대화를 이 상태로 만들 수 있습니다. 그러나 대화에 대해 받은 첫 번째 전송에 첫 번째 메시지가 모두 포함된 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대화를 CO 상태로 만들 수 있습니다.|||  
|||**CO**. 대화 중입니다. 대화가 설정되고 대화의 양쪽 모두 메시지를 보낼 수 있습니다. 일반 서비스에 대한 통신의 대부분은 대화가 이 상태일 때 수행됩니다.|||  
|||**DI**. 인바운드 연결이 끊어졌습니다. 원격 대화 상대가 END CONVERSATION을 실행했습니다. 로컬 대화 상대가 END CONVERSATION을 실행할 때까지 대화는 이 상태로 유지됩니다. 애플리케이션은 계속해서 대화 메시지를 받을 수 있습니다. 원격 대화 상대가 대화를 종료했기 때문에 애플리케이션에서 이 대화 메시지를 보낼 수는 없습니다. 애플리케이션이 END CONVERSATION을 실행하면 대화가 CD(닫힘) 상태로 전환됩니다.|||  
|||**DO**. 아웃바운드 연결이 끊어졌습니다. 로컬 대화 상대가 END CONVERSATION을 실행했습니다. 원격 대화 상대가 END CONVERSATION을 승인할 때까지 대화는 이 상태로 유지됩니다. 애플리케이션에서 대화 메시지를 보내거나 받을 수 없습니다. 원격 대화 상대가 END CONVERSATION을 승인하면 대화가 CD(닫힘) 상태로 전환됩니다.|||  
|||**ER**. 오류가 표시됩니다. 이 엔드포인트에서 오류가 발생했습니다. 오류, 심각도 및 상태 열은 발생한 특정 오류에 대한 정보를 포함합니다.|||  
|||**CD**. 종료되었습니다. 대화 엔드포인트는 더 이상 사용되지 않습니다.|||  
|**Transaction ID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|예|  
  
 다음 표에서는 이 이벤트 클래스에 대한 하위 클래스 값을 나열합니다.  
  
|ID|하위 클래스|Description|  
|--------|--------------|-----------------|  
|1|SEND Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **이 SEND 문을 실행할 때** SEND Message [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이벤트를 생성합니다.|  
|2|END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **이 WITH ERROR 절이 포함되지 않은 END CONVERSATION 문을 실행할 때** END CONVERSATION [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이벤트를 생성합니다.|  
|3|END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **이 WITH ERROR 절이 포함된 END CONVERSATION 문을 실행할 때** END CONVERSATION WITH ERROR [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이벤트를 생성합니다.|  
|4|Broker Initiated Error|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **가 오류 메시지를 만들 때마다** Broker Initiated Error [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 생성합니다. 예를 들어 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에서 대화에 대한 메시지를 성공적으로 라우팅하지 못하는 경우 Broker는 대화에 대해 오류 메시지를 만들고 이 이벤트를 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 애플리케이션이 오류로 인해 대화를 종료하는 경우 이 이벤트를 생성하지 않습니다.|  
|5|Terminate Dialog|[!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 대화를 종료했습니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 대화가 지속될 수 없는 조건에 따라 대화를 종료하지만 이러한 조건에는 오류 또는 정상적인 대화 종료가 포함되지 않습니다. 예를 들어 서비스를 삭제하면 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 해당 서비스에 대한 모든 대화를 종료합니다.|  
|6|Received Sequenced Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **에서 메시지 시퀀스 번호가 포함된 메시지를 수신할 때** Received Sequenced Message [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트 클래스를 생성합니다. 모든 사용자 정의 메시지 유형은 순차화된 메시지입니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 다음과 같은 두 경우에 순차화되지 않은 메시지를 생성합니다.<br /><br /> [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에 의해 생성된 오류 메시지가 순차화되지 않습니다.<br /><br /> 메시지 승인이 순차화되지 않을 수 있습니다. 효율성을 높이기 위해 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에는 가능한 경우 순차화된 메시지의 일부로 메시지 승인이 포함됩니다. 그러나 애플리케이션에서 특정 기간 내에 순차화된 메시지를 원격 엔드포인트에 보내지 않으면 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 가 메시지 승인에 대해 순차화되지 않은 메시지를 만듭니다.|  
|7|Received END CONVERSATION|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 대화 상대로부터 End Dialog 메시지를 수신할 때 Received END CONVERSATION 이벤트를 생성합니다.|  
|8|Received END CONVERSATION WITH ERROR|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **가 대화 상대로부터 사용자 정의 오류를 수신할 때** Received END CONVERSATION WITH ERROR [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이벤트를 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 Broker 정의 오류를 수신할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 이 이벤트를 생성하지 않습니다.|  
|9|Received Broker Error Message|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **가 대화 상대로부터 Broker 정의 오류 메시지를 수신할 때** Received Broker Error Message [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 에서 애플리케이션에 의해 생성된 오류 메시지를 수신할 때 이 이벤트를 생성하지 않습니다.<br /><br /> 예를 들어 현재 데이터베이스에 전진 데이터베이스에 대한 기본 경로가 포함된 경우 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 알 수 없는 서비스 이름이 포함된 메시지를 전진 데이터베이스에 라우팅합니다. 이 데이터베이스에서 메시지를 라우팅할 수 없으면 이 데이터베이스에 있는 Broker에서 오류 메시지를 만들고 이 오류 메시지를 현재 데이터베이스에 반환합니다. 현재 데이터베이스가 전진 데이터베이스에서 Broker 생성 오류를 수신하면 현재 데이터베이스가 **Received Broker Error Message** 이벤트를 생성합니다.|  
|10|Received END CONVERSATION Ack|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 대화 상대가 대화의 이 쪽에서 보낸 End Dialog 또는 Error 메시지를 승인할 때 **Received END CONVERSATION Ack** 이벤트 클래스를 생성합니다.|  
|11|BEGIN DIALOG|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 데이터베이스 엔진이 BEGIN DIALOG 명령을 실행할 때 **BEGIN DIALOG** 이벤트를 생성합니다.|  
|12|Dialog Created|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 대화의 엔드포인트를 만들 때 **에서는** Dialog Created [!INCLUDE[ssSB](../../includes/sssb-md.md)] 이벤트를 생성합니다. [!INCLUDE[ssSB](../../includes/sssb-md.md)] 는 새 대화가 구성될 때마다 현재 데이터베이스가 대화의 시작자 또는 대상인지에 관계없이 엔드포인트를 만듭니다.|  
|13|END CONVERSATION WITH CLEANUP|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 WITH CLEANUP 절이 포함된 END CONVERSATION 문을 실행할 때 END CONVERSATION WITH CLEANUP 이벤트를 생성합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
