---
title: "Audit Add DB User 이벤트 클래스 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Audit Add DB User 이벤트 클래스"
ms.assetid: ac9ed573-c84d-444c-81fb-923a6240c1ef
caps.latest.revision: 31
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 31
---
# Audit Add DB User 이벤트 클래스
  **Audit Add DB User** 이벤트 클래스는 데이터베이스 사용자 로그인이 데이터베이스에 추가 또는 제거될 때마다 발생합니다. 이 이벤트 클래스는 **sp_grantdbaccess**, **sp_revokedbaccess**, **sp_adduser** 및 **sp_dropuser** 저장 프로시저에 사용됩니다.  
  
 이 이벤트 클래스는 나중 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 제거될 수 있으므로 **Audit Database Principal Management** 이벤트 클래스를 대신 사용하는 것이 좋습니다.  
  
## Audit Add DB User 이벤트 클래스 데이터 열  
  
|데이터 열 이름|데이터 형식|설명|열 ID|필터 가능|  
|----------------------|---------------|-----------------|---------------|----------------|  
|**ApplicationName**|**nvarchar**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 연결한 클라이언트 응용 프로그램의 이름입니다. 이 열은 프로그램의 표시 이름이 아니라 응용 프로그램에서 전달한 값으로 채워집니다.|10|예|  
|**ClientProcessID**|**int**|클라이언트 응용 프로그램이 실행 중인 프로세스에 대해 호스트 컴퓨터가 할당한 ID입니다. 클라이언트가 클라이언트 프로세스 ID를 제공하면 이 데이터 열이 채워집니다.|9|예|  
|**ColumnPermissions**|**int**|열 사용 권한이 설정되어 있는지 나타냅니다. 문 텍스트를 구문 분석하여 어떤 사용 권한이 어떤 열에 적용되었는지 알 수 있습니다.|44|예|  
|**DatabaseID**|**int**|USE *database* 문에서 지정한 데이터베이스 ID이거나, 지정한 인스턴스에 대해 USE *database* 문을 실행하지 않은 경우 기본 데이터베이스입니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] ServerName **데이터 열이 추적에서 캡처되고 서버를 사용할 수 있으면** 에 데이터베이스 이름이 표시됩니다. DB_ID 함수를 사용하여 데이터베이스의 값을 확인할 수 있습니다.|3|예|  
|**DatabaseName**|**nvarchar**|사용자 이름이 추가 또는 제거되는 데이터베이스의 이름입니다.|35|예|  
|**DBUserName**|**nvarchar**|데이터베이스에서 발급자의 사용자 이름입니다.|40|예|  
|**EventClass**|**int**|이벤트 유형 = 109|27|아니요|  
|**EventSequence**|**int**|요청 내에 지정된 이벤트 시퀀스입니다.|51|아니요|  
|**EventSubClass**|**int**|이벤트 하위 클래스의 유형입니다.<br /><br /> 1=추가<br /><br /> 2=삭제<br /><br /> 3=데이터베이스 액세스 권한 부여<br /><br /> 4=데이터베이스 액세스 권한 취소|21|예|  
|**HostName**|**nvarchar**|클라이언트를 실행 중인 컴퓨터 이름입니다. 클라이언트가 호스트 이름을 제공하면 이 데이터 열이 채워집니다. 호스트 이름을 확인하려면 HOST_NAME 함수를 사용합니다.|8|예|  
|**IsSystem**|**int**|이벤트가 시스템 프로세스에서 발생했는지 아니면 사용자 프로세스에서 발생했는지를 나타냅니다. 1 = 시스템, 0 = 사용자|60|예|  
|**LoginName**|**nvarchar**|사용자 로그인 이름(DOMAIN\username 형식의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 로그인 자격 증명 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 보안 로그인)입니다.|11|예|  
|**LoginSid**|**image**|로그인한 사용자의 SID(보안 ID)입니다. 이 정보는 **sys.server_principals** 카탈로그 뷰에 있습니다. 각 SID는 서버의 각 로그인마다 고유합니다.|41|예|  
|**NTDomainName**|**nvarchar**|사용자가 속한 Windows 도메인입니다.|7|예|  
|**NTUserName**|**nvarchar**|Windows 사용자 이름입니다.|6|예|  
|**OwnerName**|**nvarchar**|개체 소유자의 데이터베이스 사용자 이름입니다.|37|예|  
|**RequestID**|**int**|문을 포함하는 요청의 ID입니다.|49|예|  
|**RoleName**|**nvarchar**|멤버 자격이 수정되는 데이터베이스 역할의 이름입니다(**sp_adduser**와 함께 사용된 경우).|38|예|  
|**ServerName**|**nvarchar**|추적 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름입니다.|26||  
|**SessionLoginName**|**Nvarchar**|세션을 시작한 사용자의 로그인 이름입니다. 예를 들어 Login1을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결하고 Login2로 문을 실행할 경우 **SessionLoginName** 은 Login1을 표시하고 **LoginName** 은 Login2를 표시합니다. 이 열은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 로그인을 모두 표시합니다.|64|예|  
|**SPID**|**int**|이벤트가 발생한 세션의 ID입니다.|12|예|  
|**StartTime**|**datetime**|이벤트가 시작된 시간입니다(사용 가능한 경우).|14|예|  
|**성공**|**int**|1 = 성공, 0 = 실패. 예를 들어 값 1은 사용 권한 확인이 성공했음을 나타내고, 값 0은 확인이 실패했음을 나타냅니다.|23|예|  
|**TargetLoginName**|**nvarchar**|데이터베이스 액세스 권한을 수정 중인 로그인 이름입니다.|42|예|  
|**TargetLoginSid**|**image**|로그인을 대상으로 하는 동작(예: 새 로그인 추가)의 경우 대상 로그인의 SID(보안 ID)입니다.|43|예|  
|**TargetUserName**|**nvarchar**|추가 중인 데이터베이스의 사용자 이름입니다.|39|예|  
|**TransactionID**|**bigint**|시스템이 할당한 트랜잭션의 ID입니다.|4|예|  
|**XactSequence**|**bigint**|현재 트랜잭션을 설명하는 토큰입니다.|50|예|  
  
## 참고 항목  
 [확장 이벤트](../../relational-databases/extended-events/extended-events.md)   
 [sp_trace_setevent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_grantdbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [sp_revokedbaccess&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokedbaccess-transact-sql.md)   
 [sp_adduser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)   
 [sp_dropuser&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropuser-transact-sql.md)   
 [Audit Database Principal Management 이벤트 클래스](../../relational-databases/event-classes/audit-database-principal-management-event-class.md)  
  
  