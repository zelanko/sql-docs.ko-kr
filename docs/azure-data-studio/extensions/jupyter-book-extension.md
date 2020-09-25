---
title: Jupyter Book 확장 만들기
description: 확장 생성기를 사용하여 확장에 Jupyter Book을 패키지하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: a781affee2db40dbd7636c25712ca622c881650e
ms.sourcegitcommit: 8f062015c2a033f5a0d805ee4adabbe15e7c8f94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91226840"
---
# <a name="create-a-jupyter-book-extension"></a>Jupyter Book 확장 만들기

이 자습서에서는 새 Jupyter Book Azure Data Studio 확장을 만드는 방법을 보여 줍니다. 확장에는 Azure Data Studio에서 열고 실행할 수 있는 샘플 Jupyter Book이 제공됩니다. 

이 자습서에서는 다음 방법을 알아봅니다.
> [!div class="checklist"]
> - 확장 프로젝트 만들기
> - 확장 생성기 설치
> - Jupyter Book 확장 만들기
> - 확장 실행
> - 확장 패키지
> - Marketplace에 확장 게시

## <a name="apis-used"></a>사용되는 API

- `bookTreeView.openBook`

### <a name="extension-use-cases"></a>확장 사용 사례

Jupyter Book 확장을 만드는 데는 몇 가지 다양한 이유가 있습니다.

- 구성 및 섹션 분할된 대화형 문서 공유
- 전체 Book 공유(eBook과 유사하지만 Azure Data Studio를 통해 배포됨)
- 버전 및 Jupyter Book 업데이트 추적

Jupyter Book과 Notebook의 주요 차이점은 Jupyter Book은 조직을 제공한다는 점입니다. 수십 개의 Notebook을 Book의 여러 챕터로 분할할 수 있지만 Notebook 확장은 그 용도가 소수의 개별 Notebook을 전달하는 것입니다.

## <a name="prerequisites"></a>필수 조건

Azure Data Studio는 Visual Studio Code와 동일한 프레임워크를 기준으로 하므로 Azure Data Studio 확장은 Visual Studio Code를 사용하여 빌드됩니다. 시작하려면 다음 구성 요소가 필요합니다.

