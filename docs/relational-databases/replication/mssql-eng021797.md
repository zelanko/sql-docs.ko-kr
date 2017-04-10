---
title: "MSSQL_ENG021797 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG021797 오류"
ms.assetid: 54d83a1e-43fd-449c-a2b2-fdda2609a534
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 14
---
# MSSQL_ENG021797
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21797|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|'%s'은(는) '컴퓨터\\로그인' 또는 '도메인\\로그인' 형식의 올바른 Windows 로그인이어야 합니다. '%s'에 대한 설명서를 참조하십시오.|  
  
## 설명  
 에 대 한 지정 된 값이이 오류는 다음 복제 저장 프로시저에 의해 발생 된 **@job_login** 매개 변수는 null 이거나 유효 하지 않습니다. 구성원 인 경우이 오류가 발생할 수는 **db_owner** 의 이전 버전에서 스크립트를 실행 하는 고정된 데이터베이스 역할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 보안 모델이 변경되었으므로 이러한 스크립트를 업데이트해야 합니다.  
  
-   [sp_addlogreader_agent & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)  
  
-   [sp_addqreader_agent & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)  
  
-   [sp_addpublication_snapshot & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)  
  
-   [sp_addpushsubscription_agent & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)  
  
-   [sp_addpullsubscription_agent & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepushsubscription_agent & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql.md)  
  
-   [sp_addmergepullsubscription_agent & #40입니다. TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md)  
  
 이러한 저장된 프로시저의 멤버만 실행할 수는 **sysadmin** 고정된 서버 역할의 멤버 이거나 적절 한 서버에는 **db_owner** 해당 데이터베이스에 대 한 고정된 데이터베이스 역할. 저장 프로시저는 각각 에이전트 작업을 만들어 에이전트가 실행되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정을 지정할 수 있게 해줍니다. 사용자에 대 한는 **sysadmin** 역할 에이전트 작업이 암시적으로 만들어지는 Windows 계정이 지정 되지 않은 경우에 (계정이 지정은 경우에 유효 해야);의 컨텍스트 내에서 실행 하는 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 적절 한 서버에서 에이전트 서비스 계정. 계정이 반드시 필요한 것은 아니지만 에이전트에 대해 별도의 계정을 지정하는 것은 보안을 위한 최선의 구현 방법입니다. 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을(를) 참조하세요.  
  
## 사용자 동작  
 확인에 대 한 유효한 Windows 계정을 지정 하는 **@job_login** 각 프로시저의 매개 변수입니다. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가져온 복제 스크립트를 사용할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 필요한 저장 프로시저와 매개 변수를 포함하도록 스크립트를 업데이트합니다. 자세한 내용은 참조 [복제 스크립트 업그레이드 & #40; 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  