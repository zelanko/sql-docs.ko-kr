---
description: Broker:Forwarded Message Sent 이벤트 클래스
title: Broker:Forwarded Message Sent 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Forwarded Message Sent event class
ms.assetid: d0ef74d9-a4ef-4918-aa21-6b267e85569f
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb738df03a1e4ea5e9472a6bf0ff2646756d500d
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97476234"
---
# <a name="brokerforwarded-message-sent-event-class"></a>Broker:Forwarded Message Sent 이벤트 클래스

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Service Broker가 메시지를 전달할 때 Broker:Forwarded Message Sent 이벤트를 생성합니다.  
  
## <a name="brokerforwarded-message-sent-event-class-data-columns"></a>Broker:Forwarded Message Sent 이벤트 클래스 데이터 열  
  
|데이터 열|Type|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|BigintData1|**bigint**|메시지 시퀀스 번호입니다.|52|아니요|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database* 문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|DBUserName|**nvarchar**|메시지를 보낸 서비스의 Broker 인스턴스 ID입니다.|40|예|  
|EventClass|**int**|캡처된 이벤트 클래스 유형입니다. Broker:Forwarded Message Sent의 경우 항상 139입니다.|27|예|  
|EventSequence|**int**|이 이벤트의 시퀀스 번호입니다.|51|예|  
|FileName|**nvarchar**|메시지가 전송되는 서비스의 이름입니다.|36|예|  
|GUID|**uniqueidentifier**|대화의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|예|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IndexID|**int**|전달된 메시지에 대해 남아 있는 홉 수입니다.|24|예|  
|IntegerData|**int**|전달된 메시지의 조각 번호입니다.|25|예|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|ObjectId|**int**|메시지가 전달될 때 전달되는 메시지에 대한 시간 제한 값입니다.|22|예|  
|ObjectName|**nvarchar**|전달된 메시지의 메시지 ID입니다.|34|예|  
|OwnerName|**nvarchar**|메시지가 전송되는 Broker 식별자입니다.|37|예|  
|RoleName|**nvarchar**|대화 핸들의 역할입니다. 유효한 값은 다음과 같습니다.<br /><br /> 시작자 대화를 시작한 Broker입니다.<br /><br /> 대상 대화의 대상이 되는 Broker입니다.|38|예|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SPID|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|Success|**int**|전달 프로세스 동안 사용된 시간입니다.|23|예|  
|TargetLoginName|**nvarchar**|이 인스턴스가 메시지를 보내는 네트워크 주소입니다. 이 주소는 해당 메시지의 최종 대상과 다를 수도 있습니다.|42|예|  
|TargetUserName|**nvarchar**|메시지에 대한 시작 서비스의 이름입니다.|39|예|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|예|  
  
  
