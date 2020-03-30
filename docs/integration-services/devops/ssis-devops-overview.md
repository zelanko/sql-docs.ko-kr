---
title: SQL Server Integration Services DevOps 개요 | Microsoft Docs
description: Ssis DevOps 도구를 사용하여 SSIS CICD를 빌드하는 방법을 알아봅니다.
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6a1f903d0be82d6f5057af68dce80bda1e48238a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "78225925"
---
# <a name="sql-server-integration-services-ssis-devops-tools-preview"></a>SSIS(SQL Server Integration Services) DevOps 도구(미리 보기)

[SSIS DevOps 도구](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) 확장은 **Azure DevOps** 마켓플레이스에서 제공됩니다.

**Azure DevOps** 조직이 없는 경우 먼저 [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops)에 등록한 다음, [단계](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension)에 따라 **SSIS DevOps 도구** 확장을 추가합니다.

**Ssis DevOps 도구**에는 **SSIS 빌드** 작업과 **SSIS 배포** 릴리스 작업이 포함되어 있습니다.

- **SSIS 빌드** 작업은 프로젝트 배포 모델 또는 패키지 배포 모델의 dtproj 파일 빌드를 지원합니다.

- **SSIS 배포** 작업은 단일 또는 여러 ispac 파일을 온-프레미스 SSIS 카탈로그 및 Azure-SSIS IR에 배포하거나 SSISDeploymentManifest 파일 및 관련 파일을 온-프레미스 또는 Azure 파일 공유에 배포할 수 있도록 지원합니다.

## <a name="ssis-build-task"></a>SSIS 빌드 작업

![빌드 작업](media/ssis-build-task.png)

### <a name="properties"></a>속성

#### <a name="project-path"></a>프로젝트 경로

빌드할 프로젝트 폴더 또는 파일의 경로입니다. 폴더 경로를 지정하면 SSIS 빌드 작업은 이 폴더 아래에 있는 모든 dtproj 파일을 재귀적으로 검색하고 모두 빌드합니다.

프로젝트 경로는 *비워 둘 수 없으며*, **.** 으로 설정해야 리포지토리의 루트 폴더에서 빌드할 수 있습니다.

#### <a name="project-configuration"></a>프로젝트 구성

빌드에 사용할 프로젝트 구성의 이름입니다. 지정하지 않으면 기본적으로 각 dtproj 파일에 정의된 첫 번째 프로젝트 구성으로 설정됩니다.

#### <a name="output-path"></a>출력 경로

빌드 결과를 저장할 별도 폴더의 경로이며, [빌드 아티팩트 게시 작업](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops)을 통해 빌드 아티팩트로 게시할 수 있습니다.

### <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

- SSIS 빌드 작업은 빌드 에이전트의 필수 요소인 Visual Studio 및 SSIS 디자이너를 사용합니다. 따라서 파이프라인에서 SSIS 빌드 작업을 실행하려면 Microsoft 호스팅 에이전트를 위해 **vs2017-win2016**을 선택하거나, 자체 호스팅 에이전트에 Visual Studio 및 SSIS 디자이너(VS2017 + SSDT2017 또는 VS2019 + SSIS 프로젝트 확장)를 설치해야 합니다.

- OOB 구성 요소(SSIS Azure 기능 팩 및 기타 타사 구성 요소 포함)를 사용하여 SSIS 프로젝트를 빌드하려면 파이프라인 에이전트가 실행되는 머신에 OOB 구성 요소를 설치해야 합니다.  Microsoft 호스팅 에이전트의 경우 사용자가 [PowerShell 스크립트 작업](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops) 또는 [명령줄 스크립트 작업](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops)을 추가하여 SSIS 빌드 작업이 실행되기 전에 구성 요소를 다운로드하고 설치할 수 있습니다. 다음은 Azure 기능 팩을 설치하는 샘플 PowerShell 스크립트입니다. 

```powershell
wget -Uri https://download.microsoft.com/download/E/E/0/EE0CB6A0-4105-466D-A7CA-5E39FA9AB128/SsisAzureFeaturePack_2017_x86.msi -OutFile AFP.msi

start -Wait -FilePath msiexec -Args "/i AFP.msi /quiet /l* log.txt"

cat log.txt
```

- 보호 수준 **EncryptSensitiveWithPassword** 및 **EncryptAllWithPassword**는 SSIS 빌드 작업에서 지원되지 않습니다. 코드베이스의 모든 SSIS 프로젝트에서 이러한 두 보호 수준을 사용하지 않는지 확인하세요. 사용하면 SSIS 빌드 작업이 실행 중에 중단되고 시간 초과됩니다.

- **ConnectByProxy**는 SSDT에 최근 추가된 새 속성입니다. Microsoft 호스팅 에이전트에 설치된 SSDT는 업데이트되지 않으므로 자체 호스팅 에이전트를 해결 방법으로 사용하세요.

## <a name="ssis-deploy-task"></a>SSIS 배포 작업

![배포 작업](media/ssis-deploy-task.png)

### <a name="properties"></a>속성

#### <a name="source-path"></a>원본 경로

배포하려는 원본 ISPAC 또는 SSISDeploymentManifest 파일의 경로입니다. 이 경로는 폴더 경로 또는 파일 경로일 수 있습니다.

#### <a name="destination-type"></a>대상 형식

대상 유형입니다. 현재 SSIS 배포 작업은 다음 두 가지 유형을 지원합니다.

- ‘파일 시스템’:  SSISDeploymentManifest 파일 및 관련 파일을 지정된 파일 시스템에 배포합니다. 온-프레미스와 Azure 파일 공유가 모두 지원됩니다.
- *SSISDB*: 온-프레미스 SQL Server 또는 Azure-SSIS Integration Runtime에 호스트될 수 있는 지정된 SSIS 카탈로그에 ISPAC 파일을 배포합니다.

