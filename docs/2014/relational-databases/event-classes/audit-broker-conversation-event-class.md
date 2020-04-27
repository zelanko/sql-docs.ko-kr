---
title: Audit Broker Conversation 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Broker Conversation event class
ms.assetid: d58e3577-e297-42e5-b8fe-206665a75d13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e92b8dacf3f1d4c9bf4992739acc7592f2135386
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912197"
---
# <a name="audit-broker-conversation-event-class"></a>Audit Broker Conversation 이벤트 클래스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 **Audit Broker Conversation** 이벤트를 만들어 Service Broker 대화 보안과 관련된 감사 메시지를 보고합니다.  
  
## <a name="audit-broker-conversation-event-class-data-columns"></a>Audit Broker Conversation 이벤트 클래스 데이터 열  
  
|데이터 열|Type|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**BigintData1**|**bigint**|메시지에 대한 메시지 시퀀스 번호입니다.|52|예|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|**DatabaseID**|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database* 문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**오류**|**int**|이 이벤트에서 오류를 보고하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 번호입니다.|31|예|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Audit Broker Conversation** 의 경우 항상 **158**입니다.|27|예|  
|**EventSubClass**|**int**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 다음 표에서는 이 이벤트에 대한 이벤트 하위 클래스 값을 나열합니다.|21|yes|  
|**FileName**|**nvarchar**|로그인 실패 이유입니다. 로그인이 성공한 경우 이 열이 비어 있습니다.|36|예|  
|**GUID**|**uniqueidentifier**|대화의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 **HOST_NAME** 함수를 사용합니다.|8|yes|  
|**IntegerData**|**int**|메시지의 조각 번호입니다.|25|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|yes|  
|**ObjectId**|**int**|대상 서비스의 사용자 ID입니다.|22|예|  
|**RoleName**|**nvarchar**|대화 핸들의 역할입니다. 이 역할은 **시작자** 또는 **대상**입니다.|38|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**Severity**|**int**|이 이벤트에서 오류를 보고하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 심각도입니다.|29|예|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**State**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 코드 내에서 이벤트가 생성된 위치를 나타냅니다. 이 이벤트가 생성될 수 있는 각 위치의 상태 코드는 서로 다릅니다. Microsoft 지원 엔지니어는 이 상태 코드를 사용하여 이벤트가 생성된 위치를 찾을 수 있습니다.|30|예|  
|**TextData**|**ntext**|오류에 대해 실패 원인을 설명하는 메시지가 들어 있습니다. 해당 값은<br /><br /> **인증서를 찾을 수 없습니다**. 대화 프로토콜 보안에 지정된 사용자에게 인증서가 없습니다.<br /><br /> **유효한 기간이 아닙니다**. 대화 프로토콜 보안에 지정된 사용자에게 인증서가 있지만 만료되었습니다.<br /><br /> **인증서가 메모리 할당에 비해 너무 큽니다**. 대화 프로토콜 보안에 지정된 사용자에게 인증서가 있지만 너무 큽니다. Service Broker에서 지원하는 최대 인증서 크기는 32,768바이트입니다.<br /><br /> **프라이빗 키를 찾을 수 없습니다**. 대화 프로토콜 보안에 지정된 사용자에게 인증서가 있지만 이 인증서와 관련된 프라이빗 키는 없습니다.<br /><br /> **인증서의 프라이빗 키 크기가 암호화 공급자와 호환되지 않습니다**. 인증서의 프라이빗 키 크기를 성공적으로 처리할 수 없습니다. 프라이빗 키 크기는 64바이트의 배수여야 합니다.<br /><br /> **인증서의 공개 키 크기가 암호화 공급자와 호환되지 않습니다**. 인증서의 공개 키 크기를 성공적으로 처리할 수 없습니다. 공개 키 크기는 64바이트의 배수여야 합니다.<br /><br /> **인증서의 프라이빗 키 크기가 암호화된 키 교환 키와 호환되지 않습니다**. 키 교환 키에 지정된 키 크기가 인증서의 프라이빗 키 크기와 일치하지 않습니다. 이는 일반적으로 원격 컴퓨터의 인증서가 데이터베이스의 인증서와 일치하지 않음을 나타냅니다.<br /><br /> **인증서의 공개 키 크기가 보안 헤더의 서명과 호환되지 않습니다**. 보안 헤더에 인증서의 공개 키로 유효성을 검사할 수 없는 서명이 들어 있습니다. 이는 일반적으로 원격 컴퓨터의 인증서가 데이터베이스의 인증서와 일치하지 않음을 나타냅니다.|1|yes|  
  
 다음 표에서는 이 이벤트 클래스에 대한 하위 클래스 값을 나열합니다.  
  
|ID|하위 클래스|Description|  
|--------|--------------|-----------------|  
|1|No Security Header|보안 대화가 진행되는 동안 Service Broker는 세션 키가 없는 메시지를 받습니다. 보안 대화가 설정되면 대화 프로토콜에서 대화의 모든 메시지에 세션 키가 포함되도록 요구합니다.|  
|2|No Certificate|Service Broker가 대화 참가자 중 한 명에 대해 사용 가능한 인증서를 찾을 수 없습니다. 대화를 안전하게 하려면 데이터베이스에 대화의 보낸 사람과 받는 사람에 대한 인증서가 모두 포함되어 있어야 합니다.|  
|3|Invalid Signature|Broker가 보낸 사람의 인증서에 있는 공개 키를 사용하여 보낸 사람이 제공하는 메시지 서명을 확인할 수 없습니다. 이러한 경우 메시지가 손상되거나, 변조되었거나, 원격 서비스와 로컬 서비스가 같은 사용자 인증서로 구성되지 않았거나, 인증서가 오래되었음을 나타낼 수 있습니다.|  
|4|Run As Target Failure|대상 사용자에게 대상 큐에 대한 수신 권한이 없습니다. 권한이 없는 사용자가 메시지를 받지 못하도록 하기 위해 Service Broker에서는 시작하는 사용자에게 메시지를 큐에 넣을 수 있는 권한이 있는지 여부에 관계없이 대상 사용자가 큐에서 받을 수 없는 메시지를 큐에 넣지 않습니다.|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
