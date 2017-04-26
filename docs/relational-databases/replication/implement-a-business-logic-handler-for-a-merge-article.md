---
title: "병합 아티클에 대한 비즈니스 논리 처리기 구현 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], business logic handlers
- merge replication business logic handlers [SQL Server replication]
- conflict resolution [SQL Server replication], merge replication
- business logic handlers [SQL Server replication]
- BusinessLogicModule class
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
caps.latest.revision: 44
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1e8b91f880f5cc4f5db69f09fb0bded2b51aaa3c
ms.lasthandoff: 04/11/2017

---
# <a name="implement-a-business-logic-handler-for-a-merge-article"></a>병합 아티클에 대한 비즈니스 논리 처리기 구현
  이 항목에서는 복제 프로그래밍 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 병합 아티클에 대한 비즈니스 논리 처리기를 구현하는 방법에 대해 설명합니다.  
  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 네임스페이스는 병합 복제 동기화 프로세스 중에 발생하는 이벤트를 처리하는 복잡한 비즈니스 논리를 작성할 수 있게 해주는 인터페이스를 구현합니다. 비즈니스 논리 처리기의 메서드는 동기화 중에 복제되는 각 변경된 행에 대해 복제 프로세스에서 호출할 수 있습니다.  
  
 비즈니스 논리 처리기 구현을 위한 일반적인 프로세스는 다음과 같습니다.  
  
1.  비즈니스 논리 처리기 어셈블리를 만듭니다.  
  
2.  어셈블리를 배포자에 등록합니다.  
  
3.  병합 에이전트가 실행되는 서버에 어셈블리를 배포합니다. 끌어오기 구독의 경우 에이전트가 구독자에서 실행되고 밀어넣기 구독의 경우에는 배포자에서 실행됩니다. 웹 동기화를 사용할 경우 에이전트는 웹 서버에서 실행됩니다.  
  
4.  비즈니스 논리 처리기를 사용하는 아티클을 만들거나 기존 아티클을 수정하여 비즈니스 논리 처리기를 사용하도록 합니다.  
  
 사용자가 지정하는 비즈니스 논리 처리기는 동기화되는 모든 행에 대해 실행됩니다. 네트워크 서비스 또는 다른 응용 프로그램에 대한 호출과 복잡한 논리가 성능에 영향을 줄 수 있습니다. 비즈니스 논리 처리기에 대한 자세한 내용은 [병합 동기화 중 비즈니스 논리 실행](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)을 참조하세요.  
  
 **항목 내용**  
  
-   **다음을 사용하여 병합 아티클에 대한 비즈니스 논리 처리기를 구현하려면**  
  
     [복제 프로그래밍](#ReplProg)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="ReplProg"></a> 복제 프로그래밍 사용  
  
#### <a name="to-create-and-deploy-a-business-logic-handler"></a>비즈니스 논리 처리기를 만들고 배포하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio에서 비즈니스 논리 처리기를 구현하는 코드를 포함하는 .NET 어셈블리에 대한 새 프로젝트를 만듭니다.  
  
2.  다음 네임스페이스에 대해 이 프로젝트에 대한 참조를 추가합니다.  
  
    |어셈블리 참조|위치|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM(기본 설치)|  
    |<xref:System.Data>|GAC(.NET Framework 구성 요소)|  
    |<xref:System.Data.Common>|GAC(.NET Framework 구성 요소)|  
  
3.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 클래스를 덮어쓰는 클래스를 추가합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> 속성을 구현하여 처리된 변경 유형을 나타냅니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 클래스의 다음 메서드 중 하나 이상을 덮어씁니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - 동기화 중 데이터 변경 내용이 커밋될 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - DELETE 문 업로드 또는 다운로드 시 오류가 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - DELETE 문 업로드 또는 다운로드 시 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - INSERT 문 업로드 또는 다운로드 시 오류가 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - INSERT 문 업로드 또는 다운로드 시 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - 게시자와 구독자에서 UPDATE 문 충돌이 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - UPDATE 문이 게시자 및 구독자에서 DELETE 문과 충돌할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - UPDATE 문 업로드 또는 다운로드 시 오류가 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - UPDATE 문 업로드 또는 다운로드 시 호출됩니다.  
  
6.  프로젝트를 빌드하여 비즈니스 논리 처리기 어셈블리를 만듭니다.  
  
7.  어셈블리를 병합 에이전트 실행 파일(replmerg.exe)이 있는 디렉터리(기본 설치의 경우 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM)에 배포하거나 .NET GAC(전역 어셈블리 캐시)에 설치합니다. 병합 에이전트 이외의 다른 응용 프로그램에서 어셈블리에 액세스해야 하는 경우 어셈블리를 GAC에만 설치해야 합니다. .NET Framework SDK에 제공되는 전역 어셈블리 캐시 도구(**Gacutil.exe** )를 사용하여 GAC에 어셈블리를 설치할 수 있습니다.  
  
    > [!NOTE]  
    >  비즈니스 논리 처리기는 병합 에이전트가 실행되는 모든 서버에 배포해야 합니다. 여기에는 웹 동기화를 사용할 때 replisapi.dll을 호스팅하는 IIS 서버도 포함됩니다.  
  
#### <a name="to-register-a-business-logic-handler"></a>비즈니스 논리 처리기를 등록하려면  
  
1.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)를 실행하여 어셈블리가 이미 비즈니스 논리 처리기로 등록되어 있지 않은지 확인합니다.  
  
