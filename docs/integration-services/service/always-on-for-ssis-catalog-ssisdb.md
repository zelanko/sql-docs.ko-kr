---
title: "Always On for SSIS Catalog (SSISDB) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.ssms.alwayson.f1"
ms.assetid: 7f089455-35ee-4c13-884e-9254b685d07d
caps.latest.revision: 17
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 16
---
# Always On for SSIS Catalog (SSISDB)
  Always On 가용성 그룹 기능은 데이터베이스 미러링에 대한 엔터프라이즈 수준의 대안을 제공하는 고가용성 및 재해 복구 솔루션입니다. 가용성 그룹은 함께 장애 조치(Failover)되는 사용자 데이터베이스(가용성 데이터베이스라고 함)의 불연속 집합에 대한 장애 조치(Failover) 환경을 지원합니다. 자세한 내용은 [Always On 가용성 그룹](https://msdn.microsoft.com/library/hh510230.aspx)을 참조하세요.  
  
 SSIS 카탈로그(SSISDB) 및 해당 콘텐츠(프로젝트, 패키지, 실행 로그 등)에 대한 고가용성을 제공하기 위해 Always On 가용성 그룹에 SSISDB 데이터베이스(다른 사용자 데이터베이스와 동일하게)를 추가할 수 있습니다. 장애 조치(Failover)가 발생하면 보조 노드 중 하나가 자동으로 새 주 노드가 됩니다.  
 
 > [!IMPORTANT]  장애 조치(failover)가 수행될 경우 실행 중이던 패키지가 다시 시작되지 않습니다. 
 
 **항목 내용:**  
  
1.  [필수 구성 요소](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#prereq)  
  
2.  [Always On에 대한 SSIS 지원 구성](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Firsttime)  
  
3.  [가용성 그룹에서 SSISDB 업그레이드](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade)  
  
##  <a name="a-nameprereqa-prerequisites"></a><a name="prereq"></a> 필수 구성 요소  
 SSISDB 데이터베이스에 대한 Always On 지원을 활성화하기 전에 다음 필수 구성 요소를 수행해야 합니다.  
  
1.  Windows 장애 조치(Failover) 클러스터를 설정합니다. 지침은 [Windows Server 2012용 장애 조치(Failover) 클러스터 기능 및 도구 설치](http://blogs.msdn.com/b/clustering/archive/2012/04/06/10291601.aspx) 블로그 게시물을 참조하세요. 모든 클러스터 노드에 기능 및 도구를 설치해야 합니다.  
  
2.  클러스터의 각 노드에 Integration Services 기능이 포함된 SQL Server 2016(SSIS)을 설치합니다.  
  
3.  각 SQL Server 인스턴스에 대해 Always On 기능을 활성화합니다. 자세한 내용은 [Always On 가용성 그룹 활성화](https://msdn.microsoft.com/library/ff878259.aspx) 를 참조하세요.  
  
##  <a name="a-namefirsttimea-configure-ssis-support-for-always-on"></a><a name="Firsttime"></a> Always On에 대한 SSIS 지원 구성  
  
-   [1단계: Integration Services 카탈로그 만들기](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step1)  
  
-   [2단계: Always On 가용성 그룹에 SSISDB 추가](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2)  
  
-   [3단계: Always On에 대한 SSIS 지원 활성화](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)  
  
> [!IMPORTANT]  
>  -   가용성 그룹의 **주 노드** 에서 이러한 단계를 수행해야 합니다.  
> -   Always On 그룹에 SSISDB를 추가한 후 **Always On에 대한 SSIS 지원** 을 활성화해야 합니다.  
  
###  <a name="a-namestep1a-step-1-create-integration-services-catalog"></a><a name="Step1"></a> 1단계: Integration Services 카탈로그 만들기  
  
1.  **SQL Server Management Studio** 를 시작하고 SSISDB에 대한 Always On 고가용성 그룹의 **주 노드** 로 설정하려는 클러스터의 SQL Server 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 서버 노드를 확장하고 **Integration Services 카탈로그** 노드를 마우스 오른쪽 단추로 클릭한 다음 **카탈로그 만들기**를 클릭합니다.  
  
3.  **CLR 통합 사용**을 클릭합니다. 카탈로그에 CLR 저장 프로시저가 사용됩니다.  
  
4.  **SQL Server 시작 시 Integration Services 저장 프로시저 자동 실행** 을 클릭하여 SSIS 서버 인스턴스를 다시 시작할 때마다 [catalog.startup](https://msdn.microsoft.com/library/hh230984.aspx) 저장 프로시저를 실행하도록 지정합니다. 저장 프로시저에서는 SSISDB 카탈로그에 대한 작업의 상태를 유지 관리합니다. SSIS 서버 인스턴스가 다운될 때 실행 중이었던 패키지의 상태를 수정합니다.  
  
5.  **암호**를 입력하고 **확인**을 클릭합니다. 암호는 카탈로그 데이터를 암호화하는 데 사용되는 데이터베이스 마스터 키를 보호합니다. 암호를 안전한 위치에 저장하십시오. 데이터베이스 마스터 키도 백업하는 것이 좋습니다. 자세한 내용은 [Back Up a Database Master Key](https://msdn.microsoft.com/library/aa337546.aspx)을 참조하세요.  
  
###  <a name="a-namestep2a-step-2-add-ssisdb-to-an-always-on-availability-group"></a><a name="Step2"></a> 2단계: Always On 가용성 그룹에 SSISDB 추가  
 Always On 가용성 그룹에 SSISDB 데이터베이스를 추가하는 것은 가용성 그룹에 다른 사용자 데이터베이스를 추가하는 것과 거의 동일합니다. [가용성 그룹 마법사 사용](https://msdn.microsoft.com/library/hh403415.aspx)을 참조하세요.  
  
 **새 가용성 그룹** 마법사의 **데이터베이스 선택** 페이지에서 SSIS 카탈로그를 만드는 동안 지정한 암호를 제공해야 합니다.  
  
 ![New Availability Group](../../integration-services/service/media/ssis-newavailabilitygroup.png "New Availability Group")  
  
###  <a name="a-namestep3a-step-3-enable-ssis-support-for-always-on"></a><a name="Step3"></a> 3단계: Always On에 대한 SSIS 지원 활성화  
 통합 서비스 카탈로그를 만든 후 **통합 서비스 카탈로그** 노드를 마우스 오른쪽 단추로 클릭하고 **Always On 지원 활성화…**를 클릭합니다. 다음 **Always On에 대한 지원 활성화** 대화 상자를 참조해야 합니다. 이 메뉴 항목이 비활성화된 경우 모든 필수 구성 요소를 설치했는지 확인하고 **새로 고침**을 클릭합니다.  
  
 ![Enable Support for AlwaysOn](../../integration-services/service/media/ssis-enablesupportforalwayson.png "Enable Support for AlwaysOn")  
  
> [!WARNING]  
>  Always On에 대한 SSIS 지원을 활성화할 때까지 SSISDB 데이터베이스의 자동 장애 조치(Failover)는 지원되지 않습니다.  
  
 AlwayOn 가용성 그룹에서 새로 추가된 보조 복제본이 테이블에 표시됩니다. 목록에서 각 복제본에 대한 **연결…** 단추를 클릭하고 인증 자격 증명을 입력하여 복제본에 연결합니다. 사용자 계정은 SSIS Always On 지원을 활성화하도록 각 복제본에서 sysadmin 그룹의 구성원이어야 합니다. 각 복제본에 성공적으로 연결한 후 **확인** 을 클릭하여 Always On에 대한 SSIS 지원을 활성화합니다.  
  
##  <a name="a-nameupgradea-upgrading-ssisdb-in-an-availability-group"></a><a name="Upgrade"></a> 가용성 그룹에서 SSISDB 업그레이드  
 이전 버전에서 SQL Server를 업그레이드하고 SSISDB가 Always On 가용성 그룹에 있는 경우 업그레이드는 "Always On 가용성 그룹의 SSISDB 검사" 규칙에 의해 차단될 수 있습니다. 이 차단은 업그레이드는 단일 사용자 모드에서 실행되는 반면 가용성 데이터베이스는 다중 사용자 데이터베이스여야 하기 때문에 발생합니다. 따라서 업그레이드 또는 패치되는 동안 SSISDB를 포함하는 모든 가용성 데이터베이스는 오프라인으로 전환되고 업그레이드 또는 패치되지 않습니다. 업그레이드를 계속하려면 먼저 가용성 그룹에서 SSISDB를 제거한 다음 각 노드를 업그레이드 또는 패치하고 가용성 그룹에 SSISDB를 다시 추가해야 합니다.  
  
 "Always On 가용성 그룹의 SSISDB 검사" 규칙에 의해 차단되는 경우 SQL Server를 업그레이드하려면 다음 단계를 수행해야 합니다.  
  
1.  가용성 그룹에서 SSISDB 데이터베이스를 제거합니다. 자세한 내용은 [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md) 및 [가용성 그룹에서 주 데이터베이스 제거&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/remove-a-primary-database-from-an-availability-group-sql-server.md)를 참조하세요.  
  
2.  업그레이드 마법사에서 **다시 실행**을 클릭합니다. “Always On 가용성 그룹의 SSISDB 검사” 규칙을 통과합니다.  
  
3.  **다음** 을 클릭하여 업그레이드를 계속합니다.  
  
4.  모든 노드를 업그레이드한 후 Always On 가용성 그룹에 SSISDB 데이터베이스를 다시 추가합니다. 자세한 내용은 [가용성 그룹에 데이터베이스 추가&#40;SQL Server&#41;](../../database-engine/availability-groups/windows/add-a-database-to-an-availability-group-sql-server.md)를 참조하세요.  
  
 SQL Server를 업그레이드할 때 차단되지 않고 SSISDB가 Always On 가용성 그룹에 있는 경우 SQL Server 데이터베이스 엔진을 업그레이드한 후 SSISDB를 개별적으로 업그레이드해야 합니다. 다음 절차에 설명된 대로 SSIS 업그레이드 마법사를 사용하여 SSISDB를 업그레이드합니다.  
  
1.  SSISDB가 가용성 그룹의 유일한 데이터베이스인 경우 가용성 그룹에서 SSISDB 데이터베이스를 이동하거나 가용성 그룹을 삭제합니다. 이 작업을 수행하려면 가용성 그룹의 **주 노드** 에서 **SQL Server Management Studio** 를 시작해야 합니다.  
  
2.  모든 **복제본 노드**에서 SSISDB 데이터베이스를 제거합니다.  
  
3.  **주 노드**에서 SSISDB 데이터베이스를 업그레이드합니다. SQL Server Management Studio의**개체 탐색기** 에서 **Integration Services 카탈로그**를 확장하고 **SSISDB**를 마우스 오른쪽 단추로 클릭한 다음 **데이터베이스 업그레이드**를 선택합니다. 데이터베이스를 업그레이드하려면 **SSISDB 업그레이드 마법사** 의 지침을 따릅니다. **주 노드** 에서 **SSIDB 업그레이드 마법사**를 로컬로 시작해야 합니다.  
  
4.  [2단계: Always On 가용성 그룹에 SSISDB 추가](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step2) 의 지침에 따라 가용성 그룹에 SSISDB를 다시 추가합니다.  
  
5.  [3단계: Always On에 대한 SSIS 지원 활성화](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Step3)의 지침을 따릅니다.  
  
  