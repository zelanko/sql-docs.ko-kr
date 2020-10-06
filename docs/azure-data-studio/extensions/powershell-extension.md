---
title: PowerShell 확장
description: 스크립트를 작성하고 디버그하기 위한 다양한 기능을 갖춘 PowerShell 편집기 지원을 제공하는 Azure Data Studio PowerShell 확장을 설치하고 사용하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
ms.reviewer: alayu, maghan, sstein
ms.custom: ''
ms.date: 04/19/2019
ms.openlocfilehash: ede862fe5bbfe975e7c8694782960ced974122b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725138"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Azure Data Studio에 대한 PowerShell 편집기 지원

이 확장은 [Azure Data Studio](https://github.com/Microsoft/azuredatastudio)에서 다양한 PowerShell 편집기를 지원합니다.
이제 Azure Data Studio에서 제공하는 뛰어난 IDE 유사 인터페이스를 사용하여 PowerShell 스크립트를 작성하고 디버그할 수 있습니다.

![PowerShell 확장](media/powershell-extension/powershell-extension.png)

## <a name="features"></a>기능

- 구문 강조 표시
- 코드 조각
- cmdlet 등에 대한 IntelliSense
- [PowerShell 스크립트 분석기](http://github.com/PowerShell/PSScriptAnalyzer)에서 제공하는 규칙 기반 분석
- cmdlet 및 변수 정의로 이동
- cmdlet 및 변수의 참조 찾기
- 문서 및 작업 영역 기호 검색
- <kbd>F8</kbd> 키를 사용하여 선택한 PowerShell 코드 실행
- <kbd>Ctrl</kbd>+<kbd>F1</kbd>을 사용하여 커서 아래에 있는 기호에 대한 온라인 도움말 시작
- 기본 대화형 콘솔 지원

## <a name="installing-the-extension"></a>확장 설치

[Azure Data Studio 설명서](./add-extensions.md)의 단계에 따라 PowerShell 확장의 공식 릴리스를 설치할 수 있습니다.
확장 창에서 "PowerShell" 확장을 검색하여 설치합니다.  후속 확장 업데이트에 대한 알림이 자동으로 제공됩니다.

[릴리스 페이지](https://github.com/PowerShell/vscode-powershell/releases)에서 VSIX 패키지를 설치하고 명령줄을 통해 설치할 수도 있습니다.

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>플랫폼 지원

- Windows PowerShell v3 이상 및 PowerShell Core를 포함하는 **Windows 7 ~ 10**
- PowerShell Core를 포함하는 **Linux**(모든 PowerShell 지원 배포판)
- PowerShell Core를 포함하는 **macOS**

일반적인 질문에 대한 대답을 보려면 [FAQ](https://github.com/PowerShell/vscode-powershell/wiki/FAQ)를 참조하세요.

## <a name="installing-powershell-core"></a>PowerShell Core 설치

macOS 또는 Linux에서 Azure Data Studio를 실행하는 경우 PowerShell Core를 설치해야 할 수도 있습니다.

PowerShell Core는 [GitHub](https://github.com/powershell/powershell)의 오픈 소스 프로젝트입니다.
macOS 또는 Linux 플랫폼에 PowerShell Core를 설치하는 방법에 대한 자세한 내용은 다음 문서를 참조하세요.

- [Linux에서 PowerShell Core 설치](/powershell/scripting/install/installing-powershell-core-on-linux)
- [macOS에서 PowerShell Core 설치](/powershell/scripting/install/installing-powershell-core-on-macos)

## <a name="example-scripts"></a>예제 스크립트

확장의 `examples` 폴더에는 PowerShell 편집 및 디버깅 기능을 검색하는 데 사용할 수 있는 몇 가지 예제 스크립트가 있습니다.  사용 방법을 자세히 알아보려면 포함된 [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) 파일을 확인하세요.

이 폴더는 다음 경로에서 찾을 수 있습니다.

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

또는 확장의 미리 보기 버전을 사용하는 경우

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

Azure Data Studio에서 확장의 예제를 열어서 보려면 PowerShell 명령 프롬프트에서 다음 코드를 실행합니다.

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>파일 만들기 및 열기

편집기 내에서 새 파일을 만들고 열려면 PowerShell 통합 터미널 내에서 New-EditorFile을 사용합니다.

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

이 명령은 PowerShell 파일 뿐만 아니라 모든 파일 형식에 작동합니다.

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

Azure Data Studio에서 하나 이상의 파일을 열려면 `Open-EditorFile` 명령을 사용합니다.

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>실행 시 콘솔에 포커스 없음

SSMS 작업을 수행하는 데 익숙한 사용자의 경우, 쿼리를 실행한 다음, 쿼리 창으로 다시 전환하지 않고도 쿼리를 다시 실행할 수 있을 것입니다.  이 경우 코드 편집기의 기본 동작이 사용자에게 이상하게 느껴질 수 있습니다.  <kbd>F8</kbd> 키를 사용하여 실행할 때 편집기에 포커스를 유지하려면 다음 설정을 변경합니다.

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

기본값은 액세스 가능성을 위해 `true`가 됩니다.

이 설정을 사용하면 `Get-Credential`과 같이, 입력을 명시적으로 호출하는 명령을 사용하는 경우에도 포커스가 콘솔로 이동되지 않도록 합니다.

## <a name="sql-powershell-examples"></a>SQL PowerShell 예제

아래 예제를 사용하려면 [PowerShell 갤러리](https://www.powershellgallery.com/packages/SqlServer)에서 SqlServer 모듈을 설치해야 합니다.

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> 버전 `21.1.18102` 이상에서 `SqlServer` 모듈은 Windows PowerShell 외에 [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 이상을 지원합니다.

이 예제에서는 `Get-SqlInstance` cmdlet을 사용하여 ServerA 및 ServerB의 서버 SMO 개체를 가져옵니다.  이 명령의 기본 출력에는 인스턴스의 인스턴스 이름, 버전, 서비스 팩 및 CU 업데이트 수준이 포함됩니다.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

다음은 예상 출력을 보여 주는 샘플입니다.

```console
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```

`SqlServer` 모듈에는 다음과 같은 저장된 SQL Server 연결 유형에 프로그래밍 방식으로 액세스할 수 있는 `SQLRegistration`이라는 공급자가 포함되어 있습니다.

+ 데이터베이스 엔진 서버(등록된 서버)
+ CMS(중앙 관리 서버)
+ Analysis Services
+ Integration Services
+ Reporting Services

 다음 예제에서는 `dir`(`Get-ChildItem`에 대한 별칭)을 수행하여 등록된 서버 파일에 나열된 모든 SQL Server 인스턴스의 목록을 가져옵니다.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse
```

다음은 예상 출력을 보여 주는 샘플입니다.

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

데이터베이스 또는 데이터베이스 내의 개체를 사용하는 많은 작업에서 `Get-SqlDatabase` cmdlet을 사용할 수 있습니다.  `-ServerInstance` 및 `-Database` 매개 변수의 값을 제공하는 경우 해당 데이터베이스 개체만 검색됩니다.  그러나 `-ServerInstance` 매개 변수만 지정하면 해당 인스턴스에 있는 모든 데이터베이스의 전체 목록이 반환됩니다.

다음은 예상 출력을 보여 주는 샘플입니다.

```console
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

다음 예제에서는 `Get-SqlDatabase` cmdlet을 사용하여 ServerB 인스턴스의 모든 데이터베이스 목록을 검색한 다음, `Out-GridView` cmdlet을 사용하여 백업할 데이터베이스를 선택하기 위한 그리드/테이블을 표시합니다.  사용자가 "확인" 단추를 클릭하면 강조 표시된 데이터베이스만 백업됩니다.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

이 예제에서는 등록된 서버 파일에 나열된 모든 SQL Server 인스턴스의 목록을 다시 가져온 다음, 나열된 각 SQL Server 인스턴스에 대해 자정 이후에 실패한 모든 SQL 에이전트 작업을 보고하는 `Get-SqlAgentJobHistory`를 호출합니다.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

이 예제에서는 `dir`(`Get-ChildItem`에 대한 별칭)을 수행하여 등록된 서버 파일에 나열된 모든 SQL Server 인스턴스의 목록을 가져온 다음, `Get-SqlDatabase` cmdlet을 사용하여 각 해당 인스턴스의 데이터베이스 목록을 가져옵니다.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

다음은 예상 출력을 보여 주는 샘플입니다.

```console
Name                 Status           Size  Space     Recovery Compat. Owner
                                            Available Model    Level
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

PowerShell 확장에 문제가 발생하는 경우 [문제 해결 설명서](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md)에서 이슈 진단 및 보고에 대한 내용을 참조하세요.

### <a name="security-note"></a>보안 정보

보안 이슈에 대한 자세한 내용은 [여기](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security)를 참조하세요.

## <a name="contributing-to-the-code"></a>코드에 기여

이 확장에 참여하는 방법에 대한 자세한 내용은 [개발 설명서](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md)를 참조하세요.

## <a name="maintainers"></a>유지 관리자

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- Tyler Leonhardt - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>License

이 확장은 [MIT 라이선스에 따라 사용이 허가](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt)됩니다. 이 프로젝트의 릴리스에 포함되는 타사 이진 파일에 대한 자세한 내용은 [타사 알림](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt) 파일을 참조하세요.

## <a name="code-of-conduct"></a>준수 사항

이 프로젝트는 [Microsoft 오픈 소스 준수 사항][conduct-code]을 채택했습니다.
자세한 내용은 [준수 사항 FAQ][conduct-FAQ]를 참조하고, 추가 질문이나 의견이 있는 경우에는 [opencode@microsoft.com][conduct-email]으로 문의하세요.

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com