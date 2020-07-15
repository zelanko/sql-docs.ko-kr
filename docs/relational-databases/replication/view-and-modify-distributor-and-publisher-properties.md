---
title: 배포자와 게시자 속성 보기 및 수정
description: SSMS(SQL Server Management Studio), T-SQL(Transact-SQL) 또는 RMO(복제 관리 개체)를 사용하여 배포자와 게시자의 속성을 수정하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- Distributors [SQL Server replication], modifying
- modifying replication properties, Distributors
- Distributors [SQL Server replication], properties
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: 18b5f2e898638823e20aa237d9bbbc43bb025967
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85720592"
---
# <a name="view-and-modify-distributor-and-publisher-properties"></a>게시자 및 배포자 속성 보기 및 수정
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 배포자 및 게시자 속성을 보고 수정하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 배포자 및 게시자 속성을 보고 수정하려면**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [RMO(복제 관리 개체)](#RMOProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> 권장 사항  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이전 버전을 실행하는 게시자의 경우, **sysadmin** 고정 서버 역할의 사용자가 **구독자** 페이지에서 구독자를 등록할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 더 이상 복제에 대해 구독자를 명시적으로 등록하지 않아도 됩니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
 가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-view-and-modify-distributor-properties"></a>배포자 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 배포자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **배포자 속성**을 클릭합니다.  
  
3.  **배포자 속성 - \<Distributor>** 대화 상자에서 속성을 보고 수정합니다.  
  
    -   배포 데이터베이스의 속성을 보고 수정하려면 대화 상자의 **일반** 페이지에서 해당 데이터베이스에 대한 속성 단추( **...** )를 클릭합니다.  
  
    -   배포자와 관련된 게시자 속성을 보고 수정하려면 대화 상자의**게시자**페이지에서 해당 게시자에 대한 속성 단추 ( **...** )를 클릭합니다.  
  
    -   복제 에이전트에 대한 프로필에 액세스하려면 대화 상자의 **일반** 페이지에서 **프로필 기본값** 단추를 클릭합니다. 자세한 내용은 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)을 참조하세요.  
  
    -   관리 저장 프로시저가 게시자에서 실행되고 배포자에서 정보를 업데이트할 때 사용되는 계정의 암호를 변경하려면 대화 상자의 **게시자** 페이지에서 **암호** 및 **암호 확인** 상자에 새 암호를 입력합니다. 자세한 내용은 [배포자 보안 설정](../../relational-databases/replication/security/secure-the-distributor.md)을 참조하세요.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>게시자 속성을 보고 수정하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 게시자에 연결한 다음 해당 서버 노드를 확장합니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **게시자 속성**을 클릭합니다.  
  
3.  **게시자 속성 - < Publisher >** 대화 상자에서 속성을 보고 수정합니다.  
  
    -   **sysadmin** 고정 서버 역할의 사용자는 **게시 데이터베이스** 페이지에서 복제에 사용할 데이터베이스를 설정할 수 있습니다. 데이터베이스를 설정한다고 해서 그 데이터베이스가 게시되는 것은 아닙니다. 데이터베이스를 설정하면 설정된 데이터베이스에 대한 **db_owner** 고정 데이터베이스 역할의 사용자가 그 데이터베이스에 하나 이상의 게시를 만들 수 있습니다.  
  
4.  필요한 경우 속성을 수정한 다음 **확인**을 클릭합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 게시자와 배포자 속성을 볼 수 있습니다.  
  
#### <a name="to-view-distributor-and-distribution-database-properties"></a>배포자 및 배포 데이터베이스 속성을 보려면  
  
1.  배포자, 배포 데이터베이스 및 작업 디렉터리에 대한 정보를 반환하려면 [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) 를 실행합니다.  
  
2.  지정한 배포 데이터베이스에 대한 속성을 반환하려면 [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) 를 실행합니다.  
  
#### <a name="to-change-distributor-and-distribution-database-properties"></a>배포자 및 배포 데이터베이스 속성을 변경하려면  
  
1.  배포자 속성을 수정하려면 배포자에서 [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) 를 실행합니다.  
  
