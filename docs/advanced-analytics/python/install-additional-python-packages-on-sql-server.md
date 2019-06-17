---
title: 새 Python 언어 패키지-SQL Server Machine Learning 설치
description: SQL Server 2017 Machine Learning Services (In-database) 및 Machine Learning Server (독립 실행형)에 새로운 Python 패키지를 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/16/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0c6c4384dd6c02e35fe77a6fb2bfc4017a445b1b
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140716"
---
# <a name="install-new-python-packages-on-sql-server"></a>SQL Server에 새로운 Python 패키지 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 SQL Server 2017의 Machine Learning Services의 인스턴스에서 새 Python 패키지를 설치 하는 방법을 설명 합니다. 일반적으로 새 패키지를 설치 하기 위한 프로세스는 표준 Python 환경에서와 유사 합니다. 그러나 몇 가지 추가 단계가 필요한 서버에 인터넷 연결이 없는 경우.

패키지 위치 및 설치 경로 대 한 자세한 내용은 참조 하세요. [가져오려면 R 또는 Python 패키지 정보](../package-management/installed-package-information.md)합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-services-windows-install.md) Python 언어 옵션을 사용 하 여 합니다. 

+ 패키지에는 Windows에서 Python 3.5 준수 하 고 실행 해야 합니다. 

+ 서버에 대 한 관리 액세스는 패키지를 설치 해야 합니다.

## <a name="considerations"></a>고려 사항

패키지에 추가 하기 전에 패키지에 적합 한 SQL Server 환경 인지 하는 것이 좋습니다. 일반적으로 데이터베이스 서버는 여러 워크 로드를 수용 하는 공유 자산입니다. 서버에 너무 많은 계산 압력을 배치 하는 패키지에 추가 하면 성능이 저하 됩니다. 

또한 몇 가지 인기 있는 Python 패키지 (예: Flask)는 독립 실행형 환경에 더 적합 하는 작업, 웹 개발 등을 수행 합니다. 단순히 데이터베이스를 쿼리 하는 작업 보다는 machine learning과 같은 데이터베이스 엔진을 사용 하 여 긴밀 한 통합을 활용 하는 작업에 대 한 데이터베이스에서 Python을 사용 하는 것이 좋습니다.

데이터베이스 서버는 자주 잠겨 있습니다. 대부분의 경우 인터넷 완전히 차단 됩니다. 종속성의 긴 목록이 포함 된 패키지에 대 한 이러한 종속성을 사전에 식별 하 고 각각을 수동으로 설치할 수 해야 합니다.

## <a name="add-a-new-python-package"></a>새 Python 패키지를 추가 합니다.

예를 들어 SQL Server 컴퓨터에서 직접 새 패키지를 설치 하려는 가정 합니다.

패키지 설치가 인스턴스당입니다. Machine Learning Services의 여러 인스턴스가 있는 경우에 각각에 패키지를 추가 해야 합니다.

