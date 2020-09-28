---
title: 확장 만들기
description: 확장을 사용하여 Azure Data Studio에 기능을 추가할 수 있습니다. 확장을 만들고 확장 갤러리에 게시하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu
ms.custom: ''
ms.date: 08/26/2020
ms.openlocfilehash: 92c6a5d9522d015786eafdefaeea64b46925b92b
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364040"
---
# <a name="extend-functionality-by-creating-azure-data-studio-extensions"></a>Azure Data Studio 확장을 만들어 기능 확장

Azure Data Studio의 확장을 사용하면 기본 Azure Data Studio 설치에 다른 기능을 쉽게 추가할 수 있습니다.

확장은 Azure Data Studio 팀(Microsoft) 및 타사 커뮤니티(사용자)가 제공합니다.

## <a name="author-an-extension"></a>확장 작성

Azure Data Studio를 확장하는 데 관심이 있는 경우 고유한 확장을 만들어 확장 갤러리에 게시할 수 있습니다.

### <a name="write-an-extension"></a>확장 작성

#### <a name="prerequisites"></a>사전 요구 사항

확장을 개발하려면 [Node.js](https://nodejs.org/)를 설치하고 `$PATH`에서 사용할 수 있어야 합니다. Node.js에는 확장 생성기를 설치하는 데 사용되는 Node.js 패키지 관리자인 npm이 포함되어 있습니다.

새 확장을 만들려면 Azure Data Studio 확장 생성기를 사용하면 됩니다. Yeoman [확장 생성기](https://www.npmjs.com/package/generator-azuredatastudio)는 확장 프로젝트의 좋은 시작점이 됩니다. 생성기를 시작하려면 명령 프롬프트에 다음 명령을 입력합니다.

```console
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

확장 템플릿을 시작하는 방법에 대한 자세한 내용은 확장을 만드는 과정을 안내하는 [키맵 확장](keymap-extension.md)을 참조하세요.

### <a name="extensibility-references"></a>확장성 참조

Azure Data Studio 확장성에 대해 알아보려면 [확장성 개요](../extensibility.md)를 참조하세요. 기존 [샘플](https://github.com/Microsoft/azuredatastudio/tree/main/samples)에서 API 사용 방법의 예제를 확인할 수도 있습니다.

## <a name="debug-an-extension"></a>확장 디버그

Visual Studio Code 확장 [Azure Data Studio 디버그](https://github.com/kevcunnane/sqlops-debug)를 사용하여 새 확장을 디버그할 수 있습니다.

확장을 디버그하려면 다음을 수행합니다.

1. [Visual Studio Code](https://code.visualstudio.com/)를 사용하여 확장을 엽니다.
2. Azure Data Studio 디버그 확장을 설치합니다.
3. **F5**를 선택하거나 **디버그** 아이콘을 선택한 다음, **시작**을 선택합니다.
4. Azure Data Studio의 새 인스턴스가 특수 모드(확장 개발 호스트)에서 시작됩니다. 이 새 인스턴스는 이제 확장을 인식합니다.

## <a name="create-an-extension-package"></a>확장 패키지 만들기

확장을 작성한 후에는 Azure Data Studio에 설치되는 VSIX 패키지를 만들어야 합니다. [vscode-vsce](https://github.com/Microsoft/vscode-vsce)(Visual Studio Code 확장)를 사용하여 VSIX 패키지를 만들 수 있습니다.

```console
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

VSIX 패키지를 사용하면 .vsix 파일을 공유하고 명령 팔레트에서 **확장: VSIX 파일에서 설치** 명령을 사용하여 확장을 Azure Data Studio에 설치하여 로컬 및 비공개로 확장을 공유할 수 있습니다.

## <a name="publish-an-extension"></a>확장 게시

Azure Data Studio에 새 확장을 게시하려면

1. [확장 갤러리](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json)에 확장을 추가합니다.
2. 현재 타사 확장을 호스트할 수 있는 기능이 없습니다. 확장을 다운로드하는 대신 Azure Data Studio에는 다운로드 페이지로 이동할 수 있는 옵션이 있습니다. 확장에 대한 다운로드 페이지를 설정하려면 **Microsoft.AzureDataStudio.DownloadPage** 자산 값을 설정합니다.
3. 릴리스/확장 분기에 대한 PR을 만듭니다.
4. 팀에 검토 요청을 보냅니다.

확장이 검토되고 확장 갤러리에 추가됩니다.

### <a name="publish-extension-updates"></a>확장 업데이트 게시

업데이트를 게시하는 프로세스는 확장을 게시하는 프로세스와 비슷합니다. 버전이 package.json에서 업데이트되었는지 확인하세요.

## <a name="next-steps"></a>다음 단계

시작 방법에 대한 단계별 지침은 다음 확장 작성 자습서 중 하나를 참조하세요.

- [키맵 확장 자습서](keymap-extension.md)
- [대시보드 확장 자습서](dashboard-extension.md)
- [Notebook 확장 자습서](notebook-extension.md)
- [Jupyter Book 확장 자습서](jupyter-book-extension.md)
- [마법사 확장 자습서](wizard-extension.md)
