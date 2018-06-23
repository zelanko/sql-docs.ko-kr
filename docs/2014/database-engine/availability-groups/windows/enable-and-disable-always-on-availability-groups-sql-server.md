---
title: AlwaysOn 가용성 그룹 (SQL Server) 활성화 및 비활성화 | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], server instance
- Availability Groups [SQL Server], deploying
- Availability Groups [SQL Server], disabling
- Availability Groups [SQL Server], enabling
ms.assetid: 7c326958-5ae9-4761-9c57-905972276a8f
caps.latest.revision: 58
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.openlocfilehash: 1851a658ad1c955bf321b985b4d848767e8b0d69
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090520"
---
# <a name="enable-and-disable-alwayson-availability-groups-sql-server"></a>AlwaysOn 가용성 그룹 활성화 및 비활성화(SQL Server)
  먼저 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 을 사용하도록 설정해야만 서버 인스턴스에서 가용성 그룹을 사용할 수 있습니다. 가용성 그룹을 만들고 구성하려면 먼저 하나 이상의 가용성 그룹에 대한 가용성 복제본을 호스팅할 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 각 인스턴스에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능을 사용하도록 설정해야 합니다.  
  
> [!IMPORTANT]  
>  WSFC 클러스터를 삭제한 다음 다시 만들려는 경우 원본 WSFC 클러스터에서 가용성 복제본을 호스팅한 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 의 각 인스턴스에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 기능을 사용하지 않도록 설정한 후 다시 사용하도록 설정해야 합니다.  
  
