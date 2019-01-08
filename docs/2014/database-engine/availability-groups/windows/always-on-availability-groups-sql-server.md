---
title: Always On 가용성 그룹(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], about
- secondary replicas, see Availability Groups [SQL Server]
- availability [SQL Server]
- AlwaysOn [SQL Server], see Availability Groups [SQL Server]
- Availability Groups [SQL Server]
ms.assetid: aa427606-8422-4656-b205-c9e665ddc8c1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f1e86eec76a94a3858ede48fc0fb1b0703de4508
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356251"
---
# <a name="always-on-availability-groups-sql-server"></a>Always On 가용성 그룹(SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 기능은 데이터베이스 미러링에 대한 엔터프라이즈 수준의 대안을 제공하는 고가용성 및 재해 복구 솔루션입니다. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]에 도입된 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 엔터프라이즈 사용자 데이터베이스 집합의 가용성을 극대화합니다. *가용성 그룹* 은 함께 장애 조치(Failover)되는 사용자 데이터베이스( *가용성 데이터베이스*라고 함)의 불연속 집합에 대한 장애 조치(Failover) 환경을 지원합니다. 가용성 그룹은 읽기/쓰기 주 데이터베이스 집합과 1~8개의 해당 보조 데이터베이스 집합을 지원합니다. 필요한 경우 보조 데이터베이스에 대해 읽기 전용 액세스를 설정하거나 일부 백업 작업에 사용되도록 설정할 수 있습니다.  
  
 가용성 그룹은 가용성 복제본의 수준에서 장애 조치(Failover)됩니다. 따라서 데이터 파일 손실, 데이터베이스 삭제, 트랜잭션 로그 손상 등으로 인해 주의 대상 데이터베이스가 발생할 경우 이러한 데이터베이스 문제로는 장애 조치(Failover)가 수행되지 않습니다.  
  
  
##  <a name="Benefits"></a> 이점  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 에서는 데이터베이스 가용성을 향상시키고 리소스 사용을 개선시켜 주는 다양한 옵션을 제공합니다. 주요 구성 요소는 다음과 같습니다.  
  
