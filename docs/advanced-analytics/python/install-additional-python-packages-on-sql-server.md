---
title: 새 Python 언어 패키지 설치
description: SQL Server 2017 Machine Learning Services (데이터베이스 내) 및 Machine Learning Server (독립 실행형)에 새 Python 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0e305f778ee132c06e9a2b08c8cec64f0535846a
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345519"
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server에 새 Python 패키지를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2017 Machine Learning Services의 인스턴스에 새 Python 패키지를 설치 하는 방법을 설명 합니다. 일반적으로 새 패키지를 설치 하는 프로세스는 표준 Python 환경의 경우와 유사 합니다. 그러나 서버에 인터넷 연결이 없는 경우에는 몇 가지 추가 단계가 필요 합니다.

패키지 위치 및 설치 경로에 대 한 자세한 내용은 [R 또는 Python 패키지 정보 가져오기](../package-management/installed-package-information.md)를 참조 하세요.

## <a name="prerequisites"></a>사전 요구 사항

+ Python 언어 옵션을 사용 하 여 [2017 Machine Learning Services (데이터베이스 내)를 SQL Server](../install/sql-machine-learning-services-windows-install.md) 합니다. 

+ 패키지는 Python 3.5 호환 되며 Windows에서 실행 되어야 합니다. 

+ 패키지를 설치 하려면 서버에 대 한 관리자 권한이 필요 합니다.

## <a name="considerations"></a>고려 사항

패키지를 추가 하기 전에 패키지가 SQL Server 환경에 적합 한지 여부를 고려 합니다. 일반적으로 데이터베이스 서버는 여러 작업을 수용 하는 공유 자산입니다. 서버에 너무 많은 계산 압력을 주는 패키지를 추가 하는 경우 성능이 저하 됩니다. 

또한 널리 사용 되는 일부 Python 패키지 (예: Flask)는 독립 실행형 환경에 보다 적합 한 작업 (예: 웹 개발)을 수행 합니다. 데이터베이스를 단순히 쿼리 하는 작업이 아니라 machine learning과 같은 데이터베이스 엔진과의 긴밀 한 통합을 활용 하는 태스크에는 Python 데이터베이스 내를 사용 하는 것이 좋습니다.

데이터베이스 서버는 자주 잠깁니다. 대부분의 경우 인터넷 액세스가 완전히 차단 됩니다. 긴 종속성 목록이 포함 된 패키지의 경우 이러한 종속성을 미리 식별 하 여 각 종속성을 수동으로 설치 해야 합니다.

## <a name="add-a-new-python-package"></a>새 Python 패키지 추가

이 예에서는 SQL Server 컴퓨터에 새 패키지를 직접 설치 하려고 한다고 가정 합니다.

패키지 설치는 인스턴스당입니다. Machine Learning Services 인스턴스가 여러 개 있는 경우 패키지를 각각에 추가 해야 합니다.

