---
title: 명령 프롬프트에서 SSIS 패키지 실행 | Microsoft Docs
ms.date: 05/21/2018
ms.topic: quickstart
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 964fdf4d4abb58d7baf27ee9e2f8b6900a7d0bbb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71295716"
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>명령 프롬프트에서 DTExec.exe를 사용하여 SSIS 패키지 실행

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


이 빠른 시작에서는 명령 프롬프트에서 적절한 매개 변수로 `DTExec.exe`를 실행하여 SSIS 패키지를 실행하는 방법을 보여줍니다.

> [!NOTE]
> 이 문서에 설명된 메서드는 Azure SQL Database 서버에 배포되는 패키지에서 테스트를 거치지 않았습니다.

`DTExec.exe`에 대한 자세한 내용은 [dtexec Utility](https://docs.microsoft.com/sql/integration-services/packages/dtexec-utility)를 참조하세요.

## <a name="supported-platforms"></a>지원 플랫폼

이 빠른 시작의 정보를 사용하여 다음과 같은 플랫폼에서 SSIS 패키지를 실행할 수 있습니다.

-   Windows의 SQL Server

이 문서에 설명된 메서드는 Azure SQL Database 서버에 배포되는 패키지에서 테스트를 거치지 않았습니다. Azure에서 패키지를 배포하고 실행하는 방법에 대한 자세한 내용은 [SQL Server Integration Services 워크로드를 클라우드로 리프트 앤 시프트](lift-shift/ssis-azure-lift-shift-ssis-packages-overview.md)를 참조하세요.

이 빠른 시작의 정보를 사용하여 Linux에서 SSIS 패키지를 실행할 수 없습니다. Linux에서 패키지를 실행하는 방법에 대한 자세한 내용은 [Linux에서 SSIS를 사용하여 데이터 추출, 변환 및 로드](../linux/sql-server-linux-migrate-ssis.md)를 참조하세요.

## <a name="run-a-package-with-dtexec"></a>dtexec를 사용하여 패키지 실행

`DTExec.exe`를 포함하고 있는 폴더가 `path` 환경 변수 내에 없으면 `cd` 명령을 사용하여 해당 디렉터리로 변경해야 합니다. SQL Server 2017의 경우 이 폴더는 일반적으로 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`입니다.

프로그램에서는 SSIS 서버, 즉 SSISDB(SSIS 카탈로그 데이터베이스)를 호스팅하는 서버에서 지정된 폴더 경로에서 다음 예제에 사용된 매개 변수 값을 사용하여 패키지를 실행합니다. `/Server` 매개 변수는 서버 이름을 제공합니다. 프로그램에서는 현재 사용자로 Windows 통합 인증에 연결합니다. SQL 인증을 사용하려면 적절한 값을 사용하여 `/User` 및 `Password` 매개 변수를 지정합니다.

1. 명령 프롬프트 창을 엽니다.

2. 다음 예제와 같이 `DTExec.exe` 명령을 실행하고 최소한 `ISServer` 및 `Server` 매개 변수의 값을 입력합니다.

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>다음 단계
- 패키지를 실행하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
