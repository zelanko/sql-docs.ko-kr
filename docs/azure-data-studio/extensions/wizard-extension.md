---
title: 마법사 확장 만들기
description: 이 자습서에서는 Azure Data Studio에 사용자 지정 기능을 추가하는 마법사 확장을 만드는 방법을 보여 줍니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 50440aca120dad6cfd165262bd4bfd2e139393cf
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364060"
---
# <a name="create-an-azure-data-studio-wizard-extension"></a>Azure Data Studio 마법사 확장 만들기

이 자습서에서는 새 **Azure Data Studio 마법사 확장**을 만드는 방법을 보여 줍니다. 확장은 Azure Data Studio에서 사용자와 상호 작용할 수 있는 마법사를 기여합니다.

이 문서에서는 다음 방법을 알아봅니다.
> [!div class="checklist"]
> - 확장 생성기 설치
> - 확장 만들기
> - 확장에 사용자 지정 마법사 추가
> - 확장 테스트
> - 확장 패키지
> - Marketplace에 확장 게시

## <a name="prerequisites"></a>필수 조건

Azure Data Studio는 Visual Studio Code와 동일한 프레임워크를 기준으로 하므로 Azure Data Studio 확장은 Visual Studio Code를 사용하여 빌드됩니다. 시작하려면 다음 구성 요소가 필요합니다.

