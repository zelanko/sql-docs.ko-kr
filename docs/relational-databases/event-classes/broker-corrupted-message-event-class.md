---
title: Broker:Corrupted Message 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Broker:Corrupted Message event class
ms.assetid: 084bf198-2138-438e-bdc7-4ff1e04300f7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0ef3eaafc0d9eb5953db7d26c594020466c1e488
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745991"
---
# <a name="brokercorrupted-message-event-class"></a>Broker:Corrupted Message 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 Service Broker가 손상된 메시지를 수신할 때 **Broker:Corrupted Message** 이벤트를 발생시킵니다.  
  
## <a name="brokercorrupted-message-event-class-data-columns"></a>Broker:Corrupted Message 이벤트 클래스 데이터 열  
  
|데이터 열|형식|설명|열 번호|필터 가능|  
|-----------------|----------|-----------------|-------------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|**BigintData1**|**bigint**|이 메시지의 시퀀스 번호입니다.|52|아니오|  
|**BinaryData**|**image**|메시지의 메시지 본문입니다.|2|사용자 계정 컨트롤|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|**DatabaseID**|**int**|USE *database* 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 실행된 USE *database* 문이 없는 경우 기본 데이터베이스 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|**오류**|**int**|이벤트의 텍스트에 대한 **sys.messages** 의 메시지 ID 번호입니다.|31|아니오|  
|**EventClass**|**int**|캡처된 이벤트 클래스 유형입니다. **Broker:Corrupted Message** 의 경우 항상 **161**입니다.|27|아니오|  
|**EventSequence**|**int**|이 이벤트의 시퀀스 번호입니다.|51|아니오|  
|**FileName**|**nvarchar**|원격 엔드포인트의 네트워크 주소입니다.|36|아니오|  
|**GUID**|**uniqueidentifier**|손상된 메시지가 속하는 대화의 대화 ID입니다. 이 식별자는 메시지의 일부로 전송되며 양쪽 대화 상대 간에 공유합니다.|54|아니오|  
|**Host Name**|**nvarchar**|클라이언트를 실행 중인 컴퓨터의 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|**IntegerData**|**int**|이 메시지의 조각 번호입니다.|25|사용자 계정 컨트롤|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|아니오|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|**NTUserName**|**nvarchar**|이 이벤트를 생성한 연결을 소유하고 있는 사용자의 이름입니다.|6|사용자 계정 컨트롤|  
|**ObjectName**|**nvarchar**|원격 데이터베이스에서 이 데이터베이스에 연결하기 위해 사용된 연결 문자열 및 대화의 다른 한 쪽의 서비스 이름입니다.|34|아니오|  
|**RoleName**|**nvarchar**|이 메시지를 수신하는 엔드포인트의 역할입니다. 다음 값 중 하나일 수 있습니다.<br /><br /> **시작자**: 수신 엔드포인트가 대화의 시작자입니다.<br /><br /> **대상**: 수신 엔드포인트가 대화의 대상입니다.|38|아니오|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|**Severity**|**int**|오류로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 메시지를 삭제한 경우 오류의 심각도입니다.|29|아니오|  
|**SPID**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 클라이언트와 관련된 프로세스에 할당한 서버 프로세스 ID입니다.|12|사용자 계정 컨트롤|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|**State**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 코드 내에서 이벤트가 생성된 위치를 나타냅니다. 이 이벤트가 생성될 수 있는 각 위치의 상태 코드는 서로 다릅니다. Microsoft 지원 엔지니어는 이 상태 코드를 사용하여 이벤트가 생성된 위치를 찾을 수 있습니다.|30|아니오|  
|**TextData**|**ntext**|발견된 손상에 대한 설명입니다.|1|사용자 계정 컨트롤|  
|**Transaction ID**|**bigint**|시스템이 할당한 트랜잭션 ID입니다.|4|아니오|  
  
 이 이벤트의 **TextData** 열에는 메시지의 문제를 기술하는 메시지가 포함됩니다.  
  
  
