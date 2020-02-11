---
title: Broker:Conversation Group 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Broker:Conversation Group event class
ms.assetid: 6595bef6-9d40-42eb-a934-735622dd23fb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 23e39e48b8c4c20ab0e847d87b7193179e8d74ab
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62664236"
---
# <a name="brokerconversation-group-event-class"></a>Broker:Conversation Group 이벤트 클래스
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Service Broker에서 새 대화 그룹을 만들거나 기존 대화 그룹을 삭제할 때 **Broker:Conversation Group** 이벤트를 생성합니다.  
  
## <a name="brokerconversation-group-event-class-data-columns"></a>Broker:Conversation Group 이벤트 클래스 데이터 열  
  
|데이터 열|Type|Description|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**ClientProcessID**|`int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|**DatabaseID**|`int`|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database* 문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**ServerName** 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있는 경우 데이터베이스의 이름을 표시 합니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**EventClass**|`int`|캡처된 이벤트 클래스 유형입니다. 
  **Broker:Conversation Group** 의 경우 항상 **136**입니다.|27|예|  
|**EventSequence**|`int`|이 이벤트의 시퀀스 번호입니다.|51|예|  
|**EventSubClass**|`nvarchar`|각 이벤트 클래스에 대한 자세한 정보를 제공하는 이벤트 하위 클래스 유형입니다. 이 열에는 다음 값이 포함될 수 있습니다.<br /><br /> **만들기**. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 새 대화 그룹을 만들었습니다.<br /><br /> **Drop**. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 대화 그룹을 삭제했습니다.|21|yes|  
|**EID**|`uniqueidentifier`|이 이벤트가 기술하는 대화 그룹의 대화 그룹 식별자입니다.|54|예|  
|**N**|`nvarchar`|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|**IsSystem**|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginSid**|`image`|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**NTDomainName**|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|`nvarchar`|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|yes|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SPID**|`int`|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|yes|  
|**StartTime**|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**TransactionID**|`bigint`|시스템이 할당한 트랜잭션 ID입니다.|4|예|  
  
  
