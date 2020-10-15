---
title: Python 패키지 정보 가져오기
description: SQL Server Machine Learning Services에서 버전 및 설치 위치를 포함하여 설치된 Python 패키지에 대한 정보를 가져오는 방법을 알아봅니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/03/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions'
ms.openlocfilehash: 6513c3333bb852b0d899b785073f4ecbc31daab3
ms.sourcegitcommit: afb02c275b7c79fbd90fac4bfcfd92b00a399019
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2020
ms.locfileid: "91956957"
---
# <a name="get-python-package-information"></a>Python 패키지 정보 가져오기

[!INCLUDE [SQL Server 2017 SQL MI](../../includes/applies-to-version/sqlserver2017-asdbmi.md)]

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions"
이 문서에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md) 및 [빅 데이터 클러스터](../../big-data-cluster/machine-learning-services.md)에서 버전 및 설치 위치를 포함하여 설치된 Python 패키지에 대한 정보를 가져오는 방법을 설명합니다. 예제 Python 스크립트는 설치 경로 및 버전과 같은 패키지 정보를 나열하는 방법을 보여 줍니다.
::: moniker-end
::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
이 문서에서는 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)에서 버전 및 설치 위치를 포함하여 설치된 Python 패키지에 대한 정보를 가져오는 방법을 설명합니다. 예제 Python 스크립트는 설치 경로 및 버전과 같은 패키지 정보를 나열하는 방법을 보여 줍니다.
::: moniker-end
::: moniker range="=azuresqldb-mi-current||=sqlallproducts-allversions"
이 문서에서는 [Azure SQL Managed Instance Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)에서 버전 및 설치 위치를 포함하여 설치된 Python 패키지에 대한 정보를 가져오는 방법을 설명합니다. 예제 Python 스크립트는 설치 경로 및 버전과 같은 패키지 정보를 나열하는 방법을 보여 줍니다.
::: moniker-end

## <a name="default-python-library-location"></a>기본 Python 라이브러리 위치

SQL Server를 사용하여 기계 학습을 설치하는 경우 설치하는 각 언어의 인스턴스 수준에서 단일 패키지 라이브러리가 생성됩니다. 인스턴스 라이브러리는 SQL Server에 등록된 보안 폴더입니다.

SQL Server의 데이터베이스 내에서 실행되는 모든 스크립트나 코드는 인스턴스 라이브러리에서 함수를 로드해야 합니다. SQL Server는 다른 라이브러리에 설치된 패키지에 액세스할 수 없습니다. 이것은 원격 클라이언트에도 적용됩니다. 서버 컴퓨팅 컨텍스트에서 실행되는 모든 Python 코드는 인스턴스 라이브러리에 설치된 패키지만 사용할 수 있습니다.
서버 자산을 보호하려면 컴퓨터 관리자만 기본 인스턴스 라이브러리를 수정할 수 있습니다.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Python에 대한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`

여기서는 기본 SQL 인스턴스인 MSSQLSERVER를 가정합니다. SQL Server가 사용자 정의 명명된 인스턴스로 설치된 경우에는 지정된 이름이 대신 사용됩니다.
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Python에 대한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`

여기서는 기본 SQL 인스턴스인 MSSQLSERVER를 가정합니다. SQL Server가 사용자 정의 명명된 인스턴스로 설치된 경우에는 지정된 이름이 대신 사용됩니다.
::: moniker-end

다음 SQL 명령을 실행하여 외부 스크립트를 사용하도록 설정합니다.

```sql
sp_configure 'external scripts enabled', 1;
RECONFIGURE WITH override;
```

현재 인스턴스의 기본 라이브러리를 확인하려면 다음 SQL 문을 실행합니다. 이 예제에서는 Python `sys.path` 변수에 포함된 폴더 목록을 반환합니다. 이 목록에는 현재 디렉터리와 표준 라이브러리 경로가 포함됩니다.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

변수 `sys.path` 및 이 변수가 모듈에 대한 인터프리터의 검색 경로를 설정하는 데 사용되는 방법에 대한 자세한 내용은 [모듈 검색 경로](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)를 참조하세요.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
> [!NOTE]
> **pip** 또는 유사한 메서드를 사용하여 SQL 패키지 라이브러리에 직접 Python 패키지를 설치하지 마세요. 대신 **sqlmlutils**를 사용하여 SQL 인스턴스에 패키지를 설치합니다. 자세한 내용은 [sqlmlutils를 사용하여 Python 패키지 설치](install-additional-python-packages-on-sql-server.md)를 참조하세요.
::: moniker-end

