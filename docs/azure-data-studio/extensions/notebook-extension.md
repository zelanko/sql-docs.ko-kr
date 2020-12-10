---
title: Jupyter Notebook 확장 만들기
description: 확장 생성기를 사용하여 Notebook을 확장에 패키지하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 44080250d95d21cecca16ff605ca22683e5b4440
ms.sourcegitcommit: 7f76975c29d948a9a3b51abce564b9c73d05dcf0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96900816"
---
# <a name="create-a-jupyter-notebook-extension"></a>Jupyter Notebook 확장 만들기

이 자습서에서는 새 Jupyter Notebook Azure Data Studio 확장을 만드는 방법을 보여 줍니다. 확장에는 Azure Data Studio에서 열고 실행할 수 있는 샘플 Jupyter Notebook이 제공됩니다.

이 문서에서는 다음 방법을 알아봅니다.

> [!div class="checklist"]
> - 확장 프로젝트를 만듭니다.
> - 확장 생성기를 설치합니다.
> - Notebook 확장을 만듭니다.
> - 확장을 실행합니다.
> - 확장을 패키지합니다.
> - 확장을 마켓플레이스에 게시합니다.

## <a name="apis-used"></a>사용되는 API

- `azdata.nb.showNotebookDocument`

### <a name="extension-use-cases"></a>확장 사용 사례

Notebook 확장을 만드는 데는 몇 가지 다양한 이유가 있습니다.
- 대화형 문서 공유
- Notebook 저장 및 상시 액세스
- 사용자가 따를 수 있는 코딩 문제 제공
- 버전 및 Notebook 업데이트 추적

## <a name="prerequisites"></a>필수 조건

Azure Data Studio는 Visual Studio Code와 동일한 프레임워크를 기반으로 하여 빌드되므로 Azure Data Studio 확장은 Visual Studio Code를 사용하여 빌드됩니다. 시작하려면 다음 구성 요소가 필요합니다.

