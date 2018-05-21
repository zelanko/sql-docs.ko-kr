---
title: SQL 작업 Studio (미리 보기)에서 통합된 터미널 | Microsoft Docs
description: SQL 작업 Studio (미리 보기)에서 통합된 터미널에 알아봅니다.
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
ms.openlocfilehash: 0754c66c182acefd2fdff799b791fbf135356d7b
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="integrated-terminal"></a>통합된 터미널

[!INCLUDE[name-sos](../includes/name-sos-short.md)], 작업 영역 루트에서 시작 하는 처음 통합된 터미널을 열 수 있습니다. Windows를 전환 하거나 빠른 명령줄 작업을 수행 하는 기존 터미널의 상태를 변경할 필요가 없습니다 편리 하 게이 될 수 있습니다.

열려면 터미널 합니다.

* 사용 하 여는 **Ctrl +'** 억음 악센트 문자 바로 가기 키입니다.
* 사용 하 여는 **보기** | **통합 터미널** 메뉴 명령입니다.
* **명령 팔레트** (**Ctrl + Shift + P**)를 사용 하 여는 **보기: 토글 통합 터미널** 명령입니다.

![터미널](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 탐색기와 외부 셸을 열 수 있습니다 **명령 프롬프트에서 열고** 명령 (**터미널에서 열** Mac 또는 Linux) 외부에서 실행 되도록 선호 하는 경우 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다.

## <a name="managing-multiple-terminals"></a>여러 터미널 관리

여러 터미널에 다른 위치를 만들 수 있으며 서로 쉽게 탐색할 수 있습니다. 더하기 아이콘의 오른쪽 위에을 클릭 하 여 터미널 인스턴스를 추가할 수 있습니다는 **터미널** 패널 또는으로 트리거하는 **Ctrl + Shift +'** 명령입니다. 이 둘 사이 전환 하는 데 사용할 수 있는 드롭다운 목록에서 다른 항목을 만듭니다.

![여러 터미널](media/integrated-terminal/terminal-multiple-instances.png)

휴지통 단추 수를 눌러 터미널 인스턴스를 제거 합니다.

> [!TIP]
> 여러 단말을 광범위 하 게 사용 하는 경우에 대 한 키 바인딩을 추가할 수 있습니다는 `focusNext`, `focusPrevious` 및 `kill` 명령에 나와 있는 [키 바인딩 섹션](#key-bindings) 키보드만 사용 하 여 간의 탐색을 허용 하도록 합니다.

## <a name="configuration"></a>Configuration

기본값을 사용 하는 셸 `$SHELL` Linux 및 Windows 10에서 PowerShell 및 cmd.exe 이전 버전의 Windows에서 macOS 등. 설정 하 여 수동으로 재정의할 수 이러한 `terminal.integrated.shell.*` 에 [설정을](settings.md)합니다. Linux 및 macOS 사용에 터미널 셸에 인수를 전달할 수는 `terminal.integrated.shellArgs.*` 설정 합니다.

### <a name="windows"></a>Windows

Windows에서 셸에서 올바르게 구성 합니다. 올바른 실행 파일을 찾아 설정을 업데이트 하는 것입니다. 다음은 일반적인 셸 실행 파일 및 해당 기본 위치 목록입니다.

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> 통합된 터미널으로 사용할 셸 실행 파일에는 콘솔 응용 프로그램 이어야 합니다 있도록 `stdin/stdout/stderr` 리디렉션할 수 있습니다.

> [!TIP]
> 터미널 integrated shell의 권한으로 실행 되 고 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다. 와 같은 플랫폼 유틸리티를 관리자 권한 (관리자) 또는 다른 사용 권한이 있는 셸 명령을 실행 해야 할 경우 사용할 수 있습니다 `runas.exe` 터미널 내에서.

### <a name="shell-arguments"></a>셸 인수

시작 시 셸에 인수를 전달할 수 있습니다.

예를 들어, 로그인 셸으로 실행 중인 bash를 사용 하도록 설정 하려면 (실행할 `.bash_profile`), 전달는 `-l` (큰따옴표)로 인수:

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>터미널 디스플레이 설정

다음 설정을 갖는 선 높이 통합 된 터미널 글꼴을 사용자 지정할 수 있습니다.

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>터미널 키 바인딩

**보기: 토글 통합 터미널** 명령에 바인딩된 **Ctrl +'** 신속 하 게 보기 내부 및 외부 통합된 터미널 패널을 전환 합니다.

다음은 신속 하 게 통합된 터미널 안에서 이동 하려면 바로 가기 키:

Key|Command
---|---
**Ctrl +'**|통합된 터미널 표시
**Ctrl + Shift +'**|새 터미널 만들기
**Ctrl + 위쪽**|위로 스크롤
**Ctrl + 아래쪽**|아래로 스크롤하여
**Ctrl + PageUp**|페이지 위로 스크롤
**Ctrl + PageDown**|페이지 아래로 스크롤
**Ctrl + Home**|맨 위로 스크롤
**Ctrl + End**|아래쪽으로 스크롤하여
**Ctrl + K**|터미널의 선택을 취소합니다

다른 터미널 명령을 사용할 수 있으며 사용자 기본 바로 가기 키에 바인딩할 수 있습니다.

반환할 수 있습니다.

* `workbench.action.terminal.focus`: 터미널을 집중 합니다. 이 설정/해제와 같은 아니지만 표시 되는 경우 터미널 숨기 거 나, 대신 중점을 둡니다.
* `workbench.action.terminal.focusNext`: 다음 터미널 인스턴스 중점을 둡니다.
* `workbench.action.terminal.focusPrevious`: 이전 터미널 인스턴스 중점을 둡니다.
* `workbench.action.terminal.kill`: 현재 터미널 인스턴스를 제거 합니다.
* `workbench.action.terminal.runSelectedText`: 터미널 인스턴스에서 선택한 텍스트를 실행 합니다.
* `workbench.action.terminal.runActiveFile`: 활성 파일 터미널 인스턴스에서 실행 합니다.

### <a name="run-selected-text"></a>선택한 텍스트를 실행 합니다.

사용 하는 `runSelectedText` 명령 텍스트를 편집기에서 선택한 명령을 실행 **터미널: 활성 터미널의 선택 된 텍스트 실행** 통해는 **명령 팔레트** (**Ctrl + Shift + P**). 터미널 선택한 텍스트를 실행 하려고 시도 합니다.

![선택한 텍스트를 실행 합니다.](media/integrated-terminal/terminal_run_selected.png)

활성 편집기에서 선택한 텍스트가 없는 경우에 커서에 있는 터미널에서 실행 됩니다.

### <a name="copy--paste"></a>복사 및 붙여넣기

복사 및 붙여넣기를 위한 keybindings 플랫폼 표준을 준수 합니다.

* Linux: **Ctrl + Shift + C** 및 **Ctrl + Shift + V**
* Mac: **Cmd + C** 및 **Cmd + V**
* Windows: **Ctrl + C** 및 **Ctrl + V**

### <a name="find"></a>찾기

통합 터미널에으로 트리거될 수 있는 기본 찾기 기능이 **Ctrl + F**합니다.

원하는 경우 **Ctrl + F** 찾기 위젯 Linux 및 Windows를 실행 하는 대신 셸 돌아가려면는 keybinding을 제거 해야 같이:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>터미널 세션 이름 바꾸기

통합된 터미널 세션 이제 이름을 바꿀 수 있습니다를 사용 하 여 **터미널: 이름 바꾸기** (`workbench.action.terminal.rename`) 명령입니다. 새 이름은 터미널 선택 드롭다운 목록에에서 표시 됩니다.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>키 바인딩 터미널을 통과 하도록을 강제 적용

통합된 터미널에 포커스가 있는 동안 키 바인딩을 키 입력에 전달 되어 터미널 자체에서 사용 되므로 작동 하지 않습니다. `terminal.integrated.commandsToSkipShell` 설정은이 가져오는 데 사용할 수 있습니다. 해당 키 바인딩 셸에서 처리를 건너뛰고 대신에서 처리할 수 있는 명령 이름의 배열을 포함는 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 바인딩 시스템 키입니다. 기본적으로 여기에 select 몇 가지 자주 사용 되는 키 바인딩 외에도 모든 터미널 키 바인딩 포함 됩니다.