## <a name="default-microsoft-python-packages"></a>기본 Microsoft Python 패키지

설치하는 동안 Python 기능을 선택하면 다음 Microsoft Python 패키지가 SQL Server Machine Learning Services와 함께 설치됩니다.

| 패키지 | 버전 |  Description |
| ---------|---------|--------------|
| [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.4.7 | 데이터 가져오기 및 변환, 모델링, 시각화 및 분석을 위해 원격 컴퓨팅 컨텍스트, 스트리밍, rx 함수의 병렬 실행에 사용됩니다. |
| [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.4.7 | Python에서 기계 학습 알고리즘을 추가합니다. |

포함된 Python 버전에 대한 자세한 내용은 [Python 및 R 버전](../sql-server-machine-learning-services.md#versions)을 참조하세요.

### <a name="component-upgrades"></a>구성 요소 업그레이드

기본적으로 Python 패키지는 서비스 팩 및 누적 업데이트를 통해 새로 고쳐집니다. 핵심 Python 구성 요소의 추가 패키지 및 전체 버전 업그레이드는 제품 업그레이드를 통해서 또는 Python 지원을 Microsoft Machine Learning Server에 바인딩하는 경우에만 가능합니다.

자세한 내용은 [SQL Server에서 R 및 Python 구성 요소업그레이드](../install/upgrade-r-and-python.md)를 참조하세요.

## <a name="default-open-source-python-packages"></a>기본 오픈 소스 Python 패키지

설치하는 동안 Python 언어 옵션을 선택하면 Anaconda 4.2 배포판(Python 3.5 이상)이 설치됩니다. Python 코드 라이브러리 외에도 표준 설치에는 샘플 데이터, 단위 테스트 및 샘플 스크립트가 포함되어 있습니다.

> [!IMPORTANT]
> SQL Server 설치 프로그램을 통해 설치된 Python 버전을 웹의 최신 버전으로 수동으로 덮어쓰지 않도록 합니다. Microsoft Python 패키지는 특정 버전의 Anaconda을 기준으로 합니다. 설치를 수정하면 불안정해질 수 있습니다.

## <a name="list-all-installed-python-packages"></a>설치된 모든 Python 패키지 나열

다음 예제 스크립트는 SQL Server 인스턴스에 설치된 모든 Python 패키지 목록을 표시합니다.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
import pkg_resources
import pandas as pd
installed_packages = pkg_resources.working_set
installed_packages_list = sorted(["%s==%s" % (i.key, i.version) for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

## <a name="find-a-single-python-package"></a>단일 Python 패키지 찾기

Python 패키지를 설치하고 특정 SQL Server 인스턴스에서 사용할 수 있도록 하려면 저장 프로시저를 실행하여 패키지를 찾아서 메시지를 반환할 수 있습니다.

예를 들어, 다음 코드는 `scikit-learn` 패키지를 찾습니다.
패키지가 발견되면 코드에서 패키지 버전을 출력합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pkg_name = "scikit-learn"
try:
    version = pkg_resources.get_distribution(pkg_name).version
    print("Package " + pkg_name + " is version " + version)
except:
    print("Package " + pkg_name + " not found")
'
```

결과:

```text
STDOUT message(s) from external script: Package scikit-learn is version 0.20.2
```

<a name="bkmk_SQLPythonVersion"></a>
## <a name="view-the-version-of-python"></a>Python 버전 보기

다음 예제 코드는 SQL Server 인스턴스에 설치된 Python 버전을 반환합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import sys
print(sys.version)
'
```

## <a name="next-steps"></a>다음 단계

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
+ [Python 도구를 사용하여 패키지 설치](install-python-packages-standard-tools.md)
::: moniker-end
::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15||=azuresqldb-mi-current||=sqlallproducts-allversions"
+ [sqlmlutils를 사용하여 새 Python 패키지 설치](install-additional-r-packages-on-sql-server.md)
::: moniker-end