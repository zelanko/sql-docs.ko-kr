---
title: Python 패키지 정보 가져오기
description: SQL Server Machine Learning Services에서 버전 및 설치 위치를 포함 하 여 설치 된 Python 패키지에 대 한 정보를 가져오는 방법에 대해 알아봅니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/22/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1aa12da4a138ea8f292fa8b64db00456d3c35fe3
ms.sourcegitcommit: 01c8df19cdf0670c02c645ac7d8cc9720c5db084
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000444"
---
# <a name="get-python-package-information"></a>Python 패키지 정보 가져오기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server Machine Learning Services에서 버전 및 설치 위치를 포함 하 여 설치 된 Python 패키지에 대 한 정보를 가져오는 방법을 설명 합니다. 예제 Python 스크립트는 설치 경로 및 버전과 같은 패키지 정보를 나열 하는 방법을 보여 줍니다.

## <a name="default-python-library-location"></a>기본 Python 라이브러리 위치

SQL Server를 사용 하 여 기계 학습을 설치 하는 경우 설치 하는 각 언어에 대 한 인스턴스 수준에서 단일 패키지 라이브러리가 생성 됩니다. Windows에서 인스턴스 라이브러리는 SQL Server에 등록 된 보안 폴더입니다.

SQL Server에서 데이터베이스 내에서 실행 되는 모든 스크립트나 코드는 인스턴스 라이브러리에서 함수를 로드 해야 합니다. 다른 라이브러리에 설치 된 패키지에는 액세스할 수 SQL Server. 이는 원격 클라이언트에도 적용 됩니다. 서버 계산 컨텍스트에서 실행 되는 모든 Python 코드는 인스턴스 라이브러리에 설치 된 패키지만 사용할 수 있습니다.
서버 자산을 보호 하려면 컴퓨터 관리자만 기본 인스턴스 라이브러리를 수정할 수 있습니다.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
Python에 대 한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
Python에 대 한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES`
::: moniker-end

여기서는 기본 SQL 인스턴스인 MSSQLSERVER를 가정 합니다. SQL Server 사용자 정의 명명 된 인스턴스로 설치 된 경우에는 지정 된 이름이 대신 사용 됩니다.

다음 문을 실행 하 여 현재 인스턴스의 기본 라이브러리를 확인 합니다. 이 예에서는 Python `sys.path` 변수에 포함 된 폴더 목록을 반환 합니다. 이 목록에는 현재 디렉터리와 표준 라이브러리 경로가 포함 됩니다.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

변수에 대 한 자세한 내용 및 `sys.path` 변수를 사용 하 여 모듈의 인터프리터 검색 경로를 설정 하는 방법에 대 한 자세한 내용은 [모듈 검색 경로](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)를 참조 하세요.

## <a name="default-python-packages"></a>기본 Python 패키지

설치 하는 동안 Python 기능을 선택 하면 다음 Python 패키지가 SQL Server Machine Learning Services 설치 됩니다.

| 패키지 | 버전 |  설명 |
| ---------|---------|--------------|
| [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) | 9.2 | 데이터 가져오기 및 변환, 모델링, 시각화 및 분석을 위해 원격 계산 컨텍스트, 스트리밍, rx 함수의 병렬 실행에 사용 됩니다. |
| [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) | 9.2 | Python에서 기계 학습 알고리즘을 추가 합니다. |

### <a name="component-upgrades"></a>구성 요소 업그레이드

기본적으로 Python 패키지는 서비스 팩 및 누적 업데이트를 통해 새로 고쳐집니다. 핵심 Python 구성 요소에 대 한 추가 패키지 및 전체 버전 업그레이드는 제품 업그레이드 또는 Python 지원을 Microsoft Machine Learning Server에 바인딩하는 경우에만 가능 합니다.

자세한 내용은 [SQL Server에서 R 및 Python 구성 요소 업그레이드](../install/upgrade-r-and-python.md)를 참조 하세요.

## <a name="default-open-source-python-packages"></a>기본 오픈 소스 Python 패키지

설치 하는 동안 Python 언어 옵션을 선택 하면 Anaconda 4.2 배포 (Python 3.5)가 설치 됩니다. Python 코드 라이브러리 외에도 표준 설치에는 샘플 데이터, 단위 테스트 및 샘플 스크립트가 포함 되어 있습니다.

> [!IMPORTANT]
> 설치를 SQL Server 하 여 설치 된 Python 버전을 웹의 새 버전으로 수동으로 덮어쓰지 마십시오. Microsoft Python 패키지는 특정 버전의 Anaconda을 기반으로 합니다. 설치를 수정 하면 불안정 해질 수 있습니다.

## <a name="list-all-installed-python-packages"></a>설치 된 모든 Python 패키지 나열

다음 예제 스크립트는 설치 된 패키지와 해당 버전의 목록을 표시 합니다.

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

Python 패키지를 설치 하 고 특정 SQL Server 인스턴스에 사용할 수 있도록 하려는 경우 저장 프로시저를 실행 하 여 패키지를 로드 하 고 메시지를 반환할 수 있습니다.

예를 들어 다음 코드는 `scikit-learn` 패키지를 찾습니다.
패키지가 있으면 코드에서 "Package scikit-get-help가 설치 되었습니다." 라는 메시지를 반환 합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import pkg_resources
pckg_name = "scikit-learn"
pckgs = pandas.DataFrame([(i.key) for i in pkg_resources.working_set], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
  '
```

<a name="get-package-vers"></a>

다음 예에서는 revoscalepy 패키지 및 Python의 버전을 반환 합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
import revoscalepy
import sys
print(revoscalepy.__version__)
print(sys.version)
  '
```

## <a name="next-steps"></a>다음 단계

+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [R 패키지 정보 가져오기](r-package-information.md)
+ [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)
+ [R 및 Python 자습서](../tutorials/machine-learning-services-tutorials.md)
