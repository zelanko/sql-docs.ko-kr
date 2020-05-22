---
title: sqlmlutils를 사용하여 Python 패키지 설치
description: Python pip를 사용하여 SQL Server Machine Learning Services 인스턴스에 새 Python 패키지를 설치하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/24/2020
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 69da04eaad729225ed0629ba78d2f214b30ba942
ms.sourcegitcommit: dc965772bd4dbf8dd8372a846c67028e277ce57e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83606493"
---
# <a name="install-python-packages-with-sqlmlutils"></a>sqlmlutils를 사용하여 Python 패키지 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) 패키지의 함수를 사용하여 SQL Server Machine Learning Services 인스턴스에 새 Python 패키지를 설치하는 방법을 설명합니다. 설치한 패키지는 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) T-SQL 문을 사용하여 데이터베이스 내에서 실행되는 Python 스크립트에서 사용할 수 있습니다.

패키지 위치 및 설치 경로에 대한 자세한 내용은 [Python 패키지 정보 가져오기](../package-management/python-package-information.md)를 참조하세요.

> [!NOTE]
> 이 문서에서 설명하는 **sqlmlutils** 패키지는 SQL Server 2019 이상에 Python 패키지를 추가하는 데 사용됩니다. SQL Server 2017 이전 버전의 경우 [Python 도구를 사용하여 패키지 설치](https://docs.microsoft.com/sql/machine-learning/package-management/install-python-packages-standard-tools?view=sql-server-2017&viewFallbackFrom=sql-server-ver15)를 참조하세요.

## <a name="prerequisites"></a>사전 요구 사항

+ Python 언어 옵션과 함께 설치된 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)가 있어야 합니다.

+ SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에 [python](https://www.python.org/)을 설치합니다. [Python 확장](https://marketplace.visualstudio.com/items?itemName=ms-python.python)이 있는 [Visual Studio Code](https://code.visualstudio.com/download)와 같은 Python 개발 환경을 원할 수도 있습니다. 

+ SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is)를 설치합니다. 다른 데이터베이스 관리 또는 쿼리 도구를 사용할 수 있지만, 이 문서에서는 Azure Data Studio를 사용한다고 가정합니다.

### <a name="other-considerations"></a>기타 고려 사항

