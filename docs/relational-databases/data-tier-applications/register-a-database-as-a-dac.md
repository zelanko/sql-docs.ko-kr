---
title: DAC로 데이터베이스 등록 | Microsoft 문서
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: data-tier-applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.registerdacwizard.summary.f1
- sql13.swb.registerdacwizard.introduction.f1
- sql13.swb.registerdacwizard.setproperties.f1
- sql13.swb.registerdacwizard.registerdac.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d14994b4e90429cdd4d3e8a9b58c2b3998492b3d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="register-a-database-as-a-dac"></a>DAC로 데이터베이스 등록
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **데이터 계층 응용 프로그램 등록 마법사** 또는 Windows PowerShell 스크립트를 사용하여 기존 데이터베이스의 개체를 설명하는 DAC(데이터 계층 응용 프로그램)를 작성하고 이 DAC 정의를 **msdb** 시스템 데이터베이스(**의** master [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)])에 등록할 수 있습니다.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **DAC 업그레이드에 사용되는 도구:**  [데이터 계층 응용 프로그램 등록 마법사](#UsingRegisterDACWizard), [PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 등록 프로세스에서는 데이터베이스의 개체를 정의하는 DAC 정의를 만듭니다. DAC 정의와 데이터베이스의 결합으로 DAC 인스턴스가 형성됩니다. DAC를 데이터베이스 엔진의 관리되는 인스턴스에 DAC로 등록할 경우 등록된 DAC는 유틸리티 컬렉션 집합이 인스턴스에서 유틸리티 제어 지점으로 다음에 전송될 때 SQL Server 유틸리티에 통합됩니다. DAC에 있게 됩니다는 **배포 된 데이터 계층 응용 프로그램** 의 노드는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **유틸리티 탐색기** 에 보고 된 **배포 된 데이터 계층 응용 프로그램**세부 정보 페이지입니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]또는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4(서비스 팩 4) 이상의 데이터베이스에서만 DAC 등록을 수행할 수 있습니다. DAC가 데이터베이스에 이미 등록된 경우에는 DAC 등록을 수행할 수 없습니다. 예를 들어 데이터베이스가 DAC를 배포하는 방식으로 만들어진 경우 **데이터 계층 응용 프로그램 등록 마법사**를 실행할 수 없습니다.  
  
 DAC 또는 포함된 사용자가 지원하지 않는 개체가 데이터베이스에 있는 경우 DAC를 등록할 수 없습니다. DAC에서 지원되는 개체 유형에 대한 자세한 내용은 [DAC Support For SQL Server Objects and Versions](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)을 참조하세요.  
  
###  <a name="Permissions"></a> 권한  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 DAC를 등록하려면 하나 이상의 ALTER ANY LOGIN과 데이터베이스 범위 VIEW DEFINITION 권한, **sys.sql_expression_dependencies**에 대한 SELECT 권한 및 **dbcreator** 고정 서버 역할의 멤버 자격이 필요합니다. **sysadmin** 고정 서버 역할의 멤버 또는 기본 제공 SQL Server 시스템 관리자 계정인 **sa** 도 DAC를 등록할 수 있습니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 로그인이 없는 DAC를 등록하려면 **dbmanager** 또는 **serveradmin** 역할의 멤버 자격이 필요합니다. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 에 로그인이 있는 DAC를 등록하려면 **loginmanager** 또는 **serveradmin** 역할의 멤버 자격이 필요합니다.  
  
##  <a name="UsingRegisterDACWizard"></a> 데이터 계층 응용 프로그램 등록 마법사 사용  
 **마법사를 사용하여 DAC를 등록하려면**  
  
1.  **개체 탐색기**에서 DAC로 등록할 데이터베이스가 포함된 인스턴스에 대한 노드를 확장합니다.  
  
2.  **데이터베이스** 노드를 확장합니다.  
  
3.  등록할 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **데이터 계층 응용 프로그램으로 등록…**을 선택합니다.  
  
4.  마법사 대화 상자를 완료합니다.  
  
    1.  [소개 페이지](#Introduction)  
  
    2.  [속성 설정 페이지](#Set_properties)  
  
    3.  [유효성 검사 및 요약 페이지](#Summary)  
  
    4.  [DAC 등록 페이지](#Register)  
  
##  <a name="Introduction"></a> 소개 페이지  
 이 페이지에서는 데이터 계층 응용 프로그램을 등록하는 단계에 대해 설명합니다.  
  
 **이 페이지를 다시 표시 안 함** - 앞으로 이 페이지가 표시되지 않도록 하려면 이 확인란을 클릭합니다.  
  
 **다음 >** - **속성 설정** 페이지로 이동합니다.  
  
 **취소** - DAC를 등록하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
##  <a name="Set_properties"></a> 속성 설정 페이지  
 이 페이지를 사용하여 응용 프로그램 이름 및 버전과 같은 DAC 수준 속성을 지정할 수 있습니다.  
  
 **응용 프로그램 이름.** - DAC 정의를 식별하는 데 사용되는 이름을 지정하는 문자열입니다. 이 필드는 데이터베이스 이름으로 채워집니다.  
  
 **버전.** - DAC의 버전을 식별하는 숫자 값입니다. DAC 버전은 Visual Studio에서 개발자가 작업 중인 DAC의 버전을 식별하는 데 사용됩니다. DAC를 배포하는 경우 이 버전은 **msdb** 데이터베이스에 저장되고 나중에 **의** 데이터 계층 응용 프로그램 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]노드에서 볼 수 있습니다.  
  
 **설명** - 선택 사항입니다. DAC의 용도를 설명하는 텍스트입니다. DAC를 배포하는 경우 이 설명은 **msdb** 데이터베이스에 저장되고 나중에 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 **데이터 계층 응용 프로그램** 노드에서 볼 수 있습니다.  
  
 **< 이전** - **소개** 페이지로 돌아갑니다.  
  
 **다음 >** - 데이터베이스의 개체로 DAC를 작성할 수 있는지 확인하고 **유효성 검사 및 요약** 페이지에 결과를 표시합니다.  
  
 **취소** - DAC를 등록하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
##  <a name="Summary"></a> 유효성 검사 및 요약 페이지  
 이 페이지를 사용하여 DAC를 등록할 때 마법사가 수행할 동작을 검토할 수 있습니다. 이 페이지는 데이터베이스의 개체로 DAC를 작성할 수 있는지 확인할 때 세 가지 상태로 전환됩니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
### <a name="retrieving-objects"></a>개체 검색  
 **데이터베이스 및 서버 개체 검색** - 마법사가 데이터베이스의 모든 필요한 개체 및 데이터베이스 엔진의 인스턴스를 검색할 때 진행률 표시줄을 표시합니다.  
  
 **< 이전** - 입력한 값을 변경하기 위해 **속성 설정** 페이지로 돌아갑니다.  
  
 **다음 >** - DAC를 등록하고 **DAC 등록** 페이지에 결과를 표시합니다.  
  
 **취소** - DAC를 등록하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
### <a name="validating-objects"></a>개체 유효성 확인  
 **.**  *.* **를 실행할 수 없습니다.** *ObjectName* **를 실행할 수 없습니다.** - 마법사가 검색된 개체의 종속성을 확인하고 모두 DAC에 유효한 개체인지 확인할 때 진행률 표시줄을 표시합니다. *SchemaName ***.*** ObjectName*은 현재 확인 중인 개체가 무엇인지 식별합니다.  
  
 **< 이전** - 입력한 값을 변경하기 위해 **속성 설정** 페이지로 돌아갑니다.  
  
 **다음 >** - DAC를 등록하고 **DAC 등록** 페이지에 결과를 표시합니다.  
  
 **취소** - DAC를 등록하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
### <a name="summary"></a>요약  
 **다음 설정이 DAC를 등록하는 데 사용됩니다.** - DAC에 포함될 속성 및 개체에 대한 보고서를 표시합니다.  
  
 **보고서 저장** - 유효성 검사 보고서의 복사본을 HTML 파일로 저장하려면 이 단추를 선택합니다. 기본 폴더는 Windows 계정의 Documents 폴더에 있는 **SQL Server Management Studio\DAC Packages** 폴더입니다.  
  
 **< 이전** - 입력한 값을 변경하기 위해 **속성 설정** 페이지로 돌아갑니다.  
  
 **다음 >** - DAC를 등록하고 **DAC 등록** 페이지에 결과를 표시합니다.  
  
 **취소** - DAC를 등록하지 않고 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
##  <a name="Register"></a> DAC 등록 페이지  
 이 페이지에서는 등록의 성공 또는 실패를 보고합니다.  
  
 **DAC 등록** - DAC를 등록하기 위해 수행한 각 동작의 성공 또는 실패를 보고합니다. 정보를 검토하여 각 동작의 성공 또는 실패를 확인합니다. 오류가 발생한 동작에는 모두 **결과** 열에 링크가 있습니다. 링크를 선택하면 해당 동작의 오류에 대한 보고서가 표시됩니다.  
  
 **보고서 저장** - 등록 보고서를 HTML 파일로 저장하려면 이 단추를 선택합니다. 파일은 모든 동작에서 생성된 모든 오류를 비롯하여 각 동작의 상태를 보고합니다. 기본 폴더는 Windows 계정의 Documents 폴더에 있는 **SQL Server Management Studio\DAC Packages** 폴더입니다. 파일 이름의 형식은 \<DACPackageName>_RegisterDACReport_yyyymmdd.html이며, 여기서 \<*DACPackageName*>은 배포할 패키지의 이름이고 *yyyy*는 현재 연도, *mm*은 현재 월, *dd*는 현재 날짜입니다.  
  
 **마침** - 마법사를 종료합니다.  
  
 [데이터 계층 응용 프로그램 등록 마법사 사용](#UsingRegisterDACWizard)  
  
##  <a name="RegisterDACPowerShell"></a> PowerShell을 사용하여 DAC 등록  
 **PowerShell 스크립트에서 Register() 메서드를 사용하여 데이터베이스를 DAC로 등록하려면**  
  
1.  SMO Server 개체를 만든 후 이 개체를 DAC로 등록할 데이터베이스를 포함하는 인스턴스로 설정합니다.  
  
2.  데이터베이스의 이름을 지정하는 변수를 추가합니다.  
  
3.  DAC에 대한 메타데이터(예: DAC 이름, 버전 및 설명)를 지정합니다.  
  
4.  위에서 지정한 정보로 Register 메서드를 실행합니다.  
  
### <a name="example-powershell"></a>예제(PowerShell)  
 다음 예에서는 MyDB라는 데이터베이스를 DAC로 등록합니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 응용 프로그램](../../relational-databases/data-tier-applications/data-tier-applications.md)  
  
  
