---
title: "트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "트랜잭션 복제, 업데이트 가능 구독"
  - "업데이트 가능 구독, 활성화"
  - "구독 [SQL Server 복제], 업데이트 가능"
ms.assetid: 539d5bb0-b808-4d8c-baf4-cb6d32d2c595
caps.latest.revision: 42
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 42
---
# 트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 트랜잭션 게시에 대해 구독 업데이트를 설정하는 방법에 대해 설명합니다.  
  
> **참고!!** [!INCLUDE[ssNoteDepFutureAvoid](../../../includes/ssnotedepfutureavoid-md.md)]  
  

##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사의 **게시 유형** 페이지에서 트랜잭션 게시에 대해 구독 업데이트를 설정합니다.  
  
 구독 업데이트를 사용하려면 새 구독 마법사에서도 옵션을 구성해야 합니다.  
  
#### 구독 업데이트를 설정하려면  
  
1.  새 게시 마법사의 **게시 유형** 페이지에서 **업데이트할 수 있는 구독이 있는 트랜잭션 게시**를 선택합니다.  
  
2.  **에이전트 보안** 페이지에서 스냅숏 에이전트, 로그 판독기 에이전트 및 큐 판독기 에이전트에 대한 보안 설정을 지정합니다. 큐 판독기 에이전트가 실행되는 계정에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하세요.  
  
    > **참고:** 만 즉시 업데이트 구독을 사용 하는 경우에 큐 판독기 에이전트가 구성 되어 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 트랜잭션 게시를 만들 때 즉시 업데이트 구독 또는 지연 업데이트 구독을 설정할 수 있습니다.  
  
#### 즉시 업데이트 구독을 지원하는 게시를 만들려면  
  
