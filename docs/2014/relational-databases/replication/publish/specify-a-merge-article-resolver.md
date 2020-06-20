---
title: 병합 아티클 해결 프로그램 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
- merge replication conflict resolution [SQL Server replication], merge article resolvers
ms.assetid: a40083b3-4f7b-4a25-a5a3-6ef67bdff440
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ca32ef4936f31ca5c75dfc2df1eb965d17f7b039
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060389"
---
# <a name="specify-a-merge-article-resolver"></a>병합 아티클 해결 프로그램 지정
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 병합 아티클 해결 프로그램을 지정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
-   **다음을 사용하여 병합 아티클 해결 프로그램을 지정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   병합 복제에서 다음 유형의 아티클 해결 프로그램을 사용할 수 있습니다.  
  
    -   기본 해결 프로그램. 기본 해결 프로그램의 동작은 구독이 클라이언트 구독인지 서버 구독인지에 따라 달라집니다. 구독 유형을 지정하는 방법은 [병합 구독 유형 및 충돌 해결 우선 순위 지정&#40;SQL Server Management Studio&#41;](../specify-a-merge-subscription-type-and-conflict-resolution-priority.md)을 참조하세요.  
  
    -   사용자 지정 해결 프로그램 - 관리 코드로 작성된 비즈니스 논리 처리기 또는 사용자 지정 COM 기반 해결 프로그램일 수 있습니다. 자세한 내용은 [고급 병합 복제 충돌 감지 및 해결](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조 하세요. 충돌하는 행뿐만 아니라 각 복제된 행에 대해서도 실행되는 사용자 지정 논리를 구현해야 하는 경우 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../implement-a-business-logic-handler-for-a-merge-article.md)에서 병합 아티클 해결 프로그램을 지정하는 방법에 대해 설명합니다.  
  
    -   에 포함 된 표준 COM 기반 해결 프로그램입니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   기본 해결 프로그램 이외의 해결 프로그램을 사용하려면 해당 해결 프로그램을 병합 에이전트를 실행하는 컴퓨터로 복사하고 등록해야 합니다. 비즈니스 논리 처리기를 사용하는 경우에는 해당 프로그램을 게시자에서도 등록해야 합니다. 병합 에이전트는 다음에서 실행될 수 있습니다.  
  
    -   밀어넣기 구독에 대한 배포자  
  
    -   끌어오기 구독에 대한 구독자  
  
    -   웹 동기화를 사용하는 끌어오기 구독에 대한 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 서버  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 해결 프로그램을 등록 한 후 아티클이 새 게시 마법사 및 **게시 속성- \<Publication> ** 대화 상자에서 사용할 수 있는 **아티클 속성- \<Article> ** 대화 상자의 **해결** 프로그램 탭에서 해결 프로그램을 사용 하도록 지정 합니다. 마법사 사용 및 대화 상자 액세스에 대한 자세한 내용은 [게시 만들기](create-a-publication.md) 및 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-a-resolver"></a>해결 프로그램을 지정하려면  
  
1.  새 게시 마법사의 **아티클** 페이지 또는 **게시 속성- \<Publication> ** 대화 상자에서 테이블을 선택 합니다.  
  
2.  **아티클 속성**을 클릭한 다음 **선택한 테이블 아티클 속성 설정**을 클릭합니다.  
  
3.  **아티클 속성- \<Article> ** 페이지에서 **해결 프로그램** 탭을 클릭 합니다.  
  
4.  **사용자 지정 해결 프로그램 사용(배포자에 등록됨)** 을 선택하고 목록에서 해결 프로그램을 클릭합니다.  
  
5.  해결 프로그램에 열 이름과 같은 입력값이 필요하면 **해결 프로그램에 필요한 정보 입력** 입력란에 값을 지정합니다.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
7.  이 과정을 해결 프로그램이 필요한 각 아티클에서 반복합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-register-a-custom-conflict-resolver"></a>사용자 지정 충돌 해결 프로그램을 등록하려면  
  
1.  사용자 지정 충돌 해결 프로그램을 등록하려면 다음 유형 중 하나를 만듭니다.  
  
    -   관리 코드 기반 해결 프로그램(비즈니스 논리 처리기). 자세한 내용은 [병합 아티클에 대 한 비즈니스 논리 처리기 구현](../implement-a-business-logic-handler-for-a-merge-article.md)을 참조 하세요.  
  
    -   저장 프로시저 기반 해결 프로그램 및 COM 기반 해결 프로그램 자세한 내용은 [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../implement-a-custom-conflict-resolver-for-a-merge-article.md)을 참조하세요.  
  
2.  원하는 해결 프로그램이 이미 등록되어 있는지 확인하려면 모든 데이터베이스의 게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)를 실행합니다. 그러면 사용자 지정 해결 프로그램에 대한 설명, 배포자에 등록된 각 COM 기반 해결 프로그램의 CLSID(클래스 식별자) 또는 배포자에 등록된 각 비즈니스 논리 처리기의 관리 어셈블리에 대한 정보가 표시됩니다.  
  
