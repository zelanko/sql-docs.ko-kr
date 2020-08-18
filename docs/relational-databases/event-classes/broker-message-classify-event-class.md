---
description: Broker:Message Classify 이벤트 클래스
title: Broker:Message Classify 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Message Classify event class
ms.assetid: e51f3351-1239-4c41-b87c-1dd86968e027
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e5e8e0bc84e26798716ba1635580b81dbfc08c8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88331079"
---
# <a name="brokermessage-classify-event-class"></a>Broker:Message Classify 이벤트 클래스

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Service Broker가 메시지 라우팅을 확인하면 **Broker:Message Classify** 이벤트를 생성합니다.  
  
## <a name="brokermessage-classify-event-class-data-columns"></a>Broker:Message Classify 이벤트 클래스 데이터 열  
  
|데이터 열|데이터 형식|Description|열 번호|필터 가능|  
|-----------------|---------------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database* 문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Broker:Message Classify** 의 경우 항상 **141**입니다.|27|예|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|예|  
|**EventSubClass**|**nvarchar**|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **Local**: 선택한 경로에 주소 LOCAL이 있습니다.<br /><br /> **Remote**:                 선택한 경로에 LOCAL 이외의 주소가 있습니다.<br /><br /> **Delayed**:                 전달이 비활성화되거나 일치하는 경로가 없기 때문에 메시지가 지연됩니다.|21|예|  
|**FileName**|**nvarchar**|메시지가 전송되는 서비스 이름입니다.|36|예|  
|**GUID**|**uniqueidentifier**|대화의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|**OwnerName**|**nvarchar**|메시지가 전송되는 Broker 식별자입니다.|37|예|  
|**RoleName**|**nvarchar**|메시지를 네트워크에서 받았는지 아니면 메시지가 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 시작된 것인지를 나타냅니다.|38|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|**Start Time**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**TargetUserName**|**nvarchar**|다음 홉 Broker의 네트워크 주소입니다.|39|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|예|  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
