---
title: Audit Object Derived Permission 이벤트 클래스 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Audit Object Derived Permission event class
ms.assetid: cf61b789-a326-47f9-9d0c-19470782328f
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 70b9eb74a54bfeda6f0bae8547d4631a9d5d141d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068384"
---
# <a name="audit-object-derived-permission-event-class"></a>Audit Object Derived Permission 이벤트 클래스
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  **Audit Object Derived Permission** 이벤트 클래스는 특정 개체에 대해 CREATE, ALTER 또는 DROP 명령이 실행된 경우 이를 기록합니다. 이 이벤트는 해당 개체에 직접 연결된 권한이나 소유자가 없는 경우에만 발생합니다.  
  
 이 이벤트 클래스는 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 수 있으므로 대신 **Audit Schema Object Management** 이벤트 클래스를 사용하는 것이 좋습니다.  
  
## <a name="audit-object-derived-permission-event-class-data-columns"></a>Audit Object Derived Permission 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|사용자 계정 컨트롤|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|사용자 계정 컨트롤|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|사용자 계정 컨트롤|  
|**DatabaseName**|**nvarchar**|사용자 문이 실행되는 데이터베이스의 이름입니다.|35|사용자 계정 컨트롤|  
|**DBUserName**|**nvarchar**|데이터베이스의 발급자 사용자 이름입니다.|40|사용자 계정 컨트롤|  
|**EventClass**|**int**|이벤트 유형 = 118|27|아니오|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니오|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1=만들기<br /><br /> 2=변경<br /><br /> 3=삭제<br /><br /> 4=덤프<br /><br /> 11=로드|21|사용자 계정 컨트롤|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|사용자 계정 컨트롤|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|사용자 계정 컨트롤|  
|**LineNumber**|**int**|오류를 포함하는 줄 번호를 표시합니다.|5|사용자 계정 컨트롤|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|사용자 계정 컨트롤|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|사용자 계정 컨트롤|  
|**NestLevel**|**int**|@@NESTLEVEL에서 반환한 데이터를 나타내는 정수입니다.|29|사용자 계정 컨트롤|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|사용자 계정 컨트롤|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|사용자 계정 컨트롤|  
|**ObjectName**|**nvarchar**|생성, 변경 또는 삭제할 개체의 이름입니다.|34|사용자 계정 컨트롤|  
|**ObjectType**|**int**|이벤트와 관련된 개체 유형을 나타내는 값입니다. 이 값은 **sys.objects** 카탈로그 뷰의 유형 열과 일치합니다. 값은 [ObjectType 추적 이벤트 열](../../relational-databases/event-classes/objecttype-trace-event-column.md)을 참조하세요.|28|사용자 계정 컨트롤|  
|**OwnerName**|**nvarchar**|생성, 변경 또는 삭제할 개체의 소유자에 대한 데이터베이스 사용자 이름입니다.|37|사용자 계정 컨트롤|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|사용자 계정 컨트롤|  
|**데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26|아니오|  
|**SessionLoginName**|**nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|사용자 계정 컨트롤|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|사용자 계정 컨트롤|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|사용자 계정 컨트롤|  
|**성공**|**int**|1 = 성공, 0 = 실패. 예를 들어 값 1은 사용 권한 확인이 성공했음을 나타내고, 값 0은 확인이 실패했음을 나타냅니다.|23|사용자 계정 컨트롤|  
|**TextData**|**ntext**|문의 SQL 텍스트|@shouldalert|사용자 계정 컨트롤|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|사용자 계정 컨트롤|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|사용자 계정 컨트롤|  
  
## <a name="see-also"></a>참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [Audit Schema Object Management 이벤트 클래스](../../relational-databases/event-classes/audit-schema-object-management-event-class.md)  
  
  
