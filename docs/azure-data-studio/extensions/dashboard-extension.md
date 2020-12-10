---
title: 대시보드 확장 만들기
description: 이 자습서에서는 Azure Data Studio에 사용자 지정 기능을 추가하는 대시보드 확장을 만드는 방법을 보여 줍니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: c7402c8dd0d2d85d38536a0bcfea3ce8cd780657
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96900876"
---
# <a name="create-an-azure-data-studio-dashboard-extension"></a>Azure Data Studio 대시보드 확장 만들기

이 자습서에서는 새 Azure Data Studio 대시보드 확장을 만드는 방법을 보여줍니다. 확장은 Azure Data Studio 연결 대시보드에 기여하므로 사용자에게 쉽게 표시되는 방식으로 Azure Data Studio 기능을 확장할 수 있습니다.

이 문서에서는 다음 방법을 알아봅니다.

> [!div class="checklist"]
> - 확장 생성기를 설치합니다.
> - 확장을 만듭니다.
> - 확장에 있는 대시보드에 기여합니다.
> - 확장을 테스트합니다.
> - 확장을 패키지화합니다.
> - 마켓플레이스에 확장을 게시합니다.

## <a name="prerequisites"></a>필수 조건

Azure Data Studio는 Visual Studio Code와 동일한 프레임워크를 기반으로 하여 빌드되므로 Azure Data Studio 확장은 Visual Studio Code를 사용하여 빌드됩니다. 시작하려면 다음 구성 요소가 필요합니다.

