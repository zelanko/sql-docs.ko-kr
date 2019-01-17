---
title: DAC 패키지 유효성 검사 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- data-tier application [SQL Server], validate
- data-tier application [SQL Server], compare
- validate DAC
- compare DACs
- data-tier application [SQL Server], view
- view DAC
ms.assetid: 726ffcc2-9221-424a-8477-99e3f85f03bd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5e7e22f164ba8da071a93dff1535b777993e76e2
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590477"
---
# <a name="validate-a-dac-package"></a>DAC 패키지 유효성 검사
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  DAC 패키지를 프로덕션 환경에 배포하기 전에 내용을 검토하고 기존 DAC를 업그레이드하기 전에 업그레이드 동작의 유효성을 검사하는 것이 좋습니다. 사용자의 조직에서 개발되지 않은 패키지를 배포하는 경우에는 더욱 그렇습니다.  
  
1.  **시작하기 전 주의 사항:**  [필수 구성 요소](#Prerequisites)  
  
2.  **DAC를 업그레이드하려면 다음을 사용합니다.**  [DAC 내용 보기](#ViewDACContents), [데이터베이스 변경 내용 보기](#ViewDBChanges), [업그레이드 동작 보기](#ViewUpgradeActions), [DAC 비교](#CompareDACs)  
  
##  <a name="Prerequisites"></a> 사전 요구 사항  
 출처를 알 수 없거나 신뢰할 수 없는 DAC 패키지는 배포하지 않는 것이 좋습니다. 이러한 DAC에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마를 수정하여 오류가 발생할 수 있습니다. 출처를 알 수 없거나 신뢰할 수 없는 DAC를 사용하기 전에 격리된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 테스트 인스턴스에 이를 배포하고, 해당 데이터베이스에 대해 [DBCC CHECKDB&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)를 실행하며, 저장 프로시저 또는 다른 사용자 정의 코드 같은 데이터베이스의 코드도 검사하세요.  
  
##  <a name="ViewDACContents"></a> DAC 내용 보기  
 데이터 계층 애플리케이션(DAC) 패키지의 내용을 볼 수 있는 두 가지 메커니즘이 있습니다. SQL Server Developer Tools의 DAC 프로젝트로 DAC 패키지를 가져올 수 있습니다. 두 번째는 패키지 내용을 폴더에 압축을 푸는 것입니다.  
  
 **SQL Server Developer Tools에서 DAC 보기**  
  
1.  **파일** 메뉴를 열고 **새로 만들기**를 선택한 다음, **프로젝트...** 를 선택합니다.  
  
2.  **SQL Server** 프로젝트 템플릿을 선택하고 **이름**, **위치**및 **솔루션 이름**을 지정합니다.  
  
3.  **솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **속성...** 을 선택합니다.  
  
4.  **프로젝트 설정** 탭의 **출력 유형** 섹션에서 **데이터 계층 애플리케이션(.dacpac 파일)** 확인란을 선택한 다음 속성 대화 상자를 닫습니다.  
  
5.  **솔루션 탐색기**에서 프로젝트 노드를 마우스 오른쪽 단추로 클릭하고 **데이터 계층 애플리케이션 가져오기...** 를 선택합니다.  
  
6.  **솔루션 탐색기** 를 사용하여 서버 선택 정책과 배포 이전 및 배포 이후 스크립트와 같은 DAC의 모든 파일을 열 수 있습니다.  
  
7.  **스키마 뷰** 를 사용하여 스키마 내의 모든 개체를 검토할 수 있으며, 특히 함수나 저장 프로시저와 같은 개체 내의 코드를 검토할 수 있습니다.  
  
 **폴더에서 DAC 보기**  
  
-   [Unpack a DAC Package](../../relational-databases/data-tier-applications/unpack-a-dac-package.md)의 지침에 따라 폴더에 DAC 패키지의 압축을 풉니다.  
  
-   [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]스크립트를 열어서 내용을 확인합니다.  
  
-   메모장 같은 도구에서 텍스트 파일의 내용 보기  
  
##  <a name="ViewDBChanges"></a> 데이터베이스 변경 내용 보기  
 현재 버전의 DAC를 프로덕션 환경에 배포한 이후에 연결된 데이터베이스를 직접 변경하여 새 버전의 DAC에 정의된 스키마와 충돌할 수 있습니다. 따라서 새 버전의 DAC로 업그레이드하기 전에 데이터베이스가 그런 식으로 변경되었는지 확인하세요.  
  
 **마법사를 사용하여 데이터베이스 변경 내용 보기**  
  
1.  새 버전의 DAC를 포함하는 DAC 패키지와 현재 배포된 DAC를 지정하여 **데이터 계층 애플리케이션 업그레이드** 마법사를 실행합니다.  
  
2.  **변경 내용 검색** 페이지에서 데이터베이스에 대한 변경 내용 보고서를 검토합니다.  
  
3.  업그레이드를 중단하려면 **취소** 를 선택합니다.  
  
4.  마법사 사용에 대한 자세한 내용은 [데이터 계층 애플리케이션 업그레이드](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)를 참조하세요.  
  
 **PowerShell을 사용하여 데이터베이스 변경 내용 보기**  
  
1.  SMO Server 개체를 만든 다음 보려는 DAC를 포함하는 인스턴스로 설정합니다.  
  
2.  **ServerConnection** 개체를 열고 동일한 인스턴스에 연결합니다.  
  
3.  DAC 이름을 변수로 지정합니다.  
  
4.  **GetDatabaseChanges()** 메서드를 사용하여 **ChangeResults** 개체를 검색하고 개체를 텍스트 파일에 파이핑하여 새 개체, 삭제된 개체 및 변경된 개체에 대한 간단한 보고서를 생성합니다.  
  
### <a name="view-database-changes-example-powershell"></a>데이터베이스 변경 내용 보기 예(PowerShell)  
 **데이터베이스 변경 내용 보기 예(PowerShell)**  
  
 다음 예에서는 MyApplicaiton이라는 배포된 DAC에 대한 데이터베이스 변경 내용을 보고합니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the change list and save to file.  
$dacChanges = $dacstore.GetDatabaseChanges($dacName) | Out-File -Filepath C:\DACScripts\MyApplicationChanges.txt  
```  
  
##  <a name="ViewUpgradeActions"></a> 업그레이드 동작 보기  
 새 버전의 DAC 패키지를 사용하여 이전 DAC 패키지에서 배포된 DAC를 업그레이드하기 전에 업그레이드 동안 실행할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 포함된 보고서를 생성한 다음 문을 검토할 수 있습니다.  
  
 **마법사를 사용하여 업그레이드 동작 보고**  
  
1.  새 버전의 DAC를 포함하는 DAC 패키지와 현재 배포된 DAC를 지정하여 **데이터 계층 애플리케이션 업그레이드** 마법사를 실행합니다.  
  
2.  **요약** 페이지에서 업그레이드 동작 보고서를 검토합니다.  
  
3.  업그레이드를 중단하려면 **취소** 를 선택합니다.  
  
4.  마법사 사용에 대한 자세한 내용은 [데이터 계층 애플리케이션 업그레이드](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)를 참조하세요.  
  
 **PowerShell을 사용하여 업그레이드 동작 보고**  
  
1.  SMO Server 개체를 만든 다음 배포된 DAC를 포함하는 인스턴스로 설정합니다.  
  
2.  **ServerConnection** 개체를 열고 동일한 인스턴스에 연결합니다.  
  
3.  **System.IO.File** 을 사용하여 DAC 패키지 파일을 로드합니다.  
  
4.  DAC 이름을 변수로 지정합니다.  
  
5.  **GetIncrementalUpgradeScript()** 메서드를 사용하여 업그레이드를 실행할 Transact-SQL 문 목록을 가져온 다음 목록을 텍스트 파일에 파이핑합니다.  
  
6.  DAC 패키지 파일을 읽는 데 사용되는 파일 스트림을 닫습니다.  
  
### <a name="view-upgrade-actions-example-powershell"></a>업그레이드 동작 보기 예(PowerShell)  
 **업그레이드 동작 보기 예(PowerShell)**  
  
 다음 예에서는 MyApplication이라는 DAC를 MyApplication2017.dacpac 파일에 정의된 스키마로 업그레이드하기 위해 실행하는 Transact-SQL 문에 대해 보고합니다.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication2017.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Specify the DAC instance name.  
$dacName  = "MyApplication"  
  
## Generate the upgrade script and save to file.  
$dacstore.GetIncrementalUpgradeScript($dacName, $dacType) | Out-File -Filepath C:\DACScripts\MyApplicationUpgrade.sql  
  
## Close the filestream to the new DAC package.  
$fileStream.Close()  
```  
  
##  <a name="CompareDACs"></a> Compare DACs  
 DAC를 업그레이드하기 전에 데이터베이스와 인스턴스 수준 개체에서 현재와 새 DAC의 차이를 검토하는 것이 좋습니다. 현재 DAC의 패키지 복사본이 없는 경우에는 현재 데이터베이스에서 패키지를 추출할 수 있습니다.  
  
 두 DAC 프로젝트를 SQL Server Developer Tools의 DAC 프로젝트로 가져오면 스키마 비교 도구를 사용하여 두 DAC 간의 차이점을 분석할 수 있습니다.  
  
 또는 별도의 폴더에 DAC의 압축을 풉니다. 그런 다음 WinDiff 유틸리티와 같은 비교 도구를 사용하여 차이를 분석할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 계층 애플리케이션](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [데이터 계층 애플리케이션 배포](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [데이터 계층 애플리케이션 업그레이드](../../relational-databases/data-tier-applications/upgrade-a-data-tier-application.md)  
  
  
