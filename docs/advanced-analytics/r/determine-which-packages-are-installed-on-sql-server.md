---
title: SQL Server 기계 학습에서 Python 및 R 패키지 정보를 가져올 | Microsoft Docs
description: R 및 Python 패키지 버전을 확인 하 고 설치 결과 확인 컴퓨터 학습 서비스 또는 SQL Server R Services에 설치 된 패키지 목록을 가져올 수 있습니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 85ea4658ca8b60fc24d7e4f7849de1655eab6082
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34707891"
---
#  <a name="get-r-and-python-package-information"></a>R 및 Python 패키지 정보 가져오기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

실행 중인 코드에 사용 하는 예상된 환경 Python 또는 올바른 작업 영역에서 r을 확인 하는 경우가 때 사용 하는 여러 환경 또는 설치 된 R, Python, 있습니다. 예를 들어, 기계 학습을 통해 구성 요소를 업그레이드 한 경우 [바인딩](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md), R 라이브러리 경로 기본값과 다른 폴더에 있을 수 있습니다. 또한, R 클라이언트나의 독립 실행형 서버 인스턴스를 설치한 경우 컴퓨터에 여러 개의 R 라이브러리 될 수 있습니다.

이 문서에서 R 및 Python 스크립트 예제는 경로 및 버전의 SQL Server에서 사용 되는 패키지를 가져오는 방법을 보여 줍니다.

## <a name="get-the-r-library-location"></a>R 라이브러리 위치를 가져옵니다.

모든 버전의 SQL Server에 대 한 확인 하려면 다음 문을 실행 하는 [R 기본 패키지 라이브러리](installing-and-managing-r-packages.md) 현재 인스턴스에 대 한 합니다.

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

사용할 수 있습니다 [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 최신 버전의 SQL Server 2017 컴퓨터 학습 서비스에서 RevoScaleR 또는 [R Services 업그레이드 R에서 최소 RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다. 이 저장된 프로시저 인스턴스 라이브러리의 경로 및 SQL Server에서 사용 하는 RevoScaleR의 버전을 반환 합니다.

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
> [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 함수는 로컬 컴퓨터에만 실행할 수 있습니다. 함수는 원격 연결에 대 한 라이브러리 경로 반환할 수 없습니다.

**결과**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Python 라이브러리 위치를 가져옵니다.

에 대 한 **Python** SQL Server 2017 년 1에서 현재 인스턴스에 대 한 기본 라이브러리를 확인 하려면 다음 문을 실행 합니다. 이 예제는 Python에 포함 된 폴더의 목록을 반환 `sys.path` 변수입니다. 현재 디렉터리 및 표준 라이브러리 경로 목록에 포함 됩니다.

```sql
EXECUTE sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

**결과**

```text
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\python35.zip
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\DLLs
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Sphinx-1.5.4-py3.5.egg
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\win32\lib
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\Pythonwin
C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\lib\site-packages\setuptools-27.2.0-py3.5.egg
```

변수에 대 한 자세한 내용은 `sys.path` 및 모듈에 대 한 인터프리터의 검색 경로 설정 하려면 사용 하는 방법 참조는 [Python 설명서](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>모든 패키지를 나열 합니다.

현재 설치 된 패키지의 전체 목록을 얻을 수 있는 여러 가지가 있습니다. Sp_execute_external_script에서 패키지 목록을 명령 실행의 장점 중 하나는 인스턴스 라이브러리에 설치 된 패키지를 가져오려는 보장입니다.

### <a name="r"></a>R

다음 예제에서는 R 함수를 사용 하 여 `installed.packages()` 에 [!INCLUDE [tsql](..\..\includes\tsql-md.md)] 저장 프로시저는 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지의 행렬을 가져옵니다. 이 스크립트는 설명 파일에 패키지 이름 및 버전 필드를 반환, 이름만 반환 됩니다.

```SQL
EXECUTE sp_execute_external_script
  @language=N'R',
  @script = N'str(OutputDataSet);
  packagematrix <- installed.packages();
  Name <- packagematrix[,1];
  Version <- packagematrix[,3];
  OutputDataSet <- data.frame(Name, Version);',
  @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250), PackageVersion nvarchar(max) ))
```

자세한 선택적에 대 한 정보 및 R 패키지 DESCRIPTION 필드에 대 한 기본 필드를 참조 하세요. [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)합니다.

### <a name="python"></a>Python

`pip` 모듈 기본적으로 설치 되 고 표준 Python 지 원하는 것 외에도 목록 설치 패키지에 대 한 여러 작업을 지원 합니다. 실행할 수 있습니다 `pip` Python에서 명령 프롬프트에서 물론, 하지만 또한 함수를 호출할 수 일부 pip에서 `sp_execute_external_script`합니다.

```sql
EXECUTE sp_execute_external_script 
  @language = N'Python', 
  @script = N'
  import pip
  import pandas as pd
  installed_packages = pip.get_installed_distributions()
  installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
  df = pd.DataFrame(installed_packages_list)
  OutputDataSet = df'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