+ 패키지는 사용 중인 Python 버전의 규격을 준수해야 합니다. 각 SQL Server 버전에 포함된 Python 버전에 대한 자세한 내용은 [Python 및 R 버전](../sql-server-machine-learning-services.md#versions)을 참조하세요.

+ Python 패키지 라이브러리는 SQL Server 인스턴스의 Program Files 폴더에 있으며, 기본적으로 이 폴더에 설치하려면 관리자 권한이 필요합니다. 자세한 내용은 [패키지 라이브러리 위치](../package-management/python-package-information.md#default-python-library-location)를 참조하세요.

+ 패키지 설치는 인스턴스별로 진행됩니다. Machine Learning Services 인스턴스가 여러 개 있는 경우 패키지를 각각에 추가해야 합니다.

+ 패키지를 추가하기 전에 해당 패키지가 SQL Server 환경에 적합한지 여부를 고려합니다.

  + 데이터베이스를 단순히 쿼리하는 작업이 아니라, 기계 학습과 같은 데이터베이스 엔진과의 긴밀한 통합을 활용하는 태스크에는 데이터베이스 내에서 Python을 사용하는 것이 좋습니다.

  + 서버에 너무 많은 컴퓨팅 부하를 발생하는 패키지를 추가하는 경우 성능이 저하됩니다.

  + 강화된 SQL Server 환경에서는 다음을 방지해야 할 수 있습니다.
    + 네트워크 액세스가 필요한 패키지
    + 상승된 파일 시스템 액세스 권한이 필요한 패키지
    + 웹 개발 또는 SQL Server 내에서 실행해도 장점이 없는 기타 태스크에 사용되는 패키지

## <a name="install-sqlmlutils-on-the-client-computer"></a>클라이언트 컴퓨터에 sqlmlutils 설치

**sqlmlutils**를 사용하려면 먼저 SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터에 설치해야 합니다. `pip`를 설치했는지 확인합니다. 자세한 내용은 [pip 설치](https://pip.pypa.io/en/stable/installing/)를 참조하세요.

1. 최신 **sqlmlutils** zip 파일을 https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist 에서 클라이언트 컴퓨터로 다운로드합니다. 파일 압축을 풀지 마세요.

1. **명령 프롬프트**를 열고 다음 명령을 실행하여 **sqlmlutils** 패키지를 설치합니다. 다운로드한 **sqlmlutils** zip 파일의 전체 경로를 대체합니다. 이 예제에서는 다운로드한 파일을 `c:\temp\sqlmlutils-1.0.0.zip`이라고 가정합니다.

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils-1.0.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>SQL Server에 Python 패키지 추가

다음 예제에서는 SQL Server에 [text-tools](https://pypi.org/project/text-tools/) 패키지를 추가합니다.

### <a name="add-the-package-online"></a>온라인으로 패키지 추가

SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터가 인터넷에 연결되어 있는 경우 **sqlmlutils**를 사용하여 인터넷을 통해 **text-tools** 패키지와 종속성을 찾은 다음, 원격으로 SQL Server 인스턴스에 패키지를 설치할 수 있습니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

1. 클라이언트 컴퓨터에서 **Python** 또는 Python 환경을 엽니다.

1. 다음 명령을 사용하여 **text-tools** 패키지를 설치합니다. 사용자 고유의 SQL Server 데이터베이스 연결 정보로 대체합니다(Windows 인증을 사용하는 경우에는 `uid` 및 `pwd` 매개 변수 필요 없음).

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

1. 클라이언트 컴퓨터에서 **Python** 또는 Python 환경을 엽니다.

1. 다음 명령을 사용하여 **text-tools** 패키지를 설치합니다. 사용자의 SQL Server 데이터베이스 연결 정보를 대체합니다.

::: moniker-end

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="server", database="database", uid="username", pwd="password")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>오프라인으로 패키지 추가

SQL Server에 연결하는 데 사용하는 클라이언트 컴퓨터가 인터넷에 연결되지 않은 경우 인터넷에 액세스할 수 있는 컴퓨터에서 **pip**를 사용하여 패키지 및 모든 종속성 패키지를 로컬 폴더에 다운로드할 수 있습니다. 그런 다음, 패키지를 오프라인으로 설치할 수 있는 클라이언트 컴퓨터에 해당 폴더를 복사합니다.

#### <a name="on-a-computer-with-internet-access"></a>인터넷에 액세스할 수 있는 컴퓨터의 경우

1. **명령 프롬프트**를 열고 다음 명령을 실행하여 **text-tools** 패키지가 포함된 로컬 폴더를 만듭니다. 다음 예제에서는 `c:\temp\text-tools` 폴더를 만듭니다.

   ```console
   pip download text-tools -d c:\temp\text-tools
   ```

1. `text-tools` 폴더를 클라이언트 컴퓨터에 복사합니다. 다음 예제에서는 `c:\temp\packages\text-tools`로 복사했다고 가정합니다.

#### <a name="on-the-client-computer"></a>클라이언트 컴퓨터의 경우

**sqlmlutils**를 사용하여 **pip**를 통해 생성된 로컬 폴더에 사용자가 찾은 각 패키지(WHL 파일)를 설치합니다. 패키지를 설치하는 순서는 중요하지 않습니다.

이 예제에서는 **text-tools**에는 종속성이 없으므로 `text-tools` 폴더에는 설치할 파일이 1개 뿐입니다. 반면, **scikit-plot**과 같은 패키지에는 11개의 종속성이 있으므로 폴더에서 12개 파일(**scikit-plot** 패키지 및 11개의 종속성 패키지)을 찾을 수 있으며 각각을 설치합니다.

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"

다음 Python 스크립트를 실행합니다. 패키지의 실제 파일 경로와 이름, 사용자 고유의 SQL Server 데이터베이스 연결 정보로 대체합니다(Windows 인증을 사용하는 경우에는 `uid` 및 `pwd` 매개 변수 필요 없음). 폴더의 각 패키지 파일에 대해 `sqlmlutils.SQLPackageManager` 문을 반복합니다.

::: moniker-end

::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

다음 Python 스크립트를 실행합니다. 패키지의 실제 파일 경로와 이름, 사용자 고유의 SQL Server 데이터베이스 연결 정보로 대체합니다. 폴더의 각 패키지 파일에 대해 `sqlmlutils.SQLPackageManager` 문을 반복합니다.

::: moniker-end

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="username", pwd="password"))
sqlmlutils.SQLPackageManager(connection).install("text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package"></a>패키지 사용

이제 SQL Server의 Python 스크립트에서 이 패키지를 사용할 수 있습니다. 다음은 그 예입니다.

```python
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
from text_tools.finders import find_best_string
corpus = "Lorem Ipsum text"
query = "Ipsum"
first_match = find_best_string(query, corpus)
print(first_match)
  '
```

## <a name="remove-the-package-from-sql-server"></a>SQL Server에서 패키지 제거

**text-tools** 패키지를 제거하려면 이전에 정의한 것과 동일한 연결 변수를 사용하여 클라이언트 컴퓨터에서 다음 Python 명령을 사용합니다.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="next-steps"></a>다음 단계

+ SQL Server Machine Learning Services에 설치된 Python 패키지에 대한 자세한 내용은 [Python 패키지 정보 가져오기](../package-management/python-package-information.md)를 참조하세요.

+ SQL Server Machine Learning Services에서 R 패키지를 설치하는 방법에 대한 내용은 [SQL Server에 새로운 R 패키지 설치](install-additional-r-packages-on-sql-server.md)를 참조하세요.
