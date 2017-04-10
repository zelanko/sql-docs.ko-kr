---
title: "게시 액세스 목록에서 로그인 관리 | Microsoft Docs"
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
  - "로그인 [SQL Server 복제], 게시 액세스 목록"
  - "게시 [SQL Server 복제], 게시 액세스 목록"
  - "게시 액세스 목록(PAL)"
  - "PAL(게시 액세스 목록)"
  - "로그인 [SQL Server 복제], 관리"
ms.assetid: fceb216b-0b18-4e3b-8ae0-13e35920dcbc
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 게시 액세스 목록에서 로그인 관리
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 게시 액세스 목록의 로그인을 관리하는 방법에 대해 설명합니다. 게시에 대한 액세스는 PAL(게시 액세스 목록)에서 제어합니다. 로그인 및 그룹을 추가하고 PAL에서 제거할 수 있습니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소](#Prerequisites)  
  
-   **다음을 사용하여 게시 액세스 목록에서 로그인을 관리하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   PAL에 로그인을 추가하려면 먼저 게시 데이터베이스의 데이터베이스 사용자와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인을 연결해야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 게시 액세스 목록 (PAL)을 사용 하 여에 **게시 액세스 목록** 의 페이지는 **게시 속성-\< 게시>** 로그인을 관리 하려면 대화 상자입니다. 이 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### PAL에서 로그인을 관리하려면  
  
1.  에 **게시 액세스 목록** 의 페이지는 **게시 속성-\< 게시>** 대화 상자를 사용 하 여는 **추가**, **제거**, 및 **모두 제거** 단추를 추가 하 고 PAL에서 로그인 및 그룹을 제거 합니다. 제거 하지 마십시오 **distributor_admin** PAL에서. 이 계정은 복제에 사용됩니다.  
  
    > [!NOTE]  
    >  원격 배포자를 사용할 경우 PAL의 계정을 게시자와 배포자에서 모두 사용할 수 있어야 합니다. 이 계정은 두 서버 모두에 정의된 도메인 계정이나 로컬 계정이어야 합니다. 또한 두 로그인과 연결된 암호는 같아야 합니다.  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### PAL에 속한 그룹 및 로그인을 보려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_help_publication_access](../../../relational-databases/system-stored-procedures/sp-help-publication-access-transact-sql.md)합니다. 이때 **@publication**에 게시 이름을 지정합니다. 그러면 PAL의 그룹 및 로그인에 대한 정보가 표시됩니다.  
  
#### PAL에 그룹 및 로그인을 추가하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_grant_publication_access](../../../relational-databases/system-stored-procedures/sp-grant-publication-access-transact-sql.md)합니다. 이때 **@publication**에 게시 이름, **@login**에 추가할 로그인 또는 그룹 이름을 지정합니다.  
  
#### PAL에서 그룹 및 로그인을 제거하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_revoke_publication_access](../../../relational-databases/system-stored-procedures/sp-revoke-publication-access-transact-sql.md)합니다. 이때 **@publication**에 게시 이름, **@login**에 제거할 로그인 또는 그룹 이름을 지정합니다.  
  
## 참고 항목  
 [게시 액세스 목록에서 로그인 관리](../../../relational-databases/replication/security/manage-logins-in-the-publication-access-list.md)   
 [복제 에이전트 보안 모델](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [복제 토폴로지 보안 설정](../../../relational-databases/replication/security/secure-a-replication-topology.md)   
 [게시자 보안 설정](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  