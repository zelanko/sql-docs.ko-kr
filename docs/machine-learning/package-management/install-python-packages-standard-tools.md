---
title: Python 도구를 사용하여 패키지 설치
description: 표준 Python 도구를 사용하여 SQL Server Machine Learning Services 인스턴스에 새 Python 패키지를 설치하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/21/2020
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 67d5a323cfdbdb7eb765430ba264ff0bde2074f5
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870481"
---
# <a name="install-packages-with-python-tools-on-sql-server"></a>SQL Server에서 Python 도구를 사용하여 패키지 설치
[!INCLUDE [SQL Server 2017 only](../../includes/applies-to-version/sqlserver2017-only.md)]

이 문서에서는 표준 Python 도구를 사용하여 SQL Server Machine Learning Services 인스턴스에 새 Python 패키지를 설치하는 방법을 설명합니다. 일반적으로 새 패키지를 설치하는 프로세스는 표준 Python 환경의 경우와 유사합니다. 그러나 서버에 인터넷 연결이 없는 경우에는 몇 가지 추가 단계가 필요합니다.

패키지 위치 및 설치 경로에 대한 자세한 내용은 [Python 패키지 정보 가져오기](python-package-information.md)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

+ Python 언어 옵션과 함께 설치된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)가 있어야 합니다.

### <a name="other-considerations"></a>기타 고려 사항

+ 패키지는 Python 3.5과 호환되며 Windows에서 실행되어야 합니다.

