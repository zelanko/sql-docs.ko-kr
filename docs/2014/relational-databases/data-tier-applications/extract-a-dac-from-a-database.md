---
title: 데이터베이스에서 DAC 추출 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.extractdacwizard.buildandsave.f1
- sql12.swb.extractdacwizard.setdacproperties.f1
- sql12.swb.extractdacwizard.validationandsummary.f1
- sql12.swb.extractdacwizard.introduction.f1
- sql12.swb.extractdacwizard.selectdatapage.f1
helpviewer_keywords:
- extract DAC
- How to [DAC], extract
- data-tier application [SQL Server], extract
- wizard [DAC], extract
ms.assetid: ae52a723-91c4-43fd-bcc7-f8de1d1f90e5
author: stevestein
ms.author: sstein
ms.openlocfilehash: adc5a8eb0317e53b51927402608a8d9b1a09a76f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970237"
---
# <a name="extract-a-dac-from-a-database"></a>데이터베이스에서 DAC 추출
  **데이터 계층 애플리케이션 추출 마법사** 나 Windows PowerShell 스크립트를 사용하여 기존 SQL Server 데이터베이스에서 DAC(데이터 계층 애플리케이션) 패키지를 추출할 수 있습니다. 추출이 끝나면 데이터베이스 개체의 정의 및 이와 관련된 인스턴스 수준 요소를 포함하는 DAC 패키지 파일이 생성됩니다. 예를 들어 DAC 패키지 파일에는 데이터베이스 테이블, 저장 프로시저, 뷰, 사용자, 그리고 데이터베이스 사용자에 매핑되는 로그인이 포함됩니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **DAC를 추출 하려면**[데이터 계층 응용 프로그램 추출 마법사](#UsingDACExtractWizard), [PowerShell](#ExtractDACPowerShell) 을 사용 합니다.    
  
## <a name="before-you-begin"></a>시작하기 전에  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]또는 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 서비스 팩 4 이상의 인스턴스에 있는 데이터베이스에서 DAC를 추출할 수 있습니다. DAC에서 배포된 데이터베이스에 대해 추출 프로세스를 실행하는 경우 데이터베이스에서 개체 정의만 추출됩니다. 프로세스는에 등록 된 DAC `msdb` (의**master** )를 참조 하지 않습니다 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] . 추출 프로세스에서는 데이터베이스 엔진의 현재 인스턴스에 DAC 정의를 등록하지 않습니다. DAC를 등록하는 방법은 [Register a Database As a DAC](register-a-database-as-a-dac.md)을 참조하세요.  
  
###  <a name="limitations-and-restrictions"></a><a name="LimitationsRestrictions"></a> 제한 사항  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4(서비스 팩 4) 이상에서만 데이터베이스에서 DAC를 추출할 수 있습니다. DAC 또는 포함된 사용자가 지원하지 않는 개체가 데이터베이스에 있는 경우 DAC를 추출할 수 없습니다. DAC에서 지원되는 개체 유형에 대한 자세한 내용은 [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md)을 참조하세요.  
  
###  <a name="permissions"></a><a name="Permissions"></a> 권한  
 DAC를 추출하려면 **sys.sql_expression_dependencies**에 대한 SELECT 권한뿐만 아니라 최소한 ALTER ANY LOGIN 및 데이터베이스 범위 VIEW DEFINITION 권한이 있어야 합니다. DAC를 추출하려면 securityadmin 고정 서버 역할의 멤버이면서 DAC를 추출하는 데이터베이스의 database_owner 고정 데이터베이스 역할의 멤버여야 합니다. sysadmin 고정 서버 역할의 멤버 또는 기본 제공 SQL Server 시스템 관리자 계정인 **sa** 도 DAC를 추출할 수 있습니다.  
  
##  <a name="using-the-extract-data-tier-application-wizard"></a><a name="UsingDACExtractWizard"></a> 데이터 계층 애플리케이션 추출 마법사 사용  
 **마법사를 사용하여 DAC를 추출하려면**  
  
1.  **개체 탐색기**에서 DAC를 추출할 데이터베이스가 포함된 인스턴스에 대한 노드를 확장합니다.  
  
2.  **데이터베이스** 노드를 확장합니다.  
  
3.  DAC를 추출할 데이터베이스의 노드를 마우스 오른쪽 단추로 클릭 하 고 **태스크**를 가리킨 다음 **데이터 계층 응용 프로그램 추출** ...을 선택 합니다.  
  
4.  마법사 대화 상자를 완료합니다.  
  
    1.  [소개 페이지](#Introduction)  
  
    2.  [데이터 선택 페이지](#SelectData)  
  
    3.  [속성 설정 페이지](#SetProperties)  
  
    4.  [유효성 검사 및 요약 페이지](#ValidateSummary)  
  
    5.  [패키지 빌드 페이지](#BuildPackage)  
  
###  <a name="introduction-page"></a><a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 데이터 계층 애플리케이션을 추출하는 단계에 대해 설명합니다.  
  
 **이 페이지를 다시 표시 안 함** - 앞으로 이 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
 **다음 >** - **방법 선택** 페이지로 진행합니다.  
  
 **취소** - 데이터 계층 애플리케이션을 데이터베이스에서 추출하지 않고 마법사를 종료합니다.  
  
###  <a name="select-data-page"></a><a name="SelectData"></a>데이터 선택 페이지  
 마법사의 이 페이지를 사용하여 DAC(데이터 계층 애플리케이션) 패키지 파일에 포함할 참조 데이터를 선택할 수 있습니다. DAC 패키지에 데이터를 포함하는 것은 선택 사항입니다. 지원되는 모든 데이터베이스 개체 및 데이터베이스와 관련된 인스턴스 개체의 스키마는 DAC 패키지에 미리 포함됩니다.  
  
 최대 10MB의 참조 데이터를 DAC 패키지 파일에 포함할 수 있습니다. 그러나 DAC에 테이블을 포함하려는 경우 테이블에 **image** 또는 **varchar(max)** 와 같은 BLOB(Binary Large Object) 데이터 형식을 포함할 수 없습니다. 다른 데이터베이스로 전송하기 위해 많은 양의 데이터를 추출하려는 경우 SQL Server Integration Services, 대량 복사 유틸리티 또는 다른 여러 데이터 마이그레이션 방법 중 하나를 사용하세요.  
  
 **데이터베이스 테이블** - DAC 패키지에 포함할 데이터가 포함된 데이터베이스 테이블 옆의 확인란을 선택합니다. 10,000개 이하의 행이 포함된 테이블을 10개까지 선택할 수 있습니다.  
  
###  <a name="set-properties-page"></a><a name="SetProperties"></a>속성 설정 페이지  
 이 마법사 페이지를 사용하여 DAC(데이터 계층 애플리케이션)를 기술할 수 있습니다. 이러한 속성은 DAC를 식별하는 데 사용되고 다른 DAC와 구별하는 데 도움이 됩니다.  
  
 **이름** - 이 이름은 DAC를 식별합니다. DAC 이름은 DAC 패키지 파일의 이름과 다를 수 있으며 애플리케이션 특징을 기술해야 합니다. 예를 들어 데이터베이스가 재무 애플리케이션에 사용되는 경우 DAC Finance라는 이름을 지정할 수 있습니다.  
  
 **버전(xx.xx.xx.xx 사용, x는 숫자)** - DAC의 버전을 식별하는 숫자 값입니다. DAC 버전은 Visual Studio에서 개발자가 작업 중인 DAC의 버전을 식별하는 데 사용됩니다. DAC를 배포 하는 경우 버전은 데이터베이스에 저장 되 `msdb` 고 나중에의 **데이터 계층 응용 프로그램** 노드에서 볼 수 있습니다 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 **설명:** - 선택 사항입니다. DAC에 대해 설명합니다. DAC를 배포할 때 설명은 데이터베이스에 저장 `msdb` 되며 나중에의 **데이터 계층 응용 프로그램** 노드에서 볼 수 있습니다 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] .  
  
 **DAC 패키지 파일에 저장(파일 이름에 .dacpac 확장명 포함):** - DAC를 확장명이 .dacpac인 DAC 패키지 파일에 저장합니다. 파일의 이름과 위치를 지정하려면 **찾아보기** 단추를 클릭합니다.  
  
 **기존 파일 덮어쓰기** - 이름이 같은 파일이 이미 있을 경우 DAC 패키지 파일을 바꾸려면 이 확인란을 선택합니다.  
  
###  <a name="validation-and-summary-page"></a><a name="ValidateSummary"></a>유효성 검사 및 요약 페이지  
 이 페이지에서 마법사는 모든 데이터베이스 개체가 DAC(데이터 계층 애플리케이션)에 의해 지원되는지 확인합니다. 또한 데이터베이스 개체 간의 종속성도 검사하여 DAC에 성공적으로 포함될 수 있는 개체 집합을 확인합니다. 그런 다음 유효성 검사 보고서를 표시하고 이 마법사에서 선택한 옵션을 요약합니다. 옵션을 변경하려면 **이전**을 클릭하고, DAC 추출을 시작하려면 **다음**을 클릭합니다.  
  
> [!NOTE]  
>  DAC에서 지원하지 않는 개체가 하나 이상 있으면 **다음** 단추가 비활성화되고 추출 프로세스를 계속할 수 없습니다. 이 경우에는 지원되지 않는 개체를 제거하고 이 마법사를 다시 실행하는 것이 좋습니다.  
  
 **요약** - 선택한 옵션에 대한 요약 정보가 **DAC 속성**아래에 나열됩니다. 유효성 검사 결과는 **DAC 개체**아래에 나열됩니다. 유효성 검사 결과는 다음과 같은 세 가지 유형으로 나타납니다.  
  
-   **DAC에서 지원되는 개체**: 여기에 나열되는 개체 및 개체 종속성은 지원되며 DAC에 성공적으로 포함될 수 있습니다.  
  
-   **DAC에서 지원되지만 경고가 있는 개체**: 여기에 나열되는 개체는 지원되지만 DAC에서 지원하지 않는 다른 개체에 종속되어 있습니다.  
  
-   **DAC에서 지원되지 않는 개체**: 여기에 나열되는 개체는 지원되지 않으므로 DAC를 추출하기 전에 데이터베이스에서 제거해야 합니다.  
  
 유효성 프로세스에서는 여러 수준의 종속성을 검사합니다. 예를 들어 지원되지 않는 CLR 데이터 형식을 사용하는 테이블에 종속된 저장 프로시저는 **DAC에서 지원되지만 경고가 있는 개체**아래에 나열됩니다.  
  
 DAC에서 지원하지 않는 개체가 하나 이상 있으면 **다음** 단추가 비활성화되고 추출 프로세스를 계속할 수 없습니다. 이 경우에는 지원되지 않는 개체를 제거하고 이 마법사를 다시 실행하는 것이 좋습니다.  
  
 **보고서 저장** - 요약에서 **DAC 개체** 노드 아래의 모든 개체를 나열하는 HTML 기반 파일을 저장할 수 있습니다. 이 보고서는 DAC에서 일부 데이터베이스 개체가 지원되지 않는 경우 유용합니다. DAC를 다시 추출하기 전에 이 보고서를 사용하여 지원되지 않는 개체를 변경하거나 제거할 수 있습니다.  
  
###  <a name="build-package-page"></a><a name="BuildPackage"></a>패키지 빌드 페이지  
 이 페이지를 사용하여 마법사에서 DAC(데이터 계층 애플리케이션)를 추출할 때 진행률을 모니터링할 수 있습니다.  
  
 **동작** - **DAC 패키지 파일 만들기 및 저장** 동작을 수행하는 동안 마법사는 SQL Server 데이터베이스에서 DAC를 추출합니다. 그런 다음 메모리에 DAC 패키지가 만들어지고 사용자가 지정한 위치에 저장됩니다. 해당 단계의 결과를 확인하려면 **결과** 열의 링크를 클릭합니다.  
  
 **보고서 저장** - 마법사의 진행률 결과를 파일로 저장하려면 클릭합니다.  
  
 **마침** - 처리가 완료된 후에나 오류가 발생한 경우 마법사를 닫으려면 클릭합니다.  
  
##  <a name="extract-a-dac-using-powershell"></a><a name="ExtractDACPowerShell"></a>PowerShell을 사용 하 여 DAC 추출  
 **PowerShell 스크립트에서 Extract() 메서드를 사용하여 데이터베이스에서 DAC를 추출하려면**  
  
1.  SMO Server 개체를 만든 후 이 개체를 DAC를 추출할 데이터베이스를 포함하는 인스턴스로 설정합니다.  
  
2.  데이터베이스의 이름을 지정하는 변수를 추가합니다.  
  
3.  DAC에 대한 메타데이터(예: DAC 이름, 버전 및 설명)를 지정합니다.  
  
4.  추출한 DAC 패키지 파일의 경로와 파일 이름을 지정합니다.  
  
5.  위에서 지정한 정보를 사용하여 Extract 메서드를 실행합니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 다음 예에서는 MyDB 데이터베이스에서 MyApplication이라는 DAC를 추출합니다.  
  
```powershell
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = Get-Item .  
  
## Specify the database to extract to a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Specify the location and name for the extracted DAC package.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
  
## Extract the DAC.  
$extractionunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$extractionunit.Description = $description  
$extractionunit.Extract($dacpacPath)  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 애플리케이션](data-tier-applications.md)  