#### <a name="destination-server"></a>대상 서버

대상 SQL server의 이름입니다. 온-프레미스 SQL Server, Azure SQL Database 또는 Azure SQL Database 관리되는 인스턴스의 이름일 수 있습니다. 이 속성은 대상 유형이 SSISDB인 경우에만 표시됩니다.

#### <a name="destination-path"></a>대상 경로

원본 파일이 배포되는 대상 폴더의 경로입니다. 다음은 그 예입니다.

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

SSIS 배포 작업은 폴더 및 하위 폴더가 없을 경우 새로 만듭니다.

#### <a name="authentication-type"></a>인증 유형

지정된 대상 서버에 액세스하기 위한 인증 유형입니다. 이 속성은 대상 유형이 SSISDB인 경우에만 표시됩니다. 일반적으로 SSIS 배포 작업은 다음 네 가지 유형을 지원합니다.

- Windows 인증
- SQL Server 인증
- Active Directory - 암호
- Active Directory - 통합

그러나 특정 인증 유형이 지원되는지 여부는 대상 서버 유형과 에이전트 유형에 따라 달라집니다. 자세한 지원 매트릭스는 아래 표에 나와 있습니다.

| |Microsoft 호스팅 에이전트|자체 호스팅 에이전트|
|---------|---------|---------|
|SQL Server 온-프레미스 또는 VM |해당 없음|Windows 인증|
|Azure SQL|SQL Server 인증 <br> Active Directory - 암호|SQL Server 인증 <br> Active Directory - 암호 <br> Active Directory - 통합|

#### <a name="domain-name"></a>도메인 이름

지정된 파일 시스템에 액세스하기 위한 도메인 이름입니다. 이 속성은 대상 유형이 파일 시스템인 경우에만 표시됩니다.
자체 호스팅 에이전트를 실행하는 사용자 계정에 지정된 대상 경로에 대한 읽기/쓰기 권한이 부여된 경우에는 비워 둘 수 있습니다.

#### <a name="username"></a>사용자 이름

지정된 파일 시스템 또는 SSISDB에 액세스하기 위한 사용자 이름입니다. 이 속성은 대상 유형이 파일 시스템이거나 인증 유형이 SQL Server 인증 또는 Active Directory - 암호인 경우에 표시됩니다.
대상 유형이 파일 시스템이고 자체 호스팅 에이전트를 실행하는 사용자 계정에 지정된 대상 경로에 대한 읽기/쓰기 권한이 부여된 경우에는 비워 둘 수 있습니다.

#### <a name="password"></a>암호

지정된 파일 시스템 또는 SSISDB에 액세스하기 위한 암호입니다. 이 속성은 대상 유형이 파일 시스템이거나 인증 유형이 SQL Server 인증 또는 Active Directory - 암호인 경우에 표시됩니다.
대상 유형이 파일 시스템이고 자체 호스팅 에이전트를 실행하는 사용자 계정에 지정된 대상 경로에 대한 읽기/쓰기 권한이 부여된 경우에는 비워 둘 수 있습니다.

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>동일한 이름의 기존 프로젝트 또는 SSISDeploymentManifest 파일 덮어쓰기

동일한 이름의 기존 프로젝트 또는 SSISDeploymentManifest 파일을 덮어쓸지 여부를 지정합니다. ‘아니요’를 선택하면 SSIS 배포 작업은 해당 프로젝트 또는 파일 배포를 건너뜁니다.

#### <a name="continue-deployment-when-error-occurs"></a>오류 발생 시 배포 계속

오류 발생 시 tp에서 남은 프로젝트 또는 파일을 계속 배포할지 여부를 지정합니다. ‘아니요’를 선택하면 오류 발생 시 SSIS 배포 작업이 즉시 중지됩니다.

### <a name="limitations-and-known-issues"></a>제한 사항 및 알려진 문제

SSIS 배포 작업은 현재 다음 시나리오를 지원하지 않습니다.

- SSIS 카탈로그에서 환경을 구성합니다.
- MFA(다단계 인증)만 허용하는 Azure SQL Server 또는 Azure SQL Managed Instance에 ispac를 배포합니다.
- MSDB 또는 SSIS 패키지 저장소에 패키지를 배포합니다.

## <a name="release-notes"></a>릴리스 정보

### <a name="version-013-preview"></a>버전 0.1.3 미리 보기

릴리스 날짜: 2020년 1월 19일

- 원래 파일 이름이 변경된 경우 .ispac를 배포할 수 없었던 문제가 해결되었습니다.

### <a name="version-012-preview"></a>버전 0.1.2 미리 보기

릴리스 날짜: 2020년 1월 13일

- 대상 유형이 SSISDB인 경우, SSIS 배포 작업 로그에 자세한 예외 정보를 추가했습니다.
- SSIS 배포 작업의 속성 대상 경로에 대한 도움말 텍스트의 예제 대상 경로를 수정했습니다.

### <a name="version-011-preview"></a>버전 0.1.1 미리 보기

릴리스 날짜: 2020년 1월 6일

- 최소 에이전트 버전 요구 사항의 제한이 추가되었습니다. 현재 이 제품의 최소 에이전트 버전은 2.144.0입니다.
- SSIS 배포 작업의 일부 잘못된 표시 텍스트가 수정되었습니다.
- 일부 오류 메시지가 구체화되었습니다.

### <a name="version-010-preview"></a>버전 0.1.0 미리 보기

릴리스 날짜: 2019년 12월 5일

SSIS DevOps 도구의 초기 릴리스입니다. 미리 보기 릴리스입니다.

## <a name="next-steps"></a>다음 단계

- [SSIS DevOps 확장](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) 가져오기
