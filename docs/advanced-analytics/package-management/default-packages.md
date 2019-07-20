---
title: R 및 Python 패키지 정보 가져오기
description: R 및 Python 패키지 버전을 확인 하 고 설치를 확인 하 고 SQL Server R Services 또는 Machine Learning Services에 설치 된 패키지 목록을 가져옵니다.
ms.custom: ''
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: dec0fe7147eab6a4b6545decf99e1731d773957c
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68343422"
---
#  <a name="get-r-and-python-package-information"></a>R 및 Python 패키지 정보 가져오기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

여러 환경 또는 R 또는 Python 설치를 사용 하는 경우에는 실행 중인 코드가 Python에 대해 예상 되는 환경을 사용 하 고 있는지 확인 하거나 R에 올바른 작업 영역을 사용 하 고 있는지 확인 해야 합니다. 예를 들어 [r 또는 Python을 업그레이드](../install/upgrade-r-and-python.md)한 경우 r 라이브러리의 경로는 기본값과 다른 폴더에 있을 수 있습니다. 또한 R 클라이언트 또는 독립 실행형 서버 인스턴스를 설치 하는 경우 컴퓨터에 R 라이브러리가 여러 개 있을 수 있습니다.

이 문서의 R 및 Python 스크립트 예제에서는 SQL Server에서 사용 하는 패키지의 경로 및 버전을 가져오는 방법을 보여 줍니다.

## <a name="get-the-r-library-location"></a>R 라이브러리 위치 가져오기

모든 버전의 SQL Server에 대해 다음 문을 실행 하 여 현재 인스턴스의 기본 R 패키지 라이브러리를 확인 합니다.

```sql
EXECUTE sp_execute_external_script  
  @language = N'R',
  @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

필요에 따라 SQL Server 2017 Machine Learning Services의 최신 버전 RevoScaleR에서 [Rxsql 경로](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 를 사용 하거나, [r Services를 RevoScaleR 9.0.1 이상으로 업그레이드할](../install/upgrade-r-and-python.md)수 있습니다. 이 저장 프로시저는 인스턴스 라이브러리의 경로와 SQL Server에서 사용 하는 RevoScaleR 버전을 반환 합니다.

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
> [Rxsqllibpaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 함수는 로컬 컴퓨터 에서만 실행할 수 있습니다. 함수는 원격 연결에 대 한 라이브러리 경로를 반환할 수 없습니다.

**결과**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.3.0'
```

## <a name="get-the-python-library-location"></a>Python 라이브러리 위치 가져오기

SQL Server 2017에서 **Python** 의 경우 다음 문을 실행 하 여 현재 인스턴스의 기본 라이브러리를 확인 합니다. 이 예에서는 Python `sys.path` 변수에 포함 된 폴더 목록을 반환 합니다. 이 목록에는 현재 디렉터리와 표준 라이브러리 경로가 포함 됩니다.

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

변수에 대 한 자세한 내용 및 `sys.path` 변수를 사용 하 여 모듈의 인터프리터 검색 경로를 설정 하는 방법에 대 한 자세한 내용은 [Python 설명서](https://docs.python.org/2/tutorial/modules.html#the-module-search-path) 를 참조 하세요.

## <a name="list-all-packages"></a>모든 패키지 나열

여러 가지 방법으로 현재 설치 된 패키지의 전체 목록을 가져올 수 있습니다. Sp_execute_external_script에서 패키지 목록 명령을 실행 하는 경우의 이점 중 하나는 인스턴스 라이브러리에 설치 된 패키지를 가져오도록 보장 한다는 것입니다.

### <a name="r"></a>R

다음 예에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저에서 R `installed.packages()` 함수를 사용 하 여 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지의 행렬을 가져옵니다. 이 스크립트는 설명 파일에 패키지 이름 및 버전 필드를 반환 하며 이름만 반환 됩니다.

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

R 패키지 설명 필드의 옵션 및 기본 필드에 대 한 자세한 내용은을 참조 [https://cran.r-project.org](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)하십시오.

### <a name="python"></a>Python

모듈 `pip` 은 기본적으로 설치 되며, 표준 Python에서 지원 되는 패키지 외에도 설치 된 패키지를 나열 하기 위한 많은 작업을 지원 합니다. 물론 Python 명령 `pip` 프롬프트에서를 실행할 수 있지만에서 `sp_execute_external_script`pip 함수를 호출할 수도 있습니다.

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

명령줄에서 `pip` 실행 하는 경우에는 설치 `pip freeze` 된 모든 패키지를 가져오고 `pip list` ,에 의해 `pip`설치 된 패키지를 나열 하 고, pip 자체의 패키지를 나열 하지 않는 다른 많은 유용한 함수가 있습니다. 에 따라 다릅니다. 를 사용 `pip freeze` 하 여 종속성 파일을 생성할 수도 있습니다.

## <a name="find-a-single-package"></a>단일 패키지 찾기

패키지를 설치 했 고 특정 SQL Server 인스턴스에 사용할 수 있는지 확인 하려면 다음 저장 프로시저 호출을 실행 하 여 패키지를 로드 하 고 메시지만 반환할 수 있습니다.

### <a name="r"></a>R

이 예제에서는 RevoScaleR 라이브러리를 찾고 로드 합니다 (사용 가능한 경우).

```sql
EXECUTE sp_execute_external_script  
  @language =N'R',
  @script=N'require("RevoScaleR")'
GO
```

+ 패키지가 있는 경우 다음과 같은 메시지가 반환 됩니다. "명령이 성공적으로 완료 되었습니다."

+ 패키지를 찾거나 로드할 수 없으면 "" MissingPackageName "라는 패키지가 없습니다." 라는 텍스트가 포함 된 오류가 발생 합니다.

### <a name="python"></a>Python

Python 셸에서 또는 `conda` `pip` 명령을 사용 하 여 python에 해당 하는 검사를 수행할 수 있습니다. 또는 저장 프로시저에서 다음 문을 실행 합니다.

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

Management Studio를 사용 하 여 R 및 Python 패키지 버전 정보를 가져올 수 있습니다.

### <a name="r-package-version"></a>R 패키지 버전

이 문은 RevoScaleR 패키지 버전 및 기본 R 버전을 반환 합니다.

```sql
EXECUTE sp_execute_external_script
  @language = N'R',
  @script = N'
print(packageDescription("RevoScaleR"))
print(packageDescription("base"))
'
```

### <a name="python-package-version"></a>Python 패키지 버전

이 문은 revoscalepy 패키지 버전 및 Python의 버전을 반환 합니다.

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

+ [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)
+ [새 Python 패키지 설치](../python/install-additional-python-packages-on-sql-server.md)
+ [자습서, 샘플, 솔루션](../tutorials/machine-learning-services-tutorials.md)