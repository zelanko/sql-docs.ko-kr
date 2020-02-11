---
title: Audit Database Object Management 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- Audit Database Object Management event class
ms.assetid: bc5c0be2-990b-4032-a5e6-41ce98661698
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 19cb23baa6df69de9a73595dd81f8c1a095d7224
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62698997"
---
# <a name="audit-database-object-management-event-class"></a>Audit Database Object Management 이벤트 클래스
  **Audit Database Object Management** 이벤트 클래스는 스키마와 같은 데이터베이스 개체에 대해 CREATE, ALTER 또는 DROP 문이 실행 될 때 발생 합니다.  
  
> [!NOTE]  
>  공개 키와 관련된 동작은 감사되지 않습니다.  
  
## <a name="audit-database-object-management-event-class-data-columns"></a>Audit Database Object Management 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|Description|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 애플리케이션의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 애플리케이션에서 전달한 값으로 채워집니다.|10|yes|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]**ServerName** 데이터 열이 추적에서 캡처되고 서버를 사용할 수 있는 경우 데이터베이스의 이름을 표시 합니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|yes|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|yes|  
|**DBUserName**|**nvarchar**|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 이름입니다.|40|yes|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|예|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1=만들기<br /><br /> 2=변경<br /><br /> 3=삭제<br /><br /> 4=덤프<br /><br /> 10=열기<br /><br /> 11=로드<br /><br /> 12=액세스|21|yes|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공할 경우 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|yes|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|yes|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|yes|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **server_principals** 카탈로그 뷰에서 찾을 수 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|yes|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|yes|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|yes|  
|**ObjectName**|**nvarchar**|참조되는 개체의 이름입니다.|34|yes|  
|**ObjectType**|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 **sys. objects** 카탈로그 뷰의 type 열에 해당 합니다. 값은 [ObjectType 추적 이벤트 열](objecttype-trace-event-column.md)을 참조하세요.|28|yes|  
|**OwnerName**|**nvarchar**|개체 소유자의 데이터베이스 사용자 이름입니다.|37|yes|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|yes|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|예|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1를 사용 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 여에 연결 하 고 문을 Login2로 실행 하는 경우 **Sessionloginname** 은 Login1 및 **LoginName** 에 Login2를 표시 합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|yes|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|yes|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|yes|  
|**Success**|**int**|1 = 성공, 0 = 실패. 예를 들어 값 1은 사용 권한 확인이 성공했음을 나타내고, 값 0은 확인이 실패했음을 나타냅니다.|23|yes|  
|**TextData**|**ntext**|추적에서 캡처된 이벤트 클래스에 따라 달라지는 텍스트 값입니다.|1|yes|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|yes|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|yes|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql)  
  
  
