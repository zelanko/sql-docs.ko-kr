---
title: "명령 프롬프트에서 SSIS 패키지 실행 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.suite: sql
ms.custom: 
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2c2b83605714e01961c50d71e83ba57691bc3833
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>명령 프롬프트에서 DTExec.exe를 사용하여 SSIS 패키지 실행
이 빠른 시작 자습서에서는 명령 프롬프트에서 적절한 매개 변수로 `DTExec.exe`를 실행하여 SSIS 패키지를 실행하는 방법을 보여 줍니다.

> [!NOTE]
> 이 문서에 설명된 메서드는 Azure SQL Database 서버에 배포되는 패키지에서 테스트를 거치지 않았습니다.

`DTExec.exe`에 대한 자세한 내용은 [dtexec Utility](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility)를 참조하세요.

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
    - [Transact-SQL(VS 코드)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
