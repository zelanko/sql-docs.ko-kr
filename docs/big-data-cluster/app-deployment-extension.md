---
title: 앱 배포 확장
titleSuffix: SQL Server big data clusters
description: Python 또는 R 스크립트를 SQL Server 빅 데이터 클러스터에 애플리케이션으로 배포합니다.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.date: 08/21/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 74f3306167a4c2fbc248f65e5384ea9847f48f7a
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92678917"
---
# <a name="how-to-use-visual-studio-code-to-deploy-applications-to-big-data-clusters-2019"></a>Visual Studio Code를 사용하여 [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 애플리케이션을 배포하는 방법

[!INCLUDE[SQL Server 2019](../includes/applies-to-version/sqlserver2019.md)]

이 문서에서는 앱 배포 확장과 함께 Microsoft Visual Studio Code를 사용하여 SQL Server 빅 데이터 클러스터에 애플리케이션을 배포 하는 방법을 설명합니다.

## <a name="prerequisites"></a>사전 요구 사항

- [Visual Studio Code](https://code.visualstudio.com/)
- [SQL Server 빅 데이터 클러스터](big-data-cluster-overview.md)

## <a name="capabilities"></a>기능

이 확장은 Visual Studio Code에서 다음 작업을 지원합니다.

- SQL Server 빅 데이터 클러스터에 인증합니다.
- 지원되는 런타임 배포를 위해 GitHub 리포지토리에서 애플리케이션 템플릿을 검색합니다.
- 사용자의 작업 영역에서 현재 열려 있는 애플리케이션 템플릿을 관리합니다.
- YAML 형식의 사양을 통해 애플리케이션을 배포합니다.
- SQL Server 빅 데이터 클러스터 내에서 배포된 앱을 관리합니다.
- 사이드바에서 추가 정보와 함께 배포한 앱을 모두 봅니다.
- 클러스터에서 앱을 삭제하거나 앱을 사용하는 실행 사양을 생성합니다.
- 실행 사양 YAML을 통해 배포된 앱을 사용합니다.

다음 섹션에서는 설치 프로세스를 안내하고 확장 작동 방식을 간략하게 설명합니다. 

### <a name="install"></a>설치

먼저 다음과 같이 Visual Studio Code에 앱 배포 확장을 설치합니다.

1. [앱 배포 확장](https://aka.ms/app-deploy-vscode)을 다운로드하여 Visual Studio Code의 일부로 확장을 설치합니다.

1. Visual Studio Code를 시작하고 확장 사이드바로 이동합니다.

1. 사이드바의 맨 위에 있는 `…` 상황에 맞는 메뉴를 클릭하고 `Install from vsix`를 선택합니다.

   ![VSIX 설치](media/vs-extension/install_vsix.png)

1. 다운로드한 `sqlservbdc-app-deploy.vsix` 파일을 찾아서 선택하여 설치합니다.

SQL Server 빅 데이터 클러스터 앱 배포 확장이 설치된 후에 Visual Studio Code를 다시 로드하라는 메시지가 표시됩니다. 이제 Visual Studio Code 사이드바에 SQL Server BDC 앱 탐색기가 표시됩니다.

### <a name="app-explorer"></a>앱 탐색기

사이드바에서 확장을 클릭하여 앱 탐색기가 표시된 사이드 패널을 로드합니다. 앱 탐색기의 다음 샘플 스크린샷에는 사용할 수 있는 앱 또는 앱 사양이 표시되지 않습니다.

![앱 탐색기](media/vs-extension/app_explorer.png)

#### <a name="connect-to-cluster"></a>클러스터에 연결

클러스터 엔드포인트에 연결하려면 다음 방법 중 하나를 사용합니다.

- 맨 아래에서 `SQL Server BDC Disconnected`로 표시되는 상태 표시줄을 클릭합니다.
- 또는 맨 위에서 화살표가 출입구를 가리키는 `Connect to Cluster` 단추를 클릭합니다.

Visual Studio Code에서 적절한 엔드포인트, 사용자 이름 및 암호를 묻는 메시지가 표시됩니다.

연결할 엔드포인트는 포트 30080이 있는 `Cluster Management Service` 엔드포인트입니다.

또한 명령줄에서 이 엔드포인트를 찾을 수도 있습니다. 

```
azdata bdc endpoint list
```

나열된 서비스의 엔드포인트를 찾을 수 있는 Azure Data Studio 서버에서 **관리** 를 마우스 오른쪽 단추로 클릭해도 이 정보를 볼 수 있습니다.

![ADS 엔드포인트](media/vs-extension/ads_end_point.png)

사용할 엔드포인트를 찾았으면 클러스터에 연결합니다.

![새 연결](media/vs-extension/connect_to_cluster.png)

 올바른 자격 증명과 앱 엔드포인트를 제공하면 Visual Studio Code에서 클러스터에 연결되었다는 알림이 표시되고, 배포된 앱이 사이드바에 모두 채워집니다. 성공적으로 연결되면 엔드포인트와 사용자 이름이 `./sqldbc`에 사용자 프로필의 일부로 저장됩니다. 암호 또는 토큰은 저장되지 않습니다. 다시 로그인하면 프롬프트가 저장된 호스트 및 사용자 이름으로 미리 채워지지만, 암호는 항상 입력해야 합니다. 다른 클러스터 엔드포인트에 연결하려면 `New Connection`을 다시 클릭하면 됩니다. Visual Studio Code를 닫거나 다른 작업 영역을 열어서 다시 연결해야 하는 경우 연결이 자동으로 닫힙니다.

### <a name="app-template"></a>앱 템플릿

Visual Studio Code에서 앱의 아티팩트를 저장할 *작업 영역을 열어야* 합니다.

템플릿 중 하나에서 새 앱을 배포하려면 `App Specifications` 창에서 `New App Template` 단추를 클릭합니다. 여기에서 이름, 런타임 및 로컬 머신에서 새 앱을 저장할 위치를 묻는 메시지가 표시됩니다. 사용자가 제공하는 이름 및 버전은 DNS-1035 레이블이어야 하고, 소문자 영숫자 문자 또는 '-'로 구성되어야 하고, 영문자로 시작하고 영숫자 문자로 끝나야 합니다.

확장의 전체 기능을 사용할 수 있도록 현재 Visual Studio Code 작업 영역에 저장하는 것이 좋지만 로컬 파일 시스템의 어느 위치에나 저장할 수 있습니다.

![새 앱 템플릿](media/vs-extension/new_app_template.png)

작업이 완료되면 지정한 위치에 새 앱 템플릿이 스캐폴드되고, 작업 영역에서 배포 `spec.yaml`이 열립니다. 선택한 디렉터리가 작업 영역에 있는 경우 `App Specifications` 창 아래에도 표시됩니다.

![로드된 앱 템플릿](media/vs-extension/loading_app_template.png)

템플릿은 앱 사양 창에서 다음과 같이 레이아웃된 간단한 `helloworld` 앱입니다.

- **spec.yaml**
   - 클러스터에 앱을 배포하는 방법을 알려줍니다.
- **run-spec.yaml**
   - 클러스터에 앱을 호출하는 방법을 알려줍니다.

앱의 소스 코드는 작업 영역 폴더에 있습니다.

- **소스 파일 이름**
   - 이 파일은 `spec.yaml`에서 `src`로 지정된 소스 코드 파일입니다.
   - `spec.yaml`에 표시된 것처럼 앱의 `entrypoint`로 간주되는 `handler`라는 함수 1개가 있습니다. 이 함수는 `msg`라는 문자열 입력을 사용하고 `out`이라는 문자열 출력을 반환합니다. 이 설정은 `spec.yaml`의 `inputs` 및 `outputs`에 지정되어 있습니다.

스캐폴드된 템플릿을 원하지 않고 이미 빌드한 앱 배포의 `spec.yaml`을 사용하려는 경우 `New App Template` 단추 옆의 `New Deploy Spec` 단추를 클릭하고 동일한 프로세스를 진행합니다. 이제 `spec.yaml`만 표시되며, 선택 항목을 수정할 수 있습니다.

### <a name="deploy-app"></a>앱 배포

`spec.yaml`의 Code Lens `Deploy App`을 통해 이 앱을 즉시 배포하거나, 앱 사양 메뉴에서 `spec.yaml` 파일 옆에 있는 번개 폴더 단추를 누를 수 있습니다. 확장은 `spec.yaml`이 있는 디렉터리의 모든 파일을 압축하고 클러스터에 앱을 배포합니다. 

>[!NOTE]
>모든 앱 파일이 `spec.yaml`과 동일한 디렉터리에 있는지 확인합니다. `spec.yaml`은 앱 소스 코드 디렉터리의 루트 수준에 있어야 합니다. 

![앱 배포 단추](media/vs-extension/deploy_app_lightning.png)

![앱 CodeLens 배포](media/vs-extension/deploy_app_codelens.png)

사이드바에서 앱 상태에 따라 앱을 사용할 준비가 되면 알림이 표시됩니다.

![앱 배포됨](media/vs-extension/app_deploy.png)

![앱 준비 완료 사이드바](media/vs-extension/app_ready_side_bar.png)

![앱 준비 완료 알림](media/vs-extension/app_ready_notification.png)

사이드 창에서 다음이 제공되는 것을 확인할 수 있습니다.

사이드바에서 다음 정보와 함께 배포한 앱을 모두 볼 수 있습니다.

- state
- 버전
- 입력 매개 변수
- 출력 매개 변수
- 링크
  - Swagger
  - 자세히

`Links`를 클릭하면 배포된 앱의 `swagger.json`에 액세스할 수 있으므로, 해당 앱을 호출하는 고유한 클라이언트를 작성할 수 있습니다.

![swagger.json 파일을 보여 주는 VS Code UI의 스크린샷](media/vs-extension/swagger.png)

자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)을 참조하세요.

### <a name="app-run"></a>앱 실행

앱이 준비되면 앱 템플릿의 일부로 지정된 `run-spec.yaml`을 사용하여 앱을 호출합니다.

![실행 사양](media/vs-extension/run_spec.png)

`hello` 대신 사용하려는 문자열을 지정한 다음, Code Lens 링크 또는 사이드바에서 `run-spec.yaml` 옆에 있는 번개 단추를 통해 다시 실행합니다. 어떤 이유로든 실행 사양이 없는 경우 클러스터의 배포된 앱에서 새로 생성합니다.

![실행 사양 가져오기](media/vs-extension/get_run_spec.png)

실행 사양이 있고 원하는 대로 편집했으면 실행합니다. 앱 실행이 완료되면 Visual Studio Code에서 적절한 피드백이 반환됩니다.

![앱 출력](media/vs-extension/app_output.png)

위에서 볼 수 있듯이, 출력은 작업 영역의 임시 `.json` 파일에 제공됩니다. 이 출력을 유지하려면 저장합니다. 저장하지 않으면 닫을 때 삭제됩니다. 파일로 인쇄할 앱 출력이 없으면 맨 아래에 `Successful App Run` 알림만 표시됩니다. 성공적으로 실행되지 않은 경우 잘못된 항목을 확인하는 데 도움이 되는 적절한 오류 메시지가 표시됩니다.

앱을 실행할 때 여러 가지 방법으로 매개 변수를 전달할 수 있습니다.

다음과 같이 `.json`을 통해 필요한 모든 입력을 지정할 수 있습니다.

- `inputs: ./example.json`

배포된 앱을 호출할 때 입력 매개 변수가 지정된 앱 또는 사용자에게 고유하고 지정된 입력 매개 변수가 기본 형식이 아닌 배열, 벡터, 데이터 프레임, 복합 JSON 등의 형식인 경우 앱을 호출할 때 다음과 같이 인라인에서 직접 매개 변수 형식을 지정합니다.

- 벡터
    - `inputs:`
        - `x: [1, 2, 3]`
- 행렬
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

또는 앱에 필요한 형식으로 필요한 입력을 제공하는 `.txt`, `.json` 또는 `.csv`의 상대 또는 절대 파일 경로로 문자열을 지정합니다. 파일 구문 분석은 파일 경로가 `string that contains a / or \ character`로 정의되는 `Node.js Path library`를 기반으로 합니다.

필요한 입력 매개 변수를 제공하지 않으면, 문자열 파일 경로가 지정되었거나 해당 매개 변수가 잘못된 경우 적절한 오류 메시지가 잘못된 파일 경로와 함께 표시됩니다. 앱의 작성자는 정의하는 매개 변수를 잘 알고 있어야 합니다.

앱을 삭제하려면 `Deployed Apps` 사이드 창에서 앱 옆에 있는 휴지통 단추를 클릭하면 됩니다.

## <a name="next-steps"></a>다음 단계

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 배포된 앱을 고유한 애플리케이션에 통합하는 방법을 살펴봅니다. 자세한 내용은 [빅 데이터 클러스터에서 애플리케이션 사용](app-consume.md)을 참조하세요. 확장을 사용해 보려면 [앱 배포 샘플](https://aka.ms/sql-app-deploy)에서 추가 샘플을 확인할 수도 있습니다.

[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]에 대한 자세한 내용은 [[!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]란?](big-data-cluster-overview.md)을 참조하세요.


사용자에게 유용한 확장을 만들 수 있도록 피드백을 보내 주시기를 바랍니다. [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 팀](https://aka.ms/sqlfeedback)으로 보내주세요.
