---
title: 확장 추가
description: Microsoft 및 타사에서 제공하는 확장을 선택하고 설치하여 Azure Data Studio에 기능을 추가하는 방법을 알아봅니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: ''
ms.date: 10/03/2019
ms.openlocfilehash: 2e2e76c436c02f2cbc5878228f1be2d57248816c
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123455"
---
# <a name="extend-the-functionality-of-azure-data-studio"></a>Azure Data Studio의 기능 확장

Azure Data Studio의 확장을 사용하면 기본 Azure Data Studio 설치에 다른 기능을 쉽게 추가할 수 있습니다.

확장은 Azure Data Studio 팀(Microsoft) 및 타사 커뮤니티(사용자)가 제공합니다. 확장을 만드는 방법에 대한 자세한 내용은 [확장 작성](./extension-authoring.md)을 참조하세요.

## <a name="add-azure-data-studio-extensions"></a>Azure Data Studio 확장 추가

1. 확장 아이콘을 선택하거나 **보기** 메뉴에서 **확장**을 선택하여 사용 가능한 확장에 액세스합니다. **보기: 확장 표시** 명령을 사용할 수 있습니다. 이 명령은 **명령 팔레트**(F1 또는 `Ctrl+Shift+P`)에 있습니다.

    ![확장 관리자 아이콘](media/add-extensions/extension-manager-icon.png)

    `Ctrl+Shift+X`(Windows/Linux) 또는 `Command+Shift+X`(Mac)를 눌러 확장 관리자에 신속하게 액세스할 수도 있습니다.

2. 세부 정보를 보려면 사용 가능한 확장을 선택합니다.

    ![확장 세부 정보](media/add-extensions/extension-details.png)

3. 원하는 확장을 선택하고 **설치**합니다.

4. 설치가 완료되면 확장을 **다시 로드하여** Azure Data Studio에서 사용하도록 설정합니다(확장을 처음 설치하는 경우에만 필요).

