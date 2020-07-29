---
title: FailureConditionLevel 속성 설정 구성
description: FailureConditionLevel 속성을 사용하여 Always On FCI(장애 조치(Failover) 클러스터 인스턴스)가 장애 조치(Failover)되거나 다시 시작되는 조건을 설정할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f1b92e0ce9e3d705587b81604dac28a2e927d3e2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882962"
---
# <a name="configure-failureconditionlevel-property-settings"></a>FailureConditionLevel 속성 설정 구성
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  FailureConditionLevel 속성을 사용하여 Always On FCI(장애 조치(Failover) 클러스터 인스턴스)가 장애 조치(Failover)되거나 다시 시작되는 조건을 설정할 수 있습니다. 이 속성에 대한 변경 내용은 WSFC(Windows Server 장애 조치(Failover) 클러스터) 서비스 또는 FCI 리소스를 다시 시작할 필요 없이 즉시 적용됩니다.  
  
-   **시작하기 전 주의 사항:**  [FailureConditionLevel 속성 설정](#Restrictions), [보안](#Security)  
  
-   **FailureConditionLevel 속성 설정에 사용되는 도구:** [PowerShell](#PowerShellProcedure), [장애 조치(Failover) 클러스터 관리자](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="failureconditionlevel-property-settings"></a><a name="Restrictions"></a> FailureConditionLevel 속성 설정  
 실패 조건은 증가하는 범위로 설정됩니다. 수준 1-5의 경우 각 수준에는 자체 조건과 함께 이전 수준의 모든 조건이 포함됩니다. 이는 수준이 높을수록 장애 조치(Failover) 또는 다시 시작 확률이 증가함을 의미합니다.  자세한 내용은 [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md) 항목의 "실패 확정" 섹션을 참조하세요.  
  
###  <a name="security"></a><a name="Security"></a> 보안  
  
####  <a name="permissions"></a><a name="Permissions"></a> 권한  
 ALTER SETTINGS 및 VIEW SERVER STATE 사용 권한이 필요합니다.  
  
##  <a name="using-powershell"></a><a name="PowerShellProcedure"></a> PowerShell 사용  
  
##### <a name="to-configure-failureconditionlevel-settings"></a>FailureConditionLevel 설정을 구성하려면  
  
1.  **관리자 권한으로 실행**을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 Cmdlet을 사용할 수 있도록 **FailoverClusters** 모듈을 가져옵니다.  
  
3.  **Get-ClusterResource** Cmdlet을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 찾은 다음 **Set-ClusterParameter** Cmdlet을 사용하여 장애 조치(failover) 클러스터 인스턴스의 **FailureConditionLevel** 속성을 설정합니다.  
  
> [!TIP]  
>  새 PowerShell 창을 열 때마다 **FailoverClusters** 모듈을 가져와야 합니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 다음 예에서는 심각한 서버 오류 시 장애 조치(failover) 또는 다시 시작이 수행되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 "`SQL Server (INST1)`"의 FailureConditionLevel 설정을 변경합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3  
  
```  
  
### <a name="related-content-powershell"></a>관련 내용(PowerShell)  
  
-   [클러스터링 및 고가용성](https://techcommunity.microsoft.com/t5/failover-clustering/bg-p/FailoverClustering) (장애 조치(failover) 클러스터링 및 네트워크 부하 분산 팀 블로그)  
  
-   [장애 조치(Failover) 클러스터에서 Windows PowerShell 시작](https://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [클러스터 리소스 명령 및 해당 Windows PowerShell Cmdlet](https://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="using-the-failover-cluster-manager-snap-in"></a><a name="WSFC"></a> 장애 조치(Failover) 클러스터 관리자 스냅인 사용  
 **FailureConditionLevel 속성 설정을 구성하려면**  
  
1.  장애 조치(failover) 클러스터 관리자 스냅인을 엽니다.  
  
2.  **서비스 및 애플리케이션** 을 확장하고 FCI를 선택합니다.  
  
3.  **기타 리소스** 에서 **SQL Server 리소스**를 마우스 오른쪽 단추로 클릭한 다음 메뉴에서 **속성** 을 선택합니다. SQL Server 리소스 **속성** 대화 상자가 열립니다.  
  
4.  **속성** 탭을 선택하고 **FaliureConditionLevel** 속성에 대해 원하는 값을 입력한 다음 **확인** 을 클릭하여 변경 내용을 적용합니다.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 **FailureConditionLevel 속성 설정을 구성하려면**  
  
 [ALTER SERVER CONFIGURATION](../../../t-sql/statements/alter-server-configuration-transact-sql.md)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용하여 FailureConditionLevel 속성 값을 지정할 수 있습니다.  
  
###  <a name="example-transact-sql"></a><a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 FailureConditionLevel 속성을 0으로 설정하여 어떤 실패 조건에서도 장애 조치(failover) 또는 다시 시작이 자동으로 트리거되지 않음을 나타냅니다.  
  
```  
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_server_diagnostics&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md)   
 [Failover Policy for Failover Cluster Instances](../../../sql-server/failover-clusters/windows/failover-policy-for-failover-cluster-instances.md)  
  
  
