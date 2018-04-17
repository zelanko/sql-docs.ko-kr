---
title: SQL Server 기계 학습에서 Python 패키지를 새 설치 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 927d34755dbe291d1b208d968b13d36baf90bc15
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server에 새 Python 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2017 컴퓨터 학습 서비스 인스턴스의 새 Python 패키지를 설치 하는 방법을 설명 합니다.

일반적으로 새 패키지를 설치 하기 위한 프로세스는 표준 Python 환경에서와 유사 합니다. 그러나 서버에 인터넷 연결이 없는 경우 몇 가지 추가 단계는 필요 합니다.

패키지 설치 되는 위치 또는 설치 된 패키지를 파악 하는 도움말을 참조 하십시오. [설치 된 R, Python 패키지 보기](../r/determine-which-packages-are-installed-on-sql-server.md)합니다.

## <a name="prerequisites"></a>필수 구성 요소

+ Python 언어 옵션으로 컴퓨터 학습 Services (In-database) 설치 해야 합니다. 자세한 내용은 [설치할 SQL Server 2017 컴퓨터 학습 Services (In-database)](../install/sql-machine-learning-services-windows-install.md)합니다.

+ 각 서버 인스턴스에 대해 별도 패키지의 복사본을 설치 해야 합니다. 패키지는 인스턴스 간에 공유할 수 없습니다.

+ Python 3.5와 함께 되며 Windows 환경에서 사용 하려는 패키지를 작동 하는지 여부를 결정 합니다. 

+ 패키지는 SQL Server 환경에서 사용 하기 위해 가장 잘 맞는 있는지 여부를 평가 합니다. 여러 서비스 및 응용 프로그램, 데이터베이스 서버는 일반적으로 지원 하 고 파일 시스템의 리소스 제한 뿐만 아니라 서버에 연결할 수 있습니다. 대부분의 경우에서 인터넷 액세스가 완전히 차단 됩니다.

    다른 일반적인 문제 등 네트워킹 또는 방화벽 또는 Windows 컴퓨터에 설치할 수 없는 종속성이 패키지는 서버에서 차단 되는 기능입니다. 

    일부 인기 있는 Python 패키지 (예: 플라스) 독립 실행형 환경에서는 더 나은 실행 하는 웹 개발 등의 작업을 수행 합니다. 단순히 데이터베이스를 쿼리 하는 것이 아니라 데이터베이스 엔진과 긴밀 한 통합을 활용 하는 많은 데이터 처리를 필요로 하는 기계 학습 등의 작업에 대 한 데이터베이스에 Python을 사용 하는 것이 좋습니다.

+ 패키지를 설치 하는 서버에 관리자 권한이 필요 합니다.

## <a name="add-a-new-python-package"></a>새 Python 패키지 추가

이 예에서는 SQL Server 컴퓨터에서 직접 새 패키지를 설치 하려면을 가정 합니다.

