---
title: Pip를 사용 하 여 Python 패키지 설치
description: Python pip를 사용 하 여 SQL Server Machine Learning Services 인스턴스에 새 Python 패키지를 설치 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||=sqlallproducts-allversions'
ms.openlocfilehash: 50463f27f37f9da410d1598002989f7cea6d8158
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000780"
---
# <a name="install-python-packages-with-sqlmlutils"></a>Sqlmlutils를 사용 하 여 Python 패키지 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) 패키지의 함수를 사용 하 여 SQL Server Machine Learning Services 인스턴스에 새 Python 패키지를 설치 하는 방법을 설명 합니다. 설치 하는 패키지는 T-sql [sp-s q s](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) -transact-sql 문을 사용 하 여 데이터베이스 내에서 실행 되는 Python 스크립트에서 사용할 수 있습니다.

패키지 위치 및 설치 경로에 대 한 자세한 내용은 [Python 패키지 정보 가져오기](../package-management/python-package-information.md)를 참조 하세요.

> [!NOTE]
> 표준 python `pip install` 명령은 SQL Server에 Python 패키지를 추가 하는 데 권장 되지 않습니다. 대신이 문서에 설명 된 대로 **sqlmlutils** 를 사용 합니다.

## <a name="prerequisites"></a>사전 요구 사항

+ Python 언어 옵션을 사용 하 여 [SQL Server Machine Learning Services](../install/sql-machine-learning-services-windows-install.md) 설치 되어 있어야 합니다.

+ SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에 [python](https://www.python.org/) 을 설치 합니다. [Python 확장](https://marketplace.visualstudio.com/items?itemName=ms-python.python)을 사용 하 여 [Visual Studio Code](https://code.visualstudio.com/download) 같은 python 개발 환경을 원할 수도 있습니다. 

+ SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에 SSMS ( [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) 또는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS)를 설치 합니다. 다른 데이터베이스 관리 또는 쿼리 도구를 사용할 수 있지만이 문서에서는 Azure Data Studio 또는 SSMS를 가정 합니다.

### <a name="other-considerations"></a>기타 고려 사항

+ 패키지는 Python 3.5 호환 되며 Windows에서 실행 되어야 합니다.

+ Python 패키지 라이브러리는 SQL Server 인스턴스의 Program Files 폴더에 있으며, 기본적으로이 폴더에 설치 하려면 관리자 권한이 필요 합니다. 자세한 내용은 [패키지 라이브러리 위치](../package-management/python-package-information.md#default-python-library-location)를 참조 하세요.

+ 패키지 설치는 인스턴스당입니다. Machine Learning Services 인스턴스가 여러 개 있는 경우 패키지를 각각에 추가 해야 합니다.

+ 패키지를 추가 하기 전에 패키지가 SQL Server 환경에 적합 한지 여부를 고려 합니다.

  + 데이터베이스를 단순히 쿼리 하는 작업이 아니라 machine learning과 같은 데이터베이스 엔진과의 긴밀 한 통합을 활용 하는 태스크에는 Python 데이터베이스 내를 사용 하는 것이 좋습니다.

  + 서버에 너무 많은 계산 압력을 주는 패키지를 추가 하는 경우 성능이 저하 됩니다.

  + 강화 된 SQL Server 환경에서는 다음을 방지 해야 할 수 있습니다.
    + 네트워크 액세스가 필요한 패키지
    + 관리자 권한으로 파일 시스템에 액세스 해야 하는 패키지
    + 웹 개발에 사용 되는 패키지 또는 SQL Server 내에서 실행 하 여 이점을 제공 하지 않는 기타 작업

## <a name="install-sqlmlutils-on-the-client-computer"></a>클라이언트 컴퓨터에 sqlmlutils 설치

**Sqlmlutils**를 사용 하려면 먼저 SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에 설치 해야 합니다.

1. 에서 https://github.com/Microsoft/sqlmlutils/tree/master/Python/dist 클라이언트 컴퓨터로 최신 **sqlmlutils** zip 파일을 다운로드 합니다. 파일의 압축을 풀어야 합니다.

1. **명령 프롬프트** 를 열고 다음 명령을 실행 하 여 **sqlmlutils** 패키지를 설치 합니다. 전체 경로를 다운로드 한 **sqlmlutils** zip 파일로 대체 합니다 .이 예제에서는 다운로드 한 파일이 인 `c:\temp\sqlmlutils_0.6.0.zip`것으로 가정 합니다.

   ```console
   pip install --upgrade --upgrade-strategy only-if-needed c:\temp\sqlmlutils_0.6.0.zip
   ```

## <a name="add-a-python-package-on-sql-server"></a>SQL Server에 Python 패키지 추가

다음 예제에서는 SQL Server에 [텍스트 도구](https://pypi.org/project/text-tools/) 패키지를 추가 합니다.

### <a name="add-the-package-online"></a>온라인으로 패키지 추가

SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에서 인터넷에 액세스할 수 있는 경우 **sqlmlutils** 를 사용 하 여 인터넷을 통해 **텍스트 도구** 패키지와 모든 종속성을 찾은 다음 원격으로 SQL Server 인스턴스에 패키지를 설치할 수 있습니다.

1. 클라이언트 컴퓨터에서 **python** 또는 python 환경을 엽니다.

1. 다음 명령을 사용 하 여 **텍스트 도구** 패키지를 설치 합니다. 사용자 고유의 SQL Server 데이터베이스 연결 정보를 대체 합니다.

   ```python
   import sqlmlutils
   connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
   sqlmlutils.SQLPackageManager(connection).install("text-tools")
   ```

### <a name="add-the-package-offline"></a>오프 라인으로 패키지 추가

SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에서 인터넷에 연결 되지 않은 경우 인터넷에 액세스할 수 있는 컴퓨터에서 **pip** 를 사용 하 여 패키지 및 모든 종속 패키지를 로컬 폴더에 다운로드할 수 있습니다. 그런 다음 패키지를 오프 라인으로 설치할 수 있는 클라이언트 컴퓨터에 폴더를 복사 합니다.

#### <a name="on-a-computer-with-internet-access"></a>인터넷에 액세스할 수 있는 컴퓨터의 경우

1. **명령 프롬프트** 를 열고 다음 명령을 실행 하 여 **텍스트 도구** 패키지가 포함 된 로컬 폴더를 만듭니다. 이 예제에서는 폴더 `c:\temp\text-tools`를 만듭니다.

   ```command
   pip download text-tools -d c:\temp\text-tools
   ```

1. 클라이언트 컴퓨터에 폴더를 복사 합니다. `text-tools` 다음 예에서는로 `c:\temp\packages\text-tools`복사 했다고 가정 합니다.

#### <a name="on-the-client-computer"></a>클라이언트 컴퓨터에서

**Sqlmlutils** 를 사용 하 여 **pip** 가 만든 로컬 폴더에 있는 각 패키지 (whl 파일)를 설치 합니다. 패키지를 설치 하는 순서는 중요 하지 않습니다.

이 예제에서 **텍스트 도구** 에는 종속성이 없으므로 설치할 `text-tools` 폴더의 파일이 하나 뿐입니다. 이와 대조적으로 **scikit** 와 같은 패키지에는 11 개의 종속성이 있으므로 폴더에 12 개의 파일 ( **scikit 플롯** 패키지 및 11 개의 종속 패키지)을 찾아 각각 설치 합니다.

다음 Python 스크립트를 실행 합니다. 사용자 고유의 SQL Server 데이터베이스 연결 정보 및 패키지의 실제 파일 경로와 이름을 대체 합니다. 폴더의 각 패키지 파일에 대해 문을반복합니다.`sqlmlutils.SQLPackageManager`

```python
import sqlmlutils
connection = sqlmlutils.ConnectionInfo(server="yourserver", database="yourdatabase", uid="yoursqluser", pwd="yoursqlpassword")
sqlmlutils.SQLPackageManager(connection).install("c:/temp/packages/text-tools/text_tools-1.0.0-py3-none-any.whl")
```

## <a name="use-the-package-in-sql-server"></a>SQL Server에서 패키지 사용

이제 SQL Server의 Python 스크립트에서 패키지를 사용할 수 있습니다. 예를 들어 다음과 같은 가치를 제공해야 합니다.

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

## <a name="remove-the-package-from-sql-server"></a>SQL Server에서 패키지를 제거 합니다.

**텍스트 도구** 패키지를 제거 하려면 이전에 정의한 것과 동일한 연결 변수를 사용 하 여 클라이언트 컴퓨터에서 다음 Python 명령을 사용 합니다.

```python
sqlmlutils.SQLPackageManager(connection).uninstall("text-tools")
```

## <a name="see-also"></a>참조

+ SQL Server Machine Learning Services에 설치 된 Python 패키지에 대 한 정보를 보려면 [python 패키지 정보 가져오기](../package-management/python-package-information.md)를 참조 하세요.

+ SQL Server Machine Learning Services에서 R 패키지를 설치 하는 방법에 대 한 자세한 내용은 [SQL Server에 새 r 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조 하세요.
