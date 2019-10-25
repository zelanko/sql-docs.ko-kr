---
title: SSIS 카탈로그 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6ed56d36-18d9-40c2-b51f-f2a4c71d1e73
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f8db507966f9b3323e415ca7f2abfe4a12601c1c
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72798021"
---
# <a name="create-the-ssis-catalog"></a>SSIS 카탈로그 만들기
  [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 패키지를 디자인하고 테스트한 후에는 이 패키지가 포함된 프로젝트를 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 배포할 수 있습니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 서버에 프로젝트를 배포하려면 서버에 `SSISDB` 카탈로그가 있어야 합니다. [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 설치 프로그램에서 카탈로그를 자동으로 만들지 않으므로 다음 지침에 따라 카탈로그를 수동으로 만들어야 합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 SSISDB 카탈로그를 만들 수 있습니다. Windows PowerShell을 사용하여 프로그래밍 방식으로 카탈로그를 만들 수도 있습니다.  
  
### <a name="to-create-the-ssisdb-catalog-in-sql-server-management-studio"></a>SQL Server Management Studio에서 SSISDB 카탈로그를 만들려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]열기  
  
2.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스 엔진에 연결합니다.  
  
3.  개체 탐색기에서 서버 노드를 확장하고 **Integration Services 카탈로그** 노드를 마우스 오른쪽 단추로 클릭한 다음 **카탈로그 만들기**를 클릭합니다.  
  
4.  **CLR 통합 사용**을 클릭합니다.  
  
     카탈로그에 CLR 저장 프로시저가 사용됩니다.  
  
5.  **SQL Server 시작 시 Integration Services 저장 프로시저 자동 실행** 을 클릭하여 [서버 인스턴스를 다시 시작할 때마다](/sql/integration-services/system-stored-procedures/catalog-startup) catalog.startup [!INCLUDE[ssIS](../includes/ssis-md.md)] 저장 프로시저를 실행하도록 지정합니다.  
  
     저장 프로시저에서는 SSISDB 카탈로그에 대한 작업의 상태를 유지 관리합니다. [!INCLUDE[ssIS](../includes/ssis-md.md)] 서버 인스턴스가 다운될 때 실행 중이었던 패키지의 상태를 수정합니다.  
  
6.  암호를 입력하고 **확인**을 클릭합니다.  
  
     암호는 카탈로그 데이터를 암호화하는 데 사용되는 데이터베이스 마스터 키를 보호합니다. 암호를 안전한 위치에 저장하십시오. 데이터베이스 마스터 키도 백업하는 것이 좋습니다. 자세한 내용은 [데이터베이스 마스터 키 백업](../relational-databases/security/encryption/back-up-a-database-master-key.md)을 참조하세요.  
  
### <a name="to-create-the-ssisdb-catalog-programmatically"></a>SSISDB 카탈로그를 프로그래밍 방식으로 만들려면  
  
1.  다음 PowerShell 스크립트를 실행합니다.  
  
    ```powershell
    # Load the IntegrationServices Assembly  
    [Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.IntegrationServices")  
  
    # Store the IntegrationServices Assembly namespace to avoid typing it every time  
    $ISNamespace = "Microsoft.SqlServer.Management.IntegrationServices"  
  
    Write-Host "Connecting to server ..."  
  
    # Create a connection to the server  
    $sqlConnectionString = "Data Source=localhost;Initial Catalog=master;Integrated Security=SSPI;"  
    $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $sqlConnectionString  
  
    # Create the Integration Services object  
    $integrationServices = New-Object $ISNamespace".IntegrationServices" $sqlConnection  
  
    # Provision a new SSIS Catalog  
    $catalog = New-Object $ISNamespace".Catalog" ($integrationServices, "SSISDB", "P@assword1")  
    $catalog.Create()
    ```  
  
     Windows PowerShell 및 <xref:Microsoft.SqlServer.Management.IntegrationServices> 네임스페이스를 사용하는 방법의 예를 더 보려면 blogs.msdn.com에서 [SQL Server 2012의 SSIS 및 PowerShell](https://go.microsoft.com/fwlink/?LinkId=242539) 블로그 항목을 참조하세요. 네임스페이스 및 코드 예제에 대한 개요는 blogs.msdn.com에서 [SSIS 카탈로그 관리 개체 모델에 대한 이해](https://go.microsoft.com/fwlink/?LinkId=254267)블로그 항목을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [SSIS 카탈로그](catalog/ssis-catalog.md)   
 [SSIS 카탈로그 백업, 복원 및 이동](../../2014/integration-services/backup-restore-and-move-the-ssis-catalog.md)  
