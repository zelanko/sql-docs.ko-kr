---
title: "Oracle 데이터베이스에서 게시 만들기 | Microsoft Docs"
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
  - "게시 [SQL Server 복제], Oracle 데이터베이스"
  - "Oracle 게시 [SQL Server 복제], 구성"
ms.assetid: b3812746-14b0-4b22-809e-b4a95e1c8083
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# Oracle 데이터베이스에서 게시 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]의 Oracle 데이터베이스에서 구독을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [필수 구성 요소](#Prerequisites)  
  
-   **다음을 사용하여 Oracle 데이터베이스에서 게시를 만들려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   게시를 만들기 전에 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에 Oracle 소프트웨어를 설치하고 Oracle 데이터베이스를 구성해야 합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사를 사용하여 Oracle 데이터베이스에서 스냅숏 또는 트랜잭션 게시를 만듭니다.  
  
 처음으로 Oracle 데이터베이스에서 게시를 만들 때는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자에서 Oracle 게시자를 식별해야 합니다. 같은 데이터베이스의 후속 게시에 대해서는 이 작업을 수행할 필요가 없습니다. Oracle 게시자를 식별 합니다. 새 게시 마법사에서 수행할 수 있습니다 또는 **배포자 속성-\< 배포자>** 대화 상자;이 항목을 보여 줍니다는 **배포자 속성-\< 배포자>** 대화 상자입니다.  
  
#### SQL Server 배포자에서 Oracle 게시자를 식별하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 Oracle 게시자가 배포자로 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **복제** 폴더를 마우스 클릭 한 다음 **배포자 속성**합니다.  
  
3.  에 **게시자** 의 페이지는 **배포자 속성-\< 배포자>** 대화 상자를 클릭 하 여 **추가**, 클릭 하 고 **Oracle 게시자 추가**.  
  
4.  **서버에 연결** 대화 상자에서 **옵션** 단추를 클릭합니다.  
  
5.  **로그인** 탭에서 다음을 수행하세요.  
  
    1.  Oracle 데이터베이스 인스턴스 이름을 입력하거나 **서버 인스턴스** 콤보 상자에서 **더 찾아보기** 를 선택합니다.  
  
    2.  선택 **Oracle 표준 인증** (권장) 또는 **Windows 인증**합니다.  
  
         선택 하는 경우 **Windows 인증**: Windows 자격 증명을 사용 하 여 연결을 허용 하도록 Oracle 서버를 구성 해야 합니다 (자세한 내용은 Oracle 설명서 참조), 동일한를 사용 하 여 현재 로그온 해야 하 고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 복제 관리 사용자 스키마에 대해 지정한 Windows 계정입니다.  
  
    3.  **Oracle 표준 인증**을 선택하는 경우에는 구성하는 동안 Oracle 게시자에 만든 복제 관리 사용자 스키마의 로그인 및 암호를 입력합니다.  
  
6.  **연결 속성** 탭에서 게시자 유형으로 **게이트웨이** 또는 **전체**를 선택합니다.  
  
     **전체** 옵션은 Oracle 게시에 대해 지원되는 완전한 기능 집합을 스냅숏 및 트랜잭션 게시에 제공하도록 디자인되었습니다. **게이트웨이** 옵션은 복제가 시스템 간의 게이트웨이로 사용되는 경우 성능을 향상시킬 수 있도록 특정 디자인 최적화를 제공합니다. 동일한 테이블을 여러 트랜잭션 게시에 게시하려는 경우에는 **게이트웨이** 옵션을 사용할 수 없습니다. **게이트웨이**를 선택하면 트랜잭션 게시의 경우 특정 테이블이 한 번만 나타날 수 있지만 스냅숏 게시의 경우에는 이러한 제한이 없습니다.  
  
