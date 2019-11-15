---
title: R 패키지 정보 가져오기
description: SQL Server Machine Learning Services 및 SQL Server R Services에서 설치된 R 패키지에 대한 정보를 가져오는 방법을 알아봅니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 8c3cf3c1debc03c169c585521b8b46dd8b1365c5
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641160"
---
# <a name="get-r-package-information"></a>R 패키지 정보 가져오기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 SQL Server Machine Learning Services 및 SQL Server R Services에서 설치된 R 패키지에 대한 정보를 가져오는 방법을 설명합니다. 예제 R 스크립트는 설치 경로 및 버전과 같은 패키지 정보를 나열하는 방법을 보여 줍니다.

## <a name="default-r-library-location"></a>기본 R 라이브러리 위치

SQL Server를 사용하여 기계 학습을 설치하는 경우 설치하는 각 언어의 인스턴스 수준에서 단일 패키지 라이브러리가 생성됩니다. Windows에서 인스턴스 라이브러리는 SQL Server에 등록된 보안 폴더입니다.

SQL Server의 데이터베이스 내에서 실행되는 모든 스크립트는 인스턴스 라이브러리에서 함수를 로드해야 합니다. SQL Server는 다른 라이브러리에 설치된 패키지에 액세스할 수 없습니다. 이것은 원격 클라이언트에도 적용됩니다. 서버 컴퓨팅 컨텍스트에서 실행되는 모든 R 스크립트는 인스턴스 라이브러리에 설치된 패키지만 사용할 수 있습니다.
서버 자산을 보호하려면 컴퓨터 관리자만 기본 인스턴스 라이브러리를 수정할 수 있습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R에 대한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
R에 대한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
R에 대한 이진 파일의 기본 경로는 다음과 같습니다.

`C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library`
::: moniker-end

여기서는 기본 SQL 인스턴스인 MSSQLSERVER를 가정합니다. SQL Server가 사용자 정의 명명된 인스턴스로 설치된 경우에는 지정된 이름이 대신 사용됩니다.

<!-- I don't think this note is necessary. If you have these other products installed, you'd already know about them.
> [!NOTE]
> If you find other folders having similar subfolder names and files, you probably have a standalone installation of  Microsoft R Server or Machine Learning Server. These server products have different installers and paths: C:\Program Files\Microsoft\R Server\R_SERVER or C:\Program Files\Microsoft\ML SERVER\R_SERVER. For more information, see [Install R Server 9.1 for Windows](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) or [Install Machine Learning Server for Windows](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install).
-->

다음 문을 실행하여 현재 인스턴스에 대한 기본 R 패키지 라이브러리를 확인합니다.

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

다음 문은 [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths)를 사용하여 SQL Server에서 사용되는 인스턴스 라이브러리의 경로 및 RevoScaleR의 버전을 반환합니다.

