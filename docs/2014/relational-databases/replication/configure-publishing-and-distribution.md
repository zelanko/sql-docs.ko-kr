---
title: 게시 및 배포 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/30/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], distribution
- distribution configuration [SQL Server replication]
- publishing [SQL Server replication], configuring
ms.assetid: 3cfc8966-833e-42fa-80cb-09175d1feed7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 905b1ceed2df8afc854ad38ee07d2b21596530f1
ms.sourcegitcommit: 619917a0f91c8f1d9112ae6ad9cdd7a46a74f717
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2019
ms.locfileid: "73882259"
---
# <a name="configure-publishing-and-distribution"></a>게시 및 배포 구성
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 RMO(복제 관리 개체)를 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 게시 및 배포를 구성하는 방법에 대해 설명합니다.  
  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Security"></a> 보안  
 자세한 내용은 [보안 복제 배포](security/view-and-modify-replication-security-settings.md)를 참조 하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 새 게시 마법사나 배포 구성 마법사를 사용하여 배포를 구성합니다. 배포자를 구성한 다음 **배포자 속성 - \<배포자>** 대화 상자에서 속성을 확인하고 수정합니다. **db_owner** 고정 데이터베이스 역할의 멤버가 게시를 만들 수 있도록 배포자를 구성하려는 경우 또는 게시자가 아닌 원격 배포자를 구성하려는 경우 배포 구성 마법사를 사용합니다.  
  
#### <a name="to-configure-distribution"></a>배포를 구성하려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 배포자가 될 서버에 연결한 다음 서버 노드를 확장합니다. 게시자와 배포자가 같은 서버인 경우가 많습니다.  
  
2.  **복제** 폴더를 마우스 오른쪽 단추로 클릭한 다음 **배포 구성**을 클릭합니다.  
  
3.  배포 구성 마법사에 따라 다음을 수행하세요.  
  
    -   배포자를 선택합니다. 로컬 배포자를 사용하려면 **'\<ServerName>'을(를) 자체 배포자로 사용합니다. SQL Server에서 배포 데이터베이스와 로그를 만듭니다.** 를 선택합니다. 원격 배포자를 사용하려면 **다음 서버를 배포자로 사용**을 선택한 다음 서버를 선택합니다. 서버는 미리 배포자로 구성되어 있어야 하며 해당 배포자를 사용하도록 게시자를 설정해야 합니다. 자세한 내용은 [배포자에서 원격 게시자 설정&#40;SQL Server Management Studio&#41;](enable-a-remote-publisher-at-a-distributor-sql-server-management-studio.md)을 참조하세요.  
  
         원격 배포자를 선택할 경우 **관리 암호** 페이지에서 게시자에서 배포자로 연결할 때 사용될 암호를 입력합니다. 이 암호는 원격 배포자에서 게시자를 설정할 때 지정한 암호와 일치해야 합니다.  
  
    -   로컬 배포자에 대해 루트 스냅샷 폴더를 지정합니다. 스냅샷 폴더는 공유하도록 지정된 디렉터리일 뿐이며 이 폴더에 읽기/쓰기 작업을 수행하려면 에이전트에게 충분한 액세스 권한이 있어야 합니다. 이 배포자를 사용하는 각 게시자는 루트 폴더 아래에 폴더를 만들고, 각 게시는 스냅샷 파일을 저장할 게시자 폴더 아래에 폴더를 만듭니다. 폴더의 적절한 보안 유지 방법은 [스냅샷 폴더 보안 설정](security/secure-the-snapshot-folder.md)을 참조하세요.  
  
    -   로컬 배포자에 대해 배포 데이터베이스를 지정합니다. 배포 데이터베이스는 트랜잭션 복제에 대한 모든 유형의 복제 및 트랜잭션에 대한 메타데이터와 기록 데이터를 저장합니다.  
  
    -   필요에 따라 배포자를 사용할 수 있도록 다른 게시자를 설정합니다. 배포자를 사용할 수 있도록 다른 게시자를 설정한 경우 **배포자 암호** 페이지에서 이러한 게시자에서 배포자로 연결할 때 사용될 암호를 입력해야 합니다.  
  
    -   필요에 따라 구성 설정을 스크립팅합니다. 자세한 내용은 [Scripting Replication](scripting-replication.md)을 참조하세요.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 복제 저장 프로시저를 사용하여 복제 게시 및 배포를 프로그래밍 방식으로 구성할 수 있습니다.  
  
#### <a name="to-configure-publishing-using-a-local-distributor"></a>로컬 배포자를 사용하여 게시를 구성하려면  
  
1.  [sp_get_distributor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql)를 실행하여 서버가 이미 배포자로 구성되어 있는지 확인합니다.  
  
    -   결과 집합의 **installed** 값이 **0**인 경우 master 데이터베이스의 배포자에서 [sp_adddistributor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)를 실행합니다.  
  
    -   결과 집합의 **distribution db installed** 값이 **0**인 경우 master 데이터베이스의 배포자에서 [sp_adddistributiondb&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)를 실행합니다. **\@데이터베이스**에 대 한 배포 데이터베이스의 이름을 지정 합니다. 필요에 따라 **\@max_distretention** 에 대해 최대 트랜잭션 보존 기간을 지정 하 고 **\@history_retention**에 대 한 기록 보존 기간을 지정할 수 있습니다. 새 데이터베이스를 만드는 경우 원하는 데이터베이스 속성 매개 변수를 지정합니다.  
  
2.  게시자 이기도 한 배포자에서 **\@working_directory**에 대 한 기본 스냅숏 폴더로 사용할 UNC 공유를 지정 하 [sp_adddistpublisher &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)을 실행 합니다.  
  
3.  게시자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)을 실행합니다. **\@dbname**에 대해 게시할 데이터베이스를 지정 하 고, **\@optname**에 대 한 복제 유형을 지정 하 고, **\@값**에 `true` 값을 지정 합니다.  
  
