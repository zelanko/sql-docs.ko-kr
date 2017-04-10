---
title: "병합 아티클 해결 프로그램 지정 | Microsoft Docs"
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
  - "아티클 [SQL Server 복제], 충돌 해결"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
  - "병합 복제 충돌 해결 [SQL Server 복제], 병합 아티클 해결 프로그램"
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 병합 아티클 해결 프로그램 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클 해결 프로그램을 지정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 병합 아티클 해결 프로그램을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   병합 복제에서 다음 유형의 아티클 해결 프로그램을 사용할 수 있습니다.  
  
    -   기본 해결 프로그램. 기본 해결 프로그램의 동작은 구독이 클라이언트 구독인지 서버 구독인지에 따라 달라집니다. 구독 유형을 지정 하는 방법에 대 한 자세한 내용은 참조 [#40;는 병합 구독 유형 및 충돌 해결 우선 순위를 지정 합니다. SQL Server Management Studio & #41;](../../../relational-databases/replication/specify a merge subscription type and conflict resolution priority.md)합니다.  
  
    -   사용자 지정 해결 프로그램 - 관리 코드로 작성된 비즈니스 논리 처리기 또는 사용자 지정 COM 기반 해결 프로그램일 수 있습니다. 자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요. 뿐만 아니라 충돌 하는 행에 대 한 복제 된 각 행에 참조에 대해 실행 되는 사용자 지정 논리를 구현 하는 경우 [병합 아티클에 대 한 비즈니스 논리 처리기를 구현](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)합니다.  
  
    -   표준 COM 기반 해결 프로그램에 포함 되어 있는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]합니다.  
  
-   기본 해결 프로그램 이외의 해결 프로그램을 사용하려면 해당 해결 프로그램을 병합 에이전트를 실행하는 컴퓨터로 복사하고 등록해야 합니다. 비즈니스 논리 처리기를 사용하는 경우에는 해당 프로그램을 게시자에서도 등록해야 합니다. 병합 에이전트는 다음에서 실행될 수 있습니다.  
  
    -   밀어넣기 구독에 대한 배포자  
  
    -   끌어오기 구독에 대한 구독자  
  
    -   웹 동기화를 사용하는 끌어오기 구독에 대한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 서버  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 확인자를 등록 한 후 아티클을에 확인자를 사용 하도록 지정는 **확인자** 탭은 **아티클 속성-\< 문서>** 새 게시 마법사에서 사용할 수 있는 대화 상자 및 **게시 속성-\< 게시>** 대화 상자. 마법사를 사용 하 고 대화 상자에 액세스 하는 방법에 대 한 자세한 내용은 참조 [게시를 만들](../../../relational-databases/replication/publish/create-a-publication.md) 및 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
#### 해결 프로그램을 지정하려면  
  
1.  에 **문서** 새 게시 마법사의 페이지 또는 **게시 속성-\< 게시>** 대화 상자에서 테이블을 선택 합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  에 **아티클 속성-\< 문서>** 페이지는 **확인자** 탭 합니다.  
  
4.  선택 **(배포자에 등록 됨) 사용자 지정 확인자를 사용 하 여**, 목록에서 해결 프로그램을 클릭 합니다.  
  
5.  해결 프로그램 (예: 열 이름)는 입력이 필요한 경우에 지정 된 **해결 프로그램에 필요한 정보를 입력** 텍스트 상자입니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  이 과정을 해결 프로그램이 필요한 각 아티클에서 반복합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### 사용자 지정 충돌 해결 프로그램을 등록하려면  
  
1.  사용자 지정 충돌 해결 프로그램을 등록하려면 다음 유형 중 하나를 만듭니다.  
  
    -   관리 코드 기반 해결 프로그램(비즈니스 논리 처리기). 자세한 내용은 [Implement a Business Logic Handler for a Merge Article](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)을 참조하세요.  
  
    -   저장 프로시저 기반 해결 프로그램 및 COM 기반 해결 프로그램 자세한 내용은 [Implement a Custom Conflict Resolver for a Merge Article](../../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)을 참조하세요.  
  
2.  원하는 해결 프로그램은 이미 등록 한를 확인 하려면 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 모든 데이터베이스의 게시자입니다. 그러면 사용자 지정 해결 프로그램에 대한 설명, 배포자에 등록된 각 COM 기반 해결 프로그램의 CLSID(클래스 식별자) 또는 배포자에 등록된 각 비즈니스 논리 처리기의 관리 어셈블리에 대한 정보가 표시됩니다.  
  
3.  원하는 사용자 지정 해결 프로그램 아직 등록 되지 않은 경우 실행 [sp_registercustomresolver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md) 배포자입니다. 에 대 한 해결 프로그램에 대 한 이름을 지정 **@article_resolver**; 비즈니스 논리 처리기에 대 한 어셈블리의 친숙 한 이름입니다. COM 기반 해결 프로그램 지정에 대 한 DLL의 CLSID **@resolver_clsid**, 비즈니스 논리 처리기에 대 한 값을 지정 하 고 **true** 에 대 한 **@is_dotnet_assembly**, 에 대 한 어셈블리의 이름을 **@dotnet_assembly_name**, 및 재정의 하는 클래스의 정규화 된 이름을 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 에 대 한 **@dotnet_class_name**합니다.  
  
    > [!NOTE]  
    >  비즈니스 논리 처리기 어셈블리를 병합 에이전트 실행 파일과 동일한 디렉터리에 배포 되지 않은, 응용 프로그램과 같은 디렉터리에 동기적으로 시작 하는 병합 에이전트 또는 전역 어셈블리 캐시 (GAC)에 대 한 어셈블리 이름 사용 하 여 전체 경로 지정 해야 하는 경우 **@dotnet_assembly_name**합니다.  
  