1.  필요한 경우 게시 데이터베이스에 대한 로그 판독기 에이전트 작업을 만듭니다.  
  
    -   게시 데이터베이스에 대한 로그 판독기 에이전트 작업이 이미 존재하면 2단계를 실행합니다.  
  
    -   게시 된 데이터베이스에 대 한 로그 판독기 에이전트 작업이 있는지 잘 모를 경우 실행 [sp_helplogreader_agent (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 게시 데이터베이스의 게시자입니다. 결과 집합이 비어 있으면 로그 판독기 에이전트 작업을 만들어야 합니다.  
  
    -   게시자에서 실행 [sp_addlogreader_agent (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)합니다. 지정 된 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 에이전트에 대 한 실행 되는 Windows 자격 증명 **@job_name** 및 **@password**합니다. 값도 지정 해야 에이전트는 게시자에 연결할 때 SQL Server 인증을 사용 하면, **0** 에 대 한 **@publisher_security_mode** 및 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대 한 로그인 정보 **@publisher_login** 및 **@publisher_password**합니다.  
  
2.  실행 [sp_addpublication (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), 값을 지정 하면 **true** 매개 변수에 대해 **@allow_sync_tran**합니다.  
  
3.  게시자에서 실행 [sp_addpublication_snapshot (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)합니다. 에 대 한 2 단계에서 사용한 게시 이름을 지정 **@publication** 및에 대 한 스냅숏 에이전트가 실행 되는 Windows 자격 증명 **@job_name** 및 **@password**합니다. 값도 지정 해야 에이전트는 게시자에 연결할 때 SQL Server 인증을 사용 하면, **0** 에 대 한 **@publisher_security_mode** 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대 한 로그인 정보 **@publisher_login** 및 **@publisher_password**합니다. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
4.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
5.  구독자에서 이 게시에 대한 업데이트 구독을 만듭니다.   
  
#### 지연 업데이트 구독을 지원하는 게시를 만들려면  
  
1.  필요한 경우 게시 데이터베이스에 대한 로그 판독기 에이전트 작업을 만듭니다.  
  
    -   게시 데이터베이스에 대한 로그 판독기 에이전트 작업이 이미 존재하면 2단계를 실행합니다.  
  
    -   게시 된 데이터베이스에 대 한 로그 판독기 에이전트 작업이 있는지 잘 모를 경우 실행 [sp_helplogreader_agent (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 게시 데이터베이스의 게시자입니다. 결과 집합이 비어 있으면 로그 판독기 에이전트 작업을 만들어야 합니다.  
  
    -   게시자에서 실행 [sp_addlogreader_agent (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)합니다. 에이전트에 대 한 실행 되는 Windows 자격 증명 지정 **@job_name** 및 **@password**합니다. 값도 지정 해야 에이전트는 게시자에 연결할 때 SQL Server 인증을 사용 하면, **0** 에 대 한 **@publisher_security_mode** 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대 한 로그인 정보 **@publisher_login** 및 **@publisher_password**합니다.  
  
2.  필요한 경우 배포자에 대한 큐 판독기 에이전트 작업을 만듭니다.  
  
    -   배포 데이터베이스에 대한 큐 판독기 에이전트 작업이 이미 존재하면 3단계를 실행합니다.  
  
    -   배포 데이터베이스에 대 한 큐 판독기 에이전트 작업이 있는지 잘 모를 경우 실행 [sp_helpqreader_agent (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md) 배포 데이터베이스의 배포자입니다. 결과 집합이 비어 있으면 큐 판독기 에이전트 작업을 만들어야 합니다.  
  
    -   배포자에서 실행 [sp_addqreader_agent (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql.md)합니다. 에이전트에 대 한 실행 되는 Windows 자격 증명 지정 **@job_name** 및 **@password**합니다. 이러한 자격 증명은 큐 판독기 에이전트가 게시자 및 구독자에 연결할 때 사용됩니다. 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)을(를) 참조하세요.  
  
3.  실행 [sp_addpublication (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), 값을 지정 하면 **true** 매개 변수에 대해 **@allow_queued_tran** 값 **pub wins**, **sub reinit**, 또는 **wins 하위** 에 대 한 **@conflict_policy**합니다.  
  
4.  게시자에서 실행 [sp_addpublication_snapshot (TRANSACT-SQL)](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)합니다. 3 단계에서 사용 되는 게시 이름을 **@publication** 및에 대 한 스냅숏 에이전트가 실행 되는 Windows 자격 증명 **@snapshot_job_name** 및 **@password**합니다. 값도 지정 해야 에이전트는 게시자에 연결할 때 SQL Server 인증을 사용 하면, **0** 에 대 한 **@publisher_security_mode** 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에 대 한 로그인 정보 **@publisher_login** 및 **@publisher_password**합니다. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
5.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
6.  구독자에서 이 게시에 대한 업데이트 구독을 만듭니다.  
  
#### 지연 업데이트 구독을 허용하는 게시에 대한 충돌 정책을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_changepublication (& a) #40; TRANSACT-SQL &#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)합니다. 값을 지정 **conflict_policy** 에 대 한 **@property** 및 원하는 충돌 정책 모드의 **pub wins**, **sub reinit**, 또는 **wins 하위** 에 대 한 **@value**합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 즉시 업데이트 끌어오기 구독과 지연 업데이트 끌어오기 구독을 모두 지원하는 게시를 만듭니다.  
  
 [!code-sql[HowTo#sp_createtranupdatingpub](../../../relational-databases/replication/codesnippet/tsql/enable-updating-subscrip_1.sql)]  
  
## 관련 항목:  
 [지연된 업데이트 충돌 해결 옵션 &#40; 설정 SQL Server Management Studio &#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)   
 [트랜잭션 복제에 대한 게시 유형](../../../relational-databases/replication/transactional/publication-types-for-transactional-replication.md)   
 [트랜잭션 복제를 위한 업데이트 가능 구독](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [게시 만들기](../../../relational-databases/replication/publish/create-a-publication.md)   
 [트랜잭션 게시에 대해 업데이트할 수 있는 구독 만들기](https://msdn.microsoft.com/library/mt740635.aspx)   
 [트랜잭션 복제를 위한 업데이트 가능 구독](../../../relational-databases/replication/transactional/updatable-subscriptions-for-transactional-replication.md)   
 [스크립팅 변수와 함께 sqlcmd 사용](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)  
  
  