#### <a name="to-configure-publishing-using-a-remote-distributor"></a>원격 배포자를 사용하여 게시를 구성하려면  
  
1.  [sp_get_distributor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-get-distributor-transact-sql)를 실행하여 서버가 이미 배포자로 구성되어 있는지 확인합니다.  
  
    -   결과 집합의 **installed** 값이 **0**인 경우 master 데이터베이스의 배포자에서 [sp_adddistributor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)를 실행합니다. **\@암호**에 대 한 강력한 암호를 지정 합니다. **distributor_admin** 계정의 이 암호는 배포자에 연결할 때 게시자에서 사용됩니다.  
  
    -   결과 집합의 **distribution db installed** 값이 **0**인 경우 master 데이터베이스의 배포자에서 [sp_adddistributiondb&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)를 실행합니다. **\@데이터베이스**에 대 한 배포 데이터베이스의 이름을 지정 합니다. 필요에 따라 **\@max_distretention** 에 대해 최대 트랜잭션 보존 기간을 지정 하 고 **\@history_retention**에 대 한 기록 보존 기간을 지정할 수 있습니다. 새 데이터베이스를 만드는 경우 원하는 데이터베이스 속성 매개 변수를 지정합니다.  
  
2.  배포자에서 **\@working_directory**에 대 한 기본 스냅숏 폴더로 사용할 UNC 공유를 지정 하 [sp_adddistpublisher &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)을 실행 합니다. 게시자에 연결할 때 배포자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용 하는 경우 **\@security_mode** 에 값 **0** 을 지정 하 고 **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인** 및 **\@암호**에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 로그인 정보를\@합니다.  
  
3.  master 데이터베이스의 게시자에서 [sp_adddistributor&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)를 실행합니다. **\@암호**에 대해 1 단계에서 사용한 강력한 암호를 지정 합니다. 이 암호는 배포자에 연결할 때 게시자에서 사용됩니다.  
  
