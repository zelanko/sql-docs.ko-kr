---
title: "명령 프롬프트에서 SSIS 패키지를 실행 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a33b8518ec3284f5de73d38c87209057dc1c7487
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="run-an-ssis-package-from-the-command-prompt-with-dtexecexe"></a>DTExec.exe 사용 하 여 명령 프롬프트에서 SSIS 패키지를 실행 합니다.
이 빠른 시작 자습서에서는 SSIS 패키지를 실행 하 여 명령 프롬프트에서 실행 하는 방법을 설명 `DTExec.exe` 적절 한 매개 변수를 사용 합니다.

> [!NOTE]
> Azure SQL 데이터베이스 서버에 배포 패키지와 함께이 문서에서 설명 하는 방법을 테스트 되지 않은 합니다.

에 대 한 자세한 내용은 `DTExec.exe`, 참조 [dtexec 유틸리티](https://docs.microsoft.com/en-us/sql/integration-services/packages/dtexec-utility)합니다.

## <a name="run-a-package-with-dtexec"></a>Dtexec 패키지를 실행

포함 된 폴더 `DTExec.exe` 에 속하지 않는 사용자 `path` 환경 변수를 할 수 있습니다 사용할는 `cd` 명령을 해당 디렉터리로 변경 합니다. SQL Server 2017이이 폴더는 일반적으로 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`합니다.

다음 예에 사용 된 매개 변수 값을 프로그램이 지정 된 폴더 경로에 패키지 SSIS 서버-즉, SSIS 카탈로그 데이터베이스 (SSISDB)를 호스팅하는 서버에서 실행 됩니다. `/Server` 매개 변수는 서버 이름을 제공 합니다. 프로그램은 Windows 통합 인증으로 현재 사용자로 연결합니다. SQL 인증을 사용 하려면 지정 된 `/User` 및 `Password` 적절 한 값으로 매개 변수입니다.

1. 명령 프롬프트 창을 엽니다.

2. 실행 `DTExec.exe` 에 이상 값을 제공 하 고는 `ISServer` 및 `Server` 다음 예제와 같이 매개 변수:

    ```cmd
    dtexec /ISServer "\SSISDB\Project1Folder\Integration Services Project1\Package.dtsx" /Server "localhost"
    ```

## <a name="next-steps"></a>다음 단계
- 다른 방법으로 패키지를 실행 하는 것이 좋습니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

