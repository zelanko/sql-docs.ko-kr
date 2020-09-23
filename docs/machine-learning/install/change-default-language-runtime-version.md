---
title: 기본 R 또는 Python 언어 런타임 버전 변경
description: SQL Server 2017 Machine Learning Services 또는 SQL Server R Services에서 SQL 인스턴스에 사용되는 R 또는 Python 런타임의 기본 버전을 변경하는 방법을 알아봅니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 08/14/2020
ms.topic: how-to
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: d730ead0a11c240284ecb9a902a90eaedc5b1bb6
ms.sourcegitcommit: 5f658b286f56001b055a8898d97e74906516dc99
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009367"
---
# <a name="change-the-default-r-or-python-language-runtime-version"></a>기본 R 또는 Python 언어 런타임 버전 변경

[!INCLUDE[SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

이 문서에서는 [SQL Server 2016 R Services](../r/sql-server-r-services.md) 또는 [SQL Server 2017 Machine Learning Services](../sql-server-machine-learning-services.md)에 사용되는 R 또는 Python의 기본 버전을 변경하는 방법을 설명합니다.

다음은 다양한 SQL Server 버전에 포함된 R 및 Python 런타임의 버전입니다.

| SQL Server 버전 | 서비스 | 누적 업데이트 | R 런타임 버전 | Python 런타임 버전 |
|-|-|-|-|-|
| SQL Server 2016 | R 서비스 | RTM - SP2 CU13 | 3.2.2 | 사용할 수 없음 |
| SQL Server 2016 | R 서비스 | SP2 CU14 이상 | 3.2.2 및 3.5.2 | 사용할 수 없음 |
| SQL Server 2017 | Machine Learning Services | RTM - CU21 | 3.3.3 | 3.5.2 |
| SQL Server 2017 | Machine Learning Services | CU22 이상 | 3.3.3 및 3.5.2 | 3.5.2 및 3.7.2 |

## <a name="prerequisites"></a>사전 요구 사항

기본 R 또는 Python 언어 런타임 버전을 변경하려면 CU(누적 업데이트)를 설치해야 합니다.

- **SQL Server 2016:** SP(서비스 팩) 2 CU(누적 업데이트) 14 이상
- **SQL Server 2017:** CU(누적 업데이트) 22 이상

최신 누적 업데이트를 다운로드하려면 [Microsoft SQL Server에 대한 최신 업데이트](../../database-engine/install-windows/latest-updates-for-microsoft-sql-server.md)를 참조하세요.

> [!NOTE]
> SQL Server를 새로 설치하여 누적 업데이트를 통합 설치하는 경우 최신 버전의 R 및 Python 런타임만 설치됩니다.

## <a name="change-r-runtime-version"></a>R 런타임 버전 변경

SQL Server 2016 또는 2017에 대해 위의 누적 업데이트 중 하나를 설치한 경우 SQL 인스턴스에 여러 버전의 R이 있을 수 있습니다. 각 버전은 인스턴스 폴더의 `R_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* 라는 하위 폴더에 들어갑니다(원래 설치 폴더에는 폴더 이름에 버전 번호가 추가되지 않을 수도 있음).

R 3.5를 포함하는 CU를 설치하는 경우 새 `R_SERVICES` 폴더는 다음과 같습니다.

- SQL Server 2016: `C:\Program Files\Microsoft SQL Server\MSSQL13.<INSTANCE_NAME>\R_SERVICES.3.5`
- SQL Server 2017: `C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\R_SERVICES.3.5`

각 SQL 인스턴스는 이러한 버전 중 하나를 기본 버전의 R로 사용합니다. **RegisterRext.exe** 명령줄 유틸리티를 사용하여 기본 버전을 변경할 수 있습니다. 이 유틸리티는 각 SQL 인스턴스의 R 폴더 아래에 있습니다.

*&lt;SQL instance path&gt;* \R_SERVICES.n.n\library\RevoScaleR\rxLibs\x64\RegisterRext.exe

> [!Note]
> 이 문서에서 설명하는 기능은 SQL CU에 포함된 **RegisterRext.exe**의 복사본으로만 수행할 수 있습니다. 원래 SQL 설치와 함께 제공된 복사본은 사용하지 마세요.

R 런타임 버전을 변경하려면 다음 명령줄 인수를 **RegisterRext.exe**에 전달합니다.

- `/configure` - 필수. 기본 R 버전을 구성하는 것임을 지정합니다.

- `/instance:`*&lt;instance name&gt;* - 선택 사항. 구성하려는 인스턴스입니다. 지정하지 않으면 기본 인스턴스가 구성됩니다.

- `/rhome:`*&lt;path to the R_SERVICES[n.n] folder&gt;* - 선택 사항. 기본 R 버전으로 설정하려는 런타임 버전 폴더의 경로입니다.

  /rhome을 지정하지 않으면 구성된 경로는 **RegisterRext.exe**가 있는 경로입니다.

### <a name="examples"></a>예

SQL Server 2016 및 2017에서 R 런타임 버전을 변경하는 방법에 대한 예제는 다음과 같습니다.

#### <a name="change-r-runtime-version-in-sql-server-2016"></a>SQL Server 2016에서 R 런타임 버전 변경

예를 들어 SQL Server 2016에서 **R 3.5**를 인스턴스 MSSQLSERVER01에 대한 기본 버전 R로 구성하려면 다음을 수행합니다.

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

#### <a name="change-r-runtime-version-in-sql-server-2017"></a>SQL Server 2017에서 R 런타임 버전 변경

예를 들어 SQL Server 2017에서 **R 3.5**를 인스턴스 MSSQLSERVER01에 대한 기본 버전 R로 구성하려면 다음을 수행합니다.

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5\library\RevoScaleR\rxLibs\x64"

.\RegisterRext.exe /configure /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\R_SERVICES.3.5" /instance:MSSQLSERVER01
```

이 예제에서는 **RegisterRext.exe**가 있는 폴더와 동일한 폴더를 지정하기 때문에 `/rhome` 인수를 포함할 필요가 없습니다.

## <a name="change-python-runtime-version"></a>Python 런타임 버전 변경

SQL Server 2017에 CU22 이상을 설치한 경우 SQL 인스턴스에 여러 버전의 Python이 있을 수 있습니다. 각 버전은 인스턴스 폴더의 `PYTHON_SERVICES.`*&lt;major&gt;* . *&lt;minor&gt;* 라는 하위 폴더에 들어갑니다(원래 설치 폴더에는 폴더 이름에 버전 번호가 추가되지 않을 수도 있음).

예를 들어 Python 3.7을 포함하는 CU를 설치하는 경우 새 `PYTHON_SERVICES` 폴더가 만들어집니다.

`C:\Program Files\Microsoft SQL Server\MSSQL14.<INSTANCE_NAME>\PYTHON_SERVICES.3.7`  

각 SQL 인스턴스는 이러한 버전 중 하나를 기본 버전의 Python으로 사용합니다. **RegisterRExt.exe** 명령줄 유틸리티를 사용하여 기본 버전을 변경할 수 있습니다. 이 유틸리티는 각 SQL 인스턴스의 Python 폴더 아래에 있습니다.

*&lt;SQL instance path&gt;* `\PYTHON_SERVICES.n.n\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.exe`

> [!Note]
> 이 문서에서 설명하는 기능은 SQL CU에 포함된 **RegisterRExt.exe**의 복사본으로만 수행할 수 있습니다. 원래 SQL 설치와 함께 제공된 복사본은 사용하지 마세요.

Python 런타임 버전을 변경하려면 다음 명령줄 인수를 **RegisterRext.exe**에 전달합니다.

- `/configure` - 필수. 기본 Python 버전을 구성하는 것임을 지정합니다.

- `/python` - 기본 Python 버전을 구성하는 것임을 지정합니다. `/pythonhome`을 지정하는 경우 선택 사항입니다.

- `/instance:`*&lt;instance name&gt;* - 선택 사항. 구성하려는 인스턴스입니다. 지정하지 않으면 기본 인스턴스가 구성됩니다.

- `/pythonhome:`*&lt;path to the PYTHON_SERVICES[n.n] folder&gt;* - 선택 사항. 기본 Python 버전으로 설정하려는 런타임 버전 폴더의 경로입니다.

  /pythonhome을 지정하지 않으면 구성된 경로는 **RegisterRExt.exe**가 있는 경로입니다.

### <a name="example"></a>예제

예를 들어 SQL Server 2017에서 **Python 3.7**을 인스턴스 MSSQLSERVER01에 대한 기본 버전 Python으로 구성하려면 다음을 수행합니다.

```cmd
cd "C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7\Lib\site-packages\revoscalepy\rxLibs"

.\RegisterRext.exe /configure /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

이 예제에서는 **RegisterRext.exe**가 있는 폴더와 동일한 폴더를 지정하기 때문에 `/pythonhome` 인수를 포함할 필요가 없습니다.

## <a name="remove-a-runtime-version"></a>런타임 버전 제거

R 또는 Python의 특정 버전을 제거하려면 **RegisterRExt.exe**에서 앞서 설명한 `/rhome`, `/pythonhome` 및 `/instance` 인수를 `/cleanup` 명령줄 인수와 함께 사용합니다.

예를 들어 MSSQLSERVER01에서 **R 3.2** 폴더를 제거하려면 다음을 수행합니다.

```cmd
.\RegisterRext.exe /cleanup /rhome:"C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER01\R_SERVICES" /instance:MSSQLSERVER01
```

예를 들어 MSSQLSERVER01에서 **Python 3.7** 폴더를 제거하려면 다음을 수행합니다.

```cmd
.\RegisterRExt.exe /cleanup /python /pythonhome:"C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER01\PYTHON_SERVICES.3.7" /instance:MSSQLSERVER01
```

**RegisterRext.exe**는 지정된 R 런타임의 정리를 확인하는 메시지를 표시합니다.

> *지정된 런타임을 설치된 모든 패키지와 함께 영구적으로 삭제하시겠습니까? \[예(Y)/아니요(N)/기본값(예)\]:*

확인하려면 `Y`로 응답하거나 Enter 키를 누릅니다. 또는 `/cleanup` 옵션과 함께 `/y` 또는 `/Yes`를 전달하여 이 프롬프트를 건너뛸 수 있습니다.

> [!NOTE]
> 기본값으로 구성되지 않고 현재 **RegisterRext.exe**를 실행하는 데 사용되지 않는 버전만 제거할 수 있습니다.

## <a name="next-steps"></a>다음 단계

- [R 패키지 정보 가져오기](../package-management/r-package-information.md)
- [Python 패키지 정보 가져오기](../package-management/python-package-information.md)
- [R 도구를 사용하여 패키지 설치](../package-management/install-r-packages-standard-tools.md)
- [Python 도구를 사용하여 패키지 설치](../package-management/install-python-packages-standard-tools.md)