-   **시작하기 전 주의 사항:**  
  
     [필수 구성 요소](#Prerequisites)  
  
     [보안](#Security)  
  
-   **방법:**  
  
    -   [있는지 여부를 AlwaysOn 가용성 그룹을 사용할 수 확인](#IsEnabled)  
  
    -   [AlwaysOn 가용성 그룹 사용](#EnableAOAG)  
  
    -   [AlwaysOn 가용성 그룹을 사용 하지 않도록 설정](#DisableAOAG)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Prerequisites"></a> AlwaysOn 가용성 그룹 사용을 위한 필수 구성 요소  
  
-   서버 인스턴스는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 있어야 합니다.  
  
-   서버 인스턴스는 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하는 SQL Server 버전을 실행해야 합니다. 자세한 내용은 [Features Supported by the Editions of SQL Server 2014](../../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)을 참조하세요.  
  
-   한 번에 한 서버 인스턴스에서만 AlwaysOn 가용성 그룹을 사용하도록 설정합니다. AlwaysOn 가용성 그룹을 활성화 한 다음 될 때까지 기다렸다가 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 를 다른 서버 인스턴스로 진행 하기 전에 서비스가 다시 시작 합니다.  
  
 추가 필수 구성 요소를 만들고 가용성 그룹 구성에 대 한 정보를 참조 하십시오. [필수 구성 요소, 제한 사항 및 AlwaysOn 가용성 그룹에 대 한 권장 사항 &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)합니다.  
  
###  <a name="Security"></a> 보안  
 AlwaysOn 가용성 그룹의 인스턴스에서 사용 하는 동안 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], 서버 인스턴스가 WSFC 클러스터의 모든 권한을 가집니다.  
  
####  <a name="Permissions"></a> Permissions  
 로컬 컴퓨터 **관리자** 그룹의 멤버 자격과 WSFC 클러스터에 대한 모든 권한이 필요합니다. Powershell을 사용하여 AlwaysOn을 사용하도록 설정하는 경우 **관리자 권한으로 실행** 옵션을 사용하여 명령 프롬프트 창을 엽니다.  
  
 Active Directory 개체 만들기 및 개체 관리 권한이 필요합니다.  
  
##  <a name="IsEnabled"></a> 있는지 여부를 AlwaysOn 가용성 그룹을 사용할 수 확인  
  
-   다른 도구는 [SQL Server Management Studio](#SSMS1Procedure)  
  
-   [Transact-SQL](#Tsql1Procedure)  
  
-   [PowerShell](#PowerShell1Procedure)  
  
###  <a name="SSMS1Procedure"></a> SQL Server Management Studio 사용  
 **AlwaysOn 가용성 그룹을 사용할 수 있는지 여부를 확인 하려면**  
  
1.  개체 탐색기에서 서버 인스턴스를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **서버 속성** 대화 상자에서 **일반** 페이지를 클릭합니다. **HADR 사용** 속성이 다음 값 중 하나로 표시됩니다.  
  
    -   **True**, AlwaysOn 가용성 그룹을 사용할 수 있는 경우  
  
    -   **False**, AlwaysOn 가용성 그룹을 사용할 수 없는 경우  
  
###  <a name="Tsql1Procedure"></a> Transact-SQL 사용  
 **AlwaysOn 가용성 그룹을 사용할 수 있는지 여부를 확인 하려면**  
  
1.  다음 [SERVERPROPERTY](/sql/t-sql/functions/serverproperty-transact-sql) 문을 사용합니다.  
  
    ```  
    SELECT SERVERPROPERTY ('IsHadrEnabled');  
    ```  
  
     `IsHadrEnabled` 서버 속성의 설정은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스에서 AlwaysOn 가용성 그룹을 사용할 수 있는지 여부를 다음과 같이 나타냅니다.  
  
    -   경우 `IsHadrEnabled` = 1, AlwaysOn 가용성 그룹을 사용할 수 있습니다.  
  
    -   경우 `IsHadrEnabled` = 0, AlwaysOn 가용성 그룹을 사용할 수 없습니다.  
  
    > [!NOTE]  
    >  에 대 한 자세한 내용은 `IsHadrEnabled` 서버 속성 참조 [SERVERPROPERTY &#40;TRANSACT-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)합니다.  
  
###  <a name="PowerShell1Procedure"></a> PowerShell 사용  
 **AlwaysOn 가용성 그룹을 사용할 수 있는지 여부를 확인 하려면**  
  
1.  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 사용할 수 있는지 여부를 확인하려는 서버 인스턴스에 대해 기본값(`cd`)을 설정합니다.  
  
2.  다음 PowerShell `Get-Item` 명령을 입력합니다.  
  
    ```  
    PS SQLSERVER:\SQL\NODE1\DEFAULT> get-item . | select IsHadrEnabled  
    ```  
  
    > [!NOTE]  
    >  Cmdlet의 구문을 보려면에서 사용 하 여는 `Get-Help` cmdlet에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경입니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
##  <a name="EnableAOAG"></a> AlwaysOn 가용성 그룹 사용  
 **AlwaysOn을 사용 하도록 설정 하려면 사용 하 여:**  
  
-   [SQL Server 구성 관리자](#SQLCM2Procedure)  
  
-   [PowerShell](#PScmd2Procedure)  
  
###  <a name="SQLCM2Procedure"></a> SQL Server 구성 관리자 사용  
 **AlwaysOn 가용성 그룹을 사용 하도록 설정 하려면**  
  
1.  호스팅하는 Windows Server 장애 조치 클러스터링 (WSFC) 노드에 연결 하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 AlwaysOn 가용성 그룹을 사용 하도록 설정 합니다.  
  
2.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
3.  **SQL Server 구성 관리자**, 클릭 **SQL Server 서비스**, SQL Server를 마우스 오른쪽 단추로 클릭 (**<*`instance name`*>)** 여기서 **< *`instance name`* >** AlwaysOn 가용성 그룹을 사용 하도록 설정할 로컬 서버 인스턴스의 이름 및 클릭 **속성입니다.**  
  
4.  **AlwaysOn 고가용성** 탭을 선택합니다.  
  
5.  **Windows 장애 조치(failover) 클러스터 이름** 필드에 로컬 장애 조치(failover) 클러스터의 이름이 포함되어 있는지 확인합니다. 이 필드가 비어 있으면 이 서버 인스턴스에서 현재 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하지 않는 것입니다. 로컬 컴퓨터가 클러스터 노드가 아니거나 WSFC 클러스터가 종료되었거나 이 버전의 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]을 지원하지 않습니다.  
  
6.  **AlwaysOn 가용성 그룹 사용** 확인란을 선택하고 **확인**을 클릭합니다.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자가 변경 내용을 저장합니다. 그런 다음 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 수동으로 다시 시작해야 합니다. 이렇게 하면 비즈니스 요구 사항에 가장 적합한 다시 시작 시간을 선택할 수 있습니다. 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 시작 하면 AlwaysOn을 사용할 수 및 `IsHadrEnabled` 서버 속성이 1로 설정 됩니다.  
  
###  <a name="PScmd2Procedure"></a> SQL Server PowerShell 사용  
 **AlwaysOn을 사용 하도록 설정 하려면**  
  
1.  디렉터리를 AlwaysOn 가용성 그룹을 사용하도록 설정할 서버 인스턴스로 변경합니다(`cd`).  
  
2.  사용 하 여는 `Enable-SqlAlwaysOn` cmdlet AlwaysOn 가용성 그룹을 사용 하도록 합니다.  
  
     Cmdlet의 구문을 보려면에서 사용 하 여는 `Get-Help` cmdlet에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경입니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
    > [!NOTE]  
    >  제어 하는 방법에 대 한 내용은 여부는 `Enable-SqlAlwaysOn` cmdlet를 다시 시작는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 참조 하십시오 [않습니다 Cmdlet를 다시 시작 경우 SQL Server 서비스?](#WhenCmdletRestartsSQL)이 항목의 뒷부분에 나오는 합니다.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
####  <a name="ExmplEnable-SqlHadrServic"></a>예: Enable-SqlAlwaysOn  
 다음 PowerShell 명령을 사용하면 SQL Server 인스턴스( [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Computer*Instance*\\ *)에서*을 사용할 수 있습니다.  
  
```  
Enable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
```  
  
##  <a name="DisableAOAG"></a> AlwaysOn 가용성 그룹을 사용 하지 않도록 설정  
  
-   **AlwaysOn 해제 하기 전에:**  
  
     [권장 사항](#Recommendations)  
  
-   **AlwaysOn을 사용 하지 않으려면 사용 하 여:**  
  
    -   [SQL Server 구성 관리자](#SQLCM3Procedure)  
  
    -   [PowerShell](#PScmd3Procedure)  
  
-   **후속 작업:**  [AlwaysOn을 사용하지 않도록 설정한 후](#FollowUp)  
  
> [!IMPORTANT]  
>  한 번에 하나의 서버에서만 AlwaysOn을 사용하지 않도록 설정해야 합니다. AlwaysOn 가용성 그룹을 사용하지 않도록 설정한 후에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 다시 시작될 때까지 기다렸다가 다음 서버 인스턴스로 진행하도록 설정합니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
 서버 인스턴스에서 AlwaysOn을 해제하기 전 다음을 수행하는 것이 좋습니다.  
  
1.  서버 인스턴스가 사용자가 보관하려는 가용성 그룹의 주 복제본을 호스팅 중인 경우 가능한 한 가용성 그룹을 동기화된 보조 복제본으로 수동으로 장애 조치(failover)하는 것이 좋습니다. 자세한 내용은 [가용성 그룹의 계획된 수동 장애 조치(failover) 수행&#40;SQL Server&#41;](perform-a-planned-manual-failover-of-an-availability-group-sql-server.md)을 참조하세요.  
  
2.  모든 로컬 보조 복제본을 제거합니다. 자세한 내용은 [가용성 그룹에서 보조 복제본 제거&#40;SQL Server&#41;](remove-a-secondary-replica-from-an-availability-group-sql-server.md)를 참조하세요.  
  
###  <a name="SQLCM3Procedure"></a> SQL Server 구성 관리자 사용  
 **AlwaysOn을 사용 하지 않도록 설정 하려면**  
  
1.  AlwaysOn 가용성 그룹을 사용하지 않도록 설정할 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스를 호스팅하는 WSFC(Windows Server 장애 조치(failover) 클러스터링) 노드에 연결합니다.  
  
2.  **시작** 메뉴에서 **모든 프로그램**, [!INCLUDE[ssCurrentUI](../../../includes/sscurrentui-md.md)], **구성 도구**를 차례로 가리킨 다음 **SQL Server 구성 관리자**를 클릭합니다.  
  
3.  **SQL Server 구성 관리자**, 클릭 **SQL Server 서비스**, SQL Server를 마우스 오른쪽 단추로 클릭 (**<*`instance name`*>)** 여기서 **< *`instance name`* >** AlwaysOn 가용성 그룹을 사용 하지 않도록 설정 하려는 로컬 서버 인스턴스의 이름 및 클릭 **속성**합니다.  
  
4.  **AlwaysOn 고가용성**탭에서 **AlwaysOn 가용성 그룹 사용** 확인란의 선택을 취소하고 **확인**을 클릭합니다.  
  
     [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성 관리자가 변경 내용을 저장하고 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 다시 시작합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 시작하면 AlwaysOn을 사용할 수 없고 `IsHadrEnabled` 서버 속성이 0으로 설정되어 AlwaysOn 가용성 그룹을 사용할 수 없음을 나타냅니다.  
  
5.  이 항목의 뒷부분에 나오는 [후속 작업: AlwaysOn을 사용하지 않도록 설정한 후](#FollowUp)의 정보를 읽어보는 것이 좋습니다.  
  
###  <a name="PScmd3Procedure"></a> SQL Server PowerShell 사용  
 **AlwaysOn을 사용 하지 않도록 설정 하려면**  
  
1.  디렉터리를 AlwaysOn 가용성 그룹을 사용하지 않도록 설정할 서버 인스턴스(현재 사용하도록 설정되어 있음)로 변경합니다(`cd`).  
  
2.  사용 하 여는 `Disable-SqlAlwaysOn` cmdlet AlwaysOn 가용성 그룹을 사용 하도록 합니다.  
  
     다음 명령은 SQL Server 인스턴스에서 AlwaysOn 가용성 그룹을 해제 하는 예를 들어 (*컴퓨터*\\*인스턴스*).  이 명령을 사용할 경우 인스턴스를 다시 시작해야 하며, 다시 시작을 확인하는 메시지가 표시됩니다.  
  
    ```  
    Disable-SqlAlwaysOn -Path SQLSERVER:\SQL\Computer\Instance  
    ```  
  
    > [!IMPORTANT]  
    >  제어 하는 방법에 대 한 내용은 여부는 `Disable-SqlAlwaysOn` cmdlet를 다시 시작는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스를 참조 하십시오 [않습니다 Cmdlet를 다시 시작 경우 SQL Server 서비스?](#WhenCmdletRestartsSQL)이 항목의 뒷부분에 나오는 합니다.  
  
     Cmdlet의 구문을 보려면에서 사용 하 여는 `Get-Help` cmdlet에는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 환경입니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)을 참조하세요.  
  
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../../powershell/sql-server-powershell-provider.md)  
  
###  <a name="FollowUp"></a> 후속 작업: AlwaysOn을 해제 한 후  
 AlwaysOn 가용성 그룹의 인스턴스를 해제 한 후 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 다시 시작 해야 합니다. SQL 구성 관리자는 서버 인스턴스를 자동으로 다시 시작합니다. 그러나 `Disable-SqlAlwaysOn` cmdlet을 사용한 경우 서버 인스턴스를 수동으로 다시 시작해야 합니다. 자세한 내용은 [sqlservr Application](../../../tools/sqlservr-application.md)을 참조하세요.  
  
 다시 시작된 서버 인스턴스에서 다음 작업을 수행합니다.  
  
-   가용성 데이터베이스는 SQL Server 시작 기능을 시작하지 않으므로 해당 시작 기능에 액세스할 수 없습니다.  
  
-   지원 되는 유일한 AlwaysOn [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문이 [DROP AVAILABILITY GROUP](/sql/t-sql/statements/drop-availability-group-transact-sql)합니다. ALTER DATABASE의 CREATE AVAILABILITY GROUP, ALTER AVAILABILITY GROUP 및 SET HADR 옵션은 지원되지 않습니다.  
  
-   AlwaysOn 가용성 그룹을 사용하지 않도록 설정해도 WSFC의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구성과 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 메타데이터는 영향을 받지 않습니다.  
  
 하나 이상의 가용성 그룹에 대한 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 AlwaysOn 가용성 그룹을 영구적으로 해제한 경우 다음 단계를 완료하는 것이 좋습니다.  
  
1.  AlwaysOn을 해제하기 전에 로컬 가용성 복제본을 제거하지 않은 경우 서버 인스턴스가 가용성 복제본을 호스팅 중인 각 가용성 그룹을 삭제합니다. 가용성 그룹 삭제에 대한 자세한 내용은 [가용성 그룹 제거&#40;SQL Server&#41;](remove-an-availability-group-sql-server.md)를 참조하세요.  
  
2.  뒤에 남은 메타데이터를 제거하려면 원본 WSFC 클러스터의 일부인 서버 인스턴스에서 각각의 해당 가용성 그룹을 삭제합니다.  
  
3.  모든 주 데이터베이스가 계속해서 모든 연결에 액세스 가능하지만 주 데이터베이스와 보조 데이터베이스 간 데이터 동기화는 중지됩니다.  
  
4.  보조 데이터베이스가 RESTORING 상태가 됩니다. 이를 삭제하거나 RESTORE WITH RECOVERY를 사용하여 복원할 수 있습니다. 그러나 복원된 데이터베이스는 더 이상 가용성 그룹 데이터 동기화에 사용되지 않습니다.  
  
##  <a name="WhenCmdletRestartsSQL"></a> Cmdlet이 SQL Server 서비스를 다시 시작하는 경우  
 현재 실행 중인 서버 인스턴스에서 `Enable-SqlAlwaysOn` 또는 `Disable-SqlAlwaysOn`을 사용하여 현재 AlwaysOn 설정을 변경하면 SQL Server 서비스가 다시 시작될 수 있습니다. 다시 시작 동작은 다음 조건에 따라 달라집니다.  
  
|-NoServiceRestart 매개 변수가 지정되었는지 여부|-Force 매개 변수가 지정되었는지 여부|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 서비스가 다시 시작되었는지 여부|  
|--------------------------------------------|---------------------------------|---------------------------------------------------------|  
|아니요|아니요|기본적으로 선택되어 있지만 cmdlet에서 다음과 같이 묻는 메시지가 표시됩니다.<br /><br /> **이 작업을 완료하려면 '<instance_name>' 서버 인스턴스에 대한 SQL Server 서비스를 다시 시작해야 합니다. 계속하시겠습니까?**<br /><br /> **[Y] 예  [N] 아니요  [S] 일시 중단  [?] 도움말(기본값 "Y"):**<br /><br /> **N** 또는 **S**를 지정하면 서비스가 다시 시작되지 않습니다.|  
|아니요|예|서비스가 다시 시작됩니다.|  
|예|아니요|서비스가 다시 시작되지 않습니다.|  
|예|예|서비스가 다시 시작되지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [SERVERPROPERTY&#40;Transact-SQL&#41;](/sql/t-sql/functions/serverproperty-transact-sql)  
  
  
