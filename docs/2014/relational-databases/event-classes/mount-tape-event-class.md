---
title: Mount Tape 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Mount Tape event class
ms.assetid: 4c595e0a-d968-47d3-a84f-9b6857342671
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 513792c12833a14b8d1d3fc78f4b3bb6be173627
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63023455"
---
# <a name="mount-tape-event-class"></a>Mount Tape 이벤트 클래스
  Mount Tape 이벤트 클래스는 테이프 탑재 요청을 받을 때 발생합니다. 이 이벤트 클래스를 사용하여 테이프 탑재 요청 및 요청의 성공 또는 실패를 모니터링할 수 있습니다.  
  
## <a name="mount-tape-event-class-data-columns"></a>Mount Tape 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|`nvarchar`|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|ClientProcessID|`int`|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|DatabaseID|`int`|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있는 경우 데이터베이스의 이름을 표시 합니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|`nvarchar`|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|Duration|`bigint`|이벤트에 의해 사용된 시간(마이크로초)입니다.|13|yes|  
|EndTime|`datetime`|Mount Request 이벤트의 경우 제한 시간이 발생하면 탑재 제한 시간의 시간이 되고 제한 시간이 발생하지 않으면 이벤트 자체의 시간이 됩니다. 이 경우 StartTime은 해당되는 탑재 요청의 시간을 나타냅니다.|15|yes|  
|EventClass|`int`|이벤트 유형 = 195|27|예|  
|EventSequence|`int`|요청 내의 지정된 이벤트 시퀀스입니다.|51|예|  
|EventSubClass|`int`|이벤트 하위 클래스의 유형입니다.<br /><br /> 1 = 테이프 탑재 요청<br /><br /> 2 = 테이프 탑재 완료<br /><br /> 3 = 테이프 탑재 취소|21|yes|  
|GroupID|`int`|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|HostName|`nvarchar`|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|IsSystem|`int`|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|LoginName|`nvarchar`|사용자 로그인 이름 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[msCoName](../../includes/msconame-md.md)] 도메인\\*사용자 이름*형식의 Windows 로그인 자격 증명 또는 보안 로그인)입니다.|11|yes|  
|NTDomainName|`nvarchar`|사용자가 속한 Windows 도메인입니다.|7|yes|  
|NTUserName|`nvarchar`|Windows 사용자 이름입니다.|6|yes|  
|ServerName|`nvarchar`|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|`nvarchar`|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|SPID|`int`|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|`datetime`|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TextData|`ntext`|*물리적 장치 이름* [( *논리적 장치 이름* )]. 논리적 디바이스 이름은 sys.backup_devices 카탈로그 뷰에 정의되어 있는 경우에만 표시됩니다.|1|yes|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)   
 [SQL Server 데이터베이스 백업 및 복원](../backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
  
