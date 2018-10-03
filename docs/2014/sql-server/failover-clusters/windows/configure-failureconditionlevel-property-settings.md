---
title: FailureConditionLevel 속성 설정 구성 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 513dd179-9a46-46da-9fdd-7632cf6d0816
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: edda4e1653d8a2ca00019b78962fe9eeec64691a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104694"
---
# <a name="configure-failureconditionlevel-property-settings"></a>FailureConditionLevel 속성 설정 구성
  FailureConditionLevel 속성을 사용하여 AlwaysOn FCI(장애 조치(Failover) 클러스터 인스턴스)가 장애 조치(Failover)되거나 다시 시작되는 조건을 설정할 수 있습니다. 이 속성에 대한 변경 내용은 WSFC(Windows Server 장애 조치(Failover) 클러스터) 서비스 또는 FCI 리소스를 다시 시작할 필요 없이 즉시 적용됩니다.  
  
-   **시작하기 전 주의 사항:**  [FailureConditionLevel 속성 설정](#Restrictions), [보안](#Security)  
  
-   **FailureConditionLevel 속성 설정에 사용되는 도구:** [PowerShell](#PowerShellProcedure), [장애 조치(Failover) 클러스터 관리자](#WSFC), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> FailureConditionLevel 속성 설정  
 실패 조건은 증가하는 범위로 설정됩니다. 수준 1-5의 경우 각 수준에는 자체 조건과 함께 이전 수준의 모든 조건이 포함됩니다. 이는 수준이 높을수록 장애 조치(Failover) 또는 다시 시작 확률이 증가함을 의미합니다.  자세한 내용은 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md) 항목의 "실패 확정" 섹션을 참조하세요.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 ALTER SETTINGS 및 VIEW SERVER STATE 사용 권한이 필요합니다.  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
  
##### <a name="to-configure-failureconditionlevel-settings"></a>FailureConditionLevel 설정을 구성하려면  
  
1.  **관리자 권한으로 실행**을 통해 승격된 Windows PowerShell을 시작합니다.  
  
2.  클러스터 Cmdlet을 사용할 수 있도록 `FailoverClusters` 모듈을 가져옵니다.  
  
3.  사용 하 여를 `Get-ClusterResource` cmdlet을 찾을 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스를 사용 하 여 `Set-ClusterParameter` cmdlet을 설정 하는 **FailureConditionLevel** a Failover Cluster Instance에 대 한 속성.  
  
> [!TIP]  
>  새 PowerShell 창을 열 때마다를 가져와야 할는 `FailoverClusters` 모듈입니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 다음 예에서는 심각한 서버 오류 시 장애 조치(failover) 또는 다시 시작이 수행되도록 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 리소스 "`SQL Server (INST1)`"의 FailureConditionLevel 설정을 변경합니다.  
  
```powershell  
Import-Module FailoverClusters  
  
$fci = "SQL Server (INST1)"  
Get-ClusterResource $fci | Set-ClusterParameter FailureConditionLevel 3  
  
```  
  
### <a name="related-content-powershell"></a>관련 내용(PowerShell)  
  
-   [클러스터링 및 고가용성](http://blogs.msdn.com/b/clustering/archive/2009/05/23/9636665.aspx) (장애 조치(failover) 클러스터링 및 네트워크 부하 분산 팀 블로그)  
  
-   [장애 조치(Failover) 클러스터에서 Windows PowerShell 시작](http://technet.microsoft.com/library/ee619762\(WS.10\).aspx)  
  
-   [클러스터 리소스 명령 및 해당 Windows PowerShell Cmdlet](http://msdn.microsoft.com/library/ee619744.aspx#BKMK_resource)  
  
##  <a name="WSFC"></a> 장애 조치(Failover) 클러스터 관리자 스냅인 사용  
 **FailureConditionLevel 속성 설정을 구성하려면**  
  
1.  장애 조치(failover) 클러스터 관리자 스냅인을 엽니다.  
  
2.  **서비스 및 응용 프로그램** 을 확장하고 FCI를 선택합니다.  
  
3.  **기타 리소스** 에서 **SQL Server 리소스**를 마우스 오른쪽 단추로 클릭한 다음 메뉴에서 **속성** 을 선택합니다. SQL Server 리소스 **속성** 대화 상자가 열립니다.  
  
4.  **속성** 탭을 선택하고 **FaliureConditionLevel** 속성에 대해 원하는 값을 입력한 다음 **확인** 을 클릭하여 변경 내용을 적용합니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 **FailureConditionLevel 속성 설정을 구성하려면**  
  
 [ALTER SERVER CONFIGURATION](/sql/t-sql/statements/alter-server-configuration-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 사용하여 FailureConditionLevel 속성 값을 지정할 수 있습니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 FailureConditionLevel 속성을 0으로 설정하여 어떤 실패 조건에서도 장애 조치(failover) 또는 다시 시작이 자동으로 트리거되지 않음을 나타냅니다.  
  
```  
ALTER SERVER CONFIGURATION SET FAILOVER CLUSTER PROPERTY FailureConditionLevel = 0;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_server_diagnostics&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql)   
 [Failover Policy for Failover Cluster Instances](failover-policy-for-failover-cluster-instances.md)  
  
  