- `$PATH`에서 설치되고 사용할 수 있는 [Node.js](https://nodejs.org). Node.js에는 확장 생성기를 설치하는 데 사용되는 Node.js 패키지 관리자인 [npm](https://www.npmjs.com/)이 포함되어 있습니다.
- 확장을 디버그하기 위한 [Visual Studio Code](https://code.visualstudio.com)
- `azuredatastudio`가 경로에 있는지 확인합니다. Windows의 경우 setup.exe에서 **경로에 추가** 옵션을 선택했는지 확인합니다. Mac 또는 Linux의 경우 **Install 'azuredatastudio' command in PATH** 옵션을 실행합니다.

## <a name="install-the-extension-generator"></a>확장 생성기 설치

확장을 만드는 과정을 간소화하기 위해 Yeoman을 사용하여 [확장 생성기](https://www.npmjs.com/package/generator-azuredatastudio)를 빌드했습니다. 설치하려면 명령 프롬프트에서 다음 명령을 실행합니다.

```console
npm install -g yo generator-azuredatastudio
```

## <a name="create-your-extension"></a>확장 만들기

확장을 만들려면

1. 다음 명령을 사용하여 확장 생성기를 시작합니다.

   `yo azuredatastudio`

2. 확장 유형 목록에서 **새 Notebook(개별)** 을 선택합니다.

   :::image type="content" source="media/notebook-extension/notebook-extension-generator.png" alt-text="Notebook 확장 생성기":::

3. 단계에 따라 확장 이름을 입력합니다. 이 자습서에서는 **Notebook 테스트** 를 사용합니다. 그런 다음, 게시자 이름을 입력합니다. 이 자습서에서는 **Microsoft** 를 사용합니다. 마지막으로 설명을 추가합니다.

이제 몇 가지 분기가 있습니다. 이미 만든 Jupyter Notebook을 추가하거나 생성기를 통해 제공되는 Notebook 샘플을 사용할 수 있습니다.

이 자습서에서는 Python Notebook 샘플을 사용합니다.

   :::image type="content" source="media/notebook-extension/notebook-sample-generator.png" alt-text="Python 샘플 선택":::

전달하는 데 관심이 있는 Notebook이 있는 경우 전달하려는 기존 Notebook이 있다고 대답합니다. 모든 Notebook 또는 markdown 파일이 있는 절대 파일 경로를 제공합니다.

이전 단계를 완료하면 샘플 Notebook이 포함된 새 폴더가 만들어집니다. Visual Studio Code에서 폴더를 엽니다. 이제 새 Notebook 확장을 전달할 준비가 되었습니다.

## <a name="understand-your-extension"></a>확장 이해

현재 프로젝트는 다음과 같을 것입니다.

   :::image type="content" source="media/notebook-extension/notebook-file-structure-generator.png" alt-text="확장 파일 구조":::

`vsc-extension-quickstart.md` 파일은 중요한 파일에 대한 참조를 제공합니다. `README.md` 파일은 새 확장에 대한 설명서를 제공할 수 있습니다. `package.json`, `notebook.ts` 및 `pySample.ipynb` 파일이 있습니다.

게시하지 않으려는 파일 또는 폴더가 있는 경우 해당 이름을 `.vscodeignore` 파일에 포함할 수 있습니다.

`notebook.ts` 파일을 살펴보면서 새로 만든 확장에서 수행하는 작업을 이해해 보겠습니다.

```javascript
// This function is called when you run the command `Launch Notebooks: Test Notebook` from the
// command palette in Azure Data Studio. If you want any additional functionality
// to occur when you launch the book, add it to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchNotebooks.test-notebook', () => {
        let notebooksToDisplay: Array<string> = processNotebooks();
        notebooksToDisplay.forEach(name => {
            azdata.nb.showNotebookDocument(vscode.Uri.file(name));
        });
    }));

    // Add other code here if you want to register another command.
}
```

이는 **Notebook 시작: Notebook 테스트** 명령을 통해 확장을 실행할 때마다 호출되는 `notebook.ts`의 기본 함수입니다. `vscode.commands.registerCommand` API를 사용하여 새 명령을 만듭니다. 중괄호 내의 다음 정의는 명령을 호출할 때마다 실행되는 코드입니다. `processNotebooks` 함수에서 찾은 각 Notebook에 대해 `azdata.nb.showNotebookDocument`를 사용하여 Azure Data Studio에서 엽니다.

또한 `package.json` 파일은 **Notebook 시작: Notebook 테스트** 명령을 등록하는 데 중요한 역할을 합니다.

```json
"activationEvents": [
        "onCommand:launchNotebooks.test-notebook"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchNotebooks.test-notebook",
                "title": "Launch Notebooks: Test Notebook"
            }
        ]
    }
```

명령에 대한 활성화 이벤트가 있으며, 특정 기여 지점도 추가했습니다. 이러한 기여 지점은 사용자가 확장을 볼 때 확장이 게시된 확장 마켓플레이스에 표시됩니다. 더 많은 명령을 추가하려면 해당 명령을 `activationEvents` 필드에 추가해야 합니다. 자세한 옵션은 [활성화 이벤트](https://code.visualstudio.com/api/references/activation-events)를 참조하세요.

## <a name="package-your-extension"></a>확장 패키지

다른 사용자와 공유하려면 확장을 단일 파일로 패키지해야 합니다. 확장은 Azure Data Studio 확장 마켓플레이스에 게시하거나 팀 또는 커뮤니티와 공유할 수 있습니다. 이 단계를 수행하려면 명령줄에서 다른 npm 패키지를 설치해야 합니다.

```console
npm install -g vsce
```

`README.md` 파일을 원하는 대로 편집합니다. 그런 다음, 확장의 기본 디렉터리로 이동하여 `vsce package`를 실행합니다. 리포지토리를 확장에 연결하거나 연결 없이 계속 작업할 수 있습니다. 추가하려면 `package.json` 파일에 비슷한 줄을 추가합니다.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testnotebook.git"
}
```

이러한 줄이 추가되면 `my test-notebook-0.0.1.vsix` 파일이 만들어지고, 이를 설치하고 환경과 공유할 준비가 됩니다.

## <a name="run-your-extension"></a>확장 실행

확장을 실행하고 테스트하려면 Azure Data Studio를 열고, **Ctrl+Shift+P** 를 선택하여 명령 팔레트를 엽니다. **확장: VSIX에서 설치** 명령을 찾고, 새 확장이 포함된 폴더로 이동합니다.

   :::image type="content" source="media/notebook-extension/install-vsix.png" alt-text="VSIX 설치":::

이제 확장이 Azure Data Studio의 확장 패널에 표시됩니다. 명령 팔레트를 다시 엽니다. 그러면 **Book 시작: Book 테스트** 확장을 사용하여 만든 새 명령을 확인할 수 있습니다. 실행 시 확장을 사용하여 패키지한 Jupyter Book을 열어야 합니다.

   :::image type="content" source="media/notebook-extension/notebook-launch-ads.png" alt-text="Notebook 명령":::

지금까지 첫 번째 Jupyter Notebook 확장을 빌드했고, 이제 이 확장을 전달할 수 있습니다.

## <a name="publish-your-extension-to-the-marketplace"></a>Marketplace에 확장 게시

Azure Data Studio 확장 마켓플레이스는 생성 중에 있습니다. 게시하려면 확장 VSIX를 어딘가(예: GitHub 릴리스 페이지)에 호스팅합니다. 그런 다음, 확장 정보를 사용하여 [이 JSON 파일](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)을 업데이트하는 끌어오기 요청을 제출합니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> - 확장 프로젝트를 만듭니다.
> - 확장 생성기를 설치합니다.
> - Notebook 확장을 만듭니다.
> - 확장을 만듭니다.
> - 확장을 패키지합니다.
> - 확장을 마켓플레이스에 게시합니다.

이 문서를 읽은 후에는 사용자 고유의 Azure Data Studio 확장을 빌드하는 데 도움이 됩니다.

아이디어가 있지만 시작하는 방법을 잘 모르는 경우 문제를 제출하거나 [azuredatastudio](https://twitter.com/azuredatastudio)에 있는 팀에 트윗하세요.

모든 기존 API 및 패턴에 대한 자세한 내용은 [Visual Studio Code 확장 가이드](https://code.visualstudio.com/docs/extensions/overview)에서 설명합니다.