+ Python 패키지 라이브러리는 SQL Server 인스턴스의 Program Files 폴더에 있으며, 기본적으로 이 폴더에 설치하려면 관리자 권한이 필요합니다. 자세한 내용은 [패키지 라이브러리 위치](../package-management/python-package-information.md#default-python-library-location)를 참조하세요.

+ 패키지 설치는 인스턴스별로 진행됩니다. Machine Learning Services 인스턴스가 여러 개 있는 경우 패키지를 각각에 추가해야 합니다.

+ 데이터베이스 서버는 자주 잠깁니다. 대부분의 경우 인터넷 액세스가 완전히 차단됩니다. 긴 종속성 목록이 포함된 패키지의 경우 이러한 종속성을 미리 식별하여 각 종속성을 수동으로 설치할 수 있도록 준비해야 합니다.

+ 패키지를 추가하기 전에 해당 패키지가 SQL Server 환경에 적합한지 여부를 고려합니다.

  + 데이터베이스를 단순히 쿼리하는 작업이 아니라, 기계 학습과 같은 데이터베이스 엔진과의 긴밀한 통합을 활용하는 태스크에는 데이터베이스 내에서 Python을 사용하는 것이 좋습니다.

  + 서버에 너무 많은 컴퓨팅 부하를 발생하는 패키지를 추가하는 경우 성능이 저하됩니다.

  + 강화된 SQL Server 환경에서는 다음을 방지해야 할 수 있습니다.
    + 네트워크 액세스가 필요한 패키지
    + 상승된 파일 시스템 액세스 권한이 필요한 패키지
    + 웹 개발 또는 SQL Server 내에서 실행해도 장점이 없는 기타 태스크에 사용되는 패키지

## <a name="add-a-python-package-on-sql-server"></a>SQL Server에 Python 패키지 추가

SQL Server의 스크립트에서 사용할 수 있는 새 Python 패키지를 설치하려면 Machine Learning Services의 인스턴스에 패키지를 설치합니다. Machine Learning Services 인스턴스가 여러 개 있는 경우 패키지를 각각에 추가해야 합니다.

다음 예제에 설치된 패키지는 여러 유형의 신경망 사용자 지정, 학습 및 공유를 지원하는 Microsoft의 딥 러닝을 위한 프레임워크인 [CNTK](/cognitive-toolkit/)입니다.

### <a name="for-offline-install-download-the-python-package"></a>오프라인 설치의 경우 Python 패키지 다운로드

인터넷에 액세스할 수 없는 서버에 Python 패키지를 설치하는 경우 인터넷에 액세스할 수 있는 컴퓨터에서 WHL 파일을 다운로드한 다음 파일을 서버에 복사해야 합니다.

예를 들어 인터넷에 연결된 컴퓨터에서는 `cntk-2.1-cp35-cp35m-win_amd64.whl`[https://cntk.ai/PythonWheel/CPU-Only 사이트에서 ](https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl) 파일을 다운로드한 다음 파일을 SQL Server 컴퓨터의 로컬 폴더로 복사할 수 있습니다.

> [!IMPORTANT]
> 패키지의 Windows 버전이 있는지 확인합니다. 파일이 .gz로 끝나면 올바른 버전이 아닐 수 있습니다.

여러 플랫폼 및 여러 버전의 Python용 CNTK 프레임워크 다운로드에 대한 자세한 내용은 [컴퓨터에 CNTK 설치](/cognitive-toolkit/Setup-CNTK-on-your-machine)를 참조하세요.

### <a name="locate-the-python-library"></a>Python 라이브러리 찾기

SQL Server에서 사용하는 기본 Python 라이브러리 위치를 찾습니다. 여러 인스턴스를 설치한 경우 패키지를 추가하려는 인스턴스의 `PYTHON_SERVICES` 폴더를 찾습니다.

예를 들어 Machine Learning Services 기본값을 사용하여 설치되고 Machine Learning이 기본 인스턴스에서 사용되는 경우 경로는 다음과 같습니다.

```console
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES"
```

> [!TIP]
> 이후 디버깅 및 테스트를 위해 인스턴스 라이브러리와 관련된 Python 환경을 설정하는 것이 좋습니다.

### <a name="install-the-package-using-pip"></a>pip를 사용하여 패키지 설치

**pip** 설치 프로그램을 사용하여 새 패키지를 설치합니다. `pip.exe` 폴더의 `Scripts` 하위 폴더에서 `PYTHON_SERVICES`를 찾을 수 있습니다. SQL Server 설치에서는 `Scripts` 하위 폴더를 시스템 경로에 추가하지 않으므로 전체 경로를 지정하거나 Windows의 PATH 변수에 Scripts 폴더를 추가할 수 있습니다.

> [!NOTE]
> Visual Studio 2017 또는 Python 확장이 포함된 Visual Studio 2015를 사용하는 경우 `pip install`Python 환경 **창에서** 을 실행할 수 있습니다. **패키지** 를 클릭하고 텍스트 상자에 설치할 패키지의 이름 또는 위치를 입력합니다. `pip install`은 입력할 필요가 없습니다. 자동으로 채워집니다.

+ 컴퓨터가 인터넷에 연결되어 있는 경우 패키지 이름을 입력합니다.

  ```console
  scripts\pip.exe install cntk
  ```
  특정 패키지 및 버전의 URL을 지정할 수도 있습니다. 예를 들면 다음과 같습니다.

  ```console
  scripts\pip.exe install https://cntk.ai/PythonWheel/CPU-Only/cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

+ 컴퓨터에서 인터넷에 액세스할 수 없는 경우 이전에 다운로드한 WHL 파일을 지정합니다. 다음은 그 예입니다.

  ```console
  scripts\pip.exe install C:\Downloads\cntk-2.1-cp35-cp35m-win_amd64.whl
  ```

설치를 완료하기 위해 권한을 상승시키는 메시지가 표시될 수 있습니다.
설치가 진행됨에 따라 명령 프롬프트 창에서 상태 메시지를 볼 수 있습니다.

### <a name="load-the-package-or-its-functions-as-part-of-your-script"></a>패키지 또는 해당 함수를 스크립트의 일부로 로드

설치가 완료되면 SQL Server의 Python 스크립트에서 패키지 사용을 즉시 시작할 수 있습니다.

스크립트에서 패키지의 함수를 사용하려면 스크립트의 시작 줄에 표준 `import <package_name>` 문을 삽입합니다.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import cntk
# Python statements ...
'
```

## <a name="see-also"></a>참고 항목

+ [Python 패키지 정보 가져오기](python-package-information.md)
+ [SQL Server Machine Learning Services용 Python 자습서](../tutorials/python-tutorials.md)
+ [CNTK용 Python API](https://cntk.ai/pythondocs/tutorials.html).