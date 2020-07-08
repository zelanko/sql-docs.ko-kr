---
title: Audit Database Object Take Ownership 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- Audit Database Object Take Ownership event class
ms.assetid: 26409a60-9616-484b-b608-ca554aef08f6
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7cf4415847421122fd1aa28f4b70c63493924050
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85635629"
---
# <a name="audit-database-object-take-ownership-event-class"></a>Audit Database Object Take Ownership 이벤트 클래스
[!INCLUDE [SQL Server - ASDB](../../includes/applies-to-version/sql-asdb.md)]
  **Audit Database Object Take Ownership** 이벤트 클래스는 데이터베이스 범위에 있는 개체 소유자가 변경될 때 발생합니다.  
  
## <a name="audit-database-object-take-ownership-event-class-data-columns"></a>Audit Database Object Take Ownership 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|**DBUserName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 이름입니다.|40|yes|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|yes|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|**ObjectName**|**nvarchar**|참조되는 개체의 이름입니다.|34|yes|  
|**ObjectType**|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 열에 대해 반환되는 값은 **sys.objects** 카탈로그 뷰에 있는 **type** 열의 해당 값과 [ObjectType 추적 이벤트 열](../../relational-databases/event-classes/objecttype-trace-event-column.md)에 나열된 값의 조합입니다. 예를 들어 8277-U가 반환되면 개체 유형은 사용자 정의 테이블입니다.|28|yes|  
|**OwnerName**|**nvarchar**|개체 소유자의 데이터베이스 사용자 이름입니다.|37|yes|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SessionLoginName**|**Nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**Success**|**int**|1 = 성공, 0 = 실패. 예를 들어 값 1은 사용 권한 확인이 성공했음을 의미하고, 0은 확인이 실패했음을 의미합니다.|23|yes|  
|**TargetUserName**|**nvarchar**|데이터베이스 사용자를 대상으로 하는 동작(예: 사용자에게 사용 권한 부여)의 경우 해당 사용자의 이름입니다.|39|yes|  
|**TextData**|**ntext**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 텍스트 값입니다.|1|yes|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|yes|  
  
## <a name="see-also"></a>참고 항목  
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