2.  **@article_resolver**에 비즈니스 논리 처리기의 이름, **@is_dotnet_assembly**에 **true** 값, **@dotnet_assembly_name**에 어셈블리 이름, **@dotnet_class_name**에 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>을 재정의하는 정규화된 이름을 지정하여 [sp_registercustomresolver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)를 실행합니다.  
  
    > [!NOTE]  
    >  어셈블리가 병합 에이전트 실행 파일과 같은 디렉터리, 병합 에이전트를 동기적으로 시작하는 응용 프로그램과 같은 디렉터리, 또는 GAC(전역 어셈블리 캐시)에 배포되지 않은 경우 **@dotnet_assembly_name**을 참조하세요. 웹 동기화를 사용하는 경우 웹 서버에서 어셈블리의 위치를 지정해야 합니다.  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>새 테이블 아티클에서 비즈니스 논리 처리기를 사용하려면  
  
1.  **@article_resolver**에 비즈니스 논리 처리기의 이름을 지정하여 [sp_addmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>기존 테이블 아티클에서 비즈니스 논리 처리기를 사용하려면  
  
1.  **@publication**, **@article**, **@property**에 **article_resolver** 값, **@value**에 비즈니스 논리 처리기의 이름을 지정하여 [sp_changemergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다.  
  
###  <a name="TsqlExample"></a> 예(복제 프로그래밍)  
 이 예에서는 감사 로그를 만드는 비즈니스 논리 처리기를 보여 줍니다.  
  
 [!code-cs[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 다음 예에서는 배포자에 비즈니스 논리 처리기 어셈블리를 등록하고 기존 병합 아티클을 변경하여 이 사용자 지정 비즈니스 논리를 사용하도록 합니다.  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../relational-databases/replication/codesnippet/tsql/implement-a-business-log_3.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### <a name="to-create-a-business-logic-handler"></a>비즈니스 논리 처리기를 만들려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio에서 비즈니스 논리 처리기를 구현하는 코드를 포함하는 .NET 어셈블리에 대한 새 프로젝트를 만듭니다.  
  
2.  다음 네임스페이스에 대해 이 프로젝트에 대한 참조를 추가합니다.  
  
    |어셈블리 참조|위치|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM(기본 설치)|  
    |<xref:System.Data>|GAC(.NET Framework 구성 요소)|  
    |<xref:System.Data.Common>|GAC(.NET Framework 구성 요소)|  
  
3.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 클래스를 덮어쓰는 클래스를 추가합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> 속성을 구현하여 처리된 변경 유형을 나타냅니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 클래스의 다음 메서드 중 하나 이상을 덮어씁니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> - 동기화 중 데이터 변경 내용이 커밋될 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> - DELETE 문 업로드 또는 다운로드 시 오류가 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> - DELETE 문 업로드 또는 다운로드 시 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> - INSERT 문 업로드 또는 다운로드 시 오류가 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> - INSERT 문 업로드 또는 다운로드 시 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> - 게시자와 구독자에서 UPDATE 문 충돌이 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> - UPDATE 문이 게시자 및 구독자에서 DELETE 문과 충돌할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> - UPDATE 문 업로드 또는 다운로드 시 오류가 발생할 때 호출됩니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> - UPDATE 문 업로드 또는 다운로드 시 호출됩니다.  
  
    > [!NOTE]  
    >  사용자 지정 비즈니스 논리에 의해 명시적으로 처리되지 않은 모든 아티클 충돌은 아티클에 대한 기본 해결 프로그램에 의해 처리됩니다.  
  
6.  프로젝트를 빌드하여 비즈니스 논리 처리기 어셈블리를 만듭니다.  
  
#### <a name="to-register-a-business-logic-handler"></a>비즈니스 논리 처리기를 등록하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 1단계의 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>을 전달합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A>를 호출하고 반환된 <xref:System.Collections.ArrayList> 개체를 확인하여 어셈블리가 비즈니스 논리 처리기로 이미 등록되어 있지 않은지 확인합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler> 클래스의 인스턴스를 만듭니다. 다음 속성을 지정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> -.NET 어셈블리의 이름. 어셈블리가 병합 에이전트 실행 파일과 같은 디렉터리, 병합 에이전트를 동기적으로 시작하는 응용 프로그램과 같은 디렉터리, 또는 GAC에 배포되지 않은 경우 어셈블리 이름에 전체 경로를 포함해야 합니다. 웹 동기화에서 비즈니스 논리 처리기를 사용하는 경우 어셈블리 이름에 전체 경로를 포함해야 합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> - <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>을 덮어쓰고 비즈니스 논리 처리기를 구현하는 클래스의 정규화된 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> - 비즈니스 논리 처리기에 액세스할 때 사용하는 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> - **true** 값  
  
#### <a name="to-deploy-a-business-logic-handler"></a>비즈니스 논리 처리기를 배포하려면  
  
1.  병합 에이전트가 실행되는 서버에서 비즈니스 논리 처리기가 배포자에 등록될 때 지정된 파일 위치에 어셈블리를 배포합니다. 끌어오기 구독의 경우 에이전트가 구독자에서 실행되고 밀어넣기 구독의 경우에는 배포자에서 실행됩니다. 웹 동기화를 사용할 경우 에이전트는 웹 서버에서 실행됩니다. 비즈니스 논리 처리기가 등록될 때 어셈블리 이름에 전체 경로를 포함하지 않은 경우 병합 에이전트 실행 파일과 같은 디렉터리, 병합 에이전트를 동기적으로 시작하는 응용 프로그램과 같은 디렉터리에 어셈블리를 배포합니다. 동일한 어셈블리를 사용하는 응용 프로그램이 여러 개인 경우 GAC에 어셈블리를 설치할 수 있습니다.  
  
#### <a name="to-use-a-business-logic-handler-with-a-new-table-article"></a>새 테이블 아티클에서 비즈니스 논리 처리기를 사용하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> 클래스의 인스턴스를 만듭니다. 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.Name%2A>에 대한 아티클의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>에 대한 게시의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>에 대한 게시 데이터베이스의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>에 대한 비즈니스 논리 처리기의 이름(<xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>)  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Create%2A> 메서드를 호출합니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### <a name="to-use-a-business-logic-handler-with-an-existing-table-article"></a>기존 테이블 아티클에서 비즈니스 논리 처리기를 사용하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.MergeArticle> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A> 및 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 속성을 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성에 대해 1단계에서 만든 연결을 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 개체 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 3단계에서 아티클 속성이 올바르게 정의되지 않았거나 아티클이 없습니다. 자세한 내용은 [View and Modify Article Properties](../../relational-databases/replication/publish/view-and-modify-article-properties.md)을 참조하세요.  
  
6.  <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>에 대한 비즈니스 논리 처리기의 이름을 설정합니다. 이 이름은 비즈니스 논리 처리기를 등록할 때 지정된 <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> 속성의 값입니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 다음 예는 구독자에서의 삽입, 업데이트, 삭제에 대한 정보를 기록하는 비즈니스 논리 처리기입니다.  
  
 [!code-cs[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 다음 예에서는 배포자에 비즈니스 논리 처리기를 등록합니다.  
  
 [!code-cs[HowTo#rmo_RegisterBLH_10](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 다음 예에서는 비즈니스 논리 처리기를 사용하도록 기존 아티클을 변경합니다.  
  
 [!code-cs[HowTo#rmo_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## <a name="see-also"></a>참고 항목  
 [병합 아티클용 사용자 지정 충돌 해결 프로그램 구현](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [비즈니스 논리 처리기 디버깅&#40;복제 프로그래밍&#41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  
