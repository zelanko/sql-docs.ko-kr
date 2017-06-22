---
title: "데이터 계층 응용 프로그램 삭제 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deletedacwizard.deletedac.f1
- sql13.swb.deletedacwizard.summary.f1
- sql13.swb.deletedacwizard.introduction.f1
- sql13.swb.deletedacwizard.choosemethod.f1
helpviewer_keywords:
- How to [DAC], delete
- data-tier application [SQL Server], delete
- wizard [DAC], delete
- delete DAC
ms.assetid: 16fe1c18-4486-424d-81d6-d276ed97482f
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a6c69a8bbd4fa63a427658ddc7b8fdbd79b0af3b
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-data-tier-application"></a>데이터 계층 응용 프로그램 삭제
  데이터 계층 응용 프로그램 삭제 마법사 또는 Windows PowerShell 스크립트를 사용하여 데이터 계층 응용 프로그램을 삭제할 수 있습니다. 연결된 데이터베이스를 보존, 분리 또는 삭제할지를 지정할 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To upgrade a DAC, using:**  [The Register Data-tier Application Wizard](#UsingDeleteDACWizard), [PowerShell](#DeleteDACPowerShell)  
  
## <a name="before-you-begin"></a>시작하기 전에  
 DAC(데이터 계층 응용 프로그램) 인스턴스를 삭제할 때는 데이터 계층 응용 프로그램과 연결된 데이터베이스에 대해 어떠한 작업을 수행할지 지정하는 3가지 옵션 중 하나를 선택할 수 있습니다. 3가지 옵션 모두 DAC 정의 메타데이터를 삭제합니다. 각 옵션은 데이터 계층 응용 프로그램과 연결된 데이터베이스에 대해 수행되는 작업에 차이가 있습니다. 마법사는 로그인처럼 DAC 또는 데이터베이스와 연결된 인스턴스 수준 개체는 삭제하지 않습니다.  
  
|옵션|데이터베이스 동작|  
|------------|----------------------|  
|등록 삭제|연결된 데이터베이스가 그대로 유지됩니다.|  
|데이터베이스 분리|연결된 데이터베이스가 분리됩니다. 데이터베이스 엔진 인스턴스가 데이터베이스를 참조할 수는 없지만 데이터 및 로그 파일은 그대로 유지됩니다.|  
|데이터베이스 삭제|연결된 데이터베이스가 삭제됩니다. 데이터 및 로그 파일이 삭제됩니다.|  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 DAC를 삭제한 후 DAC 정의 메타데이터나 데이터베이스를 복원하는 자동 메커니즘은 없습니다. DAC 인스턴스를 수동으로 다시 작성하는 방법은 삭제 옵션에 따라 다릅니다.  
  
|옵션|DAC 인스턴스를 다시 작성하는 방법|  
|------------|-------------------------------------|  
|등록 삭제|남아 있는 데이터베이스에서 DAC를 등록합니다.|  
|데이터베이스 분리|**sp_attachdb** 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 데이터베이스를 다시 연결한 다음, 데이터베이스에 새 DAC 인스턴스를 등록합니다.|  
|데이터베이스 삭제|DAC가 삭제되기 전에 만든 전체 백업에서 데이터베이스를 복원한 다음, 데이터베이스에서 새 DAC 인스턴스를 등록합니다.|  
  
> [!WARNING]  
>  복원하거나 다시 연결한 데이터베이스에서 DAC를 등록하여 DAC 인스턴스를 다시 작성하더라도 원래 DAC의 서버 선택 정책과 같은 일부 부분은 만들어지지 않습니다.  
  
###  <a name="Permissions"></a> 권한  
 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버 또는 데이터베이스 소유자를 통해서만 DAC를 삭제할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sa **라는 기본 제공** 시스템 관리자 계정도 마법사를 시작할 수 있습니다.  
  
##  <a name="UsingDeleteDACWizard"></a> 데이터 계층 응용 프로그램 삭제 마법사 사용  
 **마법사를 사용하여 DAC를 삭제하려면**  
  
1.  **개체 탐색기**에서 삭제할 DAC가 포함된 인스턴스에 대한 노드를 확장합니다.  
  
2.  **관리** 노드를 확장합니다.  
  
3.  **데이터 계층 응용 프로그램** 노드를 확장합니다.  
  
4.  삭제할 DAC를 마우스 오른쪽 단추로 클릭한 다음 **데이터 계층 응용 프로그램 삭제...**를 선택합니다.  
  
5.  마법사 대화 상자를 완료합니다.  
  
    1.  [소개](#Introduction)  
  
    2.  [방법 선택](#Choose_method)  
  
    3.  [요약](#Summary)  
  
    4.  [데이터 계층 응용 프로그램 삭제](#Delete_datatier_application)  
  
##  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 데이터 계층 응용 프로그램을 삭제하는 단계에 대해 설명합니다.  
  
 **이 페이지를 다시 표시 안 함** - 앞으로 이 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
 **다음 >** - **방법 선택** 페이지로 진행합니다.  
  
 **취소** - 데이터 계층 응용 프로그램 또는 데이터베이스를 삭제하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 삭제 마법사 사용](#UsingDeleteDACWizard)  
  
##  <a name="Choose_method"></a> 방법 선택 페이지  
 이 페이지를 사용하여 삭제할 DAC와 연결된 데이터베이스를 처리하는 옵션을 지정할 수 있습니다.  
  
 **등록 삭제** - 데이터 계층 응용 프로그램을 정의하는 메타데이터를 제거하되 연결된 데이터베이스는 그대로 유지합니다.  
  
 **데이터베이스 분리** - 데이터 계층 응용 프로그램을 정의하는 메타데이터를 제거하고 연결된 데이터베이스를 분리합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 해당 인스턴스는 더 이상 데이터베이스를 참조할 수 없지만 데이터 및 로그 파일은 그대로 유지됩니다.  
  
 **데이터베이스 삭제** - DAC를 정의하는 메타데이터를 제거하고 연결된 데이터베이스를 삭제합니다.  
  
 데이터베이스에 대한 데이터 및 로그 파일이 영구적으로 삭제됩니다.  
  
 **< 이전** - **소개** 페이지로 돌아갑니다.  
  
 **다음 >** - **요약** 페이지로 진행합니다.  
  
 **취소** - DAC 또는 데이터베이스를 삭제하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 삭제 마법사 사용](#UsingDeleteDACWizard)  
  
##  <a name="Summary"></a> 요약 페이지  
 이 페이지를 사용하여 DAC 인스턴스를 삭제할 때 마법사가 수행할 동작을 검토합니다.  
  
 **선택 항목 요약 검토** - 상자에 표시된 DAC, 데이터베이스 및 삭제 방법을 검토합니다. 정보가 올바르면 **다음** 또는 **마침** 을 선택하여 DAC를 삭제합니다. DAC 및 데이터베이스 정보가 올바르지 않으면 **취소** 를 선택하고 올바른 DAC를 선택합니다. 삭제 방법이 올바르지 않으면 **이전** 을 선택하여 **방법 선택** 페이지로 돌아간 후 다른 방법을 선택합니다.  
  
 **< 이전** - 다른 삭제 방법을 선택할 수 있도록 **방법 선택** 페이지로 돌아갑니다.  
  
 **다음 >** - 이전 페이지에서 선택한 방법을 사용하여 DAC 인스턴스를 삭제하고 **데이터 계층 응용 프로그램 삭제** 페이지로 진행합니다.  
  
 **취소** - DAC 인스턴스를 삭제하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 삭제 마법사 사용](#UsingDeleteDACWizard)  
  
##  <a name="Delete_datatier_application"></a> 데이터 계층 응용 프로그램 삭제 페이지  
 이 페이지에서는 삭제 작업의 성공 또는 실패를 보고합니다.  
  
 **DAC 삭제** - DAC 인스턴스를 삭제하기 위해 수행한 각 동작의 성공 또는 실패를 보고합니다. 정보를 검토하여 각 동작의 성공 또는 실패를 확인합니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 선택하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **보고서 저장** - 삭제 보고서를 HTML 파일로 저장하려면 이 단추를 선택합니다. 파일은 모든 동작에서 생성된 모든 오류를 비롯하여 각 동작의 상태를 보고합니다. 기본 폴더는 Windows 계정의 Documents 폴더에 있는 SQL Server Management Studio\DAC Packages 폴더입니다.  
  
 **마침** - 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 삭제 마법사 사용](#UsingDeleteDACWizard)  
  
##  <a name="DeleteDACPowerShell"></a> PowerShell을 사용하여 DAC 삭제  
 **PowerShell 스크립트를 사용하여 DAC를 삭제하려면**  
  
1.  SMO Server 개체를 만든 다음 삭제할 DAC를 포함하는 인스턴스로 설정합니다.  
  
2.  **ServerConnection** 개체를 열고 동일한 인스턴스에 연결합니다.  
  
3.  **add_DacActionStarted** 및 **add_DacActionFinished** 를 사용하여 DAC 업그레이드 이벤트를 구독합니다.  
  
4.  삭제할 DAC를 지정합니다.  
  
5.  적합한 삭제 옵션에 따라 다음 세 개의 코드 중 하나를 사용합니다.  
  
    -   DAC 등록만 삭제하고 데이터베이스를 그대로 두려면 **Unmanage()** 메서드를 사용합니다.  
  
    -   DAC 등록을 삭제하고 데이터베이스를 분리하려면 **Uninstall()** 메서드를 사용하고 **DetachDatabase**를 지정합니다.  
  
    -   DAC 등록을 삭제하고 데이터베이스를 삭제하려면 **Uninstall()** 메서드를 사용하고 **DropDatabase**를 지정합니다.  
  
### <a name="example-deleting-the-dac-but-leaving-the-database-powershell"></a>DAC를 삭제하지만 데이터베이스를 그대로 두는 예(PowerShell)  
 다음 예제에서는 **Unmanage()** 메서드를 사용하여 MyApplication이라는 DAC는 삭제하고 데이터베이스는 그대로 둡니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Only delete the DAC definition from msdb, the associated database remains active.  
$dacstore.Unmanage($dacName)  
```  
  
 [PowerShell을 사용하여 DAC 삭제](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-detaching-the-database-powershell"></a>DAC를 삭제하지만 데이터베이스를 분리하는 예(PowerShell)  
 다음 예제에서는 **Uninstall()** 메서드를 사용하여 MyApplication이라는 DAC를 삭제하고 데이터베이스를 분리합니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and detach the associated database.  
$dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DetachDatabase)  
```  
  
 [PowerShell을 사용하여 DAC 삭제](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-dropping-the-database-powershell"></a>DAC를 삭제하고 데이터베이스를 삭제하는 예(PowerShell)  
 다음 예제에서는 **Uninstall()** 메서드를 사용하여 MyApplication이라는 DAC를 삭제하고 데이터베이스를 삭제합니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and drop the associated database.  
## $dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DropDatabase)  
```  
  
 [PowerShell을 사용하여 DAC 삭제](#DeleteDACPowerShell)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터 계층 응용 프로그램 배포](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [DAC로 데이터베이스 등록](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)   
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [데이터베이스 분리 및 연결&#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