- `$PATH`에서 설치되고 사용할 수 있는 [Node.js](https://nodejs.org). Node.js에는 확장 생성기를 설치하는 데 사용되는 Node.js 패키지 관리자인 [npm](https://www.npmjs.com/)이 포함되어 있습니다.
- 확장을 디버그하기 위한 [Visual Studio Code](https://code.visualstudio.com)
- Azure Data Studio [디버그 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug)(선택 사항). 디버그 확장을 사용하면 Azure Data Studio에 패키징하고 설치하지 않아도 확장을 테스트할 수 있습니다.
- `azuredatastudio`가 경로에 있는지 확인합니다. Windows의 경우 setup.exe에서 **경로에 추가** 옵션을 선택했는지 확인합니다. Mac 또는 Linux의 경우 **Install 'azuredatastudio' command in PATH** 옵션을 실행합니다.

## <a name="install-the-extension-generator"></a>확장 생성기 설치

확장을 만드는 과정을 간소화하기 위해 Yeoman을 사용하여 [확장 생성기](https://code.visualstudio.com/docs/extensions/yocode)를 빌드했습니다. 설치하려면 명령 프롬프트에서 다음 명령을 실행합니다.

```console
npm install -g yo generator-azuredatastudio
```

## <a name="create-your-dashboard-extension"></a>대시보드 확장 만들기

### <a name="introduction-to-the-dashboard"></a>대시보드 소개

Azure Data Studio 연결 대시보드는 사용자의 연결에 대한 인사이트를 요약 및 제공하는 강력한 도구입니다.

대시보드에는 두 가지 변형이 있습니다. *서버 대시보드* 는 전체 서버를 요약하고, *데이터베이스 대시보드* 는 개별 데이터베이스를 요약합니다. Azure Data Studio의 **연결** 뷰렛에 있는 서버 또는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **관리** 를 선택하여 대시보드에 액세스할 수 있습니다.

:::image type="content" source="media/dashboard-extension/dashboard-summary.gif" alt-text="대시보드 소개를 보여주는 스크린샷.":::

확장에서 대시보드에 기능을 추가하는 세 가지 주요 기여 지점이 있습니다.

1. **전체 대시보드 탭**: 확장에 대한 대시보드의 개별 탭입니다. 서버 또는 데이터베이스 대시보드에 추가할 수 있습니다. 위젯, 도구 모음 및 탐색 섹션을 사용하여 사용자 지정할 수 있습니다.
2. **홈페이지 작업**: 연결 도구 모음 상단에 있는 작업 단추입니다.
3. **위젯**: SQL Server에 대해 실행되는 그래프입니다.

   :::image type="content" source="media/dashboard-extension/dashboard-contrib-points.png" alt-text="기여 지점을 보여주는 스크린샷":::.

### <a name="run-the-extension-generator"></a>확장 생성기 실행

확장을 만들려면

1. 다음 명령을 사용하여 확장 생성기를 시작합니다.

   `yo azuredatastudio`

1. 확장 유형 목록에서 **새 대시보드** 를 선택합니다.

1. 표시된 대로 프롬프트를 입력하여 서버 대시보드에 탭을 기여하는 확장을 만듭니다.

   :::image type="content" source="media/dashboard-extension/dashboard-generator.png" alt-text="확장 생성기를 보여주는 스크린샷.":::

   프롬프트가 많으며, 각 질문의 의미에 대한 자세한 내용은 다음과 같습니다.

   :::image type="content" source="media/dashboard-extension/dashboard-flowchart.png" alt-text="대시보드 순서도를 보여주는 스크린샷.":::

이전 단계를 완료하면 새 폴더가 만들어집니다. Visual Studio Code에서 폴더를 열면 사용자 고유의 대시보드 확장을 만들 준비가 된 것입니다.

### <a name="run-the-extension"></a>확장 실행

확장을 실행하여 대시보드 템플릿에서 제공하는 작업을 확인해 보겠습니다. 실행하기 전에 **Azure Data Studio 디버그 확장** 이 Visual Studio Code에 설치되어 있는지 확인합니다.

Visual Studio Code에서 **F5** 를 선택하여 해당 확장이 실행되는 디버그 모드에서 Azure Data Studio를 시작합니다. 그런 다음, 기본 템플릿이 대시보드에 기여하는 방식을 확인할 수 있습니다.

다음으로, 이 기본 대시보드를 수정하는 방법을 살펴보겠습니다.

### <a name="develop-the-dashboard"></a>대시보드 개발

확장 개발을 시작하기 위한 가장 중요한 파일은 `package.json`입니다. 이 파일은 대시보드 기여가 등록되는 매니페스트 파일입니다. `dashboard.tabs`, `dashboard.insights` 및 `dashboard.containers` 섹션이 있습니다.

몇 가지 변경할 수 있는 사항은 다음과 같습니다.

- bar, horizontalBar 및 timeSeries를 포함한 인사이트 형식으로 재생합니다.
- SQL Server 연결에 대해 실행할 고유한 쿼리를 작성합니다.
- 특정 인사이트 자습서는 이 [샘플 인사이트 자습서](../tutorial-qds-sql-server.md) 또는 [이 자습서](../tutorial-table-space-sql-server.md)를 참조하세요.

## <a name="package-your-extension"></a>확장 패키지

다른 사용자와 공유하려면 확장을 단일 파일로 패키지해야 합니다. 확장은 Azure Data Studio 확장 마켓플레이스에 게시하거나 팀 또는 커뮤니티와 공유할 수 있습니다. 이 단계를 수행하려면 명령줄에서 다른 npm 패키지를 설치해야 합니다.

```console
npm install -g vsce
```

`README.md` 파일을 원하는 대로 편집합니다. 그런 다음, 확장의 기본 디렉터리로 이동하여 `vsce package`를 실행합니다. 리포지토리를 확장에 연결하거나 연결 없이 계속 작업할 수 있습니다. 추가하려면 `package.json` 파일에 비슷한 줄을 추가합니다.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

이러한 줄이 추가되면 `my-test-extension-0.0.1.vsix` 파일이 만들어지고, Azure Data Studio에 설치할 준비가 됩니다.

:::image type="content" source="media/dashboard-extension/install-vsix.png" alt-text="VSIX 설치를 보여주는 스크린샷.":::

## <a name="publish-your-extension-to-the-marketplace"></a>Marketplace에 확장 게시

Azure Data Studio 확장 마켓플레이스는 생성 중에 있습니다. 현재 프로세스는 확장 VSIX를 어딘가(예: GitHub 릴리스 페이지)에 호스팅하는 것입니다. 그런 다음, 확장 정보를 사용하여 [이 JSON 파일](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)을 업데이트하는 끌어오기 요청을 제출합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> - 확장 생성기를 설치합니다.
> - 확장을 만듭니다.
> - 확장에 있는 대시보드에 기여합니다.
> - 확장을 테스트합니다.
> - 확장을 패키지화합니다.
> - 마켓플레이스에 확장을 게시합니다.

이 문서를 읽은 후 사용자 고유의 Azure Data Studio 확장을 빌드하는 것이 좋습니다. 대시보드 인사이트(SQL Server에 대해 실행되는 매력적인 그래프), 다양한 SQL 관련 API 및 Visual Studio Code에서 상속된 기존의 방대한 확장 지점 세트가 지원됩니다.

아이디어가 있지만 시작하는 방법을 잘 모르는 경우 이슈를 열거나 [azuredatastudio](https://twitter.com/azuredatastudio)에 있는 팀에 트윗하세요.

모든 기존 API 및 패턴에 대한 자세한 내용은 [Visual Studio Code 확장 가이드](https://code.visualstudio.com/docs/extensions/overview)에서 설명합니다.

Azure Data Studio에서 T-SQL을 사용하는 방법을 알아보려면 T-SQL 편집기 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [Transact-SQL 편집기를 사용하여 데이터베이스 개체 만들기](../tutorial-sql-editor.md)
