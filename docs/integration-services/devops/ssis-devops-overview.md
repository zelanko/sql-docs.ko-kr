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
ms.openlocfilehash: eb93961b516623f0a22b3baeae4bc29026c3a994
ms.sourcegitcommit: 8515bb2021cfbc7791318527b8554654203db4ad
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/08/2020
ms.locfileid: "86091784"
---
# <a name="sql-server-integration-services-ssis-devops-tools"></a>SSIS(SQL Server Integration Services) DevOps 도구

[SSIS DevOps 도구](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) 확장은 **Azure DevOps** Marketplace에서 제공됩니다.

**Azure DevOps** 조직이 없는 경우 먼저 [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops)에 등록한 다음, [단계](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension)에 따라 **SSIS DevOps 도구** 확장을 추가합니다.

**Ssis DevOps 도구**에는 **SSIS 빌드** 작업, **SSIS 배포** 릴리스 작업 및 **SSIS 카탈로그 구성 작업**이 포함되어 있습니다.

- **[SSIS 빌드](#ssis-build-task)** 작업은 프로젝트 배포 모델 또는 패키지 배포 모델의 dtproj 파일 빌드를 지원합니다.

- **[SSIS 배포](#ssis-deploy-task)** 작업은 단일 또는 여러 ispac 파일을 온-프레미스 SSIS 카탈로그 및 Azure-SSIS IR에 배포하거나 SSISDeploymentManifest 파일 및 관련 파일을 온-프레미스 또는 Azure 파일 공유에 배포할 수 있도록 지원합니다.

- **[SSIS 카탈로그 구성](#ssis-catalog-configuration-task)** 작업은 JSON 형식의 구성 파일을 사용하여 SSIS 카탈로그의 폴더/프로젝트/환경을 구성할 수 있도록 지원합니다. 이 작업은 다음과 같은 시나리오를 지원합니다.
    - 폴더
        - 폴더를 만듭니다.
        - 폴더 설명을 업데이트합니다.
    - Project
        - 매개 변수의 구성 값입니다. literal 값과 referenced 값이 모두 지원됩니다.
        - 환경 참조를 추가합니다.
    - Environment
        - 환경을 만듭니다.
        - 환경 설명을 업데이트합니다.
        - 환경 변수를 만들거나 업데이트합니다.

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

- 보호 수준 **EncryptSensitiveWithPassword** 및 **EncryptAllWithPassword**는 SSIS 빌드 작업에서 지원되지 않습니다. 코드베이스의 모든 SSIS 프로젝트에서 이러한 두 보호 수준을 사용하지 않는지 확인하세요. 사용하면 SSIS 빌드 작업이 실행 중에 응답하지 않고 시간 초과됩니다.

## <a name="ssis-deploy-task"></a>SSIS 배포 작업

![배포 작업](media/ssis-deploy-task.png)

### <a name="properties"></a>속성

#### <a name="source-path"></a>원본 경로

배포하려는 원본 ISPAC 또는 SSISDeploymentManifest 파일의 경로입니다. 이 경로는 폴더 경로 또는 파일 경로일 수 있습니다.

#### <a name="destination-type"></a>대상 형식

대상 유형입니다. 현재 SSIS 배포 작업은 다음 두 가지 유형을 지원합니다.

- ‘파일 시스템’: SSISDeploymentManifest 파일 및 관련 파일을 지정된 파일 시스템에 배포합니다. 온-프레미스와 Azure 파일 공유가 모두 지원됩니다.
- *SSISDB*: 온-프레미스 SQL Server 또는 Azure-SSIS Integration Runtime에 호스트될 수 있는 지정된 SSIS 카탈로그에 ISPAC 파일을 배포합니다.

#### <a name="destination-server"></a>대상 서버

대상 SQL server의 이름입니다. 온-프레미스 SQL Server, Azure SQL Database 또는 Azure SQL Database 관리되는 인스턴스의 이름일 수 있습니다. 이 속성은 대상 유형이 SSISDB인 경우에만 표시됩니다.

#### <a name="destination-path"></a>대상 경로

원본 파일이 배포되는 대상 폴더의 경로입니다. 예를 들면 다음과 같습니다.

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

SSIS 배포 작업은 폴더 및 하위 폴더가 없을 경우 이를 새로 만듭니다.

#### <a name="authentication-type"></a>인증 유형

지정된 대상 서버에 액세스하기 위한 인증 유형입니다. 이 속성은 대상 유형이 SSISDB인 경우에만 표시됩니다. 일반적으로 다음과 같은 인증 유형이 지원됩니다.

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

## <a name="ssis-catalog-configuration-task"></a>SSIS 카탈로그 구성 작업

![카탈로그 구성 작업](media/ssis-catalog-configuation-task.png)

### <a name="properties"></a>속성

#### <a name="configuration-file-source"></a>구성 파일 원본

SSIS 카탈로그 구성 JSON 파일의 원본입니다. “파일 경로” 또는 “인라인”일 수 있습니다.

[구성 JSON을 정의](#define-configuration-json)하는 방법을 참조하세요.

- [샘플 인라인 구성 JSON](#a-sample-inline-configuration-json)을 참조합니다.
- [JSON 스키마](#json-schema)를 확인합니다.

#### <a name="configuration-json-file-path"></a>구성 JSON 파일 경로

SSIS 카탈로그 구성 JSON 파일의 경로입니다. 이 속성은 구성 파일 원본으로 “파일 경로”를 선택한 경우에만 표시됩니다.

구성 JSON 파일에서 [파이프라인 변수](/azure/devops/pipelines/process/variables)를 사용하려면 이 작업 앞에 [파일 변환 작업](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/file-transform?view=azure-devops)을 추가하여 구성 값을 파이프라인 변수로 대체해야 합니다. 자세한 내용은 [JSON variable substitution](https://docs.microsoft.com/azure/devops/pipelines/tasks/transforms-variable-substitution?view=azure-devops&tabs=Classic#json-variable-substitution)(JSON 변수 대체)을 참조하세요.

#### <a name="inline-configuration-json"></a>인라인 구성 JSON

SSIS 카탈로그 구성의 인라인 JSON입니다. 이 속성은 구성 파일 원본으로 “인라인”을 선택한 경우에만 표시됩니다. 파이프라인 변수는 직접 사용할 수 있습니다.

#### <a name="roll-back-configuration-when-error-occurs"></a>오류가 발생한 경우 구성 롤백

오류가 발생한 경우 이 작업에 의해 적용된 구성을 롤백할지 여부입니다.

#### <a name="target-server"></a>대상 서버

대상 SQL Server의 이름입니다. 온-프레미스 SQL Server, Azure SQL Database 또는 Azure SQL Database 관리되는 인스턴스의 이름일 수 있습니다.

#### <a name="authentication-type"></a>인증 유형

지정된 대상 서버에 액세스하기 위한 인증 유형입니다. 일반적으로 다음과 같은 인증 유형이 지원됩니다.

- Windows 인증
- SQL Server 인증
- Active Directory - 암호
- Active Directory - 통합

그러나 특정 인증 유형이 지원되는지 여부는 대상 서버 유형과 에이전트 유형에 따라 달라집니다. 자세한 지원 매트릭스는 아래 표에 나와 있습니다.

| |Microsoft 호스팅 에이전트|자체 호스팅 에이전트|
|---------|---------|---------|
|SQL Server 온-프레미스 또는 VM |해당 없음|Windows 인증|
|Azure SQL|SQL Server 인증 <br> Active Directory - 암호|SQL Server 인증 <br> Active Directory - 암호 <br> Active Directory - 통합|

#### <a name="username"></a>사용자 이름

대상 SQL Server에 액세스하기 위한 사용자 이름입니다. 이 속성은 인증 유형이 SQL Server 인증 또는 Active Directory - 암호인 경우에만 표시됩니다.

#### <a name="password"></a>암호

대상 SQL Server에 액세스하기 위한 암호입니다. 이 속성은 인증 유형이 SQL Server 인증 또는 Active Directory - 암호인 경우에만 표시됩니다.

### <a name="define-configuration-json"></a>구성 JSON 정의

구성 JSON 스키마에는 다음과 같은 3개의 레이어가 있습니다.

- 카탈로그
- 폴더
- 프로젝트 및 환경

![카탈로그 구성 스키마](media/catalog-configuration-schema.png)

#### <a name="a-sample-inline-configuration-json"></a>샘플 인라인 구성 JSON

```json
{
  "folders": [
    {
      "name": "devopsdemo",
      "description": "devops demo folder",
      "projects": [
        {
          "name": "catalog devops",
          "parameters": [
            {
              "name": "password",
              "container": "Package.dtsx",
              "value": "passwd",
              "valueType": "referenced"
            },
            {
              "name": "serverName",
              "container": "catalog devops",
              "value": "localhost",
              "valueType": "literal"
            }
          ],
          "references": [
            {
              "environmentName": "test",
              "environmentFolder": "devopsdemo"
            },
            {
              "environmentName": "test",
              "environmentFolder": "."
            }
          ]
        }
      ],
      "environments": [
        {
          "name": "test",
          "description": "test",
          "variables": [
            {
              "name": "passwd",
              "type": "string",
              "description": "",
              "value": "$(SSISDBServerAdminPassword)",
              "sensitive": true
            },
            {
              "name": "serverName",
              "type": "string",
              "description": "",
              "value": "$(TargetServerName)",
              "sensitive": false
            }
          ]
        }
      ]
    }
  ]
}
```

#### <a name="json-schema"></a>JSON 스키마

##### <a name="catalog-attributes"></a>카탈로그 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|폴더  |폴더 개체의 배열입니다. 각 개체에는 하나의 카탈로그 폴더에 대한 구성 정보가 포함되어 있습니다.|폴더 개체의 스키마는 ‘폴더 특성’을 참조하세요.|

##### <a name="folder-attributes"></a>폴더 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|name  |카탈로그 폴더의 이름입니다.|폴더가 존재하지 않는 경우 생성됩니다.|
|description|카탈로그 폴더에 대한 설명입니다.|*null*의 값은 건너뜁니다.|
|projects|프로젝트 개체의 배열입니다. 각 개체에는 하나의 프로젝트에 대한 구성 정보가 포함되어 있습니다.|프로젝트 개체의 스키마는 ‘프로젝트 특성’을 참조하세요.|
|environments|환경 개체의 배열입니다. 각 개체에는 하나의 환경에 대한 구성 정보가 포함되어 있습니다.|환경 개체의 스키마는 ‘환경 특성’을 참조하세요.|

##### <a name="project-attributes"></a>프로젝트 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|name|프로젝트의 이름입니다. |부모 폴더에 프로젝트가 없는 경우 프로젝트 개체를 건너뜁니다.|
|매개 변수|매개 변수 개체의 배열입니다. 각 개체에는 하나의 매개 변수에 대한 구성 정보가 포함되어 있습니다.|매개 변수 개체의 스키마는 ‘매개 변수 특성’을 참조하세요.|
|references|참조 개체의 배열입니다. 각 개체는 대상 프로젝트에 대한 환경 참조를 나타냅니다.|참조 개체의 스키마는 ‘참조 특성’을 참조하세요.|

##### <a name="parameter-attributes"></a>매개 변수 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|name|매개 변수의 이름입니다.|매개 변수는 ‘프로젝트 매개 변수’ 또는 ‘패키지 매개 변수’일 수 있습니다.  <br> 부모 프로젝트에 매개 변수가 없는 경우 매개 변수를 건너뜁니다.|
|container|매개 변수의 컨테이너입니다.|<li>매개 변수가 프로젝트 매개 변수이면 *container*는 프로젝트 이름이어야 합니다. <li>매개 변수가 패키지 매개 변수이면 *container*는 **.dtsx** 확장자를 갖는 패키지 이름이어야 합니다. <li> 매개 변수가 연결 관리자 속성이면 이름은 다음과 같은 형식이어야 합니다. **CM.\<Connection Manager Name>.\<Property Name>** .|
|값|매개 변수의 값입니다.|<li>*valueType*이 *referenced*인 경우: 값은 ‘문자열’ 형식의 환경 변수에 대한 참조입니다. <li> *valueType*이 *literal*인 경우: 이 특성은 임의의 유효한 ‘부울’, ‘숫자’ 및 ‘문자열’ JSON 값을 지원합니다.   <br> 값은 대상 매개 변수 형식으로 변환됩니다. 변환할 수 없는 경우 오류가 발생합니다.<li> *null* 값은 유효하지 않습니다. 작업은 이 매개 변수 개체를 건너뛰고 경고를 표시합니다.|
|valueType|매개 변수 값의 유형입니다.|유효한 유형은 다음과 같습니다. <br> *literal*: *value* 특성이 리터럴 값을 나타냅니다. <br> *referenced*: *value* 특성이 환경 변수에 대한 참조를 나타냅니다.|

##### <a name="reference-attributes"></a>참조 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|environmentFolder|환경의 폴더 이름입니다.|폴더가 존재하지 않는 경우 생성됩니다. <br> 값은 환경을 참조하는 프로젝트의 부모 폴더를 나타내는 “.”일 수 있습니다.|
|environmentName|참조된 환경의 이름입니다.|지정된 환경이 존재하지 않는 경우 생성됩니다.|

##### <a name="environment-attributes"></a>환경 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|name|환경의 이름입니다.|환경이 존재하지 않는 경우 생성됩니다.|
|description|환경에 대한 설명입니다.|*null*의 값은 건너뜁니다.|
|variables|변수 개체의 배열입니다.|각 개체에는 하나의 환경 변수에 대한 구성 정보가 포함되어 있습니다. 변수 개체의 스키마는 ‘변수 특성’을 참조하세요.|

##### <a name="variable-attributes"></a>변수 특성

|속성  |Description  |메모  |
|---------|---------|---------|
|name|환경 변수의 이름입니다.|환경 변수가 존재하지 않는 경우 생성됩니다.|
|type|환경 변수의 데이터 형식입니다.|유효한 유형은 다음과 같습니다. <br> *boolean* <br> *바이트* <br> *datetime* <br> decimal <br> *double* <br> *int16* <br> *int32* <br> *int64* <br> *sbyte* <br> *single* <br> *string* <br> *uint32* <br> *uint64*|
|description|환경 변수에 대한 설명입니다.|*null*의 값은 건너뜁니다.|
|값|환경 변수의 값입니다.|이 특성은 임의의 유효한 부울, 숫자 및 문자열 JSON 값을 지원합니다.<br> 값은 **type** 특성으로 지정된 형식으로 변환됩니다. 변환에 실패하면 오류가 발생합니다.<br>*null* 값은 유효하지 않습니다. 작업은 이 환경 변수 개체를 건너뛰고 경고를 표시합니다.|
|sensitive|환경 변수의 값이 민감한지 여부입니다.|잘못된 입력: <br> *true* <br> *false*|

## <a name="release-notes"></a>릴리스 정보

### <a name="version-102"></a>버전 1.0.2

릴리스 날짜: 2020년 5월 26일

- 구성 작업이 완료된 후 SSIS 카탈로그 구성 작업이 실패할 수 있는 문제를 해결했습니다.

### <a name="version-101"></a>버전 1.0.1

릴리스 날짜: 2020년 5월 9일

- 단일 dtproj 파일이 프로젝트 경로로 지정된 경우에도 SSIS 빌드 작업에서 항상 전체 솔루션을 빌드하는 문제를 해결했습니다.

### <a name="version-100"></a>Version 1.0.0

릴리스 날짜: 2020년 5월 8일

- GA(일반 공급) 릴리스
- 에이전트에서 최소 .NET Framework 버전의 제한을 추가했습니다. 현재 최소 .NET Framework 버전은 4.6.2입니다.
- SSIS 빌드 태스크 및 SSIS 배포 태스크에 대한 구체화된 설명입니다.

### <a name="version-020-preview"></a>버전 0.2.0 미리 보기

릴리스 날짜: 2020년 3월 31일

- SSIS 카탈로그 구성 작업이 추가되었습니다.

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
