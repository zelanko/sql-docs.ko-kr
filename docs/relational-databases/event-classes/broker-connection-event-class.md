---
title: "Broker:Connection 이벤트 클래스 | Microsoft 문서"
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
- Broker:Connection event class
ms.assetid: d3e505f2-0a43-486f-aa92-9c8e49b2dfea
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 539b14f0ac1f8ce3d720163b03100ea7325a2390
ms.lasthandoff: 04/11/2017

---
# <a name="brokerconnection-event-class"></a>Broker:Connection 이벤트 클래스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Service Broker에서 관리하는 전송 연결의 상태를 보고하기 위해 **Broker:Connection** 이벤트를 생성합니다.  
  
## <a name="brokerconnection-event-class-data-columns"></a>Broker:Connection 이벤트 클래스 데이터 열  
  
|데이터 열|유형|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database*문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. **DB_ID** 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**오류**|**int**|이벤트의 텍스트에 대한 **sys.messages** 의 메시지 ID 번호입니다. 이 이벤트에서 오류를 보고할 경우 이 열의 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 번호에 해당합니다.|31|아니요|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Broker:Connection** 의 경우 항상 **138**입니다.|27|아니요|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니요|  
|**EventSubClass**|**nvarchar**|이 연결의 연결 상태입니다. 이 이벤트의 경우 하위 클래스는 다음 값 중 하나입니다.<br /><br /> <br /><br /> **Connecting**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 전송 연결을 시작하는 중입니다.<br /><br /> **Connected**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 전송 연결을 설정했습니다.<br /><br /> **Connect Failed**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 전송 연결을 설정하지 못했습니다.<br /><br /> **Closing**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 전송 연결을 닫는 중입니다.<br /><br /> **Closed**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 전송 연결을 닫았습니다.<br /><br /> **Accept**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 다른 인스턴스의 전송 연결을 허용했습니다.<br /><br /> **Send IO Error**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 전송 오류가 발생했습니다.<br /><br /> **Receive IO Error**. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 전송 오류가 발생했습니다.|21|예|  
|**GUID**|**uniqueidentifier**|이 연결의 끝점 ID입니다.|54|아니요|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 **HOST_NAME** 함수를 사용합니다.|8|예|  
|**IntegerData**|**int**|이 연결을 닫은 횟수입니다.|25|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다.<br /><br /> 0 = 사용자<br /><br /> 1 = 시스템|60|아니요|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|**ObjectName**|**nvarchar**|대화 상자의 대화 핸들입니다.|34|아니요|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**TextData**|**ntext**|이벤트와 관련된 오류 메시지의 텍스트입니다. 오류를 보고하지 않는 이벤트의 경우 이 필드가 비어 있습니다. 오류 메시지는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 메시지나 Windows 오류 메시지입니다.|1|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|아니요|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