- `$PATH`에서 설치되고 사용할 수 있는 [Node.js](https://nodejs.org). Node.js에는 확장 생성기를 설치하는 데 사용되는 Node.js 패키지 관리자인 [npm](https://www.npmjs.com/)이 포함되어 있습니다.
- [Visual Studio Code](https://code.visualstudio.com)로 확장을 변경 및 디버그합니다.
- `azuredatastudio`가 경로에 있는지 확인합니다. Windows의 경우 setup.exe에서 `Add to Path` 옵션을 선택했는지 확인합니다. Mac 또는 Linux의 경우 *Install 'azuredatastudio' command in PATH* 옵션을 실행합니다.

## <a name="install-the-extension-generator"></a>확장 생성기 설치

확장을 만드는 과정을 간소화하기 위해 Yeoman을 사용하여 [확장 생성기](https://www.npmjs.com/package/generator-azuredatastudio)를 빌드했습니다. 설치하려면 명령 프롬프트에서 다음 명령을 실행합니다.

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>확장 만들기

확장을 만들려면

1. 다음 명령을 사용하여 확장 생성기를 시작합니다.

   `yo azuredatastudio`

2. 확장 유형 목록에서 **새 Jupyter Book**을 선택합니다.

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-extension-generator.png" alt-text="확장 생성기":::

3. 단계를 따라 확장 이름(이 자습서에서는 **Test Book** 사용)과 게시자 이름(이 자습서에서는 **Microsoft** 사용)을 입력하고 설명을 추가합니다.

기존 Jupyter Book을 제공하거나, 제공된 샘플 Book을 사용하거나, 새 Jupyter Book을 만듭니다. 아래에는 세 가지 옵션이 모두 나와 있습니다.

### <a name="providing-an-existing-book"></a>기존 Book 제공

이미 만든 Book을 전달하려면 Book 콘텐츠가 있는 폴더의 절대 파일 경로를 제공합니다. 그런 다음, 확장에 대한 학습과 전달 준비를 할 수 있습니다.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-existing-book.png" alt-text="기존 Book":::

### <a name="using-the-sample-book"></a>샘플 Book 사용

기존 Book 또는 Notebook이 없으면 생성기에서 제공된 샘플을 사용할 수 있습니다.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-sample-path.png" alt-text="샘플 Jupyter Book":::

샘플 Book은 간단한 Jupyter Book의 모습을 보여 줍니다. Jupyter Book의 사용자 지정에 관해 알아보려면 기존 Notebook을 사용하여 새 Book 만들기 관련 섹션을 참조하세요.

### <a name="creating-a-new-book"></a>새 Book 만들기

Jupyter Book에 패키지할 Notebook이 있는 경우 패키지가 가능합니다. 생성기에는 Book에 챕터가 필요한지 묻는 메시지가 표시되며, 예라고 답할 경우 챕터 수와 제목을 묻는 메시지가 표시됩니다. 선택 프로세스는 아래와 같습니다. 스페이스바를 사용하여 각 챕터에 배치하고자 하는 Notebook을 선택합니다.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-create-book.png" alt-text="Jupyter Book 만들기":::

이전 단계를 완료하면 새 Jupyter Book이 포함된 새 폴더가 만들어집니다. Visual Studio Code에서 폴더를 열면 Jupyter Book 확장을 전달할 준비가 된 것입니다.

## <a name="understanding-your-extension"></a>확장 이해

현재 프로젝트는 다음과 같을 것입니다.

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-file-structure-generator.png" alt-text="확장 파일 구조":::

`vsc-extension-quickstart.md`는 중요 파일에 대한 참조를 제공합니다. `README.md`에서 새 확장에 대한 문서를 제공할 수 있습니다. `package.json`, `jupyter-book.ts`, `content` 및 `toc.yml` 파일이 있습니다. `content` 폴더는 모든 Notebook 또는 markdown 파일을 보유합니다. `toc.yml`은 Jupyter Book을 구성하고, 확장 생성기를 통해 사용자 지정 Jupyter Book을 만드는 경우 자동으로 생성됩니다.

생성기를 사용하여 Book을 만들고 챕터를 사용한다면 폴더 구조는 약간 다를 것입니다. `content` 폴더에 있는 markdown 및 Jupyter Notebook 파일 대신 선택한 챕터 제목에 해당하는 하위 폴더가 있을 것입니다. 

게시하지 않으려는 파일이나 폴더가 있는 경우 해당 파일 또는 폴더 이름을 `.vscodeignore` 파일에 포함할 수 있습니다.

`jupyter-book.ts` 파일을 살펴보면서 새로 만든 확장에서 수행하는 작업을 이해해 보겠습니다.

```javascript
// This function is called when you run the command `Launch Book: Test Book` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchBook.test-book', () => {
        processNotebooks();
    }));

    // Add other code here if you want to register another command
}
```

`activate` 함수는 확장의 기본 작업입니다. 등록할 명령이 `launchBook.test-book` 명령과 비슷하게 `activate` 함수 내에 표시되어야 합니다. `processNotebooks` 함수 내에는 Jupyter Book을 보유하고 확장 폴더를 매개 변수로 사용하여 `bookTreeView.openBook`을 호출하는 확장 폴더가 있습니다. 

또한 `package.json` 파일은 확장의 명령을 등록하는 중요한 역할을 합니다.

```json
"activationEvents": [
        "onCommand:launchBook.test-book"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchBook.test-book",
                "title": "Launch Book: Test Book"
            }
        ]
    }
```

활성화 이벤트 `onCommand`는 명령을 호출할 때 등록한 함수를 트리거합니다. 추가 사용자 지정이 가능한 몇 가지 다른 활성화 이벤트가 있습니다. 자세한 내용은 [활성화 이벤트](https://code.visualstudio.com/api/references/activation-events)를 참조하세요.

## <a name="package-your-extension"></a>확장 패키지

다른 사용자와 공유하려면 확장을 단일 파일로 패키지해야 합니다. 이러한 패키지를 Azure Data Studio 확장 Marketplace에 게시하거나 팀 또는 커뮤니티에서 공유할 수 있습니다. 이렇게 하려면 명령줄에서 다른 npm 패키지를 설치해야 합니다.

```console
`npm install -g vsce`
```

원하는 대로 `README.md`를 편집하고 확장의 기본 디렉터리로 이동한 다음, `vsce package`를 실행합니다. 리포지토리를 확장에 연결하거나 연결 없이 계속 작업할 수 있습니다. 추가하려면 `package.json` 파일에 비슷한 줄을 추가합니다.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testbook.git"
}
```

이러한 줄이 추가된 후에는 my test-book-0.0.1.vsix 파일이 생성되었고, 이 파일을 Azure Data Studio에 설치할 준비가 되었습니다.

## <a name="run-your-extension"></a>확장 실행

확장을 실행 및 테스트하려면 Azure Data Studio를 열고 명령 팔레트(`Ctrl + Shift + P`)를 엽니다. **확장: VSIX에서 설치** 명령을 찾은 다음, 새 확장이 포함된 폴더로 이동합니다. 이제 Azure Data Studio의 확장 패널에 해당 확장이 표시될 것입니다.

   :::image type="content" source="media/jupyter-book-extension/install-vsix.png" alt-text="VSIX 설치":::

명령 팔레트를 다시 연 다음, 등록한 명령인 **Book 시작: Notebook 테스트**를 찾습니다. 실행 시 확장을 사용하여 패키지한 Jupyter Book을 열어야 합니다.

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-launch-ads.png" alt-text="Notebook 명령":::

지금까지 첫 번째 Jupyter Book 확장을 빌드했고, 이제 이 확장을 전달할 수 있습니다. Jupyter Book에 대한 자세한 내용은 [Jupyter를 사용한 Book](https://jupyterbook.org/intro.html)을 참조하세요.

## <a name="publish-your-extension-to-the-marketplace"></a>Marketplace에 확장 게시

Azure Data Studio 확장 Marketplace는 아직 완전히 구현되지 않았습니다. 게시하려면 확장 VSIX를 어딘가(예: GitHub 릴리스 페이지)에 호스트하고 확장 정보를 사용하여 [이 JSON 파일](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)의 PR 업데이트를 제출합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> - 확장 프로젝트 만들기
> - 확장 생성기 설치
> - Jupyter Book 확장 만들기
> - 확장 패키지
> - Marketplace에 확장 게시

이 자습서를 읽은 후에 Azure Data Studio 커뮤니티에 공유하고자 하는 Jupyter Book 관련 의견이 있기를 바랍니다. 

의견은 있지만 시작하는 방법을 모를 경우 이슈를 열거나 [azuredatastudio](https://twitter.com/azuredatastudio) 팀에 트윗하세요.

[Visual Studio Code 확장 가이드](https://code.visualstudio.com/docs/extensions/overview)는 기존의 모든 API 및 패턴을 포함하므로 항상 참조할 수 있습니다.
