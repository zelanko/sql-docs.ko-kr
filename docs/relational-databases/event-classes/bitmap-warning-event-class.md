---
description: Bitmap Warning 이벤트 클래스
title: Bitmap Warning 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Bitmap Warning event class
ms.assetid: 5bf9b4e3-0eba-4e67-8ba9-30ca4b48e1d4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4e53b9636295185b95281aacdfc417e597f86a00
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97474034"
---
# <a name="bitmap-warning-event-class"></a>Bitmap Warning 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Bitmap Warning** 이벤트 클래스를 사용하여 쿼리 내의 비트맵 필터 사용을 모니터링할 수 있습니다. 또한 이벤트 하위 클래스를 사용하여 쿼리 내에서 비트맵 필터가 해제되면 보고되도록 할 수 있습니다.  
  
## <a name="bitmap-warning-event-class-data-columns"></a>Bitmap Warning 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나 지정된 인스턴스에 대해 USE *database* 문이 실행되지 않은 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|예|  
|**EventClass**|**int**|이벤트 유형 = 212|27|예|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다. 0 = 비트맵 필터가 해제되었습니다.|21|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름이며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] DOMAIN\username *형식의 Windows 로그인 자격 증명 또는* 보안 로그인입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**Exchange Spill**|**int**|재분할에 관련된 해시 팀의 루트 노드 ID입니다. 실행 계획의 노드 ID와 일치합니다.|22|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
  
