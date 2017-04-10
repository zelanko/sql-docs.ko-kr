---
title: "게시자 및 배포자 속성 보기 및 수정 | Microsoft Docs"
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
  - "복제 속성 보기"
  - "배포자 [SQL Server 복제], 수정"
  - "복제 속성 수정, 배포자"
  - "배포자 [SQL Server 복제], 속성"
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# 게시자 및 배포자 속성 보기 및 수정
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 배포자 및 게시자 속성을 보고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 배포자 및 게시자 속성을 보고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-    [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]이전 버전을 실행하는 게시자의 경우 **sysadmin** 고정 서버 역할의 사용자는 **구독자** 페이지에서 구독자를 등록할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 더 이상 복제에 대해 구독자를 명시적으로 등록하지 않아도 됩니다.  
  
###  <a name="Security"></a> 보안  
 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### 배포자 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **복제** 폴더를 마우스 클릭 한 다음 **배포자 속성**합니다.  
  
3.  속성 보기 및 수정 된 **배포자 속성-\< 배포자>** 대화 상자입니다.  
  
    -   보고 수정 하는 배포 데이터베이스에 대 한 속성을 속성 단추를 클릭 (**...**) 데이터베이스의 데이터베이스에 **일반** 상자의 대화 상자 페이지입니다.  
  
    -   보고 수정 하는 배포자와 관련 된 게시자 속성을 속성 단추를 클릭 (**...**) 게시자에 대 한는 **게시자** 대화 상자의 페이지입니다.  
  
    -   복제 에이전트에 대한 프로필에 액세스하려면 대화 상자의 **일반** 페이지에서 **프로필 기본값** 단추를 클릭합니다. 자세한 내용은 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하세요.  
  
    -   관리 저장 프로시저가 게시자에서 실행되고 배포자에서 정보를 업데이트할 때 사용되는 계정의 암호를 변경하려면 대화 상자의 **게시자** 페이지에서 **암호** 및 **암호 확인** 상자에 새 암호를 입력합니다. 자세한 내용은 참조 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)합니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
#### 게시자 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  마우스 오른쪽 단추로 클릭는 **복제** 폴더를 마우스 클릭 한 다음 **게시자 속성**합니다.  
  
3.  속성 보기 및 수정 된 **게시자 속성-\< 게시자 >** 대화 상자입니다.  
  
    -   **sysadmin** 고정 서버 역할의 사용자는 **게시 데이터베이스** 페이지에서 복제에 사용할 데이터베이스를 설정할 수 있습니다. 데이터베이스를 설정 하면 해당 데이터베이스에 게시 하지 않습니다. 대신에 모든 사용자를 수 있습니다는 **db_owner** 고정된 데이터베이스 역할에는 데이터베이스에서 하나 이상의 게시를 만들 수 있습니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시자와 배포자 속성을 볼 수 있습니다.  
  
#### 배포자 및 배포 데이터베이스 속성을 보려면  
  
1.  실행 [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) 배포자, 배포 데이터베이스 및 작업 디렉터리에 대 한 정보를 반환 합니다.  
  
2.  실행 [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) 에 지정한 배포 데이터베이스의 속성을 반환 합니다.  
  
#### 배포자 및 배포 데이터베이스 속성을 변경하려면  
  
1.  배포자에서 실행 [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) 배포자 속성을 수정할 수 있습니다.  
  
2.  배포자에서 실행 [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) 배포 데이터베이스 속성을 수정할 수 있습니다.  
  
3.  배포자에서 실행 [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) 배포자 암호를 변경 합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정하세요.  
  
4.  배포자에서 실행 [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) 배포자를 사용 하는 게시자의 속성을 변경 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 예에서는 배포자와 배포자 데이터베이스에 대한 정보를 반환합니다.  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 다음 예에서는 배포자의 보존 기간, 배포자에 연결할 때 사용되는 암호, 배포자가 여러 복제 에이전트의 상태를 확인하는 간격(하트비트 간격이라고도 함)을 변경합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정하세요.  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### 배포자 속성을 보고 수정하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스입니다. 전달 된 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 개체입니다.  
  
3.  (선택 사항) 확인 된 <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> 속성을 현재 연결 된 서버가 배포자 인지 확인 합니다.  
  
4.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 메서드를 서버에서 속성을 가져옵니다.  
  
5.  (선택 사항) 속성을 변경 하려면 배포자 속성에 설정 될 수 있는 하나 이상의 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 개체입니다.  
  
6.  (선택 사항) 하는 경우는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 속성에는 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 개체가로 설정 **true**, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 커밋합니다.  
  
#### 배포 데이터베이스 속성을 보고 수정하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 클래스입니다. Name 속성을 지정 하 고 전달 된 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 개체입니다.  
  
3.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 서버에서 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 지정된 이름의 데이터베이스가 서버에 없는 것입니다.  
  
4.  (선택 사항) 속성을 변경 하려면 중 하나에 대 한 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 속성을 설정할 수 있습니다.  
  
5.  (선택 사항) 하는 경우는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 속성에는 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 개체가로 설정 **true**, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 커밋합니다.  
  
#### 게시자 속성을 보고 수정하려면  
  
1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 클래스입니다. 지정 된 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 속성 및 통과 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 1 단계에서 개체.  
  
3.  (선택 사항) 속성을 변경 하려면 중 하나에 대 한 새 값을 설정 된 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 속성을 설정할 수 있습니다.  
  
4.  (선택 사항) 하는 경우는 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 속성에는 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 개체가로 설정 **true**, 호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 서버에 변경 내용을 커밋합니다.  
  
#### 관리 연결의 암호를 게시자에서 배포자로 변경하려면  
  
1.  사용 하 여 배포자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스입니다.  
  
3.  설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1 단계에서 만든 연결 합니다.  
  
4.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 메서드를 개체의 속성을 가져옵니다.  
  
5.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 메서드. *password* 매개 변수에 대해 새 암호 값을 전달합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](http://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
6.  (옵션) 다음 단계를 수행하여 이 배포자를 사용하는 각 원격 게시자에서 암호를 변경합니다.  
  
    1.  사용 하 여 게시자에 대 한 연결을 만들기는 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스입니다.  
  
    2.  인스턴스를 만들고는 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스입니다.  
  
    3.  설정의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 6a 단계에서에서 만든 연결 합니다.  
  
    4.  호출의 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 메서드를 개체의 속성을 가져옵니다.  
  
    5.  호출 된 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 메서드. *password* 매개 변수에 대해 5단계에서 만든 새 암호 값을 전달합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 이 예에서는 배포 및 배포 데이터베이스 속성을 변경하는 방법을 보여 줍니다.  
  
> [!IMPORTANT]  
>  자격 증명을 코드에 저장하지 않도록 런타임에 새 배포자 암호가 제공됩니다.  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## 참고 항목  
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [복제 관리 개체 개념](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [배포자 및 게시자 정보 스크립트](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [복제 시스템 저장 프로시저 개념](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [정보 보기 및 게시자 및 #40;에 대 한 작업을 수행 합니다. 복제 모니터 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  