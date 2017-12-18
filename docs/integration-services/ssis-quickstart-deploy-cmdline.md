---
title: "명령 프롬프트에서 SSIS 프로젝트 배포 | Microsoft Docs"
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
ms.openlocfilehash: 6c3e7f7e3fa870c7aa5b30a5a4a324f0cef7f6ba
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>ISDeploymentWizard.exe를 사용하여 명령 프롬프트에서 SSIS 프로젝트 배포
이 빠른 시작 자습서에서는 Integration Services 배포 마법사인 `ISDeploymentWizard.exe`를 실행하여 명령 프롬프트에서 SSIS 프로젝트를 배포하는 방법을 보여줍니다.

Integration Services 배포 마법사에 대한 자세한 내용은 [ Integration Services 배포 마법사](packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)를 참조하세요.

## <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 배포 마법사 시작
1. 명령 프롬프트 창을 엽니다.

2. `ISDeploymentWizard.exe`을 실행합니다. Integration Services 배포 마법사가 열립니다.

    `ISDeploymentWizard.exe`를 포함하고 있는 폴더가 `path` 환경 변수 내에 없으면 `cd` 명령을 사용하여 해당 디렉터리로 변경해야 합니다. SQL Server 2017의 경우 이 폴더는 일반적으로 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`입니다.

## <a name="deploy-a-project-with-the-wizard"></a>마법사를 사용하여 프로젝트 배포
1. 마법사의 **소개** 페이지에서 소개를 검토합니다. **다음**을 클릭하여 **원본 선택** 페이지를 엽니다.

2. **원본 선택** 페이지에서 배포할 기존 SSIS 프로젝트를 선택합니다.
    -   만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다.
    -   SSIS 카탈로그에 있는 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 다음 카탈로그에 있는 프로젝트의 서버 이름과 경로를 입력합니다.
    **다음** 을 클릭하여 **대상 선택** 페이지를 표시합니다.
  
3.  **대상 선택** 페이지에서 프로젝트의 대상을 선택합니다.
    -   정규화된 서버 이름을 입력합니다. 대상 서버가 Azure SQL Database 서버인 경우 이름은 `<server_name>.database.windows.net` 형식입니다.
    -   그런 다음 **찾아보기**를 클릭하여 SSISDB에서 대상 폴더를 선택합니다.
    **다음**을 클릭하여 **검토** 페이지를 엽니다.  
  
4.  **검토** 페이지에서 선택한 설정을 검토합니다.
    -   **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다.
    -   **배포** 를 클릭해 배포 프로세스를 시작합니다.
  
5.  배포 프로세스가 완료되면 **결과** 페이지가 열립니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다.
    -   작업이 실패하면 **결과** 열에서 **실패**를 클릭하여 해당 오류에 대한 설명을 표시합니다.
    -   필요에 따라 **보고서 저장...**을 클릭하여 결과를 XML 파일에 저장합니다.
    -   **닫기**를 클릭하여 마법사를 종료합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포하는 다른 방법을 고려합니다.
    - [SSMS를 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [PowerShell을 사용하여 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
    - [C#을 사용하여 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포된 패키지를 실행합니다. 패키지를 실행하려면 여러 도구와 언어 중에서 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조하세요.
    - [SSMS를 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-ssms.md)
    - [Transact-SQL(SSMS)을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-SQL(VS Code)을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell을 사용하여 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#을 사용하여 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 