3.  원하는 사용자 지정 해결 프로그램이 아직 등록되지 않은 경우 배포자에서 [sp_registercustomresolver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql)를 실행합니다. 에 대 한 해결 프로그램의 이름을 지정 합니다 **@article_resolver** . 비즈니스 논리 처리기의 경우 어셈블리의 이름입니다. COM 기반 해결 프로그램의 경우에는에 대 한 DLL의 CLSID를 지정 하 고, 비즈니스 논리 처리기의 경우에는의 값,에 **@resolver_clsid** `true` 어셈블리 이름,에 **@is_dotnet_assembly** **@dotnet_assembly_name** 대해 재정의 하는 클래스의 정규화 된 이름을 지정 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> **@dotnet_class_name** 합니다.  
  
    > [!NOTE]  
    >  비즈니스 논리 처리기 어셈블리가 병합 에이전트 실행 파일과 동일한 디렉터리에 배포 되지 않은 경우 병합 에이전트를 동기적으로 시작 하는 응용 프로그램과 동일한 디렉터리 또는 GAC (전역 어셈블리 캐시)에서 어셈블리 이름을 사용 하 여 전체 경로를 지정 해야 **@dotnet_assembly_name** 합니다.  
  
4.  COM 기반 해결 프로그램인 경우:  
  
    -   밀어넣기 구독에 대한 배포자 또는 끌어오기 구독에 대한 구독자에 사용자 지정 해결 프로그램 DLL을 복사합니다.  
  
        > [!NOTE]  
        >  [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 사용자 지정 해결 프로그램은 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM 디렉터리에 있습니다.  
  
    -   regsvr32.exe를 사용하여 운영 체제에 사용자 지정 해결 프로그램 DLL을 등록합니다. 예를 들어 명령 프롬프트에서 다음을 실행하면 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가산성 충돌 해결 프로그램이 등록됩니다.  
  
        ```  
        regsvr32 ssradd.dll  
        ```  
  
5.  해결 프로그램이 비즈니스 논리 처리기 인 경우 어셈블리를 병합 에이전트 실행 파일 (replmerg.exe)과 동일한 폴더 또는 병합 에이전트를 호출 하는 응용 프로그램과 같은 폴더에 배포 하거나 **@dotnet_assembly_name** 3 단계에서 매개 변수에 대해 지정 된 폴더에 배포 합니다.  
  
    > [!NOTE]  
    >  병합 에이전트 실행 파일의 기본 설치 위치는 [!INCLUDE[ssInstallPath](../../../includes/ssinstallpath-md.md)]COM입니다.  
  
#### <a name="to-specify-a-custom-resolver-when-defining-a-merge-article"></a>병합 아티클을 정의할 때 사용자 지정 해결 프로그램을 지정하려면  
  
1.  사용자 지정 충돌 해결 프로그램을 사용하려면 위 절차를 사용하여 해결 프로그램을 만들고 등록합니다.  
  
2.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)를 실행하고 결과 집합의 **value** 필드에서 원하는 사용자 지정 해결 프로그램의 이름을 확인합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행합니다. 에 대해 2 단계에서 해결 프로그램의 이름을 지정 하 **@article_resolver** 고 매개 변수를 사용 하 여 사용자 지정 해결 프로그램에 필요한 입력을 지정 **@resolver_info** 합니다. 저장 프로시저 기반 사용자 지정 해결 프로그램의 경우 **@resolver_info** 는 저장 프로시저의 이름입니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)]에서 제공하는 해결 프로그램에 필요한 입력에 대한 자세한 내용은 [Microsoft COM 기반 해결 프로그램](../merge/advanced-merge-replication-conflict-com-based-resolvers.md)을 참조하세요.  
  
