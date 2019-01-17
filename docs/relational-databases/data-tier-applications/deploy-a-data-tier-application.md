---
title: 데이터 계층 애플리케이션 배포 | Microsoft 문서
ms.custom: ''
ms.date: 01/31/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 204aa0ea696e45fa756360df790cdf983066260f
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590977"
---
# <a name="deploy-a-data-tier-application"></a>데이터 계층 애플리케이션 배포
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  마법사 또는 PowerShell 스크립트를 사용하여 DAC 패키지의 DAC(데이터 계층 애플리케이션)를 데이터베이스 엔진 또는 Azure SQL Database의 기존 인스턴스에 배포합니다. 
  
 배포 프로세스에서는 **msdb** 시스템 데이터베이스([!INCLUDE[ssSDS](../../includes/sssds-md.md)]의 **master**)에 DAC 정의를 저장하여 DAC 인스턴스를 등록하고 데이터베이스를 만든 다음 DAC에 정의된 모든 데이터베이스 개체로 해당 데이터베이스를 채웁니다.  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>동일한 DAC 패키지를 여러 번 배포 
 동일한 DAC 패키지를 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 단일 인스턴스에 여러 번 배포할 수 있지만 한 번에 하나씩 배포를 실행해야 합니다. 지정된 DAC 인스턴스 이름은 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스 내에서 각 배포마다 고유해야 합니다.  
  
 DAC를 데이터베이스 엔진의 인스턴스로 배포하는 경우 배포된 DAC는 유틸리티 컬렉션 집합이 인스턴스에서 유틸리티 제어 지점으로 다음에 전송될 때 **SQL Server 유틸리티**에 통합됩니다. DAC에 있게 됩니다는 **배포 된 데이터 계층 애플리케이션** 의 노드는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]**유틸리티 탐색기** 에 보고 된 **배포 된 데이터 계층 애플리케이션**세부 정보 페이지입니다.  
  
###  <a name="database-options-and-settings"></a>데이터베이스 옵션 및 설정  
 기본적으로 배포 중에 생성된 데이터베이스에는 다음을 제외한 CREATE DATABASE 문의 모든 기본 설정이 적용됩니다.  
  
-   데이터베이스 데이터 정렬 및 호환성 수준은 DAC 패키지에 정의된 값으로 설정됩니다. SQL Server Developer Tools에서 데이터베이스 프로젝트를 기반으로 작성된 DAC 패키지는 데이터베이스 프로젝트에 설정된 값을 사용합니다. 기존 데이터베이스에서 추출한 패키지는 기존 데이터베이스의 값을 사용합니다.  
  
-   데이터베이스 이름과 파일 경로와 같은 일부 데이터베이스 설정을 **구성 업데이트** 페이지에서 조정할 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 배포할 때는 파일 경로를 설정할 수 없습니다.  
  
 TRUSTWORTHY, DB_CHAINING 및 HONOR_BROKER_PRIORITY와 같은 일부 데이터베이스 옵션은 배포 프로세스 도중 조정할 수 없습니다. 파일 그룹의 수, 파일의 수 및 크기와 같은 물리적 속성은 배포 프로세스 도중 변경할 수 없습니다. 배포가 완료된 후 ALTER DATABASE 문, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell을 사용하여 데이터베이스를 맞춤 구성할 수 있습니다.  
  
## <a name="limitations-and-restrictions"></a>제한 사항  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]SP4(서비스 팩 4) 이상을 실행하는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에 DAC를 배포할 수 있습니다. 이후 버전을 사용하여 DAC를 만드는 경우 DAC에 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 지원되지 않는 개체가 포함될 수 있습니다. 이러한 DAC를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]인스턴스에 배포할 수 없습니다.  
    
## <a name="security-and-permissions"></a>보안 및 사용 권한
인증 로그인은 암호 없이 DAC 패키지에 저장됩니다. 패키지가 배포 또는 업그레이드되면 생성된 암호와 함께 비활성 로그인이 생성됩니다. 로그인을 활성화하려면 ALTER ANY LOGIN 권한이 있는 로그인을 사용하여 로그인하고 ALTER LOGIN을 사용하여 로그인을 활성화하여 사용자에게 알려 줄 수 있는 새 암호를 할당합니다. Windows 인증 로그인의 경우 암호가 SQL Server에서 관리되지 않으므로 이 과정이 필요 없습니다.  
  
 **sysadmin** 또는 **serveradmin** 고정 서버 역할의 멤버를 통하거나 **dbcreator** 고정 서버 역할에 포함되고 ALTER ANY LOGIN 권한이 있는 로그인을 통해서만 DAC를 배포할 수 있습니다. 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 관리자 계정인 **sa** 도 DAC를 배포할 수 있습니다. 

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 로그인이 있는 DAC를 배포하려면 loginmanager 또는 serveradmin 역할의 멤버 자격이 필요합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 대한 로그인이 없는 DAC를 배포하려면 dbmanager 또는 serveradmin 역할의 멤버 자격이 필요합니다.  
  