이 예제에 설치 된 패키지는 [CNTK](https://docs.microsoft.com/cognitive-toolkit/), Microsoft에서 지 원하는 사용자 지정, 교육 및 다양 한 유형의 신경망의 공유 심층 학습을 위한 프레임 워크입니다.

> [!TIP]
> Python 도구를 구성 합니다. 도움이 필요 하세요? 이러한 블로그를 참조 합니다.
> 
> [서버를 학습 하는 컴퓨터를 사용 하 여 Python 웹 서비스를 시작 하기](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)
> 
> [David Crook: Microsoft Cognitive Toolkit + VS Code](http://dacrook.com/cntk-vs-code-awesome/)

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>1단계. Windows 버전의 Python 패키지 다운로드

+ 인터넷에 연결 된 서버에서 Python 패키지를 설치 하는 경우에 다른 컴퓨터로 WHL 파일을 다운로드 하 고 서버에 복사 해야 합니다.

    예를 들어 별도 컴퓨터에 다운로드할 수 있습니다 WHL 파일이이 사이트에서 [ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl), 다음 파일을 복사 하 고 `cntk-2.1-cp35-cp35m-win_amd64.whl` SQL Server 컴퓨터에 로컬 폴더에 있습니다.

+ SQL Server 2017 Python 3.5를 사용합니다. 

> [!IMPORTANT]
> 패키지의 Windows 버전을 가져올 수 있는지 확인 합니다. 파일.gz로 끝나는 경우 것은 올바른 버전 되지 않았을 수 있습니다.

이 페이지에서는 여러 플랫폼에서는 여러 Python 버전에 대 한 다운로드: [CNTK 설정](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>2단계. Python 명령 프롬프트를 열으십시오

SQL Server에서 사용 하 여 기본 Python 라이브러리 위치를 찾습니다. 여러 인스턴스를 설치한 경우 패키지를 추가 하려는 인스턴스에 대 한 PYTHON_SERVICE 폴더를 찾습니다.

예를 들어 컴퓨터 학습 서비스 설치가 완료 된 후 기본값을 사용 하 고 기계 학습이 기본 인스턴스에서 설정 하는 경우 경로가 합니다 다음과 같습니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

인스턴스와 연결 된 Python 명령 프롬프트를 엽니다.

> [!TIP]
> 이후 디버깅 및 테스트를 특정 인스턴스 라이브러리에는 Python 환경을 설정 하는 것이 좋습니다.

### <a name="step-3-install-the-package-using-pip"></a>3단계. Pip를 사용 하 여 패키지를 설치 합니다.

+ Python 명령줄을 사용 하는 데 익숙한, PIP.exe 사용 하 여 새 패키지를 설치 합니다. 찾을 수 있습니다는 **pip** 에 있는 설치 관리자는 `Scripts` 하위 폴더입니다. 

    오류가 발생 하는 경우 `pip` 인식 되지 않는 내부 또는 외부 명령, 창에는 PATH 변수에 Python 실행 파일 및 Python 스크립트 폴더의 경로 추가할 수 있습니다.

    전체 경로 **스크립트** 기본 설치에서 폴더는 다음과 같습니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ Visual Studio 2017 또는 Visual Studio 2015는 Python 확장과 함께 사용할 경우 실행할 수 있습니다 `pip install` 에서 **Python 환경** 창. 클릭 **패키지**, 하 고 텍스트 상자에 이름 또는 설치 하는 패키지의 위치를 제공 합니다. 입력 하지 않아도 `pip install`; 채워진 후 사용자에 대 한 자동으로 합니다. 

    - 컴퓨터가 인터넷에 액세스 하는 경우에 패키지의 이름 또는 URL 특정 패키지와 버전을 제공 합니다. 
    
    예를 들어 CNTK 창과 Python 3.5에 지원 되는 버전을 설치 하려면 다운로드 URL을 지정 합니다. `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 컴퓨터에 인터넷에 연결 하는 경우 설치를 시작 하기 전에 WHL 파일을 다운로드 해야 합니다. 그런 다음 로컬 파일 경로 이름을 지정 합니다. 예를 들어 다음 경로 사이트에서 다운로드 한 WHL 파일을 설치할 파일을 붙여 넣습니다. `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

설치를 완료 하는 권한 상승을 하 라는 메시지가 표시 될 수 있습니다.

설치 진행 됨에 따라 명령 프롬프트 창에서 상태 메시지를 볼 수 있습니다.

```python
pip install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
Collecting cntk==2.1 from https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  Downloading https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl (34.1MB)
    100% |################################| 34.1MB 13kB/s
...
Installing collected packages: cntk
Successfully installed cntk-2.1
```


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>4단계. 스크립트의 일부로 패키지 또는 기능을 로드

설치가 완료 되 면 다음 단계에 설명 된 대로 패키지를 사용 하 여 즉시 시작할 수 있습니다.

이 자습서를 참조 하는 CNTK를 사용 하 여 심층 학습의 예에 대 한: [CNTK에 대 한 Python API](https://cntk.ai/pythondocs/tutorials.html)

스크립트에 패키지에서 함수를 사용 하려면 표준 삽입 `import <package_name>` 스크립트의 초기 줄에서 문:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

##  <a name="how-to-view-installed-packages-using-conda"></a>Conda를 사용 하 여 설치 된 패키지를 확인 하는 방법

설치 된 패키지 목록을 얻을 수 있는 다른 방법도 있습니다. 예를 들어 설치 된 패키지에서 볼 수 있습니다는 **Python 환경** Visual Studio의 창이 있습니다.

Python 명령줄을 사용 하는 경우 사용할 수 있습니다는 **conda** SQL Server 설치 프로그램에서 추가할 Anaconda Python 환경을 포함 되어 있는 패키지 관리자.

현재 환경에 설치 된 Python 패키지를 보려면 명령 프롬프트에서이 명령을 실행 합니다.

```python
conda list
```

에 대 한 자세한 내용은 **conda** 사용 하 여 만들기 및 관리 여러 Python 환경 참조 하는 방법 및 [conda 환경을 관리](https://conda.io/docs/user-guide/tasks/manage-environments.html)합니다.
