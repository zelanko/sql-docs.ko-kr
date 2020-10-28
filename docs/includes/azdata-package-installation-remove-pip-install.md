---
author: MikeRayMSFT
ms.prod: sql
ms.topic: include
ms.date: 01/07/2020
ms.author: mikeray
ms.openlocfilehash: 0c15fb58bb076724402ab72f81e58ce46c8b7b1e
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257418"
---
### <a name="pythonpip-installation"></a>Python/Pip 설치

Linux(yum, apt 또는 zypper 사용) 또는 macOS(Homebrew 설치 패키지 관리자 사용)에 [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)]를 설치할 수 있습니다. 패키지 관리자가 출시되기 전에는 설치하려면 Python과 pip가 필요했습니다.

>[!IMPORTANT]
>계속하기 전에 시스템 전역 Python에 설치되어 있던 `azdata` 설치를 제거해야 합니다. 새 설치 프로그램 또는 네이티브 패키지는 `azdata`를 경로에 추가하지만 어떤 항목이 먼저인지는 알 수 없습니다.
시스템 전역 Python에 기존 `azdata`가 설치되어 있는 경우 제거한 다음 계속합니다.

현재 설치를 보려면 다음 명령을 실행합니다.

```bash
$ pip list --format columns
```

`azdata`가 pip으로 설치되어 있는 경우 패키지와 버전을 반환합니다. 다음은 그 예입니다.

```
 Package             Version
------------------- ----------
azdata-cli          15.0.X
azdata-cli-app      15.0.X
azdata-cli-cluster  15.0.X
azdata-cli-core     15.0.X
azdata-cli-hdfs     15.0.X
azdata-cli-notebook 15.0.X
azdata-cli-profile  15.0.X
azdata-cli-spark    15.0.X
azdata-cli-sql      15.0.X
```

다음 예에서는 `azdata`의 pip 설치를 제거합니다.

```bash
$ pip freeze | grep azdata-* | xargs pip uninstall -y
```

pip로 설치한 `azdata` 설치가 제거된 것을 확인한 후 설치를 계속합니다.