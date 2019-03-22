---
title: 앱 배포 확장
titleSuffix: SQL Server 2019 big data clusters
description: SQL Server 2019 빅 데이터 클러스터 (미리 보기)에서 응용 프로그램으로 Python 또는 R 스크립트를 배포 합니다.
author: TheBharath
ms.author: bharaths
manager: craigg
ms.date: 02/28/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 761818cd83df5db38b3877184b03b7e5d634aa63
ms.sourcegitcommit: 1c1ed8d6aa2fb9fceb6a00c39597578442f7f4e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2019
ms.locfileid: "58222027"
---
# <a name="how-to-use-vs-code-to-deploy-applications-to-sql-server-big-data-clusters"></a>VS Code를 사용 하 여 SQL Server 빅 데이터 클러스터에 응용 프로그램을 배포 하는 방법

이 문서에서는 Visual Studio Code를 사용 하 여 앱 배포 확장을 사용 하 여 SQL Server 빅 데이터 클러스터에 응용 프로그램을 배포 하는 방법을 설명 합니다. 이 기능은 CTP 2.3에서 도입 되었습니다. 

## <a name="prerequisites"></a>사전 요구 사항

- 및[Visual Studio Code](https://code.visualstudio.com/)가 있습니다.
- [SQL Server 빅 데이터 클러스터](big-data-cluster-overview.md) CTP 2.3 이상.

## <a name="capabilities"></a>Capabilities

이 확장에는 Visual Studio Code에서 다음 작업을 지원합니다.

- SQL Server 빅 데이터 클러스터를 사용 하 여 인증 합니다.
- 지원 되는 런타임 배포에 대 한 GitHub 리포지토리에서 응용 프로그램 템플릿을 검색 합니다.
- 사용자의 작업 영역에서 현재 열려 있는 응용 프로그램 템플릿 관리
- YAML 형식에서 사양을 통해 응용 프로그램을 배포 합니다.
- SQL Server 빅 데이터 클러스터 내에서 배포 된 앱을 관리 합니다.
- 추가 정보를 사용 하 여 세로 막대에서 배포한 모든 앱을 봅니다.
- 앱을 사용 하거나 클러스터에서 앱을 삭제 하기 위한 실행된 사양을 생성 합니다.
- 실행된 사양 YAML 통해 배포 된 앱을 사용 합니다.

다음 섹션에서는 설치 프로세스를 통해 탐색 하 고 확장의 작동 원리 개요를 제공 합니다. 

### <a name="install"></a>Install

먼저 VS Code에서 앱 배포 확장을 설치 합니다.

1. 다운로드 [앱 배포 확장](https://aka.ms/app-deploy-vscode) VS Code의 일환으로 확장을 설치 합니다.

1. VS Code를 시작 하 고 확장 사이드바로 이동 합니다.

1. 클릭 합니다 `…` 선택한 세로 막대 맨 위에 있는 상황에 맞는 메뉴 `Install from vsix`합니다.

   ![VSIX 설치](media/vs-extension/install_vsix.png)

1. 찾기는 `sqlservbdc-app-deploy.vsix` 파일을 다운로드 및 설치를 선택 합니다.

SQL Server 빅 데이터 클러스터 앱이 배포 후 확장 설치가 완료 된 후, VS Code를 다시 로드 하 라는 메시지를 표시 합니다. 이제 VS Code 사이드바에서 SQL Server BDC 앱 탐색기 표시 됩니다.

### <a name="app-explorer"></a>앱 탐색기

앱 탐색기를 보여 주는 측면 패널이 로드 사이드바에서 확장을 클릭 합니다. 앱 탐색기의 다음 샘플 스크린샷은 앱 또는 앱 사양을 사용할 수 없습니다.

<img src="media/vs-extension/app_explorer.png" width=350px></img>
<!--![App Explorer](media/vs-extension/app_explorer.png)-->

#### <a name="new-connection"></a>새 연결

클러스터 끝점에 연결 하려면 다음 방법 중 하나를 사용 합니다.

- 라는 아래쪽 상태 표시줄에 클릭 `SQL Server BDC Disconnected`합니다.
- 클릭 된 `New Connection` 출입구가에 화살표를 사용 하 여 맨 위에 있는 단추입니다.

   ![새 연결](media/vs-extension/connect_to_cluster.png)

VS Code는 적절 한 끝점, 사용자 이름 및 암호를 묻습니다. 앱 끝점을 확인 하 고 올바른 자격 증명을 지정 하면 VS Code에 알리고 해당 클러스터에 연결한 된 세로 막대에서 채워진 모든 배포 된 앱이 표시 됩니다. 성공적으로 연결 하는 경우 사용자 이름을 확인 하 고 끝점에 저장 됩니다 `./sqldbc` 사용자 프로필의 일부로. 토큰이 없거나 암호 저장 적이 됩니다. 다시 로그인 할 때 프롬프트 저장 된 호스트 및 사용자 이름을 미리 채울 됩니다 있지만 항상 암호를 입력 해야 합니다. 다른 클러스터 끝점에 연결 하려는 경우 클릭할는 `New Connection` 다시 합니다. VS Code를 닫으면 또는 다른 작업 영역을 열고 다시 연결 해야 하는 경우 연결이 자동으로 닫힙니다.

### <a name="app-template"></a>앱 템플릿

에 맞게 템플릿 중 하나에서 새 앱을 배포 하려면 클릭 합니다 `New App Template` 단추는 `App Specifications` 여기서 묻는 이름, 런타임 및 내용에 대 한 창에서 새로운 앱을 로컬 컴퓨터에 배치 하려는 위치입니다. 배치한 현재 VS Code 작업 영역에서 확장의 전체 기능을 사용할 수 있습니다 하지만 로컬 파일 시스템에서 아무 곳 이나 배치할 수 있도록 하는 것이 좋습니다.

![새 앱 템플릿](media/vs-extension/new_app_template.png)

완료 되 면 새 앱 템플릿을 스 캐 폴드 되를 지정한 위치와 배포 `spec.yaml` 작업 영역에서 열립니다. 선택한 디렉터리에 있는 경우 작업 영역도 표시 됩니다 아래에 나열 된 `App Specifications` 창:

![앱 템플릿을 로드 했습니다.](media/vs-extension/loading_app_template.png)

서식 파일은 단순 `Hello World` 다음과 같이 배치 되는 앱.

- **spec.yaml**
   - 클러스터에 앱을 배포 하는 방법을 지시합니다
- **run-spec.yaml**
   - 앱을 호출 하는 방법을 클러스터 알려 줍니다.
- **handler.py**
   - 이 소스 코드 파일에 지정 된 대로 `src` 에서 `spec.yaml`
   - 하나의 함수 호출 포함 `handler` 하는 것으로 간주 됩니다 합니다 `entrypoint` 에 표시 된 대로 앱의 `spec.yaml`합니다. 호출 하는 문자열 입력에 걸리는 `msg` 라는 문자열 출력을 반환 하 고 `out`입니다. 에 지정 된 이러한 `inputs` 하 고 `outputs` 의 `spec.yaml`합니다.

스 캐 폴드 된 템플릿으로 원하지 않는 하 고 방금 선호 하는 경우는 `spec.yaml` 이미 만든 앱의 배포를 클릭 합니다 `New Deploy Spec` 단추 옆에 `New App Template` 단추와 동일한 프로세스를 통해 이동 합니다 수신만`spec.yaml`를 선택 하는 방법을 수정할 수 있습니다.

### <a name="deploy-app"></a>앱 배포

코드 렌즈를 통해이 앱을 즉시 배포할 수 있습니다 `Deploy App` 에 `spec.yaml` 또는 번개 폴더 단추 옆에는 `spec.yaml` 앱 사양 메뉴에서 파일입니다. 확장 디렉터리에 있는 모든 파일을 zip는 위치에 `spec.yaml` 위치한 및 클러스터에 앱을 배포 합니다. 

>[!NOTE]
>동일한 디렉터리에 있는 모든 앱 파일을 확인 하십시오 프로그램 `spec.yaml`합니다. `spec.yaml` 앱 소스 코드 디렉터리의 루트 수준에 있어야 합니다. 

![배포 앱 단추](media/vs-extension/deploy_app_lightning.png)

![CodeLens 앱 배포](media/vs-extension/deploy_app_codelens.png)

앱 세로 막대에서 앱의 상태를 기반으로 사용할 준비가 되 면 알려 줍니다.

![배포 된 앱](media/vs-extension/app_deploy.png)

![앱 준비 사이드바](media/vs-extension/app_ready_side_bar.png)

![앱 준비 완료 알림](media/vs-extension/app_ready_notification.png)

왼쪽 창에서을 사용할 수 있는 다음 볼 수 있습니다.

다음 정보를 사용 하 여 세로 막대에서 배포한 모든 앱을 볼 수 있습니다.

- state
- version
- 입력 매개 변수
- 출력 매개 변수
- 링크
  - swagger
  - 자세히

클릭 하면 `Links`, 액세스할 수 있는지 표시 됩니다는 `swagger.json` 배포 된 앱의 앱을 호출 하는 고유한 클라이언트를 작성할 수 있도록 합니다.

![Swagger](media/vs-extension/swagger.png)

참조 [빅 데이터 클러스터에 응용 프로그램을 사용](big-data-cluster-consume-apps.md) 자세한 내용은 합니다.

### <a name="app-run"></a>앱 실행

앱 준비 되 면 응용 프로그램을 호출 하는 `run-spec.yaml` 앱 템플릿의 일부로 지정 된는:

![사양 실행](media/vs-extension/run_spec.png)

대신 원하는 모든 문자열을 지정할 `hello` 옆에 코드 렌즈 링크 또는 세로 막대 번개 모양 단추를 통해 실행 한 다음 다시는 `run-spec.yaml`합니다. 어떤 이유로 든 실행 고유 없으면 클러스터에 배포 된 앱에서 하나를 생성 합니다.

![사양 실행](media/vs-extension/get_run_spec.png)

하나를 만족 스럽게 편집한 후 실행 합니다. VS Code 앱 실행이 완료 된 경우 적절 한 피드백을 반환 합니다.

![앱 출력](media/vs-extension/app_output.png)

출력 임시 나오는 위에서 보시 `.json` 작업 영역에는 파일입니다. 이 출력을 유지 하려면 저장을 원하는 경우이 고, 그렇지 삭제 됩니다 닫는에 있습니다. 앱에 파일을 인쇄할 출력이 없습니다, 경우에 한 해를 `Successful App Run` 맨 아래에 알림. 실행을 성공적으로 없는 경우 문제가 무엇 인지 파악 하는 데 도움이 되는 적절 한 오류 메시지를 받게 됩니다.

앱을 실행할 때 매개 변수를 전달 하는 방법의 여러 가지가 있습니다.

통해 필요한 모든 입력을 지정할 수 있습니다는 `.json`, 즉:

- `inputs: ./example.json`

모든 입력된 매개 변수는 앱 또는 사용자 지정을 타고 및 입력된 매개 변수가 지정 된 인지는 배열, 벡터, 데이터 프레임을 기본 형식 이외의 등 복합 JSON을 지정 하는 경우 배포 된 앱을 호출할 때 매개 변수 형식을 직접에서 줄 때 즉 앱을 호출 합니다.

- 벡터
    - `inputs:`
        - `x: [1, 2, 3]`
- 행렬
    - `inputs:`
        - `x: [[A,B,C],[1,2,3]]`
- Object
    - `inputs:`
        - `x: {A: 1, B: 2, C: 3}`

상대 또는 절대 파일 경로와 문자열을 제공 하거나를 `.txt`, `.json`, 또는 `.csv` 필수 입력 하 여 앱에 필요한 형식으로 제공 합니다. 구문 분석 하는 파일 기반 `Node.js Path library`, 여기서 파일 경로 란는 `string that contains a / or \ character`합니다.

필요에 따라 입력된 매개 변수가 제공 되지 않으면 문자열 파일 경로 지정 된 경우 또는 해당 매개 변수가 잘못 되었습니다. 잘못 된 파일 경로 사용 하 여 적절 한 오류 메시지가 표시 됩니다. 책임 정의 하는 매개 변수를 파악할 수 있도록 앱의 작성자에 게 제공 됩니다.

앱을 삭제 하려면 휴지통을 클릭 하면 앱 옆에 있는 단추 수를 `Deployed Apps` 창이 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server에서 응용 프로그램에서 빅 데이터 클러스터에 배포 된 앱을 통합 하는 방법에 대해 [빅 데이터 클러스터에 응용 프로그램을 사용](big-data-cluster-consume-apps.md) 자세한 내용은 합니다. 추가 샘플을 참조할 수도 있습니다 [응용 프로그램 배포 샘플](https://aka.ms/sql-app-deploy) 확장을 사용 하 여 시도 합니다.

SQL Server 빅 데이터 클러스터에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 빅 데이터 클러스터 이란?](big-data-cluster-overview.md)합니다.


주시면 피드백 및 목표를 유용 하 게이 확장을 만들 것입니다. 보내주세요 [ [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 팀](https://aka.ms/sqlfeedback)합니다.
