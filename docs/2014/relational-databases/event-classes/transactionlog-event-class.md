---
title: TransactionLog 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
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
- TransactionLog event class
ms.assetid: bbcf09c6-3128-4775-b3de-e986a70411e0
caps.latest.revision: 33
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d894a3df24db130f041223168e5e12b040ebb0fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37236883"
---
# <a name="transactionlog-event-class"></a>TransactionLog 이벤트 클래스
  TransactionLog 이벤트 클래스를 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]인스턴스의 트랜잭션 로그에 있는 작업을 모니터링할 수 있습니다.  
  
## <a name="transactionlog-event-class-data-columns"></a>TransactionLog 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|BinaryData|`image`|추적에서 캡처된 이벤트 클래스에 의존하는 이진 값입니다.|2|예|  
|ClientProcessID|`int`|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|DatabaseID|`int`|데이터가 로깅되는 데이터베이스의 ID 입니다.|3|예|  
|DatabaseName|`nvarchar`|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|EventClass|`int`|이벤트 유형 = 54|27|아니요|  
|EventSequence|`int`|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|EventSubClass|`int`|이벤트 하위 클래스의 유형입니다.|21|예|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|예|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|IndexID|`int`|이벤트에 의해 영향 받는 개체의 인덱스 ID입니다. 개체의 인덱스 ID를 확인하려면 sys.indexes 카탈로그 뷰의 index_id 열을 사용합니다.|24|예|  
|IntegerData|`int`|추적에서 캡처된 이벤트 클래스에 의존하는 정수 값입니다.|25|예|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|LoginName|`nvarchar`|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|예|  
|LoginSid|`image`|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|예|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|예|  
|ObjectID|`int`|시스템이 할당한 개체의 ID입니다.|22|예|  
|RequestID|`int`|문을 포함하는 요청의 ID입니다.|49|예|  
|데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니요|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|예|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|TransactionID|`bigint`|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
  
## <a name="see-also"></a>관련 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)  
  
  
