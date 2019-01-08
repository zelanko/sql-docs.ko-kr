---
title: R 및 Python 패키지 정보-SQL Server Machine Learning Services 가져오기
description: R 및 Python 패키지 버전을 확인 하 고 설치를 확인 합니다. SQL Server R Services 또는 Machine Learning 서비스에서 설치 된 패키지 목록을 가져옵니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 47badb15b5f5a2d0eabc63b8fd1be3e83a0caffb
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645372"
---
#  <a name="get-r-and-python-package-information"></a>R 및 Python 패키지 정보 가져오기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

경우에 따라 작업할 때는 여러 환경 또는 R 또는 Python 설치를 확인 해야 실행 하는 코드를 사용 하는 예상된 환경 Python 또는 올바른 작업 영역 r 예를 들어, 기계 학습을 통해 구성 요소를 업그레이드 한 경우 [바인딩](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md), R 라이브러리 경로 기본값과 다른 폴더에 있을 수 있습니다. 또한 R Client 또는 독립 실행형 서버 인스턴스를 설치한 것이 있으면 R 라이브러리가 여러 개 컴퓨터에.

R 및 Python 스크립트 예제 및이 문서의 경로 및 SQL Server에서 사용 되는 패키지의 버전을 가져오는 방법을 보여 줍니다.

## <a name="get-the-r-library-location"></a>R 라이브러리 위치를 가져옵니다.

SQL Server의 모든 버전을 확인 하려면 다음 문을 실행 합니다 [기본 R 패키지 라이브러리](installing-and-managing-r-packages.md) 현재 인스턴스에 대 한 합니다.

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

사용할 수 있습니다 [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 최신 버전의 SQL Server 2017의 Machine Learning Services에서 RevoScaleR 또는 [R Services에 R을 이상 업그레이드 RevoScaleR 9.0.1](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다. 이 저장된 프로시저 인스턴스 라이브러리의 경로 SQL Server에서 사용 하는 RevoScaleR의 버전을 반환 합니다.

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
> 합니다 [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 함수는 로컬 컴퓨터 에서만 실행할 수 있습니다. 함수는 원격 연결에 대 한 라이브러리 경로 반환할 수 없습니다.

**결과**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Python 라이브러리 위치를 가져옵니다.

에 대 한 **Python** SQL Server 2017의 현재 인스턴스에 대 한 기본 라이브러리를 확인 하려면 다음 문을 실행 합니다. 이 예제에서는 Python에 포함 된 폴더의 목록을 반환 `sys.path` 변수입니다. 목록에는 현재 디렉터리 및 표준 라이브러리 경로 포함합니다.

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

변수에 대 한 자세한 내용은 `sys.path` 모듈에 대 한 인터프리터의 검색 경로 설정 하 되, 참조 및는 [Python 설명서](https://docs.python.org/2/tutorial/modules.html#the-module-search-path)

## <a name="list-all-packages"></a>모든 패키지 목록

현재 설치 된 패키지의 전체 목록을 가져올 수 있는 방법은 여러 가지가 있습니다. Sp_execute_external_script에서 패키지 목록 명령 실행의 장점 중 하나는 인스턴스 라이브러리에 설치 된 패키지를 가져오려면 보장 됩니다.

### <a name="r"></a>R

다음 예제에서는 R 함수 `installed.packages()` 에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저의 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지 매트릭스를 가져옵니다. 이 스크립트는 DESCRIPTION 파일의 패키지 이름 및 버전 필드를 반환, 이름만 반환 됩니다.

```sql
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

자세한 정보는 선택 사항 및 R 패키지 설명 필드에 대 한 기본 필드를 참조 하세요 [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)합니다.

### <a name="python"></a>Python

`pip` 모듈 기본적으로 설치 되 고 표준 Python에서 지 원하는 것 외에도 목록 설치 패키지에 대 한 많은 작업을 지원 합니다. 실행할 수 있습니다 `pip` Python에서 명령 프롬프트, 물론 있지만 함수를 호출할 수 일부 pip에서 `sp_execute_external_script`합니다.

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

실행 하는 경우 `pip` 명령줄에서 가지 다른 유용한 기능을 많이: `pip list` 반면, 설치 된 모든 패키지를 가져옵니다 `pip freeze` 하 여 설치 된 패키지 나열 `pip`, 및 패키지 자체를 pip는 표시 되지 않습니다. 에 따라 달라 집니다. 사용할 수도 있습니다 `pip freeze` 종속성 파일을 생성 합니다.

## <a name="find-a-single-package"></a>단일 패키지 찾기

패키지를 설치 하 고 특정 SQL Server 인스턴스를 사용할 수 있는지 확인 하려고 하는 경우에 패키지를 로드 하 고만 메시지를 반환 하려면 다음 저장된 프로시저 호출을 실행할 수 있습니다.

### <a name="r"></a>R

이 예제에서는 검색 하 고 사용 가능한 경우 RevoScaleR 라이브러리를 로드 합니다.

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 패키지가 없으면 메시지가 반환 됩니다. "명령이 완료 되었습니다."

+ 텍스트가 포함 된 오류가 표시 된 패키지를 찾거나 로드할 수 없습니다, 하는 경우: "'MissingPackageName' 라는 패키지가 없음 이"

### <a name="python"></a>Python

Python에서 Python에 대 한 해당 검사를 수행할 수 있습니다 사용 하 여 셸 `conda` 또는 `pip` 명령입니다. 또는 저장된 프로시저에서이 명령문을 실행 합니다.

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

<a name="get-package-vers"></a>

## <a name="get-package-version"></a>패키지 버전 가져오기

R을 가져올 수 있습니다 및 Python 패키지 Management Studio를 사용 하 여 버전 정보입니다.

### <a name="r-package-version"></a>R 패키지 버전

이 문은 RevoScaleR 패키지 버전 및 기본 R 버전을 반환합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Python 패키지 버전

이 문은 revoscalepy 패키지 버전 및 Python 버전을 반환합니다.

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

+ [새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)