- `$PATH`에서 설치되고 사용할 수 있는 [Node.js](https://nodejs.org). Node.js에는 확장 생성기를 설치하는 데 사용되는 Node.js 패키지 관리자인 [npm](https://www.npmjs.com/)이 포함되어 있습니다.
- 확장을 디버그하기 위한 [Visual Studio Code](https://code.visualstudio.com)
- Azure Data Studio [디버그 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug)(선택 사항). 이 기능을 사용하면 확장을 패키지한 후 Azure Data Studio에 설치하지 않아도 테스트할 수 있습니다.
- `azuredatastudio`가 경로에 있는지 확인합니다. Windows의 경우 setup.exe에서 `Add to Path` 옵션을 선택했는지 확인합니다. Mac 또는 Linux의 경우 *Install 'azuredatastudio' command in PATH* 옵션을 실행합니다.

## <a name="install-the-extension-generator"></a>확장 생성기 설치

확장을 만드는 과정을 간소화하기 위해 Yeoman을 사용하여 [확장 생성기](https://code.visualstudio.com/docs/extensions/yocode)를 빌드했습니다. 설치하려면 명령 프롬프트에서 다음을 실행합니다.

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-wizard-extension"></a>마법사 확장 만들기

### <a name="introduction-to-wizards"></a>마법사 소개

마법사는 작업을 수행하기 위해 사용자가 입력하는 단계별 페이지를 제공하는 사용자 인터페이스 유형입니다. 소프트웨어 설치 마법사와 문제 해결 마법사를 일반적인 예로 들 수 있습니다. 다음은 그 예입니다.

:::image type="content" source="media/wizard-extension/dacpac-wizard.gif" alt-text="Dacpac 마법사":::

마법사는 데이터를 사용하고 Azure Data Studio 기능을 확장하는 데 도움이 되는 경우가 많으므로 Azure Data Studio에서는 사용자 지정 마법사를 만들 수 있도록 API를 제공합니다. 마법사 템플릿을 생성하고 수정하여 사용자 지정 마법사를 만드는 방법을 살펴보겠습니다.

### <a name="run-the-extension-generator"></a>확장 생성기 실행

확장을 만들려면

1. 다음 명령을 사용하여 확장 생성기를 시작합니다.

   `yo azuredatastudio`

2. 확장 유형 목록에서 **새 마법사 또는 대화 상자**를 선택합니다. 그런 다음, **마법사**를 선택하고 **시작하기 템플릿**을 선택합니다.

3. 단계에 따라 확장 이름(이 자습서에서는 **My Test Extension** 사용)을 입력하고 설명을 추가합니다.

    :::image type="content" source="media/wizard-extension/extension-generator.png" alt-text="확장 생성기":::

이전 단계를 완료하면 새 폴더가 만들어집니다. Visual Studio Code에서 폴더를 열면 사용자 고유의 마법사 확장을 만들 준비가 된 것입니다.

### <a name="run-the-extension"></a>확장 실행

확장을 실행하여 마법사 템플릿에서 제공하는 작업을 확인해 보겠습니다. 실행 전에 **Azure Data Studio 디버그 확장**이 Visual Studio Code에 설치되어 있는지 확인합니다.

VS Code에서 **F5** 키를 선택하여 해당 확장이 실행되는 디버그 모드에서 Azure Data Studio를 시작합니다. 그런 다음, Azure Data Studio의 새 창에 있는 명령 팔레트(Ctr+Shift+P)에서 **마법사 시작** 명령을 실행합니다. 그러면 이 확장에서 기여하는 기본 마법사가 시작됩니다.

:::image type="content" source="media/wizard-extension/wizard-template.gif" alt-text="마법사 템플릿":::

다음에는 이 기본 마법사를 수정하는 방법을 살펴보겠습니다.

### <a name="develop-the-wizard"></a>마법사 개발

확장 개발을 시작하는 데 있어 가장 중요한 파일은 `package.json`, `src/main.ts` 및 `vsc-extension-quickstart.md`입니다.

- `package.json`: 이 파일은 **마법사 시작** 명령이 등록된 매니페스트 파일입니다. `main.ts`가 기본 프로그램 진입점으로 선언되는 파일이기도 합니다.
- `main.ts`: 페이지, 텍스트 및 단추와 같은 UI 요소를 마법사에 추가하는 코드가 포함되어 있습니다.
- `vsc-extension-quickstart.md`: 개발 시 유용한 참조가 될 수 있는 기술 문서를 포함합니다.

네 번째 빈 페이지를 추가하여 마법사를 변경해 보겠습니다. 아래와 같이 `src/main.ts` 파일을 수정하면 마법사를 시작할 때 추가 페이지가 표시됩니다.

:::image type="content" source="media/wizard-extension/wizard-main.png" alt-text="마법사 기본":::
템플릿에 익숙해지면 다음과 같은 몇 가지 추가 작업을 수행할 수 있습니다.

- 너비가 300인 단추를 새 페이지에 추가
- 단추를 넣을 플렉스 구성 요소 추가
- 단추에 작업 추가. 예를 들어 단추를 클릭하면 파일 열기 대화 상자를 시작하거나 쿼리 편집기를 엽니다.

## <a name="package-your-extension"></a>확장 패키지

다른 사용자와 공유하려면 확장을 단일 파일로 패키지해야 합니다. 이러한 패키지를 Azure Data Studio 확장 Marketplace에 게시하거나 팀 또는 커뮤니티에서 공유할 수 있습니다. 이렇게 하려면 명령줄에서 다른 npm 패키지를 설치해야 합니다.

```console
npm install -g vsce`
```

원하는 대로 `README.md`를 편집하고 확장의 기본 디렉터리로 이동한 다음, `vsce package`를 실행합니다. 리포지토리를 확장에 연결하거나 연결 없이 계속 작업할 수 있습니다. 추가하려면 `package.json` 파일에 비슷한 줄을 추가합니다.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/anjalia/my-test-extension.git"
}
```

이러한 줄이 추가된 후에는 my-test-extension-0.0.1.vsix 파일이 생성되었고, 이 파일을 Azure Data Studio에 설치할 준비가 되었습니다.

:::image type="content" source="media/wizard-extension/install-vsix.png" alt-text="VSIX 설치":::

## <a name="publish-your-extension-to-the-marketplace"></a>Marketplace에 확장 게시

Azure Data Studio 확장 Marketplace는 아직 완전히 구현되지 않았지만 현재, 임의의 위치(예: GitHub 릴리스 페이지)에 확장 VSIX를 호스트하는 과정이 진행 중입니다. 따라서 [이 JSON 파일](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)을 확장 정보로 업데이트하는 PR을 제출합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> - 확장 생성기 설치
> - 확장 만들기
> - 확장에 사용자 지정 마법사 추가
> - 확장 테스트
> - 확장 패키지
> - Marketplace에 확장 게시

이 내용을 읽으면 Azure Data Studio에 대한 고유한 확장을 빌드하는 데 도움이 될 것입니다. 대시보드 인사이트(SQL Server에 대해 실행되는 그래프), 다양한 SQL 관련 API 및 Visual Studio Code에서 상속된 기존의 방대한 확장 지점 세트가 지원됩니다.

생각은 있지만 시작하는 방법을 모를 경우 [azuredatastudio](https://twitter.com/azuredatastudio) 팀에서 이슈를 열거나 트윗하세요.

[Visual Studio Code 확장 가이드](https://code.visualstudio.com/docs/extensions/overview)는 기존의 모든 API 및 패턴을 포함하므로 항상 참조할 수 있습니다.

Azure Data Studio에서 T-SQL을 사용하는 방법을 알아보려면 T-SQL 편집기 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [Transact-SQL 편집기를 사용하여 데이터베이스 개체 만들기](../tutorial-sql-editor.md)
