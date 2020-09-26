---
title: 통합 터미널
description: Azure Data Studio에 통합된 터미널을 여는 방법을 알아봅니다. 통합 터미널은 별도의 터미널보다 편리할 수 있습니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 09876b320e4761e6d73756d9cf7db5fc6c66a0b6
ms.sourcegitcommit: 63aef5a96905f0b026322abc9ccb862ee497eebe
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2020
ms.locfileid: "91364000"
---
# <a name="integrated-terminal"></a>통합 터미널

Azure Data Studio에서는 처음에는 작업 영역의 루트에서 시작하여 통합 터미널을 열 수 있습니다. 이 기능을 사용하면 빠른 명령줄 작업을 수행하기 위해 창을 전환하거나 기존 터미널의 상태를 변경할 필요가 없기 때문에 편리할 수 있습니다.

터미널을 열려면 다음을 수행합니다.

* **Ctrl+`** (억음 문자) 바로 가기 키를 사용합니다.
* **보기** | **통합 터미널** 메뉴 명령을 사용합니다.
* **명령 팔레트**(**Ctrl+Shift+P**)에서 **보기:통합 터미널 토글** 명령을 사용합니다.

![터미널](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Azure Data Studio 외부에서 작업하려는 경우 탐색기 **명령 프롬프트에서 열기** 명령(Mac 또는 Linux에서는 **터미널에서 열기**)을 사용하여 여전히 외부 셸을 열 수 있습니다.

## <a name="managing-multiple-terminals"></a>여러 터미널 관리

각기 다른 위치에 열려 있는 여러 터미널을 만들어 위치 간에 쉽게 탐색할 수 있습니다. **터미널** 패널의 오른쪽 위에 있는 더하기 아이콘을 누르거나 **Ctrl+Shift+'** 명령을 트리거하면 터미널 인스턴스를 추가할 수 있습니다. 그러면 항목 간 전환에 사용할 수 있는 또 다른 항목이 드롭다운 목록에 만들어집니다.

![여러 터미널](media/integrated-terminal/terminal-multiple-instances.png)

휴지통 단추를 눌러 터미널 인스턴스를 제거합니다.

> [!TIP]
> 여러 터미널을 광범위하게 사용하는 경우 [키 바인딩 섹션](#key-bindings)에 설명된 `focusNext`, `focusPrevious` 및 `kill` 명령의 키 바인딩을 추가하면 키보드만 사용하여 터미널 간에 탐색할 수 있습니다.

## <a name="configuration"></a>구성

기본적으로 사용되는 셸은 Linux 및 macOS의 경우 `$SHELL`, Windows 10의 경우 PowerShell, 이전 Windows 버전의 경우 cmd.exe입니다. [설정](settings.md)에서 `terminal.integrated.shell.*`을 설정하면 이 기본값을 수동으로 재정의할 수 있습니다. `terminal.integrated.shellArgs.*` 설정을 사용하여 Linux 및 macOS의 터미널 셸에 인수를 전달할 수 있습니다.

### <a name="windows"></a>Windows

Windows에서 셸을 올바르게 구성하려면 올바른 실행 파일을 찾아 설정을 업데이트하는 것이 중요합니다. 다음은 일반적인 셸 실행 파일 목록 및 기본 위치입니다.

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
> 통합 터미널로 사용하려면 `stdin/stdout/stderr`을 리디렉션할 수 있도록 셸 실행 파일이 콘솔 애플리케이션이어야 합니다.

> [!TIP]
> 통합 터미널 셸은 Azure Data Studio의 사용 권한으로 실행되고 있습니다. 관리자 권한이나 다른 사용 권한으로 셸 명령을 실행해야 하는 경우 터미널 내에서 `runas.exe` 등의 플랫폼 유틸리티를 사용할 수 있습니다.

### <a name="shell-arguments"></a>셸 인수

셸을 시작할 때 셸에 인수를 전달할 수 있습니다.

예를 들어 `.bash_profile`을 실행하는 로그인 셸로 bash를 실행하려면 `-l` 인수(큰따옴표 포함)를 전달합니다.

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>터미널 표시 설정

다음 설정을 사용하여 통합 터미널 글꼴 및 줄 높이를 사용자 지정할 수 있습니다.

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a name="terminal-key-bindings"></a><a id="key-bindings"></a>터미널 키 바인딩

**보기: 통합 터미널 토글** 명령은 통합 터미널 패널을 빠르게 표시하고 숨기기 위해 **Ctrl+`** 에 바인딩되어 있습니다.