## <a name="deploy-a-dac-using-the-wizard"></a>마법사를 사용하여 DAC 배포  
  
1.  **개체 탐색기**에서 DAC를 배포할 인스턴스에 대한 노드를 확장합니다.  
  
2.  **데이터베이스** 노드를 마우스 오른쪽 단추로 클릭한 다음, **데이터 계층 애플리케이션 배포…** 를 선택합니다.  
  
3.  마법사 대화 상자를 완료하고 마침을 클릭합니다.
아래 마법사 페이지 중 일부에 대한 자세한 정보: 
     
### <a name="select-dac-package-page"></a>DAC 패키지 선택 페이지  
 배포할 데이터 계층 애플리케이션을 포함하는 DAC 패키지를 지정합니다. 이 페이지는 세 가지 상태로 전환됩니다.  
    
### <a name="select-the-dac-package"></a>DAC 패키지 선택  
 배포할 DAC 패키지를 선택합니다. DAC 패키지는 유효한 DAC 패키지 파일이어야 하며 확장자가 .dacpac여야 합니다.  
  
 **DAC 패키지** - 배포할 데이터 계층 애플리케이션이 포함된 DAC 패키지의 경로와 파일 이름을 지정합니다. 입력란 오른쪽의 **찾아보기** 단추를 선택하여 DAC 패키지의 위치를 찾아볼 수 있습니다.  
  
 **애플리케이션 이름** - DAC를 만들거나 데이터베이스에서 추출할 때 할당된 DAC 이름을 표시하는 읽기 전용 입력란입니다.  
  
 **버전** - DAC를 만들거나 데이터베이스에서 추출할 때 할당된 버전을 표시하는 읽기 전용 입력란입니다.  
  
 **설명** - DAC를 만들거나 데이터베이스에서 추출할 때 작성된 설명을 표시하는 읽기 전용 입력란입니다.  
  
### <a name="validating-the-dac-package"></a>DAC 패키지 유효성 검사  
 선택한 파일이 유효한 DAC 패키지인지 마법사에서 확인하는 동안 진행률 표시줄이 표시됩니다. DAC 패키지의 유효성이 확인되면 마법사는 유효성 검사 결과를 검토할 수 있는 **패키지 선택** 페이지의 최종 버전으로 진행합니다. 파일이 유효한 DAC 패키지가 아닌 경우 마법사는 **DAC 패키지 선택**상태로 유지됩니다. 이 경우 다른 유효한 DAC 패키지를 선택하거나 마법사를 취소하고 새 DAC 패키지를 생성할 수 있습니다.  
  
  ### <a name="review-policy-page"></a>정책 검토 페이지  
 DAC 서버 선택 정책을 평가한 결과를 검토합니다(사용하는 경우). DAC 서버 선택 정책은 선택적이며 Visual Studio에서 DAC를 만들면 여기에 할당됩니다. 정책에서는 서버 선택 정책 패싯을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스가 DAC를 호스팅하기 위해 충족해야 하는 조건을 지정합니다.  
  
 **정책 조건의 평가 결과** - DAC 배포 정책 조건이 성공했는지 여부를 보여 줍니다. 각 조건을 평가한 결과가 별도의 행에 보고됩니다.  
  
 DAC를 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 배포하는 경우 운영 체제 버전, 언어, 명명된 파이프 설정, 플랫폼, tcp 설정 등의 서버 선택 정책을 평가한 결과가 항상 false입니다.  
  
 **정책 위반을 무시합니다.** - 정책 조건이 한 개 이상 위반되더라도 배포를 진행하려면 이 확인란을 사용합니다. 실패한 모든 조건이 DAC 작동에 영향을 주지 않는 것이 확실한 경우에만 이 옵션을 선택합니다.  
   
