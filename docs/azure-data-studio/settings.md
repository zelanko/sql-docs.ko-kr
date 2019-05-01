---
title: 사용자 및 작업 영역 설정
titleSuffix: Azure Data Studio
description: 사용자 및 작업 영역 설정을 수정 하 여 Azure Data Studio를 사용자 지정 하는 방법입니다.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 8983e874e9f1a7a5dc875774304c87ad23fa60ea
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63312837"
---
# <a name="modify-user-and-workspace-settings"></a>사용자 및 작업 영역 설정 수정

구성 하는 것이 쉽습니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 설정을 통해 원하는 대로 합니다. 거의 모든 부분 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 편집기, 사용자 인터페이스 및 기능 동작 옵션이 수정할 수 있습니다.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 설정에 대 한 두 개의 서로 다른 범위를 제공합니다.

* **사용자** 이러한 설정을 전역적으로의 모든 인스턴스에 적용 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 열입니다.
* **작업 영역** 작업 영역 설정 설정은 관련 컴퓨터의 폴더 및 폴더 탐색기 사이드바에서 열릴 때만 사용할 합니다. 이 범위에 정의 된 설정은 사용자 범위를 재정의 합니다.

## <a name="creating-user-and-workspace-settings"></a>사용자 및 작업 영역 설정 만들기

메뉴 명령 **파일** > **기본 설정** > **설정** (**코드**  >  **기본 설정** > **설정** Mac에서) 사용자 및 작업 영역 설정을 구성 하려면 진입점을 제공 합니다. 기본 설정 목록으로 제공 됩니다. 적절 한 변경 하려는 모든 설정을 복사 `settings.json` 파일입니다. 오른쪽에 있는 탭을 통해 사용자와 작업 영역 설정 파일 간에 빠르게 전환할 수 있습니다.

사용자 및 작업 영역 설정을 열 수도 있습니다는 **명령 팔레트** (**Ctrl + Shift + P**) 사용 하 여 **기본 설정: 사용자 설정 열기** 고 **기본 설정: 작업 영역 설정을 엽니다** 바로 가기 키를 사용 하거나 (**Ctrl +,**).

다음 예제에서는 편집기에서 줄 번호를 사용 하지 않도록 설정 하 고 자동으로 들여쓰기 됩니다 코드 줄을 구성 합니다.

![예제 설정](media/settings/sample-settings.png)

설정 변경 하 여 다시 로드 됩니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 수정 된 후 `settings.json` 파일이 저장 됩니다.

>**참고:** 작업 영역 설정을 팀에서 프로젝트 관련 설정을 공유 하는 데 유용 합니다.

## <a name="settings-file-locations"></a>설정 파일 위치

플랫폼에 따라 사용자 설정 파일은 여기 있습니다.

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

작업 영역 설정 파일을 아래에 있는 `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` 프로젝트 폴더에에서 있습니다.

## <a name="hot-exit"></a>핫 종료

Azure 데이터 Studio는 기본적으로 종료할 때 파일에 저장 되지 않은 변경을 기억 합니다. Visual Studio Code에서 바로 가기 종료 기능으로 동일합니다.

핫 종료는 기본적으로 해제 되어 있습니다. 편집 하 여 실행 부하 과다 종료를 사용 하도록 설정 된 `files.hotExit` 설정 합니다. 세부 정보를 참조 하세요 [(Visual Studio Code 설명서)에서 실행 부하 과다 종료](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)합니다.


## <a name="tab-color"></a>탭 색

를 간소화 하기 위해 사용 하는 연결을 식별 편집기에서 열려 있는 탭에 속하는 연결 된 서버 그룹의 색과 일치 하도록 설정 하 고 색을 가질 수 있습니다. 기본적으로 탭 색은 기본적으로 해제 되어 있습니다. 편집 하 여 탭 색을 사용 하도록 설정 된 `sql.tabColorMode` 설정 합니다.

## <a name="additional-resources"></a>추가 리소스

때문에 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 설정에 대 한 자세한 내용은 Visual Studio Code에서 기능은 사용자 및 작업 영역 설정을 상속 합니다 [Visual Studio Code에 대 한 설정을](https://code.visualstudio.com/docs/getstarted/settings) 문서.