이 예제의 설치 패키지가 [CNTK](https://docs.microsoft.com/cognitive-toolkit/), Microsoft에서 사용자 지정을 지 원하는 다양 한 신경망의 공유 하 고 교육, 심층 학습을 위한 프레임 워크입니다.

### <a name="step-1-download-the-windows-version-of-the-python-package"></a>1단계. Windows 버전의 Python 패키지를 다운로드 합니다.

+ 인터넷 액세스 없이 서버의 Python 패키지를 설치 하는 경우에 다른 컴퓨터로 WHL 파일을 다운로드 하 고 서버에 복사 해야 합니다.

    예를 들어, 별개의 컴퓨터에 다운로드할 수 있습니다 WHL 파일에서이 사이트 [ https://cntk.ai/PythonWheel/CPU-Only ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl), 다음 파일을 복사 하 고 `cntk-2.1-cp35-cp35m-win_amd64.whl` SQL Server 컴퓨터의 로컬 폴더에 있습니다.

+ SQL Server 2017에서는 Python 3.5를 사용합니다. 

> [!IMPORTANT]
> 패키지의 Windows 버전을 가져올 수 있는지 확인 합니다. 파일.gz로 끝나는 경우 것 올바른 버전 되지 않을 수 있습니다.

이 페이지에서는 여러 플랫폼 및 여러 Python 버전 다운로드: [CNTK 설정](https://docs.microsoft.com/cognitive-toolkit/Setup-CNTK-on-your-machine)

### <a name="step-2-open-a-python-command-prompt"></a>2단계. Python 명령 프롬프트를 열으십시오

SQL Server에서 사용 하는 기본 Python 라이브러리 위치를 찾습니다. 여러 인스턴스를 설치한 경우 패키지를 추가 하려는 인스턴스에 대 한 PYTHON_SERVICE 폴더를 찾습니다.

예를 들어 기본값을 사용 하 여 Machine Learning Services가 설치 되어 있으며 기계 학습 기본 인스턴스에서 설정 되어 있는 경우 경로 다음과 같을 수 됩니다.

    `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

인스턴스와 연결 된 Python 명령 프롬프트를 엽니다.

> [!TIP]
> 향후 디버깅 및 테스트를 위해 특정 인스턴스 라이브러리에 Python 환경을 설정 하는 것이 좋습니다.

### <a name="step-3-install-the-package-using-pip"></a>3단계. Pip를 사용 하 여 패키지를 설치 합니다.

+ Python 명령줄을 사용 하 여 익숙한 PIP.exe를 사용 하 여 새 패키지를 설치 합니다. 찾을 수 있습니다 합니다 **pip** 에서 설치 관리자를 `Scripts` 하위 폴더입니다. 

  SQL Server 설치는 시스템 경로에 스크립트를 추가 하지 않습니다. 오류가 발생 하는 경우 `pip` Windows에서 경로 변수에 스크립트 폴더를 추가할 수는 내부 또는 외부 명령으로 인식 되지 않습니다.

  전체 경로 **스크립트** 기본 설치에서 폴더는 다음과 같습니다.

    C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

+ Python 확장을 사용 하 여 Visual Studio 2017 또는 Visual Studio 2015를 사용 하는, 하는 경우 실행할 수 있습니다 `pip install` 에서 합니다 **Python 환경** 창입니다. 클릭 **패키지**, 텍스트 상자에 이름 또는 설치 패키지의 위치를 제공 합니다. 입력 필요가 `pip install`;이를 자동으로 채워집니다. 

    - 컴퓨터가 인터넷에 액세스 하는 경우 패키지의 이름 또는 버전을 특정 패키지의 URL을 제공 합니다. 
    
    예를 들어, Windows 및 Python 3.5에 대 한 지원 되는 CNTK의 버전을 설치 하려면 다운로드 URL을 지정 합니다. `https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl`

    - 컴퓨터에 인터넷 액세스가 없는 경우 설치를 시작 하기 전에 WHL 파일을 다운로드 해야 합니다. 그런 다음 로컬 파일 경로 이름을 지정 합니다. 예를 들어 다음 경로 및 사이트에서 다운로드 한 WHL 파일을 설치 하는 파일을 붙여넣습니다. `"C:\Downloads\CNTK\cntk-2.1-cp35-cp35m-win_amd64.whl"`

설치를 완료 하는 권한을 상승 하 라는 메시지가 표시 될 수 있습니다.

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


### <a name="step-4-load-the-package-or-its-functions-as-part-of-your-script"></a>4단계. 스크립트의 일부로 해당 함수나 패키지 로드

설치가 완료 되 면 다음 단계에 설명 된 대로 패키지를 사용 하 여 바로 시작할 수 있습니다.

CNTK를 사용 하 여 딥 러닝의 예로, 이러한 자습서를 참조 하세요. [Python API for CNTK](https://cntk.ai/pythondocs/tutorials.html)

스크립트에 패키지에서 함수를 사용 하려면 표준 삽입 `import <package_name>` 스크립트의 초기 줄에서 문:

```python
import numpy as np
import cntk as cntk
cntk._version_
```

## <a name="list-installed-packages-using-conda"></a>Conda를 사용 하 여 설치 된 패키지를 나열 합니다.

설치 된 패키지 목록을 가져올 수 있는 여러 가지가 있습니다. 예를 들어,에 설치 된 패키지를 볼 수 있습니다 합니다 **Python 환경** Visual Studio의 창.

Python 명령줄을 사용 하는 경우 중 하나를 사용할 수 있습니다 **Pip** 또는 **conda** SQL Server 설치 프로그램에서 추가 Anaconda Python 환경에 포함 된 패키지 관리자입니다.

1. Go to C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 마우스 오른쪽 단추로 클릭 **conda.exe** > **관리자 권한으로 실행**를 입력 하 고 `conda list` 현재 환경에 설치 된 패키지 목록을 반환 합니다.

1. 마찬가지로, 마우스 오른쪽 단추로 클릭 **pip.exe** > **관리자 권한으로 실행**, enter `pip list` 동일한 정보를 반환 합니다. 

에 대 한 자세한 내용은 **conda** 만들고 여러 Python 환경을 관리 하며, 참조 하 여 하는 방법 및 [conda 사용 하 여 환경을 관리](https://conda.io/docs/user-guide/tasks/manage-environments.html)합니다.

> [!Note]
> SQL Server 설치 프로그램에서 Pip 또는 Conda를 시스템 경로 및 프로덕션 SQL Server 인스턴스에서 유지 필수적이 지 않은 실행 파일 경로에서 가장 좋은 방법은 추가 되지 않습니다. 그러나 개발 및 테스트 환경에 대 한 모든 위치에서 명령에 Pip와 Conda를 실행 하려면 시스템 PATH 환경 변수에 스크립트 폴더를 추가할 수 있습니다.
