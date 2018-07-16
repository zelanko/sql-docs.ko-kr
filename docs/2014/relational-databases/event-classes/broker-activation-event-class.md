---
title: Broker:Activation 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Activation event class
ms.assetid: 481d5b13-657e-4b51-8783-ccac3595bd45
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f95424242f62c946dc5d0787e54c8095e2f71a1f
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250203"
---
# <a name="brokeractivation-event-class"></a>Broker:Activation 이벤트 클래스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 큐 모니터가 활성화 저장 프로시저를 시작하고 QUEUE_ACTIVATION 알림을 보내거나 큐 모니터에서 시작한 활성화 저장 프로시저가 있는 경우에 **Broker:Activation** 이벤트를 생성합니다.  
  
## <a name="brokeractivation-event-class-data-columns"></a>Broker:Activation 이벤트 클래스 데이터 열  
  
|데이터 열|형식|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ClientProcessID**|`int`|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|`int`|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database*문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**EventClass**|`int`|캡처된 이벤트 클래스 유형입니다. **Broker:Activation** 의 경우 항상 **163**입니다.|27|아니요|  
|**EventSequence**|`int`|이 이벤트의 시퀀스 번호입니다.|51|아니요|  
|**EventSubClass**|`nvarchar`|이 이벤트가 보고하는 특정 동작입니다. 다음 값 중 하나입니다.<br /><br /> **시작**: <br />                [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 활성화 저장 프로시저를 시작했습니다.<br /><br /> **종료**: 활성화 저장 프로시저가 정상적으로 종료 되었습니다.<br /><br /> **중단**: 활성화 저장 프로시저가 오류로 인해 종료 되었습니다.|21|아니요|  
|**HostName**|`nvarchar`|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IntegerData**|`int`|이 큐에 활성화된 태스크의 개수입니다.|25|아니요|  
|**IsSystem**|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|아니요|  
|**LoginSid**|`image`|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|`nvarchar`|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|예|  
|**Exchange Spill**|`int`|이 이벤트와 연결된 큐입니다.|22|아니요|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|**SPID**|`int`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|예|  
|**StartTime**|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**TransactionID**|`bigint`|시스템이 할당한 트랜잭션 ID입니다.|4|아니요|  
  
  
