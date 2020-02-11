---
title: 사용자 및 작업 영역 설정
titleSuffix: Azure Data Studio
description: 사용자 및 작업 영역 설정을 수정하여 Azure Data Studio를 사용자 지정하는 방법입니다.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a874aaf9ec136ff9ea27cbeaa92011a07f3718c7
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67959278"
---
# <a name="modify-user-and-workspace-settings"></a>사용자 및 작업 영역 설정 수정

설정을 통해 원하는 대로 쉽게 [!INCLUDE[name-sos](../includes/name-sos-short.md)]를 구성할 수 있습니다. [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 거의 모든 편집기, 사용자 인터페이스 및 기능 동작 부분에 수정할 수 있는 옵션이 있습니다.

[!INCLUDE[name-sos](../includes/name-sos-short.md)]에서는 다음과 같은 두 가지 설정 범위를 제공합니다.

* **사용자** 이러한 설정은 사용자가 여는 모든 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 인스턴스에 전역적으로 적용됩니다.
* **작업 영역** 작업 영역 설정은 컴퓨터의 폴더와 관련된 설정이며, 탐색기 사이드바에 폴더가 열려 있는 경우에만 사용할 수 있습니다. 이 범위에서 정의한 설정은 사용자 범위를 재정의합니다.

## <a name="creating-user-and-workspace-settings"></a>사용자 및 작업 영역 설정 만들기

메뉴 명령 **파일** > **기본 설정** > **설정**(Mac의 **코드** > **기본 설정** > **설정**)에서는 사용자 및 작업 영역 설정을 구성하기 위한 진입점을 제공합니다. 기본 설정 목록이 제공됩니다. 변경하려는 설정을 적절한 `settings.json` 파일로 복사합니다. 오른쪽의 탭에서는 사용자 및 작업 영역 설정 파일 간을 빠르게 전환할 수 있습니다.

**명령 팔레트**(**Ctrl+Shift+P**)의 사용자 및 작업 영역 설정을 **기본 설정: 사용자 설정 열기** 및 **기본 설정 열기: 작업 영역 설정 열기**를 통해 열거나 바로 가기 키(**Ctrl+,** )를 사용할 수도 있습니다.

다음 예제에서는 편집기에서 줄 번호를 사용하지 않도록 설정하고 코드 줄을 자동으로 들여쓰도록 구성합니다.

![예제 설정](media/settings/sample-settings.png)

수정한 `settings.json` 파일을 저장한 후에는 [!INCLUDE[name-sos](../includes/name-sos-short.md)]에서 설정 변경 내용이 다시 로드됩니다.

>**참고:** 작업 영역 설정은 팀 전체에서 프로젝트 관련 설정을 공유하는 데 유용합니다.

## <a name="settings-file-locations"></a>설정 파일 위치

플랫폼에 따라 사용자 설정 파일은 다음 위치에 있습니다.

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

작업 영역 설정 파일은 프로젝트의 `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` 폴더 아래에 있습니다.

## <a name="hot-exit"></a>Hot Exit

Azure Data Studio는 기본적으로 종료될 때 저장하지 않은 파일 변경 내용을 기억합니다. 이 기능은 Visual Studio Code의 Hot Exit 기능과 동일합니다.

기본적으로 Hot Exit는 해제되어 있습니다. `files.hotExit` 설정을 편집하여 Hot Exit를 사용하도록 설정합니다. 자세한 내용은 [Hot Exit(Visual Studio Code 설명서)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)를 참조하세요.


## <a name="tab-color"></a>탭 색

사용 중인 연결을 간편하게 식별하기 위해 편집기의 열린 탭 색을 연결이 속하는 서버 그룹의 색과 일치하도록 설정할 수 있습니다. 기본적으로 탭 색은 해제되어 있습니다. `sql.tabColorMode` 설정을 편집하여 탭 색을 사용하도록 설정합니다.

## <a name="additional-resources"></a>추가 리소스

[!INCLUDE[name-sos](../includes/name-sos-short.md)]는 Visual Studio Code의 사용자 및 작업 영역 설정 기능을 상속하기 때문에 설정에 대한 자세한 내용을 [Visual Studio Code 설정](https://code.visualstudio.com/docs/getstarted/settings) 문서에서 참조할 수 있습니다.