### <a name="update-configuration-page"></a>구성 업데이트 페이지  
 배포된 DAC 인스턴스와 배포를 통해 생성된 데이터베이스의 이름을 지정하고 데이터베이스 옵션을 설정합니다.  
  
 **데이터베이스 이름:** - 배포를 통해 생성된 데이터베이스의 이름을 지정합니다. 기본은 DAC가 추출된 원본 데이터베이스 이름입니다. 이름은 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스 내에서 고유해야 하며 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 식별자 규칙을 준수해야 합니다.  
  
 데이터베이스 이름을 변경하면 새 값에 맞게 데이터 파일과 로그 파일의 이름이 변경됩니다.  
  
 데이터베이스 이름은 DAC 인스턴스 이름에도 사용됩니다. 인스턴스 이름은 **개체 탐색기** 의 **데이터 계층 애플리케이션**노드 아래에 있는 DAC에 대한 노드나 **유틸리티 탐색기** 의 **배포된 데이터 계층 애플리케이션**노드에 표시됩니다.  
  
 다음 옵션은 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에는 적용되지 않으며 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에 배포할 때는 표시되지 않습니다.  
  
 **기본 데이터베이스 위치 사용** - [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스에 대한 기본 위치에 데이터베이스 파일과 로그 파일을 생성하려면 이 옵션을 선택합니다. 파일 이름은 데이터베이스 이름을 사용하여 생성됩니다.  
  
 **데이터베이스 파일 지정** - 데이터와 로그 파일의 다른 위치나 이름을 지정하려면 이 옵션을 선택합니다.  
  
 **데이터 파일 경로 및 이름: -** 데이터 파일의 전체 경로와 파일 이름을 지정합니다. 입력란은 기본 경로와 파일 이름으로 채워집니다. 입력란의 문자열을 편집하여 기본값을 변경하거나 찾아보기 단추를 사용하여 데이터 파일이 있는 폴더를 탐색할 수 있습니다.  
  
 **로그 파일 경로 및 이름:** - 로그 파일의 전체 경로와 파일 이름을 지정합니다. 입력란은 기본 경로와 파일 이름으로 채워집니다. 입력란의 문자열을 편집하여 기본값을 변경하거나 **찾아보기** 단추를 사용하여 로그 파일이 있는 폴더를 탐색할 수 있습니다.  
  
###  <a name="Summary"></a> 요약 페이지  
 이 페이지를 사용하여 DAC를 배포할 때 마법사가 수행할 동작을 검토할 수 있습니다.  
  
 **DAC를 배포하는 데 사용되는 설정은 다음과 같습니다.** - 표시된 정보를 검토하여 수행할 동작이 올바른지 확인합니다. 창에는 선택한 DAC 패키지와 배포하도록 선택한 DAC 인스턴스 이름이 표시됩니다. 창에는 DAC와 연결된 데이터베이스를 만들 때 사용되는 설정도 표시됩니다.  
   
### <a name="deploy-page"></a>배포 페이지  
 이 페이지에서는 배포 작업의 성공 또는 실패를 보고합니다.  
  
 **DAC를 배포하는 중** - DAC를 배포하기 위해 수행한 각 동작의 성공 또는 실패를 보고합니다. 정보를 검토하여 각 동작의 성공 또는 실패를 확인합니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 선택하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **보고서 저장** - 배포 보고서를 HTML 파일로 저장하려면 이 단추를 선택합니다. 파일은 모든 동작에서 생성된 모든 오류를 비롯하여 각 동작의 상태를 보고합니다. 기본 폴더는 Windows 계정의 Documents 폴더에 있는 SQL Server Management Studio\DAC Packages 폴더입니다.  
  
  
##  <a name="deploy-a-dac-using-powershell"></a>PowerShell을 사용하여 DAC 배포  
  
1.  SMO Server 개체를 만든 다음 DAC를 배포할 인스턴스로 설정합니다.  
  
2.  **ServerConnection** 개체를 열고 동일한 인스턴스에 연결합니다.  
  
3.  **System.IO.File** 을 사용하여 DAC 패키지 파일을 로드합니다.  
  
4.  **add_DacActionStarted** 및 **add_DacActionFinished** 를 사용하여 DAC 배포 이벤트를 구독합니다.  
  
5.  **DatabaseDeploymentProperties**를 설정합니다.  
  
6.  **DacStore.Install** 메서드를 사용하여 DAC를 배포합니다.  
  
7.  DAC 패키지 파일을 읽는 데 사용되는 파일 스트림을 닫습니다.  
  
## <a name="powershell-examples"></a>PowerShell 예제  
 다음 예에서는 MyApplication.dacpac 패키지의 DAC 정의를 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)]의 기본 인스턴스에서 MyApplication이라는 DAC를 배포합니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>자세한 정보 
 [데이터 계층 애플리케이션](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터베이스에서 DAC 추출](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [데이터베이스 식별자](../../relational-databases/databases/database-identifiers.md)  
  
  
