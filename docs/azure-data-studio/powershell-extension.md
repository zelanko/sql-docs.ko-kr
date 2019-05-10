---
title: PowerShell 확장
titleSuffix: Azure Data Studio
description: 설치 하 고 PowerShell을 사용 하 여 Azure Data Studio에 대 한
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: c7a2dbdccf92a52d5733a04915acc3f76dc3f033
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105954"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Azure Data Studio 용 PowerShell 편집기 지원

이 확장 프로그램에서 다양 한 PowerShell 편집기 지원 제공 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio)합니다.
이제 작성 하 고 Azure Data Studio 제공 하는 훌륭한 IDE 비슷한 인터페이스를 사용 하는 PowerShell 스크립트를 디버그할 수 있습니다.

![PowerShell 확장](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>기능

- 구문 강조 표시
- 코드 조각
- Cmdlet 및 기타 정보에 대 한 IntelliSense
- 제공 하는 규칙 기반 분석 [PowerShell 스크립트 분석기](http://github.com/PowerShell/PSScriptAnalyzer)
- Cmdlet 및 변수 정의로 이동
- Cmdlet 및 변수의 참조 찾기
- 문서 및 작업 영역 기호 검색
- 사용 하 여 PowerShell 코드의 선택 된 선택 항목 실행 <kbd>F8</kbd>
- 사용 하 여 커서 아래의 기호에 대 한 온라인 도움말을 시작할 <kbd>Ctrl</kbd>+<kbd>F1</kbd>
- 기본 대화형 콘솔 지원도 가능 합니다.


## <a name="installing-the-extension"></a>확장 설치

단계를 수행 하 여 PowerShell 확장의 공식 릴리스를 설치할 수 있습니다 합니다 [Azure Data Studio 설명서](https://docs.microsoft.com/sql/azure-data-studio/extensions)합니다.
확장 창에서 "PowerShell" 확장에 대 한 검색 하 고 설치 합니다.  알림을 받을 수 자동으로 모든 향후 확장 업데이트에 대 한!

VSIX 패키지를 설치할 수도 있습니다 우리의 [릴리스 페이지](https://github.com/PowerShell/vscode-powershell/releases) 및 명령줄을 통해 설치:

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>플랫폼 지원

- **Windows 7 ~ 10** 이상 및 Windows PowerShell v3 및 PowerShell Core
- **Linux** PowerShell core (모든 PowerShell 지원 배포)
- **macOS** PowerShell Core를 사용 하 여

읽기를 [FAQ](https://github.com/PowerShell/vscode-powershell/wiki/FAQ) 일반적인 질문에 답변 합니다.

## <a name="installing-powershell-core"></a>PowerShell Core 설치

MacOS 또는 Linux에서 Azure Data Studio를 실행 하는 경우 PowerShell Core를 설치 해야 할 수 있습니다.

PowerShell Core는 오픈 소스 프로젝트 켜져 [GitHub](https://github.com/powershell/powershell)합니다.
MacOS 또는 Linux 플랫폼에서 PowerShell Core 설치에 대 한 자세한 내용은 다음 문서를 참조 하세요.

- [Linux에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [MacOS에서 PowerShell Core 설치](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>예제 스크립트

일부 예제 스크립트에에서 있는 확장의 `examples` PowerShell 편집 및 디버깅 기능을 검색 하는 데 사용할 수 있는 폴더입니다.  포함 된 확인해 [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) 파일을 사용 하는 방법에 자세히 알아봅니다.

이 폴더는 다음 경로에서 찾을 수 있습니다.

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

확장의 미리 보기 버전을 사용 하는 경우 또는

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

보기로 열기/확장의 예제에서 Azure Data Studio, PowerShell 명령 프롬프트에서 다음 코드를 실행 합니다.

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>만들기 및 파일 열기

를 만들고 편집기 내에서 새 파일을 열고는 새로 만들기-EditorFile에서 PowerShell 통합 터미널 내에서 사용 합니다.

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

이 명령은 PowerShell 파일 뿐 아니라 모든 파일 형식에 대해 작동합니다.

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

사용 하 여 Azure Data Studio에서 하나 이상의 파일을 여는 `Open-EditorFile` 명령입니다.

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>실행할 때 콘솔에서 포커스 없음

SSMS를 사용 하는 데 사용 되는 해당 사용자의 경우 익숙한 쿼리를 실행할 수 있도록 하 고 다음 다시 쿼리 창으로 전환 하지 않고도 다시 실행할 수 있습니다.  이 경우 코드 편집기의 기본 동작에 이상한 생각 될 수도 있습니다.  사용 하 여 실행 하면 편집기에서 포커스를 유지할 <kbd>F8</kbd> 다음 설정을 변경 합니다.

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

기본값은 `true` 편리한 액세스를 위해.

이 설정은 명시적으로 입력에 대 한 호출 명령을 사용 하는 경우에 콘솔에 변경에서 포커스를 못합니다 주의 `Get-Credential`합니다.

## <a name="sql-powershell-examples"></a>SQL PowerShell 예제
이러한 예제 (아래)를 사용 하려면에서 SqlServer 모듈을 설치 해야 합니다 [PowerShell 갤러리](https://www.powershellgallery.com/packages/SqlServer)합니다.

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> 버전을 사용 하 여 `21.1.18102` 이상, 합니다 `SqlServer` 모듈은 지원 [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 이상, Windows PowerShell 외에도 합니다.

이 예에서 사용 된 `Get-SqlInstance` ServerA 및 ServerB에 대 한 SMO Server 개체를 가져오려는 cmdlet.  이 명령은 인스턴스 이름을 포함 됩니다에 대 한 출력의 기본 버전, 서비스 팩 & 인스턴스의 CU 업데이트 수준입니다.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

다음은 샘플에 출력 같이 표시 됩니다.

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```
합니다 `SqlServer` 라는 공급자를 포함 하는 모듈 `SQLRegistration` 다음 형식에 저장 된 SQL Server 연결을 프로그래밍 방식으로 액세스할 수 있습니다.

+ 데이터베이스 엔진 서버 (등록 된 서버)
+ 중앙 관리 서버 (CMS)
+ Analysis Services
+ Integration Services
+ Reporting Services

 다음 예에서는 작업을 수행 합니다는 `dir` (별칭 `Get-ChildItem`)에 등록 된 서버 파일에 나열 된 모든 SQL Server 인스턴스 목록을 가져올 수 있습니다.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse 
```

다음은 샘플에 출력은 다음과 같을 수 있습니다.

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

데이터베이스 또는 데이터베이스 내의 개체를 포함 하는 여러 가지 작업에는 `Get-SqlDatabase` cmdlet을 사용할 수 있습니다.  모두에 대 한 값을 제공 합니다 `-ServerInstance` 및 `-Database` 매개 변수를 해당 데이터베이스 개체만 검색 됩니다.  그러나 지정 하는 경우는 `-ServerInstance` 매개 변수를 해당 인스턴스에서 모든 데이터베이스의 전체 목록이 반환 됩니다.

다음은 샘플에 출력 같이 표시 됩니다.

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa
master               Normal        6.00 MB  368.00 KB Simple       140 sa
model                Normal       16.00 MB    5.53 MB Full         140 sa
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa
```

이 다음 예제에서는 `Get-SqlDatabase` ServerB 인스턴스에서 모든 데이터베이스 목록을 검색 하는 cmdlet은 다음 표/테이블을 제공 (사용 하 여를 `Out-GridView` cmdlet) 백업할 데이터베이스를 선택 합니다.  사용자가 "확인" 단추를 클릭 한 후 강조 표시 된 데이터베이스만 백업 됩니다.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

이 예제에서는 마찬가지로: 등록 된 서버 파일에 나열 된 모든 SQL Server 인스턴스의 목록 가져오기 호출을 `Get-SqlAgentJobHistory` 나열 된 각 SQL Server 인스턴스에 대 한 자정 이후의 모든 실패 한 SQL 에이전트 작업을 보고 하는 합니다.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

이 예에서는 작업을 수행 합니다는 `dir` (별칭 `Get-ChildItem`)를 등록 된 서버 파일에 나열 된 모든 SQL Server 인스턴스 목록을 가져오고 사용 하 여는 `Get-SqlDatabase` 해당 인스턴스의 각 데이터베이스의 목록을 확인 하는 cmdlet입니다.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

다음은 샘플에 출력 같이 표시 됩니다.

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level      
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa   
master               Normal        6.00 MB  368.00 KB Simple       140 sa   
model                Normal       16.00 MB    5.53 MB Full         140 sa   
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa   
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa   
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa   
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa   
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa   
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa   
```

## <a name="reporting-problems"></a>문제 보고

PowerShell 확장을 사용 하 여 문제가 있으면 참조 [문제 해결 문서](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md) 진단 및 문제를 보고에 대 한 정보에 대 한 합니다.

#### <a name="security-note"></a>보안 정보

모든 보안 문제에 대 한 참조 [여기](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security)합니다.

## <a name="contributing-to-the-code"></a>코드에 영향을 주는

체크 아웃 합니다 [개발 설명서](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md) 이 확장에 참여 하는 방법에 대 한 자세한 내용은!

## <a name="maintainers"></a>유지 관리자

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>라이선스

이 확장은 [MIT 라이선스에 따라 사용이 허가](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt)합니다. 이 프로젝트의 릴리스를 사용 하 여 포함 하는 타사 이진 파일에 대 한 내용은 참조는 [제 3 자 통지](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt) 파일입니다.

## <a name="code-of-conductconduct-md"></a>[사용 규정][conduct-md]

이 프로젝트에 도입 된 [Microsoft 오픈 소스 준수 사항][conduct-code]합니다.
자세한 내용은 참조는 [준수 사항 FAQ] [ conduct-FAQ] 에 게 문의 하거나 [ opencode@microsoft.com ] [ conduct-email] 추가 질문이 나 의견을 사용 하 여 합니다.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
