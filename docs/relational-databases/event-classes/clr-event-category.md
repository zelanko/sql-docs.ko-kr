---
title: CLR 이벤트 범주 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- event classes [SQL Server], CLR event category
- SQL Server event classes, CLR event category
- CLR event category [SQL Server]
ms.assetid: a7c0cd60-3bec-42be-ad5e-473bd26a06d9
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 978067f0d035fcd781d275bf77177e2b95383fdb
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85762989"
---
# <a name="clr-event-category"></a>CLR 이벤트 범주
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **CLR** 이벤트 범주에는 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 내의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR(공용 언어 런타임) 개체를 실행하여 만들어지는 이벤트 클래스가 포함됩니다.  
 
 ## <a name="assembly-load-event-class"></a>Assembly Load 이벤트 클래스 
  **Assembly Load** 이벤트 클래스는 어셈블리 로드 요청을 실행할 때 발생합니다.  
  
 어셈블리 로드를 모니터링하려는 추적에 **Assembly Load** 이벤트 클래스를 포함시키십시오. 이 이벤트는 CLR 쿼리를 실행하는 서버가 느리게 동작할 때의 문제 해결 또는 사용자, 데이터베이스, 성공 여부 또는 다른 어셈블리 로드 관련 정보를 수집하기 위한 서버 모니터링과 같이 CLR(공용 언어 런타임)을 사용하는 쿼리의 문제를 해결하려는 경우에 유용합니다.  
  
## <a name="assembly-load-event-class-data-columns"></a>Assembly Load 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|로드를 요청한 애플리케이션의 이름입니다.|10|yes|  
|**ClientProcessID**|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|**DatabaseID**|**int**|USE database 문으로 지정한 데이터베이스 ID이거나 지정한 인스턴스에 대해 USE database 문을 실행하지 않은 경우 기본 데이터베이스의 ID입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**GroupID**|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|**LoginName**|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|yes|  
|**LoginSID**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|**Exchange Spill**|**int**|어셈블리 ID입니다.|22|yes|  
|**ObjectName**|**nvarchar**|정규화된 어셈블리의 이름입니다.|34|yes|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**Success**|**int**|어셈블리 로드의 성공(1) 또는 실패(0) 여부를 나타냅니다.|23|yes|  
|**TextData**|**ntext**|로드가 성공한 경우 "Assembly Load Succeeded" 그렇지 않으면 "Assembly Load Failed"입니다.|1|yes|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [어셈블리&#40;데이터베이스 엔진&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)  
  
   
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)  
  
  