```sql
EXECUTE sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 함수는 로컬 컴퓨터에서만 실행할 수 있습니다. 이 함수는 원격 연결에 대한 라이브러리 경로를 반환할 수 없습니다.

## <a name="default-r-packages"></a>기본 R 패키지

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"

다음 R 패키지는 SQL Server R Services와 함께 설치됩니다.

|패키지 | 버전 옵션 | 설명 |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 8.0.3 | 데이터 가져오기 및 변환, 모델링, 시각화 및 분석을 위해 원격 컴퓨팅 컨텍스트, 스트리밍, rx 함수의 병렬 실행에 사용됩니다. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 8.0.3 | 저장 프로시저에 R 스크립트를 포함하는 데 사용됩니다. |

::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"

설치하는 동안 R 기능을 선택하면 다음 R 패키지가 SQL Server Machine Learning Services와 함께 설치됩니다.

|패키지 | 버전 옵션 | 설명 |
|---------|---------|-------------|
| [RevoScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)  | 9.2 | 데이터 가져오기 및 변환, 모델링, 시각화 및 분석을 위해 원격 컴퓨팅 컨텍스트, 스트리밍, rx 함수의 병렬 실행에 사용됩니다. |
| [sqlrutils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) | 9.2 | 저장 프로시저에 R 스크립트를 포함하는 데 사용됩니다. |
| [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)| 9.2 | R에서 기계 학습 알고리즘을 추가합니다. | 
| [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) | 9.2 | R에서 MDX 문을 작성하는 데 사용됩니다. |

::: moniker-end

### <a name="component-upgrades"></a>구성 요소 업그레이드

기본적으로 R 패키지는 서비스 팩 및 누적 업데이트를 통해 새로 고쳐집니다. 핵심 R 구성 요소의 추가 패키지 및 전체 버전 업그레이드는 제품 업그레이드를 통해서 또는 R 지원을 Microsoft Machine Learning Server에 바인딩하는 경우에만 가능합니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
또한 구성 요소 업그레이드를 통해 SQL Server 인스턴스에 MicrosoftML 및 olapR 패키지를 추가할 수 있습니다.
::: moniker-end

자세한 내용은 [SQL Server에서 R 및 Python 구성 요소업그레이드](../install/upgrade-r-and-python.md)를 참조하세요.

## <a name="default-open-source-r-packages"></a>기본 오픈 소스 R 패키지

R 지원은 기본 R 함수를 호출하고 추가 오픈 소스 및 타사 패키지를 설치할 수 있도록 오픈 소스 R을 포함합니다. R 언어 지원에는 **base**, **stats**, **utils** 등의 핵심 기능이 포함되어 있습니다. R의 기본 설치에는 **RGui**(경량 대화형 편집기) 및 **RTerm**(R 명령 프롬프트)과 같은 다양한 샘플 데이터 세트 및 표준 R 도구도 포함되어 있습니다.

설치에 포함된 오픈 소스 R 배포판은 [MRO(Microsoft R Open)](https://mran.microsoft.com/open)입니다. MRO는 [Intel Math Kernel Library](https://en.wikipedia.org/wiki/Math_Kernel_Library)와 같은 추가 오픈 소스 패키지를 포함하여 기본 R에 값을 추가합니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Services 설치 프로그램을 사용할 때 MRO에서 제공하는 R 버전은 3.2.2입니다.
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Services 설치 프로그램을 사용할 때 MRO에서 제공하는 R 버전은 3.3.3입니다.
::: moniker-end

> [!IMPORTANT]
> SQL Server 설치 프로그램을 통해 설치된 R 버전을 웹의 최신 버전으로 수동으로 덮어쓰지 않도록 합니다. Microsoft R 패키지는 특정 버전의 R을 기준으로 합니다. 설치를 수정하면 불안정해질 수 있습니다.

## <a name="list-all-installed-r-packages"></a>설치된 모든 R 패키지 나열

다음 예제에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 R 함수 `installed.packages()`를 사용하여 현재 SQL 인스턴스에 대한 R_SERVICES 라이브러리에 설치된 R 패키지 목록을 표시합니다. 이 스크립트는 설명 파일에 패키지 이름 및 버전 필드를 반환합니다.

```sql
EXECUTE sp_execute_external_script
  @language=N'R',
@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
Name <- packagematrix[,1];
Version <- packagematrix[,3];
OutputDataSet <- data.frame(Name, Version);',
@input_data_1 = N'
  '
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

R 패키지 설명 필드의 옵션 및 기본 필드에 대한 자세한 내용은 [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)을 참조하세요.

## <a name="find-a-single-r-package"></a>단일 R 패키지 찾기

R 패키지를 설치하고 특정 SQL Server 인스턴스에서 사용할 수 있도록 하려면 저장 프로시저를 실행하여 패키지를 로드하고 메시지를 반환할 수 있습니다.

예를 들어, 다음 문은 [glue](https://cran.r-project.org/web/packages/glue/) 패키지(사용 가능한 경우)를 찾아서 로드합니다.
패키지를 찾거나 로드할 수 없으면 "'glue'라는 패키지가 없습니다."라는 텍스트를 포함하는 오류 메시지가 표시됩니다.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("glue")'
GO
```

패키지에 대한 자세한 내용을 보려면 `packageDescription`을 확인하세요.
다음 문은 **glue** 패키지에 대한 정보를 반환합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("glue"))
  '
```

## <a name="next-steps"></a>다음 단계

+ [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)
+ [Python 패키지 정보 가져오기](python-package-information.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [R 및 Python 자습서](../tutorials/machine-learning-services-tutorials.md)