7.  **연결**을 클릭하면 Oracle 게시자에 연결되고 이 게시자가 복제용으로 구성됩니다.  **서버에 연결** 대화 상자가 닫히고에 반환 되는 **배포자 속성-\< 배포자>** 대화 상자입니다.  
  
    > [!NOTE]  
    >  네트워크 구성에 문제가 있는 경우 이 시점에 오류가 표시됩니다. Oracle 데이터베이스 연결에 문제가 있으면 [Troubleshooting Oracle Publishers](../../../relational-databases/replication/non-sql/troubleshooting-oracle-publishers.md)의 "SQL Server 배포자가 Oracle 데이터베이스 인스턴스에 연결할 수 없습니다" 섹션을 참조하세요.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### Oracle 데이터베이스에서 게시를 만들려면  
  
1.  Oracle 게시자가 배포자로 사용할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장합니다.  
  
3.  마우스 오른쪽 단추로 클릭는 **로컬 게시** 폴더를 마우스 클릭 한 다음 **새 Oracle 게시**합니다.  
  
4.  새 게시 마법사의 **Oracle 게시자** 페이지에서 Oracle 게시자를 선택합니다. Oracle 게시자가 표시되지 않으면 **Oracle 게시자 추가**를 클릭하여 표시되는 이전 절차의 단계를 따르세요.  
  
5.  **게시 유형** 페이지에서 **스냅숏 게시** 또는 **트랜잭션 게시**를 선택합니다.  
  
6.  **아티클** 페이지에서 게시할 데이터베이스 개체를 선택합니다.  
  
     필요에 따라 테이블을 확장한 다음 하나 이상의 열에 대한 확인란의 선택을 취소하는 방법으로 테이블 열을 필터링하여 제외시킵니다. **아티클 속성** 을 클릭하여 아티클 속성을 보고 수정하며 필요에 따라 대체 데이터 형식 매핑을 지정합니다. 데이터 형식 매핑에 대 한 자세한 내용은 참조 [Oracle 게시자에 대 한 데이터 형식 매핑을 지정](../../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)합니다.  
  
7.  **테이블 행 필터** 페이지에서 필요에 따라 필터를 적용하여 하나 이상의 테이블에서 데이터 하위 집합을 게시합니다.  
  
8.  모든 개체를 만들고 필요한 모든 데이터를 구독 데이터베이스에 추가한 경우에만 **스냅숏 에이전트** 페이지에서 **즉시 스냅숏 만들기** 의 선택을 취소합니다.  
  
9. 에 **에이전트 보안** 페이지 (모든 게시의 경우)에 대 한 스냅숏 에이전트 및 로그 판독기 에이전트 (트랜잭션 게시용)에 대 한 자격 증명을 지정 합니다. 사용자가 지정한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows 계정의 컨텍스트를 사용하여 에이전트를 실행하고 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 배포자에 연결합니다. 에이전트는 복제 관리 사용자 스키마로 지정한 계정의 컨텍스트를 사용하여 Oracle 데이터베이스에 연결합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
     각 에이전트에 필요한 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 및 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)을 참조하세요.  
  
10. **마법사 동작** 페이지에서 필요에 따라 게시를 스크립팅합니다. 자세한 내용은 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)을 참조하세요.  
  
11. **마법사 완료** 페이지에서 게시의 이름을 지정합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 Oracle 데이터베이스를 게시자로 구성한 경우 시스템 저장 프로시저를 사용하여 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자와 동일한 방법으로 트랜잭션 또는 스냅숏 게시를 만들 수 있습니다.  
  
#### Oracle 게시를 만들려면  
  
