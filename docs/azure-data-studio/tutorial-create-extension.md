---
title: '자습서: 확장 만들기'
titleSuffix: Azure Data Studio
description: 이 자습서에는 Azure Data Studio를 사용자 지정 기능을 추가 하려면 확장을 만드는 방법을 보여 줍니다.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: kevcunnane
ms.author: kcunnane
manager: jroth
ms.openlocfilehash: 2f031ec68cc6ae342b8bac51c450ee40a9df0555
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797962"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>자습서: Azure Data Studio 확장 만들기

이 자습서에는 새 Azure Data Studio 확장 프로그램을 만드는 방법을 보여 줍니다. 확장에서 Azure Data Studio SSMS의 친숙 한 키 바인딩을 만듭니다.

이 자습서에서 다음과 같은 방법을 배웁니다.
> [!div class="checklist"]
> * 확장 프로젝트 만들기
> * 확장 프로그램 생성기 설치
> * 확장 프로그램을 만들려면
> * 확장을 테스트 합니다
> * 확장 패키지
> * 확장 프로그램을 marketplace에 게시

## <a name="prerequisites"></a>사전 요구 사항

Azure Data Studio Visual Studio Code와 같은 프레임 워크에 기본 제공 되므로 Azure Data Studio 확장 Visual Studio Code를 사용 하 여 빌드됩니다. 시작 하려면 다음 구성 요소가 필요 합니다.

