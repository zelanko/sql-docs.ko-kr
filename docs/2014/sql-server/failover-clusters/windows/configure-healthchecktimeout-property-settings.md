---
title: HealthCheckTimeout 속성 설정 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 3bbeb979-e6fc-4184-ad6e-cca62108de74
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: a38cd6e9e4718a2f1c136e5412cde340e92f14c1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85062508"
---
# <a name="configure-healthchecktimeout-property-settings"></a>HealthCheckTimeout 속성 설정 구성
  HealthCheckTimeout 설정은 SQL Server 리소스 DLL이 AlwaysOn FCI (장애 조치 (Failover) 클러스터 인스턴스)를 응답 하지 않는 것으로 보고 하기 전에 [sp_server_diagnostics](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql) 저장 프로시저에서 반환 되는 정보를 대기 해야 하는 시간 (밀리초)을 지정 하는 데 사용 됩니다. 제한 시간 설정에 대한 변경 내용은 즉시 적용되며 SQL Server 리소스를 다시 시작하지 않아도 됩니다.  
  
-   **시작하기 전 주의 사항:**  [제한 사항](#Limits), [보안](#Security)  
  
-   **HeathCheckTimeout 설정을 구성하려면:**  [PowerShell](#PowerShellProcedure), [장애 조치(failover) 클러스터 관리자](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="limitations-and-restrictions"></a><a name="Limits"></a> 제한 사항  
 이 속성의 기본값은 60,000밀리초(60초)이고, 최소값은 15,000밀리초(15초)입니다.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 ALTER SETTINGS 및 VIEW SERVER STATE 사용 권한이 필요합니다.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell 사용  
  
### <a name="to-configure-healthchecktimeout-settings"></a>HealthCheckTimeout 설정을 구성하려면  
  
1.  **관리자 권한으로 실행**을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 Cmdlet을 사용할 수 있도록 `FailoverClusters` 모듈을 가져옵니다.  
  
3.  Cmdlet을 사용 `Get-ClusterResource` 하 여 리소스를 찾은 다음 cmdlet을 사용 하 여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `Set-ClusterParameter` 장애 조치 (failover) 클러스터 인스턴스에 대 한 **HealthCheckTimeout** 속성을 설정 합니다.  
  
> [!TIP]  
>  새 PowerShell 창을 열 때마다 `FailoverClusters` 모듈을 가져와야 합니다.  

 다음 예에서는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 "`SQL Server (INST1)`"의 HealthCheckTimeout 설정을 60000밀리초로 번경합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter HealthCheckTimeout 60000  
```  
  
### <a name="related-content-powershell"></a>관련 내용(PowerShell)  
  
-   [클러스터링 및 고가용성](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (장애 조치(failover) 클러스터링 및 네트워크 부하 분산 팀 블로그)  
  
-   [장애 조치(Failover) 클러스터에서 Windows PowerShell 시작](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [클러스터 리소스 명령 및 해당 Windows PowerShell Cmdlet](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="using-the-failover-cluster-manager-snap-in"></a><a name="WSFC"></a> 장애 조치(Failover) 클러스터 관리자 스냅인 사용  
 **HealthCheckTimeout 설정을 구성하려면**  
  
1.  장애 조치(failover) 클러스터 관리자 스냅인을 엽니다.  
  
2.  **서비스 및 애플리케이션** 을 확장하고 FCI를 선택합니다.  
  
3.  **기타 리소스** 에서 **SQL Server 리소스** 를 마우스 오른쪽 단추로 클릭한 다음 오른쪽 클릭 메뉴에서 **속성** 을 선택합니다. SQL Server 리소스 **속성** 대화 상자가 열립니다.  
  
4.  **속성** 탭을 선택하고 **HealthCheckTimeout** 속성에 대해 원하는 값을 입력한 다음 **확인** 을 클릭하여 변경 내용을 적용합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql) 문을 사용 하 여 [!INCLUDE[tsql](../../../includes/tsql-md.md)] HealthCheckTimeOut 속성 값을 지정할 수 있습니다.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 HealthCheckTimeout 옵션을 15,000밀리초(15초)로 설정합니다.  
  
```sql
ALTER SERVER CONFIGURATION   
SET FAILOVER CLUSTER PROPERTY HealthCheckTimeout = 15000;  
```  
  
## <a name="see-also"></a>참고 항목  
 [장애 조치 (Failover) 클러스터 인스턴스에 대 한 장애 조치 정책](failover-policy-for-failover-cluster-instances.md)  