Azure Data Studio에서 확장 관리자에 액세스하는 데 문제가 있는 경우 [GitHub Wiki](https://github.com/microsoft/azuredatastudio/wiki/List-of-Extensions)에서 필요한 확장을 다운로드할 수 있습니다.

## <a name="manage-extensions"></a>확장 관리

### <a name="list-installed-extensions"></a>설치된 확장 나열

기본 확장 보기는 현재 사용하도록 설정된 확장, 사용자에게 권장되는 모든 확장 및 현재 사용하지 않도록 설정된 모든 확장의 축소된 컨테이너를 표시합니다. **확장: 설치된 확장 표시** 명령(**명령 팔레트** 또는 **추가 작업** `(...)` 드롭다운 메뉴에서 제공)은 사용하지 않도록 설정된 확장을 포함하는 모든 설치된 확장 목록을 표시합니다.

### <a name="uninstall-an-extension"></a>확장 제거

확장을 제거하려면 확장 항목 오른쪽에 있는 기어 아이콘을 클릭하고 드롭다운 메뉴에서 **제거**를 선택합니다. 이렇게 하면 선택한 확장이 제거되고 Azure Data Studio를 다시 로드하라는 메시지가 표시됩니다.

 ![확장 드롭다운](media/add-extensions/extension-gear-dropdown.png)

### <a name="disable-an-extension"></a>확장을 사용하지 않도록 설정

확장을 영구적으로 제거하는 대신 일시적으로 사용하지 않도록 설정할 수 있습니다. 모든 Azure Data Studio 세션에서 확장을 사용하지 않도록 설정하거나(**사용 안 함**) 현재 작업 영역에 대해서만 사용하지 않도록 설정할 수 있습니다(**사용 안 함(작업 영역)** ). **명령 팔레트**를 통해서 현재 설치된 모든 확장을 사용하지 않도록 설정할 수도 있습니다. 이렇게 하려면 **확장: 모든 확장 사용 안 함** 및 **확장: 모든 확장 사용 안 함(작업 영역)** 을 사용하면 됩니다.

### <a name="enable-an-extension"></a>확장 사용

사용하지 않도록 설정된 확장은 확장 목록의 **사용 안 함** 섹션으로 이동되며 ***사용 안 함***으로 표시됩니다. 해당 확장은 드롭다운 메뉴의 **사용** 또는 **사용(작업 영역)** 명령을 사용하여 다시 사용하도록 설정할 수 있습니다. **명령 팔레트**에서 **확장: 모든 확장 사용** 및 **확장: 모든 확장 사용(작업 영역)** 명령을 사용하여 모든 확장을 사용하도록 설정할 수도 있습니다.

![확장을 사용하도록 설정](media/add-extensions/extensions-enable.png)

### <a name="updating-an-extension"></a>확장 업데이트

Azure Data Studio는 설치된 확장에 대한 업데이트를 자동으로 확인하고 설치합니다. 자동 업데이트 기능을 해제하려는 경우 **확장: 확장 자동 업데이트 사용 안 함** 명령을 사용하여 자동 업데이트를 사용하지 않도록 설정할 수 있습니다.

확장을 수동으로 업데이트하려면 **확장: 만료된 확장 표시** 명령을 사용하여 확장 업데이트를 확인할 수 있습니다. 이 명령은 `@outdated` 필터를 사용하여 확장 목록을 검색하고 현재 설치된 모든 확장에 대해 사용할 수 있는 업데이트를 표시합니다. 만료된 확장에서 **업데이트** 단추를 클릭하면 업데이트가 설치됩니다. 그런 다음 Azure Data Studio를 다시 로드하라는 메시지가 표시됩니다. **확장: 모든 확장 업데이트** 명령을 사용하여 모든 만료된 확장을 동시에 업데이트할 수도 있습니다.

**확장: 확장 업데이트 확인** 명령은 사용 가능한 업데이트가 있는 확장을 확인하는 또 다른 방법입니다.

## <a name="install-from-a-vsix"></a>VSIX에서 설치

확장 보기 명령 드롭다운의 **VSIX에서 설치** 명령을 사용하여 `.vsix` 파일로 패키징된 Azure Data Studio 확장을 수동으로 설치할 수 있습니다. 또는 명령 팔레트에서 **확장: VSIX에서 설치 명령**을 사용하여 확장의 `.vsix` 파일을 가리켜서 확장을 수동으로 설치할 수 있습니다.

## <a name="access-installed-azure-data-studio-extensions"></a>설치된 Azure Data Studio 확장에 액세스

각 확장은 다른 방식으로 Azure Data Studio의 작업 환경을 향상시킵니다. 따라서 확장의 진입점은 다를 수 있습니다. 설치한 후 확장의 기능에 액세스하는 방법에 대한 내용은 설치된 확장의 개별 설명서를 참조하세요.

## <a name="extensions-view-filters"></a>Extensions 보기 필터

확장 보기 검색 상자는 확장을 찾고 관리하는 데 도움이 되도록 필터를 지원합니다. **설치된 확장 표시** 명령과 **권장되는 확장 표시** 명령은 검색 상자에서 `@installed` 및 `@recommended`와 같은 필터를 사용합니다.

확장 검색 상자에 @를 입력하고 권장 사항을 살펴보며 모든 필터의 전체 목록을 보고 명령을 정렬할 수 있습니다.

![확장 정렬](media/add-extensions/extension-sort.png)

확장 보기 필터는 다음과 같습니다.

- `@builtin` - Azure Data Studio와 함께 제공되는 확장을 표시합니다. 유형을 기준으로 그룹화됩니다(프로그래밍 언어, 테마 등).
- `@disabled` - 사용하지 않도록 설정된 설치된 확장을 표시합니다.
- `@enabled` - 사용하도록 설정된 설치된 확장을 표시합니다. 확장은 개별적으로 사용하거나 사용하지 않도록 설정할 수 있습니다.
- `@installed` - 설치된 확장을 표시합니다.
- `@outdated` - 만료된 설치된 확장을 표시합니다. Marketplace에서 최신 버전을 사용할 수 있습니다.
- `@recommended` - 권장되는 확장을 표시합니다. 작업 영역용 또는 범용으로 그룹화됩니다.
- `@category` - 지정된 범주에 속하는 확장을 표시합니다. 다음은 몇 가지 지원되는 범주입니다. 전체 목록을 보려면 @category를 입력하고 제안 목록에서 옵션을 따릅니다.
    - `@category:themes`
    - `@category:formatters`
    - `@category:snippets` 이러한 필터도 결합하여 사용할 수 있습니다. 예를 들어 `@installed @category:themes`는 설치된 모든 테마를 표시합니다.

필터를 제공하지 않으면 확장 보기에 현재 설치된 확장과 권장되는 확장이 표시됩니다.

### <a name="sorting"></a>정렬

`@sort` 필터를 사용하여 확장을 정렬할 수 있습니다. 이 필터는 다음 값을 가질 수 있습니다.

- `installs` - 확장 갤러리 설치 수를 기준으로 내림차순으로 정렬합니다.
- `rating` - 확장 갤러리 등급(별 1~5개)을 기준으로 내림차순으로 정렬합니다.
- `name` - 확장 이름을 기준으로 사전순으로 정렬합니다.

## <a name="common-questions"></a>일반적인 질문

### <a name="where-are-extensions-installed"></a>확장은 어디에 설치되나요?

확장은 사용자별 확장 폴더에 설치됩니다. 플랫폼에 따라 위치는 다음 폴더가 됩니다.

- Windows `%USERPROFILE%\.azuredatastudio\extensions`
- macOS `~/.azuredatastudio/extensions`
- Linux `~/.azuredatastudio/extensions`
