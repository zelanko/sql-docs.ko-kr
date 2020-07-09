---
title: Object:Altered 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Object:Altered event class
ms.assetid: f94e3b59-ff2f-4d8d-8479-e85ce5b3483e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9757556741c36f5644d3d58a44744270a02b9c82
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85756012"
---
# <a name="objectaltered-event-class"></a>Object:Altered 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  Object:Altered 이벤트 클래스는 ALTER INDEX, ALTER TABLE 또는 ALTER DATABASE 문 등에 의해 개체가 변경되었음을 나타냅니다. 이 이벤트 클래스는 개체가 변경되었는지 확인하는 데 사용할 수 있습니다. 예를 들어 임시 저장 프로시저를 자주 만드는 ODBC 애플리케이션의 경우 개체가 자주 변경될 수 있으므로 이 이벤트 클래스를 사용하면 유용합니다.  
  
 Object:Altered 이벤트 클래스는 항상 두 이벤트로 발생합니다. 첫 번째 이벤트는 시작 단계를 나타내며 두 번째 이벤트는 롤백 또는 커밋 단계를 나타냅니다.  
  
 LoginName 및 NTUserName 데이터 열을 모니터링하여 개체를 생성, 삭제 또는 변경하는 사용자의 이름을 확인할 수 있습니다.  
  
## <a name="objectaltered-event-class-data-columns"></a>Object:Altered 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|ApplicationName|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|ClientProcessID|**int**|클라이언트 애플리케이션이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|yes|  
|DatabaseID|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 에 ServerName 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|DatabaseName|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|EventClass|**int**|이벤트 유형 = 164|27|예|  
|EventSequence|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|EventSubClass|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 0=시작<br /><br /> 1=커밋<br /><br /> 2=롤백|21|yes|  
|GroupID|**int**|SQL 추적 이벤트가 발생한 작업 그룹의 ID입니다.|66|yes|  
|HostName|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|IndexID|**int**|이벤트에 의해 영향 받는 개체의 인덱스 ID입니다. 개체의 인덱스 ID를 확인하려면 sys.indexes 카탈로그 뷰의 index_id 열을 사용합니다.|24|yes|  
|IntegerData|**int**|해당 시작 이벤트의 이벤트 시퀀스 번호입니다. 이 열은 커밋 또는 롤백 유형의 이벤트 하위 클래스에서만 사용할 수 있습니다.|25|yes|  
|IsSystem|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, NULL = 사용자|60|yes|  
|LoginName|**nvarchar**|사용자 로그인 이름이며 DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인입니다.|11|yes|  
|LoginSid|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 sys.server_principals 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|NTDomainName|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|NTUserName|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|ObjectID|**int**|시스템이 할당한 개체의 ID입니다.|22|yes|  
|ObjectID2|**bigint**|파티션 스키마가 변경될 때는 파티션 함수 ID, 서비스가 변경될 때는 큐 ID, XML 스키마가 변경될 때는 컬렉션 스키마 ID입니다.|56|yes|  
|ObjectName|**nvarchar**|참조되는 개체의 이름입니다.|34|yes|  
|ObjectType|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 sys.objects 카탈로그 뷰의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](../../relational-databases/event-classes/objecttype-trace-event-column.md)을 참조하세요.|28|yes|  
|RequestID|**int**|문을 포함하는 일괄 처리 요청의 ID입니다.|49|yes|  
|ServerName|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|SessionLoginName|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 SessionLoginName은 Login1을 표시하고 LoginName은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|SPID|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|StartTime|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|TransactionID|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|XactSequence|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|yes|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