4.  게시자에서 [sp_replicationdboption&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql)을 실행합니다. **\@dbname**에 대해 게시할 데이터베이스를 지정 하 고, **\@optname**에 대 한 복제 유형을 지정 하 고, **\@값**에 true 값을 지정 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예제에서는 게시 및 배포를 프로그래밍 방식으로 구성하는 방법을 보여 줍니다. 이 예제에서 게시자 및 로컬 배포자로 구성할 서버의 이름은 스크립팅 변수를 사용하여 제공됩니다. 복제 저장 프로시저를 사용하여 복제 게시 및 배포를 프로그래밍 방식으로 구성할 수 있습니다.  
  
 [!code-sql[HowTo#AddDistPub](../../snippets/tsql/SQL15/replication/howto/tsql/adddistpub.sql#adddistpub)]  
  
##  <a name="RMOProcedure"></a> RMO(복제 관리 개체) 사용  
  
#### <a name="to-configure-publishing-and-distribution-on-a-single-server"></a>단일 서버에서 게시 및 배포를 구성하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 서버 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 을 전달합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 클래스의 인스턴스를 만듭니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> 속성을 데이터베이스 이름으로 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 으로 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 메서드를 호출하여 배포자를 설치합니다. 3단계에서 만든 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 개체를 전달합니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 클래스의 인스턴스를 만듭니다.  
  
7.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher>의 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - 게시자의 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> - 5단계에서 만든 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> - 스냅샷 파일에 액세스하는 데 사용되는 공유  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> - 게시자에 연결할 때 사용되는 보안 모드입니다. <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 을 사용하는 것이 좋습니다.  
  
8.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> 메서드를 호출합니다.  
  
#### <a name="to-configure-publishing-and-distribution-using-a-remote-distributor"></a>원격 배포자를 사용하여 게시 및 배포를 구성하려면  
  
1.  <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 원격 배포자 서버에 대한 연결을 만듭니다.  
  
2.  <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 을 전달합니다.  
  
3.  <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 클래스의 인스턴스를 만듭니다.  
  
4.  <xref:Microsoft.SqlServer.Replication.DistributionDatabase.Name%2A> 속성을 데이터베이스 이름으로 설정하고 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 속성을 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 으로 설정합니다.  
  
5.  <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 메서드를 호출하여 배포자를 설치합니다. 원격 배포자에 연결할 때 게시자에서 사용되는 보안 암호 및 3단계에서 만든 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 개체를 지정합니다. 자세한 내용은 [배포자 보안 설정](security/secure-the-distributor.md)을 참조하세요.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 [Windows .NET Framework에서 제공하는](https://go.microsoft.com/fwlink/?LinkId=34733) 암호화 서비스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 사용합니다.  
  
6.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 클래스의 인스턴스를 만듭니다.  
  
7.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher>의 다음 속성을 설정합니다.  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> - 로컬 게시자 서버 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> - 1단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.DistributionDatabase%2A> - 5단계에서 만든 데이터베이스 이름  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.WorkingDirectory%2A> - 스냅샷 파일에 액세스하는 데 사용되는 공유  
  
    -   <xref:Microsoft.SqlServer.Replication.DistributionPublisher.PublisherSecurity%2A> - 게시자에 연결할 때 사용되는 보안 모드입니다. <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 을 사용하는 것이 좋습니다.  
  
8.  <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Create%2A> 메서드를 호출합니다.  
  
9. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 클래스를 사용하여 로컬 게시자 서버에 대한 연결을 만듭니다.  
  
10. <xref:Microsoft.SqlServer.Replication.ReplicationServer> 클래스의 인스턴스를 만듭니다. 9단계에서 만든 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 을 전달합니다.  
  
11. <xref:Microsoft.SqlServer.Replication.ReplicationServer.InstallDistributor%2A> 메서드를 호출합니다. 5단계에서 지정된 원격 배포자 이름 및 원격 배포자 암호를 전달합니다.  
  
    > [!IMPORTANT]  
    >  가능한 경우 런타임 시 사용자에게 보안 자격 증명을 입력하라는 메시지가 표시됩니다. 자격 증명을 저장해야 하는 경우 Windows .NET Framework에서 제공하는 [암호화 서비스](https://go.microsoft.com/fwlink/?LinkId=34733) 를 사용합니다.  
  
###  <a name="PShellExample"></a> 예(RMO)  
 RMO(복제 관리 개체)를 사용하여 프로그래밍 방식으로 복제 게시 및 배포를 구성할 수 있습니다.  
  
 [!code-csharp[HowTo#rmo_AddDistPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_adddistpub)]  
  
 [!code-vb[HowTo#rmo_vb_AddDistPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_adddistpub)]  
  
## <a name="see-also"></a>참고 항목  
 [배포자 및 게시자 속성 보기 및 수정](view-and-modify-distributor-and-publisher-properties.md)   
 [Replication System Stored Procedures Concepts](concepts/replication-system-stored-procedures-concepts.md)   
 [배포 구성](configure-distribution.md)   
 [복제 관리 개체 개념](concepts/replication-management-objects-concepts.md)   
 [AlwaysOn 가용성 그룹 &#40;SQL Server에 대 한 복제 구성&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md) 
  
  