- [Node.js](https://nodejs.org) 설치 되 고 사용 가능한 프로그램 `$PATH`합니다. 포함 하는 Node.js [npm](https://www.npmjs.com/), 확장 생성기를 설치 하는 데 사용 되는 Node.js 패키지 관리자입니다.
- [Visual Studio Code](https://code.visualstudio.com) 확장을 디버그 합니다.
- Azure 데이터 스튜디오 [확장을 디버그](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (선택 사항). 이 패키지 및 Azure Data Studio에 설치 하지 않고도 확장 프로그램을 테스트할 수 있습니다.
- 확인 `azuredatastudio` 가 경로에 있습니다. Windows에 대 한 선택 했는지 확인 합니다 `Add to Path` setup.exe에 대 한 옵션입니다. Mac 또는 Linux를 실행 합니다 *설치 경로에 'azuredatastudio' 명령을* 옵션입니다.


## <a name="install-the-extension-generator"></a>확장 프로그램 생성기 설치

확장을 만드는 프로세스를 간소화 하기 빌드한를 [확장 생성기](https://code.visualstudio.com/docs/extensions/yocode) Yeoman을 사용 합니다. 을 설치 하려면 명령 프롬프트에서 다음을 실행 합니다.

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>확장 프로그램을 만들려면

확장 프로그램을 만들려면:

1. 다음 명령 사용 하 여 확장 생성기를 시작 합니다.

   `yo azuredatastudio`

2. 선택할 **새 키맵** 확장 프로그램 유형 목록에서:

   ![확장 생성기](./media/tutorial-create-extension/extension-generator.png)

3. 확장 이름을 입력 하는 단계에 따라 (이 자습서에서는 사용 하 여 **ssmskeymap2**), 설명을 추가 하 고 있습니다.

새 폴더를 만듭니다 이전 단계를 완료 합니다. Open Visual Studio Code에서 폴더를 만들 준비가 사용자 고유의 키 바인딩 확장!


### <a name="add-a-keyboard-shortcut"></a>바로 가기 키를 추가 합니다.

**1단계: 대체 하는 바로 가기를 찾을합니다**

이제 사용할 준비가 되셨나요 확장 했으므로 일부 SSMS 키보드 바로 가기 (또는 키 바인딩) Azure Data Studio에 추가 합니다. 사용한 [Andy Mallon 치트 시트](https://am2.co/2018/02/updated-cheat-sheet/) 및 RedGate의 키보드 바로 가기 목록 아이디어를 얻으세요.

누락 된 봤 가장 중요 한 가지는 다음과 같습니다.

- 사용 하도록 설정 하는 실제 실행 계획을 사용 하 여 쿼리를 실행 합니다. 이것이 **Ctrl + M** SSMS에서 Azure Data Studio에 바인딩이 없습니다.
- 것 **CTRL + SHIFT + E** 쿼리를 실행 하는 두 번째 방법으로 합니다. 사용자 의견에 따르면이 누락 되었습니다.
- 것 **alt+f1** 실행 `sp_help`합니다. Azure Data Studio에서이 추가 했습니다 하지만 해당 바인딩을 이미 사용 되었으므로 되도록 매핑한 **alt+f2** 대신 합니다.
- 전체 화면 설정/해제 (**SHIFT + ALT + ENTER**).
- **F8** 표시할 **개체 탐색기** / **서버 보기**합니다.

찾기 및 바꾸기 이러한 키 바인딩 하기 쉽습니다. 실행 *열린 바로 가기 키* 표시할 합니다 **바로 가기 키** 탭에서 Azure Data Studio, 검색할 *쿼리* 를 선택한 후 **변경 키 바인딩**. 완료 되 면는 키 바인딩을 변경, 업데이트 되는 매핑의 keybindings.json 파일에서 볼 수 있습니다 (실행할 *열린 바로 가기 키* 하는지 확인 하려면).

![바로 가기 키](./media/tutorial-create-extension/keyboard-shortcuts.png)

![keybindings.json extension](./media/tutorial-create-extension/keybindings-json.png)


**2단계: 확장에 바로 가기 추가**

확장에 바로 가기를 추가 하려면 엽니다는 *package.json* 바꾸고 파일 (확장)를 `contributes` 섹션을 다음:

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

## <a name="test-your-extension"></a>확장을 테스트 합니다

확인 `azuredatastudio` Azure Data Studio에서 명령 경로에서 설치 azuredatastudio 명령을 실행 하 여가 경로에 있습니다.

Visual Studio Code에서 Azure 데이터 Studio 디버그 확장이 설치 되어 있는지 확인 합니다.

선택 **F5** 디버그 모드에서 실행 중인 확장을 사용 하 여 Azure Data Studio를 시작 하려면:

![확장 설치](./media/tutorial-create-extension/install-extension.png)

![테스트 확장](./media/tutorial-create-extension/test-extension.png)

키 맵에 되므로 만들려면 빠른 확장명 중 하나에서 새 확장명 성공적으로 작동 하 고 공유할 준비가 됩니다.

## <a name="package-your-extension"></a>확장 패키지

다른 사용자와 공유할 확장 단일 파일로 패키지 해야 합니다. Azure Data Studio 확장 marketplace에 게시 또는 팀 또는 커뮤니티에서 공유 될 수 있습니다. 이렇게 하려면 명령줄에서 다른 npm 패키지를 설치 해야 합니다.

`npm install -g vsce`

확장의 기본 디렉터리로 이동 하 고 실행 `vsce package`합니다. 추가 줄을 중지 하려면 여러 가지 추가 해야 하는 경우는 *vsce* 불평에서 도구:

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

이 작업이 완료 된 후 내 ssmskeymap 0.1.0.vsix 파일이 생성 되 고 설치 하 고 사람들과 공유할 준비가 되었습니다!

![확장 설치](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>확장 프로그램을 marketplace에 게시

Azure Data Studio 확장 marketplace 완전히 아직 구현 되지 않았습니다, 있지만 현재 프로세스는 확장을 VSIX 어딘가에 (예: GitHub 릴리스 페이지)를 호스트 하 다음 전송할 업데이트 PR [이 JSON 파일](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) 사용 하 여 프로그램 확장 정보입니다.


## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음과 같은 방법을 학습했습니다.
> [!div class="checklist"]
> * 확장 프로젝트 만들기
> * 확장 프로그램 생성기 설치
> * 확장 프로그램을 만들려면
> * 확장을 테스트 합니다
> * 확장 패키지
> * 확장 프로그램을 marketplace에 게시


Azure Data Studio 용 고유한 확장을 빌드에 영감을 얻은 것이 읽은 후 바랍니다. 대시보드 정보 (SQL Server를 실행 하는 깔끔한 그래프), 많은 SQL 관련 Api 및 Visual Studio Code에서 상속 하는 확장 지점 중 큰 기존 집합을 지원을 했습니다.

문제 또는 팀에서 트 윗 여세요 아이디어가 해도 시작 하는 방법을 모를 경우: [azuredatastudio](https://twitter.com/azuredatastudio)합니다.

항상 참조할 수 있습니다 합니다 [Visual Studio Code 확장 가이드](https://code.visualstudio.com/docs/extensions/overview) 모든 기존 Api 및 패턴 적용 하기 때문입니다.


Azure Data Studio에서 T-SQL을 사용 하는 방법에 알아보려면 T-SQL 편집기 자습서를 완료 합니다.

> [!div class="nextstepaction"]
> [TRANSACT-SQL 편집기를 사용 하 여 데이터베이스 개체를 만드는](tutorial-sql-editor.md)합니다.