4.  COM 기반 해결 프로그램인 경우:  
  
    -   밀어넣기 구독에 대한 배포자 또는 끌어오기 구독에 대한 구독자에 사용자 지정 해결 프로그램 DLL을 복사합니다.  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 사용자 지정 해결 프로그램을 찾을 수 있습니다는 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM 디렉터리입니다.  
  
    -   regsvr32.exe를 사용하여 운영 체제에 사용자 지정 해결 프로그램 DLL을 등록합니다. 예를 들어 명령 프롬프트에서 다음을 실행하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가산성 충돌 해결 프로그램이 등록됩니다.  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  비즈니스 논리 처리기는 해결 프로그램을 사용 하는 경우 병합 에이전트 실행 파일 (replmerg.exe)와 같은 폴더에 어셈블리에 대 한 지정 된 폴더 또는 병합 에이전트를 호출 하는 응용 프로그램 같은 폴더에서 배포는 **@dotnet_assembly_name** 3 단계에서 매개 변수입니다.  
  
    > [!NOTE]  
    >  병합 에이전트 실행 파일의 기본 설치 위치는 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM입니다.  
  
#### 병합 아티클을 정의할 때 사용자 지정 해결 프로그램을 지정하려면  
  
1.  사용자 지정 충돌 해결 프로그램을 사용하려면 위 절차를 사용하여 해결 프로그램을 만들고 등록합니다.  
  
2.  게시자에서 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 원하는 사용자 지정 해결 프로그램의 이름을 확인 하 고는 **값** 결과 집합의 필드입니다.  
  
3.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. 에 대 한 2 단계에서 해결 프로그램의 이름을 지정 **@article_resolver** 를 사용 하 여 사용자 지정 해결 프로그램에 필요한 입력 하 고는 **@resolver_info** 매개 변수입니다. 저장된 프로시저 기반 사용자 지정 확인자에 대 한 **@resolver_info** 저장된 프로시저의 이름입니다. 제공 하는 해결 프로그램에 필요한 입력에 대 한 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)], 참조 [Microsoft COM 기반 해결 프로그램](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)합니다.  
  
#### 기존 병합 아티클에 대한 사용자 지정 해결 프로그램을 지정하거나 변경하려면  
  
1.  아티클에 대해 사용자 지정 해결 프로그램을 정의한 경우 확인 또는 해결 프로그램의 이름을 가져오는 데 실행 [sp_helpmergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)합니다. 문서에 대해 정의 된 사용자 지정 확인자 이면 해당 이름에 표시 됩니다는 **article_resolver** 필드입니다. 해결 프로그램에 제공 된 모든 입력에 표시 되도록는 **resolver_info** 결과 집합의 필드입니다.  
  
2.  게시자에서 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 원하는 사용자 지정 해결 프로그램의 이름을 확인 하 고는 **값** 결과 집합의 필드입니다.  
  
3.  게시 데이터베이스의 게시자에서 실행 [sp_changemergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)합니다. 값을 지정 **article_resolver**, 에 대 한 비즈니스 논리 처리기에 대 한 전체 경로 포함 하 여 **@property**, 2 단계의 원하는 사용자 지정 해결 프로그램의 이름과 **@value**합니다.  
  
4.  사용자 지정 해결 프로그램에 필요한 입력을 변경 하려면 실행 [sp_changemergearticle (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 다시 실행 합니다. 값을 지정 **resolver_info** 에 대 한 **@property** 에 대 한 사용자 지정 해결 프로그램에 필요한 입력 및 **@value**합니다. 저장된 프로시저 기반 사용자 지정 확인자에 대 한 **@resolver_info** 저장된 프로시저의 이름입니다. 필요한 입력에 대 한 자세한 내용은 참조 [Microsoft COM 기반 해결 프로그램](../../../relational-databases/replication/merge/microsoft-com-based-resolvers.md)합니다.  
  
#### 사용자 지정 충돌 해결 프로그램의 등록을 취소하려면  
  
1.  게시자에서 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 제거할 사용자 지정 해결 프로그램의 이름을 확인 하 고는 **값** 결과 집합의 필드입니다.  
  
2.  실행 [sp_unregistercustomresolver (& a) #40; TRANSACT-SQL & #41;](../../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md) 배포자입니다. 1 단계의 사용자 지정 해결 프로그램의 전체 이름을 지정 **@article_resolver**합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 새 아티클을 만들고 충돌이 발생하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 평균 충돌 해결 프로그램을 사용하여 **UnitPrice** 열의 평균을 계산하도록 지정합니다.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_1.sql)]  
  
 이 예에서는 아티클을 변경하여 충돌이 발생한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가산 충돌 해결 프로그램을 사용하여 **UnitsOnOrder** 열의 합을 계산하도록 지정합니다.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../relational-databases/replication/codesnippet/tsql/specify-a-merge-article-_2.sql)]  
  
## 참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)  
  
  