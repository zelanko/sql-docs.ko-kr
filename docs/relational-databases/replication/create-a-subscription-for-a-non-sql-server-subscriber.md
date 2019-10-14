---
title: SQL Server 이외 구독자에 대한 구독 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication], non-SQL Server Subscribers
- Subscribers [SQL Server replication], non-SQL Server Subscribers
- non-SQL Server Subscribers, subscriptions
ms.assetid: 5020ee68-b988-4d57-8066-67d183e61237
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3f37431c1d8359eface4a5ad374ed8ba6717708a
ms.sourcegitcommit: 8732161f26a93de3aa1fb13495e8a6a71519c155
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71710438"
---
# <a name="create-a-subscription-for-a-non-sql-server-subscriber"></a>SQL Server 이외 구독자에 대한 구독 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 SQL Server 이외 구독자에 대한 구독을 만드는 방법에 대해 설명합니다. 트랜잭션 복제와 스냅샷 복제는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자로의 데이터 게시를 지원합니다. 지원되는 구독자 플랫폼에 대한 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)에서 SQL Server 이외 구독자에 대한 구독을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **SQL Server 이외 구독자에 대한 구독을 만들려면:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 구독을 만들려면 다음을 수행하세요.  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 배포자에 적절한 클라이언트 소프트웨어 및 OLE DB 공급자를 설치하고 구성합니다. 자세한 내용은 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) 및 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)를 참조하세요.  
  
