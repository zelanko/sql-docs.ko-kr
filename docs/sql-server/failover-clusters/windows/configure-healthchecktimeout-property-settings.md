---
title: 가용성 그룹에 대한 HealthCheckTimeout 구성
description: SQL Server 리소스 DLL이 응답하지 않는 것으로 보고되기 전에 대기해야 하는 시간을 지정하는 데 사용되는 Always On 가용성 그룹에 대한 HealthCheckTimeout을 구성합니다.
ms.custom: seo-lt-2019
ms.date: 03/09/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3e03c9f0a62896daa192fa33e7b1e0a549b1b46f
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "74822001"
---
# <a name="configure-healthchecktimeout-property-settings"></a>HealthCheckTimeout 속성 설정 구성
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  HealthCheckTimeout 설정은 SQL Server 리소스 DLL이 Always On FCI(장애 조치(failover) 클러스터 인스턴스)가 응답하지 않는 것으로 보고하기 전에 [sp_server_diagnostics](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 저장 프로시저에서 반환되는 정보를 대기해야 하는 시간(밀리초)을 지정하는 데 사용됩니다. 제한 시간 설정에 대한 변경 내용은 즉시 적용되며 SQL Server 리소스를 다시 시작하지 않아도 됩니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Limits), [보안](#Security)  
  
-   **다음을 사용하여 HeathCheckTimeout 설정 구성:**  [PowerShell](#PowerShellProcedure), [장애 조치(Failover) 클러스터 관리자](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Limits"></a> 제한 사항  
 이 속성의 기본값은 30,000밀리초(30초)이고, 최소값은 15,000밀리초(15초)입니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> 권한  
 ALTER SETTINGS 및 VIEW SERVER STATE 사용 권한이 필요합니다.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
  
##### <a name="to-configure-healthchecktimeout-settings"></a>HealthCheckTimeout 설정을 구성하려면  
  
1.  **관리자 권한으로 실행**을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 Cmdlet을 사용할 수 있도록 **FailoverClusters** 모듈을 가져옵니다.  
  
3.  **Get-ClusterResource** cmdlet을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 찾은 다음 **Set-ClusterParameter** cmdlet을 사용하여 장애 조치(failover) 클러스터 인스턴스의 **HealthCheckTimeout** 속성을 설정합니다.  
  
> [!TIP]  
>  새 PowerShell 창을 열 때마다 **FailoverClusters** 모듈을 가져와야 합니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 다음 예에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 "`SQL Server (INST1)`"의 HealthCheckTimeout 설정을 60000밀리초로 번경합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
  
```  
  
### <a name="related-content-powershell"></a>관련 내용(PowerShell)  
  
-   [클러스터링 및 고가용성](https://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (장애 조치(failover) 클러스터링 및 네트워크 부하 분산 팀 블로그)  
  
-   [장애 조치(Failover) 클러스터에서 Windows PowerShell 시작](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [클러스터 리소스 명령 및 해당 Windows PowerShell Cmdlet](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> 장애 조치(Failover) 클러스터 관리자 스냅인 사용  
 **HealthCheckTimeout 설정을 구성하려면**  
  
1.  장애 조치(failover) 클러스터 관리자 스냅인을 엽니다.  
  
2.  **서비스 및 애플리케이션** 을 확장하고 FCI를 선택합니다.  
  
3.  **기타 리소스** 에서 **SQL Server 리소스** 를 마우스 오른쪽 단추로 클릭한 다음 오른쪽 클릭 메뉴에서 **속성** 을 선택합니다. SQL Server 리소스 **속성** 대화 상자가 열립니다.  
  
4.  **속성** 탭을 선택하고 **HealthCheckTimeout** 속성에 대해 원하는 값을 입력한 다음 **확인** 을 클릭하여 변경 내용을 적용합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용하여 HealthCheckTimeOut 속성 값을 지정할 수 있습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 HealthCheckTimeout 옵션을 15,000밀리초(15초)로 설정합니다.  
  
```  
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>참고 항목  
 [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