이 예제에 설치 된 패키지는 다양 한 유형의 신경망의 사용자 지정, 학습 및 공유를 지 원하는 Microsoft의 심층 학습을 위한 [CNTK](https://docs.microsoft.com/cognitive-toolkit/)입니다.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>1단계. Windows 버전의 Python 패키지 다운로드

+ 인터넷에 액세스할 수 없는 서버에 Python 패키지를 설치 하는 경우에는 WHL 파일을 다른 컴퓨터에 다운로드 한 다음 서버에 복사 해야 합니다.

    예를 들어 별도의 컴퓨터에서이 사이트 [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl)에서 whl 파일을 다운로드 한 다음 SQL Server 컴퓨터의 로컬 폴더에 파일 `cntk-2.1-cp35-cp35m-win_amd64.whl` 을 복사할 수 있습니다.

+ SQL Server 2017는 Python 3.5를 사용 합니다. 

> [!IMPORTANT]
> 패키지의 Windows 버전을 가져올 수 있는지 확인 합니다. 파일이 release.tar.gz로 끝나면 올바른 버전이 아닐 수 있습니다.

이 페이지에는 여러 플랫폼에 대 한 다운로드와 여러 Python 버전이 포함 되어 있습니다. [CNTK 설정](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>2단계. Python 명령 프롬프트를 엽니다.

SQL Server에서 사용 하는 기본 Python 라이브러리 위치를 찾습니다. 여러 인스턴스를 설치한 경우 패키지를 추가 하려는 인스턴스의 PYTHON_SERVICE 폴더를 찾습니다.

예를 들어 Machine Learning Services 기본값을 사용 하 여 설치 되 고 Machine Learning이 기본 인스턴스에서 사용 되는 경우 경로는 다음과 같습니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

인스턴스와 연결 된 Python 명령 프롬프트를 엽니다.

> [!TIP]
> 이후 디버깅 및 테스트를 위해 인스턴스 라이브러리와 관련 된 Python 환경을 설정 하는 것이 좋습니다.

### <a name="step-3-install-the-package-using-pip"></a>3단계. Pip를 사용 하 여 패키지 설치

+ Python 명령줄을 사용 하는 데 익숙한 경우 PIP를 사용 하 여 새 패키지를 설치 합니다. `Scripts` 하위 폴더에서 **pip** 설치 관리자를 찾을 수 있습니다. 

  SQL Server 설치 프로그램은 시스템 경로에 스크립트를 추가 하지 않습니다. 내부 또는 외부 명령으로 인식 `pip` 되지 않는 오류가 발생 하는 경우 Windows의 경로 변수에 Scripts 폴더를 추가할 수 있습니다.

  기본 설치에서 **Scripts** 폴더의 전체 경로는 다음과 같습니다.

    C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Visual studio 2017 또는 python 확장을 사용 하 여 visual studio 2015를 사용 하는 경우 `pip install` **python 환경** 창에서를 실행할 수 있습니다. **패키지**를 클릭 하 고 텍스트 상자에 설치할 패키지의 이름 또는 위치를 제공 합니다. 를 입력할 `pip install`필요가 없으며 자동으로 채워집니다. 

    - 컴퓨터가 인터넷에 연결 되어 있는 경우 패키지 이름 또는 특정 패키지와 버전의 URL을 입력 합니다. 
    
    예를 들어 Windows 및 Python 3.5에 대해 지원 되는 CNTK 버전을 설치 하려면 다운로드 URL을 지정 합니다.`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 컴퓨터에서 인터넷에 액세스할 수 없는 경우에는 설치를 시작 하기 전에 WHL 파일을 다운로드 해야 합니다. 그런 다음 로컬 파일 경로와 이름을 지정 합니다. 예를 들어 사이트에서 다운로드 한 WHL 파일을 설치 하려면 다음 경로와 파일을 붙여 넣습니다.`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

설치를 완료 하기 위해 권한을 상승 시키는 메시지가 표시 될 수 있습니다.

설치가 진행 됨에 따라 명령 프롬프트 창에서 상태 메시지를 볼 수 있습니다.

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>4단계. 패키지 또는 해당 기능을 스크립트의 일부로 로드

설치가 완료 되 면 다음 단계에 설명 된 대로 패키지 사용을 즉시 시작할 수 있습니다.

CNTK를 사용 하는 심층 학습의 예제는 다음 자습서를 참조 하세요. [CNTK 용 Python API](https://cntk.ai/pythondocs/tutorials.html)

스크립트에서 패키지의 함수를 사용 하려면 스크립트의 초기 줄에 `import <package_name>` 표준 문을 삽입 합니다.

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Conda를 사용 하 여 설치 된 패키지 나열

설치 된 패키지 목록을 가져오는 방법에는 여러 가지가 있습니다. 예를 들어 Visual Studio의 **Python 환경** 창에서 설치 된 패키지를 볼 수 있습니다.

Python 명령줄을 사용 하는 경우 SQL Server 설치 프로그램에 의해 추가 된 Anaconda Python 환경에 포함 된 **Pip** 또는 **conda** 패키지 관리자를 사용할 수 있습니다.

1. C:\Program Files\Microsoft SQL Server\MSSQL14.로 이동 합니다. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. `conda list` **Conda** > 를**관리자 권한으로 실행**을 마우스 오른쪽 단추로 클릭 하 고를 입력 하 여 현재 환경에 설치 된 패키지 목록을 반환 합니다.

1. 마찬가지로 **pip** > 를**관리자 권한으로 실행**을 마우스 오른쪽 단추로 클릭 하 고 `pip list` 를 입력 하 여 동일한 정보를 반환 합니다. 

**Conda** 및이를 사용 하 여 여러 Python 환경을 만들고 관리 하는 방법에 대 한 자세한 내용은 [conda를 사용 하 여 환경 관리](https://conda.io/docs/user-guide/tasks/manage-environments.html)를 참조 하세요.

> [!Note]
> 설치 프로그램에서 Pip 또는 Conda를 시스템 경로 및 프로덕션 SQL Server 인스턴스에 추가 하지 않으므로 불필요 한 실행 파일을 경로에서 제외 하는 것이 가장 좋습니다. SQL Server 그러나 개발 및 테스트 환경에서는 시스템 경로 환경 변수에 Scripts 폴더를 추가 하 여 모든 위치에서 Pip 및 Conda on 명령을 실행할 수 있습니다.