2.  새 게시 마법사를 사용하여 게시를 만듭니다. 게시를 만드는 방법에 대한 자세한 내용은 [게시 만들기](../../relational-databases/replication/publish/create-a-publication.md) 및 [Oracle 데이터베이스에서 게시 만들기](../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)를 참조하세요. 새 게시 마법사에서 다음 옵션을 지정합니다.  
  
    -   **게시 유형** 페이지에서 **스냅샷 게시** 또는 **트랜잭션 게시**를 선택합니다.  
  
    -   **스냅샷 에이전트** 페이지에서 **즉시 스냅샷 만들기**의 선택을 취소합니다.  
  
         스냅샷 에이전트에서[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 적합한 스냅샷 및 초기화 스크립트를 생성하려면[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 게시를 설정한 다음 스냅샷을 만듭니다.  
  
3.  **게시 속성 - \<PublicationName>** 대화 상자를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 게시를 사용하도록 설정합니다. 이 단계에 대한 자세한 내용은 [Publication Properties, Subscription Options](../../relational-databases/replication/publication-properties-subscription-options.md) 을 참조하세요.  
  
4.  새 구독 마법사를 사용하여 구독을 만듭니다. 이 항목에는 이 단계에 대한 자세한 정보를 제공합니다.  
  
5.  (옵션) **pre_creation_cmd** 아티클 속성을 변경하여 구독자에서 테이블을 유지합니다. 이 항목에는 이 단계에 대한 자세한 정보를 제공합니다.  
  
6.  게시에 대한 스냅샷을 생성합니다. 이 항목에는 이 단계에 대한 자세한 정보를 제공합니다.  
  
7.  구독을 동기화합니다. 자세한 내용은 [밀어넣기 구독 동기화](../../relational-databases/replication/synchronize-a-push-subscription.md)을 참조하세요.  
  
#### <a name="to-enable-a-publication-for-non-sql-server-subscribers"></a>SQL Server 이외 구독자에 대한 게시를 설정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
3.  게시를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **구독 옵션** 페이지에서 **SQL Server 이외 구독자 허용** 옵션에 대해 **True**값을 선택합니다. 이 옵션을 선택하면 게시가[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자와 호환되도록 많은 속성이 변경됩니다.  
  
    > [!NOTE]  
    >  **True** 를 선택하면 **pre_creation_cmd** 아티클 속성 값이 'drop'으로 설정됩니다. 이 설정은 구독자의 테이블이 아티클의 테이블 이름과 일치하는 경우 복제가 구독자의 테이블을 삭제하도록 지정합니다. 구독자에서 기존 테이블을 계속 유지하려는 경우 각 아티클에 대해 [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 저장 프로시저를 사용하고 **pre_creation_cmd**에 'none' 값을 지정합니다. `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 게시에 대한 새 스냅샷을 만들라는 메시지가 표시됩니다. 지금 스냅숏을 만들지 않으려면 나중에 다음 "방법" 절차에서 설명한 단계를 사용합니다.  
  
#### <a name="to-create-a-subscription-for-a-non-sql-server-subscriber"></a>SQL Server 이외 구독자에 대한 구독을 만들려면  
  
1.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
2.  적절한 게시를 마우스 오른쪽 단추로 클릭한 다음 **새 구독**을 클릭합니다.  
  
3.  **배포 에이전트 위치** 페이지에서 **배포자에서 모든 에이전트 실행** 을 선택합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자는 구독자에서의 에이전트 실행을 지원하지 않습니다.  
  
4.  **구독자** 페이지에서 **구독자 추가** 를 클릭한 다음 **SQL Server 이외 구독자 추가**를 클릭합니다.  
  
5.  **SQL Server 이외 구독자 추가** 대화 상자에서 구독자 유형을 선택합니다.  
  
6.  **데이터 원본 이름**에 다음과 같이 값을 입력합니다.  
  
    -   Oracle의 경우 구성한 TNS(Transparent Network Substrate) 이름을 입력합니다.  
  
    -   IBM의 경우 아무 이름이나 입력할 수 있습니다. 일반적으로 구독자의 네트워크 주소를 지정합니다.  
  
     이 단계에서 입력한 데이터 원본 이름과 9단계에서 지정한 자격 증명은 이 마법사에서 확인하지 않고 구독에 대해 배포 에이전트가 실행되어야 복제에서 사용됩니다. 클라이언트 도구(예: Oracle의 경우 **sqlplus** )를 통해 구독자에 연결하여 모든 값이 테스트되었는지 확인합니다. 자세한 내용은 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md) 및 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)를 참조하세요.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] 마법사의 **구독자** 페이지에서 이제 구독자가 **구독자** 열에 표시되며 **구독 데이터베이스** 열에서는 읽기 전용 **(기본 대상)** 입니다.  
  
    -   Oracle의 경우 한 대의 서버에 데이터베이스가 하나만 있으므로 데이터베이스를 지정할 필요가 없습니다.  
  
    -   IBM DB2의 경우 데이터베이스가 DB2 연결 문자열의 **Initial Catalog** 속성에 지정됩니다. 이 연결 문자열은 이 과정의 뒷부분에서 설명하는 **추가 연결 옵션** 필드에 입력할 수 있습니다.  
  
8.  **배포 에이전트 보안** 페이지에서 구독자 옆에 있는 속성 단추 ( **...** )를 클릭하여 **배포 에이전트 보안** 대화 상자에 액세스합니다.  
  
9. **배포 에이전트 보안** 대화 상자에서 다음을 수행하세요.  
  
    -   **프로세스 계정**, **암호**및 **암호 확인** 필드에서 배포 에이전트가 실행되고 배포자에 로컬로 연결될 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정과 암호를 입력합니다.  
  
         계정에는 최소 사용 권한인 배포 데이터베이스에서의 **db_owner** 고정 데이터베이스 역할의 멤버, PAL(게시 액세스 목록)의 멤버, 스냅샷 공유에 대한 읽기 권한 및 OLE DB 공급자의 설치 디렉터리에 대한 읽기 권한이 필요합니다. PAL에 대한 자세한 내용은 [게시자 보안 설정](../../relational-databases/replication/security/secure-the-publisher.md)을 참조하세요.  
  
    -   **구독자에 연결**의 **로그인**, **암호**및 **암호 확인** 필드에서 구독자 연결에 사용할 로그인과 암호를 입력합니다. 이 로그인은 이미 구성되어 있어야 하며 구독 데이터베이스에서 개체를 만들 수 있는 충분한 권한을 갖고 있어야 합니다.  
  
    -   **추가 연결 옵션** 필드에서 연결 문자열의 형식으로 구독자에 대한 연결 옵션을 지정합니다. Oracle에서는 추가 옵션이 필요하지 않습니다. 각 옵션은 세미콜론으로 구분해야 합니다. 다음은 DB2 연결 문자열의 예입니다. 이 예에서는 읽기 쉽도록 줄 바꿈을 넣었습니다.  
  
        ```  
        Provider=DB2OLEDB;Initial Catalog=MY_SUBSCRIBER_DB;Network Transport Library=TCP;Host CCSID=1252;  
        PC Code Page=1252;Network Address=MY_SUBSCRIBER;Network Port=50000;Package Collection=MY_PKGCOL;  
        Default Schema=MY_SCHEMA;Process Binary as Character=False;Units of Work=RUW;DBMS Platform=DB2/NT;  
        Persist Security Info=False;Connection Pooling=True;  
        ```  
  
         이 문자열의 옵션 대부분은 구성 중인 DB2 서버와만 관련이 있지만 **Process Binary as Character** 옵션은 항상 **False**로 설정해야 합니다. 구독 데이터베이스를 식별하려면 **Initial Catalog** 옵션 값을 지정해야 합니다.  
  
10. **동기화 일정** 페이지에 있는 **에이전트 일정** 메뉴에서 배포 에이전트에 대한 일정을 선택합니다. 일정은 일반적으로 **계속 실행**입니다.  
  
11. **구독 초기화** 페이지에서 구독의 초기화 여부를 지정하고 초기화하는 경우 초기화 시기를 지정합니다.  
  
    -   개체를 모두 만들고 구독 데이터베이스에 필요한 데이터를 모두 추가한 경우에만 **초기화** 의 선택을 취소합니다.  
  
    -   이 마법사가 완료된 다음 배포 에이전트가 스냅샷 파일을 구독자에게 전송하게 하려면 **초기화 시기** 열의 드롭다운 목록에서 **즉시** 를 선택합니다. 에이전트가 다음 실행 일정에 파일을 전송하게 하려면 **첫 번째 동기화 시** 를 선택합니다.  
  
12. **마법사 동작** 페이지에서 필요에 따라 구독을 스크립팅합니다. 자세한 내용은 [Scripting Replication](../../relational-databases/replication/scripting-replication.md)을 참조하세요.  
  
#### <a name="to-retain-tables-at-the-subscriber"></a>구독자에서 테이블을 유지하려면  
  
-   기본적으로[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대해 게시를 설정하면 **pre_creation_cmd** 아티클 속성 값이 'drop'으로 설정됩니다. 이 설정은 구독자의 테이블이 아티클의 테이블 이름과 일치하는 경우 복제가 구독자의 테이블을 삭제하도록 지정합니다. 구독자에서 기존 테이블을 계속 유지하려는 경우 각 아티클에 대해 [sp_changearticle](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 저장 프로시저를 사용하고 **pre_creation_cmd**에 'none' 값을 지정합니다. `sp_changearticle @publication= 'MyPublication', @article= 'MyArticle', @property='pre_creation_cmd', @value='none'`입니다.  
  
#### <a name="to-generate-a-snapshot-for-the-publication"></a>게시에 대한 스냅샷을 생성하려면  
  
1.  **복제** 폴더를 확장한 다음 **로컬 게시** 폴더를 확장합니다.  
  
2.  게시를 마우스 오른쪽 단추로 클릭한 다음 **스냅샷 에이전트 상태 보기**를 클릭합니다.  
  
3.  **스냅샷 에이전트 상태 보기 - \<게시&gt;** 대화 상자에서 **시작**을 클릭합니다.  
  
 스냅샷 에이전트에서 스냅샷 생성을 마치면 "[100%] 17개 아티클의 스냅샷이 생성되었습니다"라는 메시지가 표시됩니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자로의 밀어넣기 구독을 만들 수 있습니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 스크립트 파일에 저장해야 하는 경우에는 파일에 무단으로 액세스하지 못하도록 보안을 설정해야 합니다.  
  
#### <a name="to-create-a-push-subscription-for-a-transactional-or-snapshot-publication-to-a-non-sql-server-subscriber"></a>SQL Server 이외 구독자로의 트랜잭션 또는 스냅샷 게시에 대한 밀어넣기 구독을 만들려면  
  
1.  게시자와 배포자 모두에[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자에 대한 최신 OLE DB 공급자를 설치합니다. OLE DB 공급자에 대한 복제 요구 사항은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md), [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)및 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)를 참조하세요.  
  
2.  게시 데이터베이스의 게시자에서 [sp_helppublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md)을 실행하여 게시에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자를 지원하는지 확인합니다.  
  
    -   **enabled_for_het_sub** 값이 1인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자가 지원됩니다.  
  
    -   **enabled_for_het_sub**의 값이 0이면 `@property`에 **enabled_for_het_sub**, `@value`에 **true**를 지정하고 [sp_changepublication&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md)을 실행합니다.  
  
        > [!NOTE]  
        >  **enabled_for_het_sub** 을 **true**로 변경하기 전에 게시에 대한 기존 구독을 모두 삭제해야 합니다. 게시에서 업데이트 구독도 지원하는 경우 **enabled_for_het_sub** 을 **true** 로 설정할 수 없습니다. **enabled_for_het_sub** 변경은 다른 게시 속성에도 영향을 줍니다. 자세한 내용은 [Non-SQL Server Subscribers](../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)을(를) 참조하세요.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)을 실행합니다. `@publication`, `@subscriber`를 지정하고 `@destination_db`에 `(default destination)` 값, `@subscription_type`에 **push** 값, `@subscriber_type`에 3 값을 지정합니다(OLE DB 공급자 지정).  
  
4.  게시 데이터베이스의 게시자에서 [sp_addpushsubscription_agent&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql.md)를 실행합니다. 다음을 지정합니다.  
  
    -   `@subscriber` 및 `@publication` 매개 변수  
  
    -   `@subscriber_db`에 **(기본 대상)** 값  
  
    -   `@subscriber_provider`, `@subscriber_datasrc`, `@subscriber_location`, `@subscriber_provider_string` 및 `@subscriber_catalog`에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외의 데이터 원본 속성  
  
    -   `@job_login` 및 `@job_password`에 배포자에서 배포 에이전트 실행에 사용되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 자격 증명  
  
       > [!NOTE]  
       > Windows 통합 인증을 사용하여 만든 연결은 항상 `@job_login` 및 `@job_password`로 지정된 Windows 자격 증명을 사용합니다. 배포 에이전트는 항상 Windows 통합 인증을 사용하여 배포자에 대한 로컬 연결을 만듭니다. 기본적으로 에이전트는 Windows 통합 인증을 사용하여 구독자에 연결합니다.  
  
    -   `@subscriber_security_mode`에 **0** 값, `@subscriber_login` 및 `@subscriber_password`에 OLE DB 공급자 로그인 정보  
  
    -   이 구독에 대한 배포 에이전트 작업 일정. 자세한 내용은 [Specify Synchronization Schedules](../../relational-databases/replication/specify-synchronization-schedules.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  게시자에서 원격 배포자를 사용하여 밀어넣기 구독을 만드는 경우 *job_login* 및 *job_password*를 비롯한 모든 매개 변수에 제공된 값이 일반 텍스트로 배포자에게 보내집니다. 이 저장 프로시저를 실행하기 전에 게시자와 해당 원격 배포자 간 연결을 암호화해야 합니다. 자세한 내용은 [데이터베이스 엔진에 암호화 연결 사용&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [IBM DB2 Subscribers](../../relational-databases/replication/non-sql/ibm-db2-subscribers.md)   
 [Oracle Subscribers](../../relational-databases/replication/non-sql/oracle-subscribers.md)   
 [다른 SQL Server 이외 구독자](../../relational-databases/replication/non-sql/other-non-sql-server-subscribers.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
