---
title: '자습서: 확장 만들기'
titleSuffix: Azure Data Studio
description: 이 자습서에서는 Azure Data Studio에 사용자 지정 기능을 추가하는 확장을 만드는 방법을 보여 줍니다.
ms.custom: seodec18
ms.date: 12/10/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: rothja
ms.author: jroth
ms.openlocfilehash: a8a8481653f7161b39cc752878f4544f98751261
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "75241760"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>자습서: Azure Data Studio 확장 만들기

이 자습서에서는 새 Azure Data Studio 확장을 만드는 방법을 보여 줍니다. 이 확장은 Azure Data Studio에서 친숙한 SSMS 키 바인딩을 만듭니다.

이 자습서에서는 다음 방법을 알아봅니다.
> [!div class="checklist"]
> * 확장 프로젝트 만들기
> * 확장 생성기 설치
> * 확장 만들기
> * 확장 테스트
> * 확장 패키지
> * Marketplace에 확장 게시

## <a name="prerequisites"></a>사전 요구 사항

Azure Data Studio는 Visual Studio Code와 동일한 프레임워크를 기준으로 하므로 Azure Data Studio 확장은 Visual Studio Code를 사용하여 빌드됩니다. 시작하려면 다음 구성 요소가 필요합니다.

- `$PATH`에서 설치되고 사용할 수 있는 [Node.js](https://nodejs.org). Node.js에는 확장 생성기를 설치하는 데 사용되는 Node.js 패키지 관리자인 [npm](https://www.npmjs.com/)이 포함되어 있습니다.
- 확장을 디버그하기 위한 [Visual Studio Code](https://code.visualstudio.com)
- Azure Data Studio [디버그 확장](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug)(선택 사항). 이 기능을 사용하면 확장을 패키지한 후 Azure Data Studio에 설치하지 않아도 테스트할 수 있습니다.
- `azuredatastudio`가 경로에 있는지 확인합니다. Windows의 경우 setup.exe에서 `Add to Path` 옵션을 선택했는지 확인합니다. Mac 또는 Linux의 경우 *Install 'azuredatastudio' command in PATH* 옵션을 실행합니다.


## <a name="install-the-extension-generator"></a>확장 생성기 설치

확장을 만드는 과정을 간소화하기 위해 Yeoman을 사용하여 [확장 생성기](https://code.visualstudio.com/docs/extensions/yocode)를 빌드했습니다. 설치하려면 명령 프롬프트에서 다음을 실행합니다.

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>확장 만들기

확장을 만들려면

1. 다음 명령을 사용하여 확장 생성기를 시작합니다.

   `yo azuredatastudio`

2. 확장 유형 목록에서 **New Keymap**을 선택합니다.

   ![확장 생성기](./media/tutorial-create-extension/extension-generator.png)

3. 단계에 따라 확장 이름(이 자습서에서는 **ssmskeymap2** 사용)을 입력하고 설명을 추가합니다.

이전 단계를 완료하면 새 폴더가 만들어집니다. Visual Studio Code에서 폴더를 열면 사용자 고유의 키 바인딩 확장을 만들 준비가 된 것입니다.


### <a name="add-a-keyboard-shortcut"></a>바로 가기 키 추가

**1단계: 대체할 바로 가기 찾기**

확장 준비를 완료했으므로 일부 SSMS 바로 가기 키(또는 키 바인딩)를 Azure Data Studio에 추가합니다. 영감을 얻기 위해 [Andy Mallon의 참고 자료](https://am2.co/2018/02/updated-cheat-sheet/) 및 RedGate의 바로 가기 키 목록을 사용했습니다.

누락된 상위 항목은 다음과 같습니다.

- 실제 실행 계획을 사용하도록 설정하여 쿼리를 실행합니다. SSMS에서는 **Ctrl+M**이며 Azure Data Studio에는 바인딩이 없습니다.
- 쿼리를 실행하는 두 번째 방법인 **Ctrl+Shift+E**. 사용자 의견에 따르면 이 내용이 누락된 것으로 나타납니다.
- **Alt+F1**을 사용하여 `sp_help`를 실행. 이 키 조합을 Azure Data Studio에 추가했지만 해당 바인딩이 이미 사용되고 있으므로 대신 **Alt+F2**에 매핑했습니다.
- 전체 화면을 설정/해제합니다(**Shift+Alt+Enter**).
- **개체 탐색기** / **서비스 보기**를 표시하기 위한 **F8**.

이러한 키 바인딩을 쉽게 찾아서 바꿀 수 있습니다. Azure Data Studio에서 *바로 가기 키 열기*를 실행하여 **바로 가기 키** 탭을 표시하고, *쿼리*를 검색한 후 **키 바인딩 변경**을 선택합니다. 키 바인딩을 다 변경했으면 keybindings.json 파일에서 업데이트된 매핑을 볼 수 있습니다(*바로 가기 키 열기*를 실행하여 확인).

![바로 가기 키](./media/tutorial-create-extension/keyboard-shortcuts.png)

![keybindings.json 확장](./media/tutorial-create-extension/keybindings-json.png)


**2단계: 확장에 바로 가기 추가**

확장에 바로 가기를 추가하려면 *package.json* 파일(확장에 있음)을 열고 `contributes` 섹션을 다음으로 바꿉니다.

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>확장 테스트

Azure Data Studio에서 Install azuredatastudio command in PATH 명령을 실행하여 `azuredatastudio`가 PATH에 있는지 확인합니다.

Azure Data Studio 디버그 확장이 Visual Studio Code에 설치되어 있는지 확인합니다.

**F5** 키를 선택하여 해당 확장이 실행되는 디버그 모드에서 Azure Data Studio를 시작합니다.

![확장 설치](./media/tutorial-create-extension/install-extension.png)

![확장 테스트](./media/tutorial-create-extension/test-extension.png)

키맵은 만들 수 있는 가장 빠른 확장 중 하나이므로 이제 새 확장이 성공적으로 작동하고 공유할 준비가 되었습니다.

## <a name="package-your-extension"></a>확장 패키지

다른 사용자와 공유하려면 확장을 단일 파일로 패키지해야 합니다. 이러한 패키지를 Azure Data Studio 확장 Marketplace에 게시하거나 팀 또는 커뮤니티에서 공유할 수 있습니다. 이렇게 하려면 명령줄에서 다른 npm 패키지를 설치해야 합니다.

`npm install -g vsce`

확장의 기본 디렉터리로 이동하고 `vsce package`를 실행합니다. *vsce* 도구가 문제를 발생하지 않도록 하기 위해 몇 개의 줄에 추가해야 했습니다.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

이 작업이 완료된 후에 ssmskeymap-0.1.0 파일이 생성되었으며 이 파일을 설치하고 전 세계 사용자와 공유할 수 있습니다.

![확장 설치](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>Marketplace에 확장 게시

Azure Data Studio 확장 Marketplace는 아직 완전히 구현되지 않았지만 현재, 임의의 위치(예: GitHub 릴리스 페이지)에 확장 VSIX를 호스트하는 과정이 진행 중입니다. 따라서 [이 JSON 파일](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)을 확장 정보로 업데이트하는 PR을 제출합니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 확장 프로젝트 만들기
> * 확장 생성기 설치
> * 확장 만들기
> * 확장 테스트
> * 확장 패키지
> * Marketplace에 확장 게시


이 내용을 읽으면 Azure Data Studio에 대한 고유한 확장을 빌드하는 데 도움이 될 것입니다. 대시보드 인사이트(SQL Server에 대해 실행되는 그래프), 다양한 SQL 관련 API 및 Visual Studio Code에서 상속된 기존의 방대한 확장 지점 세트가 지원됩니다.

생각은 있지만 시작하는 방법을 모를 경우 [azuredatastudio](https://twitter.com/azuredatastudio) 팀에서 이슈를 열거나 트윗하세요.

[Visual Studio Code 확장 가이드](https://code.visualstudio.com/docs/extensions/overview)는 기존의 모든 API 및 패턴을 포함하므로 항상 참조할 수 있습니다.


Azure Data Studio에서 T-SQL을 사용하는 방법을 알아보려면 T-SQL 편집기 자습서를 완료합니다.

> [!div class="nextstepaction"]
> [Transact-SQL 편집기를 사용하여 데이터베이스 개체를 만듭니다](tutorial-sql-editor.md).
