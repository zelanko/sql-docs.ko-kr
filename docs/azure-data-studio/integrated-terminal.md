---
title: 통합된 터미널
titleSuffix: Azure Data Studio
description: Azure Data Studio에서 통합된 터미널에 알아봅니다.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: d29234810e30efd204f498e2f7c63ba6571cbfe7
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797543"
---
# <a name="integrated-terminal"></a>통합된 터미널

[!INCLUDE[name-sos](../includes/name-sos-short.md)], 작업 영역의 루트에서 시작 하는 처음에 통합된 터미널에서 열 수 있습니다. Windows를 전환 하거나 빠른 명령줄 작업을 수행 하는 기존 터미널의 상태를 변경할 필요가 대로 편리할 수 있습니다.

터미널을 열려면:

* 사용 된 **Ctrl +'** 억음 악센트 문자를 사용 하 여 바로 가기 키입니다.
* 사용 된 **뷰** | **통합 터미널** 메뉴 명령입니다.
* **명령 팔레트** (**Ctrl + Shift + P**)를 사용 합니다 **보기: 토글 통합 터미널** 명령 합니다.

![터미널](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> 탐색기를 사용 하 여 외부 셸을 열 수 있습니다 **명령 프롬프트에서 열기** 명령 (**터미널에서 열기** Mac 또는 Linux) 외부에서 작동 하려는 경우 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다.

## <a name="managing-multiple-terminals"></a>여러 터미널 관리

여러 터미널 열기를 다른 위치를 만들 하 고 사이 쉽게 탐색할 수 있습니다. 오른쪽 상단에 있는 더하기 아이콘을 눌러 터미널 인스턴스를 추가할 수 있습니다 합니다 **터미널** 패널에서 트리거 또는 합니다 **Ctrl + Shift +'** 명령입니다. 이 전환에 사용할 수 있는 드롭다운 목록에서 다른 항목을 만듭니다.

![여러 터미널](media/integrated-terminal/terminal-multiple-instances.png)

휴지통을 눌러 터미널 인스턴스를 제거 단추 수 있습니다.

> [!TIP]
> 여러 터미널을 광범위 하 게 사용 하는 경우에 대 한 키 바인딩을 추가할 수 있습니다는 `focusNext`, `focusPrevious` 및 `kill` 에 설명 된 명령을 합니다 [키 바인딩 섹션](#key-bindings) 키보드만 사용 하 여 간의 탐색을 허용 하도록 합니다.

## <a name="configuration"></a>Configuration

기본값을 사용 하는 셸에서 `$SHELL` Linux 및 macOS, Windows 10에서 PowerShell 및 cmd.exe 이전 버전의 Windows에서. 설정 하 여 수동으로 재정의할 수 이러한 `terminal.integrated.shell.*` 에 [설정을](settings.md)합니다. Linux 및 macOS를 사용 하 여 터미널 셸에 인수를 전달할 수 있습니다는 `terminal.integrated.shellArgs.*` 설정 합니다.

### <a name="windows"></a>Windows

올바른 실행 파일 및 설정을 업데이트는 Windows에서 셸을 올바르게 구성입니다. 일반적인 셸 실행 파일 목록과 해당 기본 위치는 다음과 같습니다.

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
> 통합된 된 터미널으로 사용할 셸 실행 파일에는 콘솔 응용 프로그램을 이어야 합니다 하 `stdin/stdout/stderr` 리디렉션될 수 있습니다.

> [!TIP]
> 통합된 터미널 셸을의 권한으로 실행 중인 [!INCLUDE[name-sos](../includes/name-sos-short.md)]합니다. 상승 된 권한 (관리자) 또는 다른 권한으로 셸 명령을 실행 해야 할 경우 사용할 수 플랫폼 유틸리티와 같은 `runas.exe` 터미널 내에서.

### <a name="shell-arguments"></a>셸 인수

이 시작 되 면 셸에 인수를 전달할 수 있습니다.

예를 들어 로그인 셸으로 실행 중인 bash를 사용 하도록 설정 하려면 (실행 되는 `.bash_profile`)를 전달 합니다 `-l` (큰따옴표)로 인수:

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>터미널 표시 설정

다음 설정을 사용 하 여 줄 높이 통합 된 터미널 글꼴을 사용자 지정할 수 있습니다.

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>터미널 키 바인딩

**보기: 통합 터미널을 설정/해제** 명령에 바인딩된 **Ctrl +'** 신속 하 게 보기 내부 및 외부 통합된 터미널 패널을 전환 하려면.

통합된 터미널 내에서 빠르게 탐색할 키보드 바로 가기는 다음과 같습니다.

|Key|Command|  
|---|---|  
|**Ctrl+\`**|통합된 터미널을 표시|  
|**Ctrl+Shift+\`**|새 터미널 만들기|  
|**Ctrl+Up**|위로 스크롤|  
|**Ctrl+Down**|아래로 스크롤하여|  
|**Ctrl+PageUp**|위로 페이지 스크롤|  
|**Ctrl+PageDown**|아래로 페이지 스크롤|  
|**Ctrl+Home**|맨 위로 스크롤|  
|**Ctrl+End**|맨 아래로 스크롤|  
|**Ctrl+K**|터미널을 선택 취소|  

다른 터미널 명령을 제공 되며 기본 바로 가기에 바인딩할 수 있습니다.

구현되지 않은 것은 다음과 같습니다.

* `workbench.action.terminal.focus`: 터미널을 집중 합니다. 설정/해제와 같은 이지만 표시 된 경우 숨기 거 나, 대신 터미널 중점을 둡니다.
* `workbench.action.terminal.focusNext`: 다음 터미널 인스턴스 중점을 둡니다.
* `workbench.action.terminal.focusPrevious`: 이전 터미널 인스턴스 중점을 둡니다.
* `workbench.action.terminal.kill`: 현재 터미널 인스턴스를 제거 합니다.
* `workbench.action.terminal.runSelectedText`: 터미널 인스턴스에서 선택한 텍스트를 실행 합니다.
* `workbench.action.terminal.runActiveFile`: 터미널 인스턴스에서 활성 파일을 실행 합니다.

### <a name="run-selected-text"></a>선택한 텍스트를 실행 합니다.

사용 하는 `runSelectedText` 명령, 편집기에서 텍스트를 선택 하 고 명령을 실행 **터미널. 활성 터미널에서 선택한 텍스트 실행** 를 통해 합니다 **명령 팔레트** (**Ctrl + Shift + P**). 터미널에서 선택한 텍스트를 실행 하려고 합니다.

![선택한 텍스트를 실행 합니다.](media/integrated-terminal/terminal_run_selected.png)

활성 편집기에서 선택 된 텍스트가 줄에 커서가 있는 여는 터미널에서 실행 됩니다.

### <a name="copy--paste"></a>복사 및 붙여넣기

플랫폼 표준을 따라야 하는 복사 및 붙여넣기에 대 한 키 바인딩:

* Linux: **Ctrl + Shift + C** 고 **Ctrl + Shift + V**
* Mac: **Cmd + C** 고 **Cmd + V**
* Windows: **Ctrl + C** 고 **Ctrl + V**

### <a name="find"></a>찾기

통합 터미널에으로 트리거될 수 있는 기본 찾기 기능이 있습니다 **Ctrl + F**합니다.

원하는 경우 **Ctrl + F** 찾기 위젯 Linux 및 Windows에서 실행 하는 대신 셸에 이동할 제거 해야 하는 키 바인딩을 다음과 같이 합니다.

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>터미널 세션 이름 바꾸기

통합된 터미널 세션 이제 이름을 바꿀 수 있습니다 사용 하 여 **터미널. 이름 바꾸기** (`workbench.action.terminal.rename`) 명령입니다. 새 이름이 터미널 선택 드롭다운 목록에에서 표시 됩니다.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>키 바인딩 터미널을 통과 하도록 강제 적용

통합 터미널에서에 포커스가 있을 때 키 입력에 전달 되어 자체 터미널에서 사용 되므로 많은 키 바인딩이 작동 하지 않습니다. `terminal.integrated.commandsToSkipShell` 설정 문제를 해결할 가져오는 데 사용할 수 있습니다. 해당 키 바인딩 셸에서 처리를 건너뛰고 대신에서 처리할 수 있는 명령 이름의 배열을 포함 합니다 [!INCLUDE[name-sos](../includes/name-sos-short.md)] 바인딩 시스템 키입니다. 기본적으로 여기에 선택 몇 가지 자주 사용 되는 키 바인딩 외에도 모든 터미널 키 바인딩.

