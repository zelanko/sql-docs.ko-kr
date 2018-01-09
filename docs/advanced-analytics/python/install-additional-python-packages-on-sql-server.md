---
title: "SQL Server에 새 Python 패키지 설치 | Microsoft Docs"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: python
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 78a76403f3212c7619afbf02577075161699fbd6
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server에 새 Python 패키지 설치

이 문서에서는 SQL Server 2017의 인스턴스에서 새 Python 패키지를 설치 하는 방법을 설명 합니다.

또한 현재 환경에 설치 된 패키지를 나열 하는 방법을 설명 합니다.

## <a name="prerequisites"></a>사전 요구 사항

새 패키지를 설치 하기 위한 프로세스를 대부분 그렇게 표준 Python 환경에 합니다. 그러나 서버에 인터넷 연결이 없는 경우 몇 가지 추가 단계는 필요 합니다.

+ Python 언어 옵션으로 컴퓨터 학습 Services (In-database) 설치 해야 합니다. 자세한 내용은 [Python 컴퓨터 학습 서비스 설정](setup-python-machine-learning-services.md)합니다.

+ 각 서버 인스턴스에 대해 별도 패키지의 복사본을 설치 해야 합니다. 패키지는 인스턴스 간에 공유할 수 없습니다.

+ Python 3.5와 함께 되며 Windows 환경에서 사용 하려는 패키지를 작동 하는지 여부를 결정 합니다. 

    일반적으로 가져오고 SQL Server 환경에서 사용할 수 있는 패키지에 대 한 몇 가지 제한이 있습니다. 가능한 문제는 서버 또는 방화벽으로 차단 된 네트워킹 기능을 사용 하는 패키지 또는 Windows 컴퓨터에 설치할 수 없는 종속성을 사용 하 여 패키지를 포함 합니다.

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

    예를 들어 별도 컴퓨터에 다운로드할 수 있습니다 WHL 파일이이 사이트에서 [https://cntk.ai/PythonWheel/CPU-Only](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl), 다음 파일을 복사 하 고 `cntk-2.1-cp35-cp35m-win_amd64.whl` SQL Server 컴퓨터에 로컬 폴더에 있습니다.

+ SQL Server 2017 Python 3.5를 사용합니다. 패키지의 Windows 버전 및 Python 3.5와 호환 되는 버전을 구입 해야 합니다.

이 페이지에서는 여러 플랫폼에서는 여러 Python 버전에 대 한 다운로드: [CNTK 설정](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>2단계. Python 명령 프롬프트를 열으십시오

SQL Server에서 사용 하 여 기본 Python 라이브러리 위치를 찾습니다. 여러 인스턴스를 설치한 경우 패키지를 추가 하려는 인스턴스에 대 한 PYTHON_SERVICE 폴더를 지정 해야 합니다.

예를 들어 컴퓨터 학습 서비스 설치가 완료 된 후 기본값을 사용 하 고 기계 학습이 기본 인스턴스에서 설정 하는 경우 경로가 합니다 다음과 같습니다.

    `C:\Program Files\Microsoft SQL  Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

인스턴스와 연결 된 Python 명령 프롬프트를 엽니다.

> [!TIP]
> 설정 하는 Python 환경 컴퓨터 학습 서버 또는 SQL Server에 특정 하는 것이 좋습니다.

### <a name="step-3-install-the-package-using-pip"></a>3단계. Pip를 사용 하 여 패키지를 설치 합니다.

+ Python 명령줄을 사용 하는 데 익숙한, PIP.exe 사용 하 여 새 패키지를 설치 합니다. 찾을 수 있습니다는 **pip** 에 있는 설치 관리자는 `Scripts` 하위 폴더입니다. 

    오류가 발생 하는 경우 **pip** 인식 되지 않는 내부 또는 외부 명령, 창에는 PATH 변수에 Python 실행 파일 및 Python 스크립트 폴더의 경로 추가할 수 있습니다.

    전체 경로 **스크립트** 기본 설치에서 폴더는 다음과 같습니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts`

+ Visual Studio 2017 또는 Visual Studio 2015는 Python 확장과 함께 사용할 경우 실행할 수 있습니다 `pip install` 에서 **Python 환경** 창. 클릭 **패키지**, 하 고 텍스트 상자에 이름 또는 설치 하는 패키지의 위치를 제공 합니다. 입력 하지 않아도 `pip install`; 채워진 후 사용자에 대 한 자동으로 합니다. 

    - 컴퓨터가 인터넷에 액세스 하는 경우에 패키지의 이름 또는 URL 특정 패키지와 버전을 제공 합니다. 예를 들어 CNTK 창과 Python 3.5에 지원 되는 버전을 설치 하려면 다운로드 URL을 지정할 수 있습니다.`https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 컴퓨터에 인터넷에 연결 하는 경우 해야 파일을 다운로드 한는 WHL 미리 합니다. 그런 다음 로컬 파일 경로 이름을 지정 합니다. 예를 들어 다음 경로 사이트에서 다운로드 한 WHL 파일을 설치할 파일을 붙여 넣습니다.`"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

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

현재 환경에 설치 된 Python 패키지를 보려면 명령 프롬프트 창에서이 명령을 실행 합니다.

```python
conda list
```

에 대 한 자세한 내용은 **conda** 사용 하 여 만들기 및 관리 여러 Python 환경 참조 하는 방법 및 [conda 환경을 관리](https://conda.io/docs/user-guide/tasks/manage-environments.html)합니다.
