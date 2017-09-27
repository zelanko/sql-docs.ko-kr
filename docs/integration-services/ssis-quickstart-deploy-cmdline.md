---
title: "명령 프롬프트에서 SSIS 프로젝트 배포 | Microsoft Docs"
ms.date: 09/25/2017
ms.topic: article
ms.prod: sql-server-2017
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 656e62f36446db4ef5b232129130a0253d2aebdf
ms.openlocfilehash: a1df574e0436a9fa81e714dfdc21bcbd43c0bda8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/22/2017

---
# <a name="deploy-an-ssis-project-from-the-command-prompt-with-isdeploymentwizardexe"></a>ISDeploymentWizard.exe 사용 하 여 명령 프롬프트에서 SSIS 프로젝트 배포
이 빠른 시작 자습서에서는 Integration Services 배포 마법사를 실행 하 여 명령 프롬프트에서 SSIS 프로젝트를 배포 하는 방법을 보여 줍니다. `ISDeploymentWizard.exe`합니다.

Integration Services 배포 마법사에 대 한 자세한 내용은 참조 하십시오. [Integration Services 배포 마법사](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md#integration-services-deployment-wizard)합니다.

## <a name="start-the-integration-services-deployment-wizard"></a>Integration Services 배포 마법사를 시작 합니다.
1. 명령 프롬프트 창을 엽니다.

2. `ISDeploymentWizard.exe`을 실행합니다. Integration Services 배포 마법사가 열립니다.

    포함 된 폴더 `ISDeploymentWizard.exe` 에 속하지 않는 사용자 `path` 환경 변수를 할 수 있습니다 사용할는 `cd` 명령을 해당 디렉터리로 변경 합니다. SQL Server 2017이이 폴더는 일반적으로 `C:\Program Files (x86)\Microsoft SQL Server\140\DTS\Binn`합니다.

## <a name="deploy-a-project-with-the-wizard"></a>마법사를 사용 하 여 프로젝트를 배포 합니다.
1. 에 **소개** 페이지는 마법사의 소개를 검토 합니다. 클릭 **다음** 열려는 **원본 선택** 페이지.

2. 에 **원본 선택** 페이지에서 기존 SSIS 프로젝트 배포를 선택 합니다.
    -   만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다.
    -   SSIS 카탈로그에 프로젝트를 배포 하려면 선택 **Integration Services 카탈로그**를 선택한 다음 카탈로그에 프로젝트를 서버 이름 및 경로 입력 합니다.
    **다음** 을 클릭하여 **대상 선택** 페이지를 표시합니다.
  
3.  에 **대상 선택** 페이지, 프로젝트에 대 한 대상을 선택 합니다.
    -   정규화 된 서버 이름을 입력 합니다. 이 형식 이름이 대상 서버에 Azure SQL 데이터베이스 서버 이면: `<server_name>.database.windows.net`합니다.
    -   클릭 **찾아보기** SSISDB에 대상 폴더를 선택 합니다.
    클릭 **다음** 열려는 **검토** 페이지.  
  
4.  에 **검토** 페이지에서 선택한 설정을 검토 합니다.
    -   **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다.
    -   **배포** 를 클릭해 배포 프로세스를 시작합니다.
  
5.  배포 프로세스가 완료 된 후의 **결과** 페이지가 열립니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다.
    -   작업에 실패 한 경우 클릭 **실패** 에 **결과** 열 오류에 대 한 설명을 표시 합니다.
    -   필요에 따라 **보고서 저장... ** XML 파일로 결과 저장할 수 있습니다.
    -   클릭 **닫기** 여 마법사를 종료 합니다.

## <a name="next-steps"></a>다음 단계
- 패키지를 배포 하는 다른 방법을 고려 합니다.
    - [SSMS로 SSIS 패키지 배포](./ssis-quickstart-deploy-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지 배포](./ssis-quickstart-deploy-tsql-ssms.md)
    - [TRANSACT-SQL (VS Code)를 SSIS 패키지 배포](ssis-quickstart-deploy-tsql-vscode.md)
    - [PowerShell과 함께 SSIS 패키지 배포](ssis-quickstart-deploy-powershell.md)
    - [C#과 함께 SSIS 패키지 배포](./ssis-quickstart-deploy-dotnet.md) 
- 배포 된 패키지를 실행 합니다. 패키지를 실행 하려면 여러 가지 도구와 언어를 선택할 수 있습니다. 자세한 내용은 다음 문서를 참조 합니다.
    - [SSMS로는 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-ssms.md)
    - [Transact SQL (SSMS)를 SSIS 패키지를 실행 합니다.](./ssis-quickstart-run-tsql-ssms.md)
    - [Transact-sql (VS Code)는 SSIS 패키지를 실행 합니다.](ssis-quickstart-run-tsql-vscode.md)
    - [명령 프롬프트에서 SSIS 패키지 실행](./ssis-quickstart-run-cmdline.md)
    - [PowerShell에서 SSIS 패키지 실행](ssis-quickstart-run-powershell.md)
    - [C#과 함께 SSIS 패키지 실행](./ssis-quickstart-run-dotnet.md) 