#### <a name="to-specify-or-change-a-custom-resolver-for-an-existing-merge-article"></a>기존 병합 아티클에 대한 사용자 지정 해결 프로그램을 지정하거나 변경하려면  
  
1.  아티클에 대한 사용자 지정 해결 프로그램이 정의되어 있는지 확인하려면 [sp_helpmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql)을 실행합니다. 아티클에 대해 정의된 사용자 지정 해결 프로그램이 있으면 **article_resolver** 필드에 이름이 표시됩니다. 해결 프로그램에 제공되는 입력은 모두 결과 집합의 **resolver_info** 에 표시됩니다.  
  
2.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)를 실행하고 결과 집합의 **value** 필드에서 원하는 사용자 지정 해결 프로그램의 이름을 확인합니다.  
  
3.  게시 데이터베이스의 게시자에서 [sp_changemergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 실행합니다. **@property**에 비즈니스 논리 처리기의 전체 경로를 포함하여 **article_resolver** 값을 지정하고, **@value**에는 2단계의 원하는 사용자 지정 해결 프로그램 이름을 지정합니다.  
  
4.  사용자 지정 해결 프로그램에 필요한 입력을 변경하려면 [sp_changemergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)을 다시 실행합니다. **@property**에 **resolver_info** 값, **@value**에 사용자 지정 해결 프로그램에 필요한 입력을 지정합니다. 저장 프로시저 기반 사용자 지정 해결 프로그램의 경우 **@resolver_info** 는 저장 프로시저의 이름입니다. 필요한 입력에 대한 자세한 내용은 [Microsoft COM 기반 해결 프로그램](../merge/advanced-merge-replication-conflict-com-based-resolvers.md)을 참조하세요.  
  
#### <a name="to-unregister-a-custom-conflict-resolver"></a>사용자 지정 충돌 해결 프로그램의 등록을 취소하려면  
  
1.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)를 실행하고 결과 집합의 **value** 필드에서 제거할 사용자 지정 해결 프로그램의 이름을 확인합니다.  
  
2.  배포자에서 [sp_unregistercustomresolver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql)를 실행합니다. 에 대해 1 단계에서 가져온 사용자 지정 해결 프로그램의 전체 이름을 지정 **@article_resolver** 합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 새 아티클을 만들고 충돌이 발생하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 평균 충돌 해결 프로그램을 사용하여 **UnitPrice** 열의 평균을 계산하도록 지정합니다.  
  
 [!code-sql[HowTo#sp_addmerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_addmerge_resolver)]  
  
 이 예에서는 아티클을 변경하여 충돌이 발생한 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 가산 충돌 해결 프로그램을 사용하여 **UnitsOnOrder** 열의 합을 계산하도록 지정합니다.  
  
 [!code-sql[HowTo#sp_changemerge_resolver](../../../snippets/tsql/SQL15/replication/howto/tsql/mergearticleresolvers.sql#sp_changemerge_resolver)]  
  
## <a name="see-also"></a>참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../implement-a-business-logic-handler-for-a-merge-article.md)  
  
  
