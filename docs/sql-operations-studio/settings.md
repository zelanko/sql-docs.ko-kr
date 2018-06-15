---
title: SQL 작업 Studio (미리 보기) 사용자와 작업 영역 설정 | Microsoft Docs
description: SQL 작업 Studio (미리 보기) 사용자 및 작업 영역 설정을 수정 하는 방법.
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 67f60d30693eeb60030f3a977ec1bcf5a1f98be1
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235140"
---
# <a name="user-and-workspace-settings"></a>사용자 및 작업 영역 설정

쉽게 구성할 수 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 설정을 통해 원하는 대로 합니다. 거의 모든 부분의 [!INCLUDE[name-sos](../includes/name-sos-short.md)]의 편집기, 사용자 인터페이스 및 기능 동작에는 옵션이 수정할 수 있습니다.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] 설정에 대 한 두 개의 서로 다른 범위를 제공합니다.

* **사용자** 이러한 설정은 전체적으로 적용 되므로 인스턴스로 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 열입니다.
* **작업 영역** 작업 영역 설정은 특정 컴퓨터의 폴더로 설정 되며는 사용할 수 있는 경우에 해당 폴더는 탐색기 사이드바에서 열려 있습니다. 이 범위에 정의 된 설정은 사용자 범위를 재정의 합니다.

## <a name="creating-user-and-workspace-settings"></a>작업 영역 설정 및 사용자 만들기

메뉴 명령 **파일** > **기본 설정** > **설정** (**코드**  >  **기본 설정** > **설정을** Mac에서) 사용자 및 작업 영역 설정을 구성 하는 진입점을 제공 합니다. 기본 설정의 목록이 제공 됩니다. 적절 한 변경 하려는 모든 설정을 복사 `settings.json` 파일입니다. 오른쪽에 있는 탭을 통해 사용자 및 작업 영역 설정 파일 사이 빠르게 전환할 수 있습니다.

사용자와 작업 영역 설정을 열 수 있습니다는 **명령 팔레트** (**Ctrl + Shift + P**)와 **기본 설정: 사용자 설정을 열고** 및  **기본 설정: 작업 영역 설정 열기** 하거나 바로 가기 키를 사용 하 여 (**Ctrl +**).

다음 예에서는 편집기에서 줄 번호를 사용 하지 않도록 설정 하 고 줄의 코드를 자동으로 들여쓰기를 구성 합니다.

![설정 예](media/settings/sample-settings.png)

설정 변경 하 여 다시 로드 됩니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 수정 된 후 `settings.json` 파일이 저장 됩니다.

>**참고:** 작업 영역 설정 하는 팀에서 공유 프로젝트 관련 설정 하는 데 유용 합니다.

## <a name="settings-file-locations"></a>설정 파일 위치

플랫폼에 따라 사용자 설정 파일은 여기:

* **Windows** `%APPDATA%\sqlops\User\settings.json`
* **Mac** `$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux** `$HOME/.config/sqlops/User/settings.json`

아래에 있는 작업 영역 설정 파일의 `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` 프로젝트의 폴더에에서 있습니다.

## <a name="hot-exit"></a>핫 종료

기본적으로 종료할 때 SQL 작업 Studio 파일에 저장 되지 않은 변경을 기억 합니다. 이 Visual Studio Code에서 핫 종료 기능와 동일 합니다.

핫 종료는 기본적으로 해제 되어 있습니다. 실행 부하 과다 사용을 편집 하 여 종료는 `files.hotExit` 설정 합니다. 자세한 내용은 참조 [(Visual Studio Code 설명서)에서 핫 종료](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit)합니다.


## <a name="tab-color"></a>탭 색

를 간소화 하기 위해 사용 하는 연결을 식별 합니다. 편집기에 열려 있는 탭에 속한 연결 된 서버 그룹의 색과 일치 하도록 설정 하 고 색을 가질 수 있습니다. 기본적으로 탭 색은 기본적으로 해제 되어 있습니다. 편집 하 여 탭 색을 사용 하도록 설정 된 `sql.tabColorMode` 설정 합니다.

## <a name="additional-resources"></a>추가 리소스

때문에 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 설정에 대 한 자세한 내용은 Visual Studio Code에서 기능을 사용자와 작업 영역 설정을 상속는 [Visual Studio 코드에 대 한 설정을](https://code.visualstudio.com/docs/getstarted/settings) 문서.