-   최대 9개의 가용성 복제본을 지원합니다. *가용성 복제본* 은 SQL Server의 특정 인스턴스에 의해 호스팅되고 가용성 그룹에 속하는 각 가용성 데이터베이스의 로컬 복사본을 유지 관리하는 가용성 그룹 인스턴스화입니다. 각 가용성 그룹은 하나의 주 복제본과 최대 8개의 보조 복제본을 지원합니다. 자세한 내용은 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)를 참조하세요.  
  
    > [!IMPORTANT]  
    >  각 가용성 복제본은 단일 WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터의 서로 다른 노드에 있어야 합니다. 필수 구성 요소, 제한 사항 및 가용성 그룹에 대 한 권장 사항에 대 한 자세한 내용은 참조 하세요. [필수 구성 요소, 제한 사항 및 Always On 가용성 그룹;에 대 한 권장 사항 SQL Server; ](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   다음과 같은 대체 가용성 모드를 지원합니다.  
  
    -   *비동기-커밋 모드*. 이 가용성 모드는 여러 가용성 복제본이 상당한 거리를 두고 분산되어 있는 경우에 적합한 재해 복구 솔루션입니다.  
  
    -   *동기-커밋 모드*. 이 가용성 모드는 트랜잭션 대기 시간이 증가하더라도 성능에 비해 고가용성 및 데이터 보호를 강조합니다. 가용성 그룹 하나는 현재 주 복제본을 포함하여 최대 3개의 동기-커밋 가용성 복제본을 지원할 수 있습니다.  
  
     자세한 내용은 참조 하세요. [ 가용성 모드가 있습니다. Always On 가용성 그룹입니다. ](availability-modes-always-on-availability-groups.md).  
  
-   여러 형태의 가용성 그룹 장애 조치 지원: 자동 장애 조치(Failover), 계획된 수동 장애 조치(Failover)(간단히 "수동 장애 조치(Failover)"라고 함), 강제 수동 장애 조치(Failover)(간단히 "강제 장애 조치(Failover)"라고 함) 등 자세한 내용은 참조 하세요. [장애 조치 및 장애 조치 모드가 있습니다. Always On 가용성 그룹입니다. ](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   다음과 같은 활성 보조 기능 중 하나 또는 둘 모두를 지원하도록 가용성 복제본을 구성할 수 있습니다.  
  
    -   읽기 전용 연결 액세스. 복제본이 보조 복제본으로 실행되는 경우 복제본에 읽기 전용으로 연결하여 해당 데이터베이스에 액세스하고 데이터베이스를 읽을 수 있습니다. 자세한 내용은 참조 하세요. [활성 보조: 읽기 가능한 보조 복제본입니다. Always On 가용성 그룹](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
    -   복제본이 보조 복제본으로 실행되는 경우 해당 데이터베이스에서 백업 작업 수행. 자세한 내용은 참조 하세요. [활성 보조: 보조 복제본에 백업](https://msdn.microsoft.com/library/ff878253.aspx)).  
  
     활성 보조 기능을 사용하면 IT 효율성을 향상시키고 보다 효율적인 보조 하드웨어 리소스 활용을 통해 비용을 절감할 수 있습니다. 또한 읽기 전용 애플리케이션 및 백업 작업을 보조 복제본으로 오프로드하면 주 복제본의 성능이 향상될 수 있습니다.  
  
-   각 가용성 그룹에 대해 가용성 그룹 수신기를 지원합니다. *가용성 그룹 수신기* 는 AlwaysOn 가용성 그룹의 주 복제본 또는 보조 복제본에 있는 데이터베이스에 액세스하기 위해 클라이언트가 연결할 수 있는 서버 이름입니다. 가용성 그룹 수신기는 들어오는 연결을 주 복제본이나 읽기 전용 보조 복제본에 전달합니다. 수신기는 가용성 그룹이 장애 조치(Failover)된 후 빠른 애플리케이션 장애 조치(Failover)를 제공합니다. 자세한 내용은 참조 하세요. [가용성 그룹 수신기, 클라이언트 연결 및 응용 프로그램 장애 조치 합니다. SQL Server; ](../../listeners-client-connectivity-application-failover.md).  
  
-   가용성 그룹 장애 조치(Failover)를 효율적으로 제어할 수 있도록 유연한 장애 조치(Failover) 정책을 지원합니다. 자세한 내용은 참조 하세요. [장애 조치 및 장애 조치 모드가 있습니다. Always On 가용성 그룹입니다. ](failover-and-failover-modes-always-on-availability-groups.md).  
  
-   페이지 손상 방지를 위해 자동 페이지 복구를 지원합니다. 자세한 내용은 [자동 페이지 복구 &#40;가용성 그룹 및 데이터베이스 미러링;](../../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)합니다.  
  
-   안정적인 고성능 전송을 위한 암호화 및 압축을 지원합니다.  
  
-   다음을 비롯한 가용성 그룹을 간단하게 배포 및 관리할 수 있는 통합된 도구 집합을 제공합니다.  
  
    -   [!INCLUDE[tsql](../../../includes/tsql-md.md)] DDL 문. 자세한 내용은 참조 하세요. [Always On 가용성 그룹;에 대 한 개요의 TRANSACT-SQL 문 SQL Server; ](transact-sql-statements-for-always-on-availability-groups.md).  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 도구  
  
        -   [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] 는 가용성 그룹을 만들고 구성합니다. 일부 환경에서는 이 마법사가 보조 데이터베이스를 자동으로 준비하고 각 보조 데이터베이스에 대한 데이터 동기화를 시작할 수 있습니다. 자세한 내용은 참조 하세요. [새 가용성 그룹 대화 상자의 사용 SQL Server Management Studio; ](use-the-new-availability-group-dialog-box-sql-server-management-studio.md).  
  
        -   [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)]는 기존 가용성 그룹에 하나 이상의 주 데이터베이스를 추가합니다. 일부 환경에서는 이 마법사가 보조 데이터베이스를 자동으로 준비하고 각 보조 데이터베이스에 대한 데이터 동기화를 시작할 수 있습니다. 자세한 [가용성 그룹에 데이터베이스 추가 마법사 사용(SQL Server)](availability-group-add-database-to-group-wizard.md)을 참조하세요.  
  
        -   [!INCLUDE[ssAoAddRepWiz](../../../includes/ssaoaddrepwiz-md.md)] 는 기존 가용성 그룹에 하나 이상의 보조 복제본을 추가합니다. 일부 환경에서는 이 마법사가 보조 데이터베이스를 자동으로 준비하고 각 보조 데이터베이스에 대한 데이터 동기화를 시작할 수 있습니다. 자세한 내용은 참조 하세요. [추가 복제본을 가용성 그룹 마법사 사용 SQL Server Management Studio; ](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md).  
  
        -   [!INCLUDE[ssAoFoAgWiz](../../../includes/ssaofoagwiz-md.md)]는 가용성 그룹에 대한 수동 장애 조치(Failover)를 시작합니다. 장애 조치(Failover) 대상으로 지정하는 보조 복제본의 구성과 상태에 따라 마법사에서 계획된 수동 장애 조치(Failover) 또는 강제 수동 장애 조치(Failover)를 수행할 수 있습니다. 자세한 내용은 참조 하세요. [실패를 통해 가용성 그룹 마법사 사용; SQL Server Management Studio; ](use-the-fail-over-availability-group-wizard-sql-server-management-studio.md).  
  
    -   [!INCLUDE[ssAoDash](../../../includes/ssaodash-md.md)] 에서는 AlwaysOn 가용성 그룹, 가용성 복제본 및 가용성 데이터베이스를 모니터링하고 AlwaysOn 정책에 대한 결과를 평가합니다. 자세한 내용은 참조 하세요. [; AlwaysOn 대시보드 사용 SQL Server Management Studio; ](use-the-always-on-dashboard-sql-server-management-studio.md).  
  
    -   개체 탐색기 정보 창에 기존 가용성 그룹에 대한 기본 정보가 표시됩니다. 자세한 내용은 참조 하세요. [모니터 가용성 그룹에 개체 탐색기 정보를 사용 하 여 SQL Server Management Studio; ](use-object-explorer-details-to-monitor-availability-groups.md).  
  
    -   PowerShell cmdlet. 자세한 내용은 참조 하세요. [Always On 가용성 그룹;에 대 한 개요의 PowerShell Cmdlet SQL Serve; ](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md).  
  
##  <a name="TermsAndDefinitions"></a> 용어 및 정의  
 가용성 그룹  
 함께 장애 조치(failover)되는 데이터베이스의 집합인 *가용성 데이터베이스*의 컨테이너입니다.  
  
 가용성 데이터베이스  
 가용성 그룹에 속하는 데이터베이스입니다. 가용성 그룹은 각 가용성 데이터베이스에 대해 하나의 읽기/쓰기 복사본( *주 데이터베이스*)과 1~8개의 읽기 전용 복사본(*보조 데이터베이스*)을 유지 관리합니다.  
  
 주 데이터베이스  
 가용성 데이터베이스의 읽기/쓰기 복사본입니다.  
  
 보조 데이터베이스  
 가용성 데이터베이스의 읽기 전용 복사본입니다.  
  
 가용성 복제본  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 특정 인스턴스에 의해 호스팅되고 가용성 그룹에 속하는 각 가용성 데이터베이스의 로컬 복사본을 유지 관리하는 가용성 그룹 인스턴스화입니다. 가용성 복제본은 하나의 *주 복제본* 과 1~8개의 *보조 복제본*이라는 두 가지 유형이 있습니다.  
  
 주 복제본  
 클라이언트에서 주 데이터베이스에 읽기/쓰기 연결을 할 수 있도록 주 데이터베이스를 설정하고 각 주 데이터베이스에 대한 트랜잭션 로그 레코드를 모든 보조 복제본에 보내는 가용성 복제본입니다.  
  
 보조 복제본  
 각 가용성 데이터베이스의 보조 복사본을 유지 관리하고 가용성 그룹에 대한 잠재적인 장애 조치(Failover) 대상 역할을 하는 가용성 복제본입니다. 필요에 따라 보조 복제본은 보조 데이터베이스에 대한 읽기 전용 액세스와 보조 데이터베이스에 백업을 만드는 것을 지원할 수 있습니다.  
  
 가용성 그룹 수신기  
 Always On 가용성 그룹의 주 복제본 또는 보조 복제본에 있는 데이터베이스에 액세스하기 위해 클라이언트가 연결할 수 있는 서버 이름입니다. 가용성 그룹 수신기는 들어오는 연결을 주 복제본이나 읽기 전용 보조 복제본에 전달합니다.  
  
> [!NOTE]  
>  자세한 내용은 참조 하세요. [AlwaysOn 가용성 그룹 개요; SQL Serve; ](overview-of-always-on-availability-groups-sql-server.md).  
  
##  <a name="Interoperability"></a> 다른 데이터베이스 엔진 기능과의 상호 운용성 및 공존성  
 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 다음 기능 또는 구성 요소와 함께 사용할 수 있습니다.  
  
-   [변경 데이터 캡처; 정보 SQL Server;](../../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
-   [변경 내용 추적; 정보 SQL Serve;](../../../relational-databases/track-changes/about-change-tracking-sql-server.md)  
  
-   [포함된 데이터베이스](../../../relational-databases/databases/contained-databases.md)  
  
-   [데이터베이스 암호화](../../../relational-databases/security/encryption/transparent-data-encryption.md)  
  
-   [데이터베이스 스냅숏](database-snapshots-with-always-on-availability-groups-sql-server.md)  
  
-   [FILESTREAM](../../../relational-databases/blob/filestream-sql-server.md)  
  
-   [FileTable](../../../relational-databases/blob/filetables-sql-server.md)  
  
-   [로그 전달](../../log-shipping/about-log-shipping-sql-server.md)  
  
-   [RBS(Remote Blob Store)](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
-   [복제](../../install-windows/install-sql-server-replication.md)  
  
-   [Service Broker](../../configure-windows/sql-server-service-broker.md)  
  
-   [SQL Server 에이전트](../../../ssms/agent/sql-server-agent.md)  
  
-   [Reporting Services](reporting-services-with-always-on-availability-groups-sql-server.md)  
  
> [!WARNING]  
>  제한 사항 및 사용 하 여 다른 기능을 사용 하는 것에 대 한 제한 사항에 대 한 자세한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]를 참조 하세요 [Always On 가용성 그룹: 상호 운용성; SQL Server; ](always-on-availability-groups-interoperability-sql-server.md).  
  
##  <a name="RelatedTasks"></a> 관련 작업  
  
-   [시작 Always On 가용성 그룹입니다. SQL Server;](getting-started-with-always-on-availability-groups-sql-server.md)  
  
##  <a name="RelatedContent"></a> 관련 내용  
  
-   **블로그:**  
  
     [SQL Server Always On 팀 블로그: 공식 SQL Server AlwaysOn 팀 블로그](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 엔지니어 블로그](https://blogs.msdn.com/b/psssql/)  
  
-   **비디오:**  
  
     [Microsoft SQL Server 코드 이름된 "Denali" Always On 시리즈, 1 부: 차세대 고가용성 솔루션 소개](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI302)  
  
     [Microsoft SQL Server 코드 이름된 "Denali" Always On 시리즈, 2 부: AlwaysOn을 사용 하 여 중요 업무용 고가용성 솔루션 빌드](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2011/DBI404)  
  
-   **백서:**  
  
     [고가용성 및 재해 복구를 위한 Microsoft SQL Server Always On 솔루션 가이드](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
  
  
## <a name="see-also"></a>관련 항목  
 [Always On 가용성 그룹; 개요 SQL Server;](overview-of-always-on-availability-groups-sql-server.md)   
 [필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Always On 가용성 그룹;에 대 한 서버 인스턴스 구성 SQL Server;](always-on-availability-groups-sql-server.md)   
 [가용성 그룹의 생성 및 구성 SQL Server;](creation-and-configuration-of-availability-groups-sql-server.md)   
 [가용성 그룹을 관리 SQL Server;](administration-of-an-availability-group-sql-server.md)   
 [가용성 그룹 모니터링&#40;SQL Server&#41;](monitoring-of-availability-groups-sql-server.md)   
 [Always On 가용성 그룹;에 대 한 TRANSACT-SQL 문 개요 SQL Server;](transact-sql-statements-for-always-on-availability-groups.md)   
 [AlwaysOn 가용성 그룹에 대 한 PowerShell Cmdlet 개요 SQL Server;](overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)  
  
  