다음은 통합 터미널 내에서 빠르게 탐색하기 위한 바로 가기 키입니다.

|키|명령|  
|---|---|  
|**Ctrl+\`**|통합 터미널 표시|  
|**Ctrl+Shift+\`**|새 터미널 만들기|  
|**Ctrl+위쪽**|위로 스크롤|  
|**Ctrl+아래쪽**|아래로 스크롤|  
|**Ctrl+PageUp**|페이지 위로 스크롤|  
|**Ctrl+PageDown**|페이지 아래로 스크롤|  
|**Ctrl+Home**|맨 위로 스크롤|  
|**Ctrl+End**|맨 아래로 스크롤|  
|**Ctrl+K**|터미널 지우기|  

다른 터미널 명령도 사용할 수 있으며, 원하는 바로 가기 키에 바인딩할 수 있습니다.

아래에 이 계정과 키의 예제가 나와 있습니다.

* `workbench.action.terminal.focus`: 터미널에 포커스를 설정합니다. 토글과 유사하지만, 터미널이 표시되는 경우 숨기는 대신 터미널에 포커스를 설정합니다.
* `workbench.action.terminal.focusNext`: 다음 터미널 인스턴스에 포커스를 설정합니다.
* `workbench.action.terminal.focusPrevious`: 이전 터미널 인스턴스에 포커스를 설정합니다.
* `workbench.action.terminal.kill`: 현재 터미널 인스턴스를 제거합니다.
* `workbench.action.terminal.runSelectedText`: 터미널 인스턴스에서 선택한 텍스트를 실행합니다.
* `workbench.action.terminal.runActiveFile`: 터미널 인스턴스에서 활성 파일을 실행합니다.

### <a name="run-selected-text"></a>선택한 텍스트 실행

`runSelectedText` 명령을 사용하려면 편집기에서 텍스트를 선택한 다음, **명령 팔레트**(**Ctrl+Shift+P**)를 통해 **터미널:활성 터미널에서 선택한 텍스트 실행** 명령을 실행합니다. 터미널에서 선택한 텍스트를 실행하려고 합니다.

![선택한 텍스트 실행](media/integrated-terminal/terminal_run_selected.png)

활성 편집기에서 텍스트를 선택하지 않은 경우에는 현재 커서가 있는 줄이 터미널에서 실행됩니다.

### <a name="copy--paste"></a>복사 및 붙여넣기

복사 및 붙여넣기의 키 바인딩은 플랫폼 표준을 따릅니다.

* Linux: **Ctrl+Shift+C** 및 **Ctrl+Shift+V**
* Mac: **Cmd+C** 및 **Cmd+V**
* Windows: **Ctrl+C** 및 **Ctrl+V**

### <a name="find"></a>찾기

통합 터미널에는 **Ctrl+F**를 사용하여 트리거할 수 있는 기본 찾기 기능이 있습니다.

Linux 및 Windows에서 **Ctrl+F**를 통해 찾기 위젯을 시작하는 대신 셸로 이동하려면 다음과 같이 키 바인딩을 제거해야 합니다.

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>터미널 세션 이름 바꾸기

이제 **터미널: 이름 바꾸기**(`workbench.action.terminal.rename`) 명령을 사용하여 통합 터미널 세션의 이름을 바꿀 수 있습니다. 새 이름이 터미널 선택 드롭다운에 표시됩니다.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>터미널에서 키 바인딩 강제 적용

통합 터미널에 포커스가 설정된 경우 키 입력이 터미널 자체에 전달되고 사용되기 때문에 작동하지 않는 키 바인딩이 많습니다. 이 문제를 해결하기 위해 `terminal.integrated.commandsToSkipShell` 설정을 사용할 수 있습니다. 이 설정은 키 바인딩이 셸에서 처리되지 않고 대신 Azure Data Studio 키 바인딩 시스템에서 처리되는 명령 이름 배열을 포함합니다. 기본적으로, 자주 사용하는 일부 키 바인딩뿐만 아니라 모든 터미널 키 바인딩이 포함됩니다.

