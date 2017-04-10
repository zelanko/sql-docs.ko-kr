---
title: "MSSQL_ENG021798 | Microsoft Docs"
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
  - "MSSQL_ENG021798 오류"
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
caps.latest.revision: 16
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 16
---
# MSSQL_ENG021798
    
## 메시지 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21798|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|심볼 이름||  
|메시지 텍스트|계속하려면 먼저 '%s'을(를) 통해 '%s' 에이전트 작업을 추가해야 합니다. '%s'에 대한 설명서를 참조하십시오.|  
  
## 설명  
 게시를 만들 수 있습니다의 멤버는 **sysadmin** 고정된 서버 역할의 멤버 이거나 게시자에는 **db_owner** 게시 데이터베이스의 고정된 데이터베이스 역할입니다. 멤버인 경우는 **db_owner** 역할의 경우이 오류가 발생 합니다.  
  
-   [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]에서 스크립트를 실행하십시오. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서는 보안 모델이 변경되었으므로 이러한 스크립트를 업데이트해야 합니다.  
  
-   저장된 프로시저 **sp_addpublication** 실행 되기 전에 실행 [sp_addlogreader_agent (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)합니다. 이 조건은 모든 트랜잭션 게시에 적용됩니다.  
  
-   저장된 프로시저 **sp_addpublication** 실행 되기 전에 실행 [sp_addqreader_agent (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)합니다. 이 지연된 업데이트 구독에 대 한 활성화 된 트랜잭션 게시에 적용 됩니다 (값에 대 한 TRUE는 **@allow_queued_tran** 의 매개 변수 **sp_addpublication**).  
  
 저장된 프로시저 **sp_addlogreader_agent** 및 **sp_addqreader_agent** 에이전트 작업을 만들고 지정할 수 있도록 각는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에이전트가 실행 되는 Windows 계정입니다. 사용자에 대 한는 **sysadmin** 역할 에이전트 작업이 암시적으로 만들어지는 경우 **sp_addlogreader_agent** 및 **sp_addqreader_agent** 실행 되지 않습니다; 에이전트의 컨텍스트 내에서 실행 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에서 에이전트 서비스 계정입니다. 하지만 **sp_addlogreader_agent** 및 **sp_addqreader_agent** 사용자에 대 한 필요 없는 **sysadmin** 에이전트에 대 한 별도 계정을 지정 하려면 보안 모범 사례는 이기 역할을 합니다. 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
## 사용자 동작  
 프로시저를 올바른 순서로 실행하십시오. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)을(를) 참조하세요. 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 가져온 복제 스크립트를 사용할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에 필요한 저장 프로시저와 매개 변수를 포함하도록 스크립트를 업데이트합니다. 자세한 내용은 참조 [복제 스크립트 업그레이드 & #40; 복제 TRANSACT-SQL 프로그래밍 & #41;](../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)합니다.  
  
## 참고 항목  
 [오류 및 이벤트 참조 & #40입니다. 복제 및 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  