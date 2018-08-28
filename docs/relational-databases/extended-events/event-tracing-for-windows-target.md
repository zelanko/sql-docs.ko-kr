---
title: Windows용 이벤트 추적 대상 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- event tracing for windows target
- ETW target
- targets [SQL Server extended events], event tracing for windows target
ms.assetid: ca2bb295-b7f6-49c3-91ed-0ad4c39f89d5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ab23edff3e7c2b84dd417123dbb668ea47142900
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43072610"
---
# <a name="event-tracing-for-windows-target"></a>Windows용 이벤트 추적 대상
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  ETW(Windows용 이벤트 추적)를 대상으로 사용하려면 먼저 ETW에 대한 실무 지식을 갖추고 있는 것이 좋습니다. ETW 추적은 확장 이벤트와 함께 사용되거나 확장 이벤트의 이벤트 소비자로 사용됩니다. 다음 외부 링크를 클릭하면 ETW에 대한 배경 지식을 제공하는 항목으로 연결됩니다.  
  
-   [Windows 이벤트](http://go.microsoft.com/fwlink/?LinkId=92380)  
  
-   [ETW를 사용한 디버깅 및 성능 조정 개선](http://go.microsoft.com/fwlink/?LinkId=92381)  
  
 ETW 대상을 여러 세션에 추가할 수 있지만 이는 단일 대상입니다. 한 이벤트가 여러 세션에서 발생하는 경우 해당 이벤트는 발생 항목당 한 번만 ETW 대상으로 전파됩니다. 확장 이벤트 엔진은 프로세스당 하나의 인스턴스로 제한됩니다.  
  
> [!IMPORTANT]  
>  ETW 대상이 작동하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스 시작 계정이 Performance Log Users 그룹의 멤버여야 합니다.  
  
 ETW 세션에 있는 이벤트의 구성은 확장 이벤트 엔진을 호스팅하는 프로세스에서 제어합니다. 엔진은 발생할 이벤트 및 이벤트 실행을 위해 충족해야 할 조건을 제어합니다.  
  
 ETW 대상이 프로세스의 수명이 유지되는 동안 처음으로 확장 이벤트 세션에 연결하여 바인딩되면 ETW 대상은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자에서 단일 ETW 세션을 엽니다. ETW 세션이 이미 있으면 ETW 대상은 기존 세션에 대한 참조를 얻습니다. 이러한 ETW 세션은 지정된 컴퓨터의 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 전체에서 공유할 수 있습니다. 또한 이 ETW 세션은 ETW 대상이 있는 세션의 모든 이벤트를 수신합니다.  
  
 ETW 대상이 이벤트를 소비하고 이를 ETW로 전송하려면 공급자가 필요하므로 세션에는 모든 확장 이벤트 패키지가 활성화됩니다. 이벤트가 발생하면 ETW 대상은 이벤트에 대한 공급자가 활성화되어 있는 세션에 이벤트를 전송합니다.  
  
 ETW 대상은 이벤트를 발생시키는 스레드에서의 이벤트 동기 게시를 지원합니다. 하지만 ETW 대상은 비동기 이벤트 게시를 지원하지 않습니다.  
  
 ETW 대상은 Logman.exe와 같은 외부 ETW 컨트롤러를 제어하지 않습니다. ETW 추적을 생성하려면 ETW 대상으로 이벤트 세션을 만들어야 합니다. 자세한 내용은 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)을 참조하세요.  
  
> [!NOTE]  
>  ETW 대상을 활성화하면 이름이 XE_DEFAULT_ETW_SESSION인 ETW 세션이 생성됩니다. XE_DEFAULT_ETW_SESSION이라는 세션이 이미 있는 경우에는 기존 세션이 속성 수정 없이 그대로 사용됩니다. XE_DEFAULT_ETW_SESSION은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 모든 인스턴스 간에 공유됩니다. XE_DEFAULT_ETW_SESSION을 시작한 후에는 ETW 컨트롤러(예: Logman 도구)를 사용하여 중지해야 합니다. 예를 들어 명령 프롬프트에서 **logman stop XE_DEFAULT_ETW_SESSION -ets**명령을 실행할 수 있습니다.  
  
 다음 표에서는 ETW 대상을 구성하는 데 사용할 수 있는 옵션에 대해 설명합니다.  
  
|옵션|허용된 값|설명|  
|------------|--------------------|-----------------|  
|default_xe_session_name|최대 256자까지의 모든 문자열. 이 값은 선택 사항입니다.|확장 이벤트 세션 이름입니다. 기본적으로 이 이름은 XE_DEFAULT_ETW_SESSION입니다.|  
|default_etw_session_logfile_path|최대 256자까지의 모든 문자열. 이 값은 선택 사항입니다.|확장 이벤트 세션의 로그 파일에 대한 경로입니다. 기본적으로 이 경로는 %TEMP%\ XEEtw.etl입니다.|  
|default_etw_session_logfile_size_mb|부호 없는 정수 이 값은 선택 사항입니다. |확장 이벤트 세션의 로그 파일 크기(MB)입니다. 기본값은 20MB입니다.|  
|default_etw_session_buffer_size_kb|부호 없는 정수 이 값은 선택 사항입니다.|확장 이벤트 세션의 메모리 내 버퍼 크기(KB)입니다. 기본값은 128KB입니다.|  
|retries|부호 없는 정수|이벤트가 삭제되기 전에 ETW 하위 시스템에 이벤트 게시를 재시도한 횟수입니다. 기본값은 0입니다.|  
  
 이러한 설정의 구성은 선택 사항입니다. ETW 대상은 이러한 설정에 대해 기본값을 사용합니다.  
  
 ETW 대상의 역할은 다음과 같습니다.  
  
-   기본 ETW 세션을 생성합니다.  
  
-   ETW로 모든 확장 이벤트 패키지를 등록합니다. 이렇게 하면 이벤트가 ETW에 의해 삭제되지 않습니다.  
  
-   ETW로의 이벤트 흐름을 관리합니다. ETW 대상은 확장 이벤트 데이터를 사용하여 ETW 이벤트를 만들고 적절한 ETW 세션에 전송합니다. 이벤트가 버퍼 크기보다 크거나 데이터가 ETW 이벤트에 맞지 않는 경우 ETW는 이벤트를 조각으로 분할합니다.  
  
-   확장 이벤트 패키지를 항상 활성화된 상태로 유지합니다.  
  
 ETW에서 사용하는 기본 파일 위치는 다음과 같습니다.  
  
-   ETW 출력 파일은 %TEMP%\XEEtw.etl에 저장됩니다.  
  
    > [!IMPORTANT]  
    >  첫 번째 세션이 시작되면 파일 경로를 변경할 수 없습니다.  
  
-   MOF(Managed Object Format) 파일은 *\<설치 경로*\Microsoft SQL Server\Shared에 있습니다. 자세한 내용은 MSDN의 [Managed Object Format](http://go.microsoft.com/fwlink/?LinkId=92851) 을 참조하십시오.  
  
## <a name="adding-the-target-to-a-session"></a>세션에 대상 추가  
 확장 이벤트 세션에 ETW 대상을 추가하려면 이벤트 세션을 만들거나 변경할 때 다음 문을 포함해야 합니다.  
  
```  
ADD TARGET package0.etw_classic_sync_target  
```  
  
 데이터를 보는 방법을 비롯한 ETW 대상을 사용하는 방법을 보여 주는 전체 예에 대한 자세한 내용은 [확장 이벤트를 사용하여 시스템 작업 모니터링](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 확장 이벤트 대상](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)   
 [sys.dm_xe_session_targets&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql.md)   
 [CREATE EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/create-event-session-transact-sql.md)   
 [ALTER EVENT SESSION&#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)  
  
  