실행 하는 경우 `pip` 명령줄에서 여러 가지 다른 유용한 함수가: `pip list` 반면, 설치 된 모든 패키지를 가져옵니다 `pip freeze` 나열 하 여 설치 된 패키지 `pip`, 및 패키지 자체 pip를 나열 하지 않습니다 에 따라 다릅니다. 사용할 수도 있습니다 `pip freeze` 종속성 파일을 생성 합니다.

## <a name="find-a-single-package"></a>단일 패키지 찾기

패키지를 설치 하 고 특정 SQL Server 인스턴스를 사용할 수 있는지 확인 하려는 경우에 패키지를 로드 하 고 메시지에만 반환 하려면 다음 저장된 프로시저 호출을 실행할 수 있습니다.

### <a name="r"></a>R

이 예제에서는 찾아서 사용할 수 있는 경우 RevoScaleR 라이브러리를 로드 합니다.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 패키지를 찾을 경우 메시지가 반환 됩니다: "명령이 완료 되었습니다."

+ 패키지를 찾거나 로드할 수 없습니다, 하는 경우 텍스트를 포함 하는 오류가 발생 합니다. "라는 'MissingPackageName' 없는 패키지는"

### <a name="python"></a>Python

Python에서 Python에 대 한 해당 확인을 수행할 수 있으며 셸를 사용 하 여 `conda` 또는 `pip` 명령입니다. 또는 저장된 프로시저에서이 문을 실행 합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'Python',
  @script = N'
  import pip
  import pkg_resources
  pckg_name = "revoscalepy"
  pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
  installed_pckg = pckgs.query(''key == @pckg_name'')
  print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")'
```

## <a name="get-package-information-in-r-and-python-tools"></a>R 및 Python tools에서 패키지 정보 가져오기

모든 이전 명령이 SQL Server Management Studio (SSMS)와 같은 도구를 사용 하는 것을 가정 합니다. R 및 Python 도구를 사용 하 여 원하는 경우 다음 지침에서는 Python 또는 R 명령줄에서 라이브러리 및 패키지 정보를 가져올 방법을 설명 합니다.

### <a name="r-commands"></a>R 명령

R에 대 한 인스턴스 라이브러리는 files\microsoft SQL Server\MSSQL14입니다. MSSQLSERVER\R_SERVICES\library 합니다.

패키지 인스턴스 라이브러리에서 사용 되도록 이러한 위치에서 표준 R 도구를 시작 합니다.

+ \MSSQL14 합니다. R 명령 프롬프트에 대 한 MSSQLSERVER\R_SERVICES\bin\R.exe
+ \MSSQL14 합니다. R 콘솔 응용 프로그램에 대 한 MSSQLSERVER\R_SERVICES\bin\x64\Rgui.exe

패키지 정보를 가져올 수는 표준 R 명령 또는 RevoScaleR 명령을 사용할 수 있습니다. RevoScaleR 패키지는 자동으로 로드 됩니다. 

RevoScaleR 패키지 정보를 반환 합니다.

    > print(Revo.version)

모든 설치 된 패키지 목록을 반환 합니다.

    > installed.packages()

R:의 버전을 반환

    > packageDescription("base")

### <a name="python-commands"></a>Python 명령

Python 지원은 SQL Server 2017만 합니다. Python에 대 한 인스턴스 라이브러리는 files\microsoft SQL Server\MSSQL14입니다. MSSQLSERVER\PYTHON_SERVICES\ 합니다.

패키지 인스턴스 라이브러리에서 사용 되도록이 위치에서 Python 명령 창을 엽니다.

+ \MSSQL14 합니다. MSSQLSERVER\PYTHON_SERVICES\Python.exe

대화형 도움말을 엽니다.

    > help()

패키지 내용, 버전 및 파일 위치를 가져오는 도움말 프롬프트에서 모듈 이름 입력:

    help> revoscalepy

<a name="pip-conda"></a>

### <a name="python-package-managers-pip-and-conda"></a>Python 패키지 관리자 (Pip 및 Conda)

패키지 관리를 위한 Python 도구를 포함 하는 anaconda 합니다. 기본 인스턴스, Pip, Conda, 및 기타 도구가 \program files\microsoft SQL Server\MSSQL14 찾을 수 있습니다. MSSQLSERVER\PYTHON_SERVICES\Scripts 합니다.

SQL Server 설치 프로그램에서 Pip 또는 필수적이 지 않은 실행 파일 경로에서 유지 Conda 시스템 경로 및 프로덕션 SQL Server 인스턴스에서 가장 좋은 방법은 추가 되지 않습니다. 그러나 개발 및 테스트 환경에 대 한 명령에서 어느 위치에서 Pip와 Conda을 실행 하려면 시스템 PATH 환경 변수를 스크립트 폴더를 추가할 수 있습니다.

1. C:\Program Files\Microsoft SQL Server\MSSQL14로 이동 합니다. MSSQLSERVER\PYTHON_SERVICES\Scripts

1. 마우스 오른쪽 단추로 클릭 **conda.exe** > **관리자 권한으로 실행**, 입력 `conda list` 현재 환경에 설치 된 패키지 목록을 반환 합니다.

1. 마찬가지로, 마우스 오른쪽 단추로 클릭 **pip.exe** > **관리자 권한으로 실행**, 입력 `pip list` 동일한 정보를 반환 합니다. 


## <a name="next-steps"></a>다음 단계

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)