2.  배포자 데이터베이스 속성을 수정하려면 배포자에서 [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) 를 실행합니다.  
  
3.  배포자 암호를 변경하려면 배포자에서 [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) 를 실행합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정하세요.  
  
4.  배포자를 사용하는 게시자의 속성을 변경하려면 배포자에서 [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) 를 실행합니다.  
  
###  <a name="examples-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 예에서는 배포자와 배포자 데이터베이스에 대한 정보를 반환합니다.  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 다음 예에서는 배포자의 보존 기간, 배포자에 연결할 때 사용되는 암호, 배포자가 여러 복제 에이전트의 상태를 확인하는 간격(하트비트 간격이라고도 함)을 변경합니다.  
  
> [!IMPORTANT]  
>  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정하세요.  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### <a name="to-view-and-modify-distributor-properties"></a>배포자 속성을 보고 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
3.  (옵션) <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> 속성에서 현재 연결된 서버가 배포자인지 확인합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 메서드를 호출하여 서버에서 속성을 가져옵니다.  
  
5.  (옵션) 속성을 변경하려면 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 개체에 설정할 수 있는 하나 이상의 배포자 속성에 새 값을 설정합니다.  
  
6.  (옵션) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 개체의 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 속성이 **true**로 설정되면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출하여 서버의 변경 내용을 커밋합니다.  
  
#### <a name="to-view-and-modify-distribution-database-properties"></a>배포 데이터베이스 속성을 보고 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 클래스의 인스턴스를 만듭니다. 이름 속성을 지정하고 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 메서드를 호출하여 서버에서 속성을 가져옵니다. 이 메서드가 **false**를 반환하는 경우 지정된 이름의 데이터베이스가 서버에 없는 것입니다.  
  
4.  (옵션) 속성을 변경하려면 설정할 수 있는 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 속성 중 하나에 대해 새 값을 설정합니다.  
  
5.  (옵션) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 개체의 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 속성이 **true**로 설정되면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출하여 서버의 변경 내용을 커밋합니다.  
  
#### <a name="to-view-and-modify-publisher-properties"></a>게시자 속성을 보고 수정하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 클래스의 인스턴스를 만듭니다. <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 속성을 지정하고 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 개체를 전달합니다.  
  
3.  (옵션) 속성을 변경하려면 설정할 수 있는 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 속성 중 하나에 대해 새 값을 설정합니다.  
  
4.  (옵션) <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 개체의 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 속성이 **true**로 설정되면 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 메서드를 호출하여 서버의 변경 내용을 커밋합니다.  
  
#### <a name="to-change-the-password-for-the-administrative-connection-from-the-publisher-to-the-distributor"></a>관리 연결의 암호를 게시자에서 배포자로 변경하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 배포자 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 연결로 설정합니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 메서드를 호출합니다. *password* 매개 변수에 대해 새 암호 값을 전달합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](https://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
6.  (옵션) 다음 단계를 수행하여 이 배포자를 사용하는 각 원격 게시자에서 암호를 변경합니다.  
  
    1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 게시자 연결을 만듭니다.  
  
    2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다.  
  
    3.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 6a단계에서 만든 연결로 설정합니다.  
  
    4.  <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 메서드를 호출하여 개체 속성을 가져옵니다.  
  
    5.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 메서드를 호출합니다. *password* 매개 변수에 대해 5단계에서 만든 새 암호 값을 전달합니다.  
  
###  <a name="example-rmo"></a><a name="PShellExample"></a> 예(RMO)  
 이 예에서는 배포 및 배포 데이터베이스 속성을 변경하는 방법을 보여 줍니다.  
  
> [!IMPORTANT]  
>  자격 증명을 코드에 저장하지 않도록 런타임에 새 배포자 암호가 제공됩니다.  
  
 [!code-cs[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## <a name="see-also"></a>참고 항목  
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [게시 및 배포 해제](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)   
 [Replication Management Objects Concepts](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [배포자 및 게시자 정보 스크립트](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [Replication System Stored Procedures Concepts](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [게시자에 대한 정보 보기 및 태스크 수행&#40;복제 모니터&#41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-replication-monitor.md)  
  
  