1.  Oracle 데이터베이스를 게시자로 구성합니다. 자세한 내용은 참조 [Oracle 게시자를 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
2.  원격 배포자가 없는 경우 원격 배포자를 구성합니다. 자세한 내용은 [Configure Publishing and Distribution](../../../relational-databases/replication/configure-publishing-and-distribution.md)을 참조하세요.  
  
3.  Oracle 게시자가 사용할 원격 배포자에서 실행 [sp_adddistpublisher (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)합니다. 에 대 한 Oracle 데이터베이스 인스턴스 네트워크 TNS (Transparent Substrate) 이름을 지정 **@publisher** 값 **ORACLE** 또는 **ORACLE GATEWAY** 에 대 한 **@publisher_type**합니다. `Specify` 배포자에 연결할 때 사용하는 보안 모드를 다음 중 하나로 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 합니다.  
  
    -   기본값인 Oracle 표준 인증을 사용 하 여 값을 지정 **0** 에 대 한 **@security_mode**, 에 대 한 구성 하는 동안 Oracle 게시자에 만든 복제 관리 사용자 스키마의 로그인 **@login**, 및에 대 한 암호 **@password**합니다.  
  
        > [!IMPORTANT]  
        >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
    -   Windows 인증을 사용 하려면 값을 지정 **1** 에 대 한 **@security_mode**합니다.  
  
        > [!NOTE]  
        >  Windows 인증을 사용하려면 Windows 자격 증명을 사용한 연결을 허용하도록 Oracle 서버를 구성해야 하며(자세한 내용은 Oracle 설명서 참조), 복제 관리 사용자 스키마에 대해 지정한 Microsoft Windows 계정과 동일한 계정으로 로그인한 상태여야 합니다.  
  
4.  게시 데이터베이스에 대한 로그 판독기 에이전트 작업을 만듭니다.  
  
    -   게시 된 데이터베이스에 대 한 로그 판독기 에이전트 작업이 있는지 잘 모를 경우 실행 [sp_helplogreader_agent (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 배포자의 배포 데이터베이스의 Oracle 게시자에서 사용 합니다. **@publisher**에 대해 Oracle 게시자의 이름을 지정합니다. 결과 집합이 비어 있으면 로그 판독기 에이전트 작업을 만들어야 합니다.  
  
    -   게시 데이터베이스에 대한 로그 판독기 에이전트 작업이 이미 존재하면 5단계를 실행합니다.  
  
    -   배포 데이터베이스의 Oracle 게시자에서 사용 하는 배포자에서 실행 [sp_addlogreader_agent (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)합니다. 에이전트에 대 한 실행 되는 Windows 자격 증명 지정 **@job_login** 및 **@job_password**합니다.  
  
        > [!NOTE]  
        >   **@job_login** 매개 변수는 3 단계에서 제공 된 로그인 일치 해야 합니다. 게시자 보안 정보를 제공하지 마세요. 로그 판독기 에이전트는 3단계에 제공된 보안 정보를 사용하여 게시자에 연결합니다.  
  
5.  배포 데이터베이스의 배포자에서 실행 [sp_addpublication (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 게시 만들기 자세한 내용은 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)을 참조하세요.  
  
6.  배포 데이터베이스의 배포자에서 실행 [sp_addpublication_snapshot (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)합니다. 에 대 한 4 단계에서 사용한 게시 이름을 지정 **@publication** 및에 대 한 스냅숏 에이전트가 실행 되는 Windows 자격 증명 **@job_name** 및 **@password**합니다. 파일을 게시자에 연결할 때 Oracle 표준 인증을 사용 하려면도 지정 해야 값 **0** 에 대 한 **@publisher_security_mode** 및 Oracle 로그인 정보를 **@publisher_login** 및 **@publisher_password**합니다. 이렇게 하면 게시에 대해 스냅숏 에이전트 작업이 만들어집니다.  
  
## 참고 항목  
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [Oracle 게시자는 & #40;에 대 한 트랜잭션 세트 작업 구성 복제 TRANSACT-SQL 프로그래밍 & #41;](../../../relational-databases/replication/administration/configure the transaction set job for an oracle publisher.md)   
 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)   
 [Oracle 권한 부여 스크립트](../../../relational-databases/replication/non-sql/script-to-grant-oracle-permissions.md)  
  
  