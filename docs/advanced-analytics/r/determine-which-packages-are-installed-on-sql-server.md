---
title: SQL Server에 설치 된 Python 패키지 또는 R 보기 | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: e57c22301f69039ad2aa9466a87cce37762691e3
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="viewing-r-or-python-packages-installed-on-sql-server"></a>SQL Server에 설치 된 Python 패키지 또는 R 보기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

여러 Python 환경에 설치 하거나 여러 R 도구를 사용할 경우를 잘못 된 라이브러리 또는 환경에 패키지를 설치 하 여 다음 할 수 없습니다 나중에 찾을 쉽습니다. 

이 문서에서는 몇 가지 쿼리를 현재 버전을 확인 하 고 현재 SQL Server 환경에 설치 된 패키지를 나열를 사용할 수 있습니다.

## <a name="verify-the-current-default-library"></a>현재 기본 라이브러리를 확인 합니다.

에 대 한 **R** SQL Server의 현재 인스턴스에 대 한 기본 라이브러리를 확인 하려면 다음 문을 실행 합니다.

```sql
EXECUTE sp_execute_external_script  @language = N'R'
, @script = N'OutputDataSet <- data.frame(.libPaths());'
WITH RESULT SETS (([DefaultLibraryName] VARCHAR(MAX) NOT NULL));
GO
```

에 대 한 **Python** SQL Server의 현재 인스턴스에 대 한 기본 라이브러리를 확인 하려면 다음 문을 실행 합니다.

```sql
EXEC sp_execute_external_script
  @language =N'Python',
  @script=N'import sys; print("\n".join(sys.path))'
```

## <a name="generate-a-package-list-using-a-stored-procedure"></a>저장된 프로시저를 사용 하는 패키지 목록 생성

현재 설치 된 패키지의 전체 목록을 얻을 수 있는 여러 가지가 있습니다. Sp_execute_external_script에서 패키지 목록을 명령 실행의 장점 중 하나는 인스턴스 라이브러리에 설치 된 패키지를 가져오려는 보장입니다.

### <a name="r"></a>R

다음 예제에서는 R 함수를 사용 하 여 `installed.packages()` 에 [!INCLUDE [tsql](..\..\includes\tsql-md.md)] 저장 프로시저는 현재 인스턴스에 대 한 R_SERVICES 라이브러리에 설치 된 패키지의 행렬을 가져옵니다. DESCRIPTION 파일의 필드 구문 분석을 방지하기 위해 이름만 반환됩니다.

```SQL
EXECUTE sp_execute_external_script
@language=N'R'
,@script = N'str(OutputDataSet);
packagematrix <- installed.packages();
NameOnly <- packagematrix[,1];
OutputDataSet <- as.data.frame(NameOnly);'
, @input_data_1 = N''
WITH RESULT SETS ((PackageName nvarchar(250) ))
```

자세한 선택적에 대 한 정보 및 R 패키지 DESCRIPTION 필드에 대 한 기본 필드를 참조 하세요. [ https://cran.r-project.org ](https://cran.r-project.org/doc/manuals/R-exts.html#The-DESCRIPTION-file)합니다.

### <a name="python"></a>Python

`pip` 모듈 기본적으로 설치 되 고 표준 Python 지 원하는 것 외에도 목록 설치 패키지에 대 한 여러 작업을 지원 합니다. 실행할 수 있습니다 `pip` Python에서 명령 프롬프트에서 물론, 하지만 또한 함수를 호출할 수 일부 pip에서 `sp_execute_external_script`합니다.

```sql
execute sp_execute_external_script 
@language = N'Python', 
@script = N'
import pip
import pandas as pd
installed_packages = pip.get_installed_distributions()
installed_packages_list = sorted(["%s==%s" % (i.key, i.version)
     for i in installed_packages])
df = pd.DataFrame(installed_packages_list)
OutputDataSet = df
'
WITH RESULT SETS (( PackageVersion nvarchar (150) ))
```

실행 하는 경우 `pip` 명령줄에서 여러 가지 다른 유용한 함수가: `pip list` 반면, 설치 된 모든 패키지를 가져옵니다 `pip freeze` 나열 하 여 설치 된 패키지 `pip`, 및 패키지 자체 pip를 나열 하지 않습니다 에 따라 다릅니다. 사용할 수도 있습니다 `pip freeze` 종속성 파일을 생성 합니다.

## <a name="verify-whether-a-package-is-installed-with-an-instance"></a>패키지 인스턴스에 설치 되어 있는지 확인 하십시오.

패키지를 설치 하 고 특정 SQL Server 인스턴스를 사용할 수 있는지 확인 하려는 경우에 패키지를 로드 하 고 메시지에만 반환 하려면 다음 저장된 프로시저 호출을 실행할 수 있습니다.

### <a name="r"></a>R

이 예제에서는 찾아서 사용할 수 있는 경우 RevoScaleR 라이브러리를 로드 합니다.

```sql
EXEC sp_execute_external_script  @language =N'R',
@script=N'require("RevoScaleR")'
GO
```

+ 패키지를 찾을 경우 메시지가 반환 됩니다: "명령이 완료 되었습니다."

+ 패키지를 찾거나 로드할 수 없습니다, 하는 경우 텍스트를 포함 하는 오류가 발생 합니다. "라는 'MissingPackageName' 없는 패키지는"

### <a name="python"></a>Python

Python에서 Python에 대 한 해당 확인을 수행할 수 있으며 셸를 사용 하 여 `conda` 또는 `pip` 명령입니다. 또는 저장된 프로시저에서이 문을 실행 합니다.

```sql
exec sp_execute_external_script
       @language = N'Python'
       , @script = N'
import pip
import pkg_resources
pckg_name = "revoscalepy"
pckgs = pandas.DataFrame([(i.key) for i in pip.get_installed_distributions()], columns = ["key"])
installed_pckg = pckgs.query(''key == @pckg_name'')
print("Package", pckg_name, "is", "not" if installed_pckg.empty else "", "installed")
```

## <a name="view-installed-packages-using-a-utility-or-ide"></a>유틸리티 또는 IDE를 사용 하 여 설치 된 패키지를 보려면

대부분의 개발 도구는 설치 된 또는 현재 작업 영역 또는 환경에서 로드 된 패키지의 목록이 나 개체 브라우저를 제공 합니다. 이 섹션에서는 인기 있는 R, Python 도구를 사용 하기 위한 몇 가지 간단한 팁을 제공 합니다.

### <a name="r-tools"></a>R 도구

여러 가지 방법으로 R 유틸리티를 사용 하 여 설치 또는 로드 된 패키지 목록을 가져올 수 있습니다. 

+ 로컬 R 유틸리티를 사용 하 여 기본 R 함수를 같은 `installed.packages()`에 포함 되어 있는 `utils` 패키지 합니다. 인스턴스에 대 한 정확한 목록을 가져오려는 라이브러리 경로 명시적으로 지정 하거나 인스턴스 라이브러리와 연결 된 R 도구를 사용 하 여 해야 합니다.

### <a name="python-tools"></a>Python 도구

Visual Studio 용 Python 확장명 매우 쉽게 현재 환경에서 또는 IDE에 나열 된 다른 가상 환경에서 설치 된 패키지를 볼 수 있습니다. 구성 여러 환경, 목록에서 환경을 선택 하 고 패키지를 볼 하거나 수 해당 환경에 새 패키지를 설치 합니다.

+ [Python 환경](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

Visual Studio Code는 무료 편집기 여러 Python linters 사용할 수 있는 Python 지원입니다. VS Code 같은 Visual Studio에서 패키지 브라우저를 제공 하지 않는 하지만 구성 하 고 여러 환경 간에 전환 지원 합니다.

+ [Visual Studio Code에서 Python](https://code.visualstudio.com/docs/languages/python)

실행 하려면 몇 가지 추가 구성이 필요할 수 **revoscalepy** 명령을 원격 클라이언트에서:

+ [Windows에서 사용자 지정 Python 패키지 및 인터프리터를 로컬로 설치](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)

작업할 PyCharm을 비롯 한 다른 Python 환경 구성에 몇 가지 유용한 팁을 제공 하는이 블로그 **revoscalepy**합니다.

+ [서버를 학습 하는 컴퓨터를 사용 하 여 Python 웹 서비스 시작](https://blogs.msdn.microsoft.com/mlserver/2017/12/13/getting-started-with-python-web-services-using-machine-learning-server/)

## <a name="use-functions-from-machine-learning-server"></a>서버를 학습 하는 컴퓨터에서 함수를 사용 하 여

원격 클라이언트에서 코드의 SQL Server 지원 실행에 사용 되는 라이브러리, 패키지를 확인 하려면 이러한 함수를 사용할 수 있으므로 원격 환경에 설치 됩니다.

### <a name="revoscaler"></a>RevoScaleR

원격 클라이언트에서 작업 하는 서버에 액세스할 수 없는 경우 RevoScaleR 함수를 사용 하 여 SQL Server에 설치 된 패키지 목록을 가져올 수 있습니다. SQL Server 서버에 연결할 수 있는 권한이 있어야 하는 계산 컨텍스트를 지정 합니다. 

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) 원격 계산 컨텍스트에서 패키지에 대 한 경로 찾습니다.

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) 계산 컨텍스트에서 설치 된 패키지에 대 한 정보를 가져옵니다.

예를 들어 지정 된 SQL Server 계산 컨텍스트에서 사용할 수 있는 패키지의 목록을 가져오려면 다음 R 코드를 실행 합니다.

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;")
sqlPackages <- rxInstalledPackages(computeContext = sqlServerCompute)
sqlPackages
```

다음 예제에서는 로컬 계산 컨텍스트 및 패키지 버전에서 RevoScaleR의 라이브러리 위치를 가져옵니다.

```R
rxFindPackage(RevoScaleR, "local")
packageVersion("RevoScaleR")
```

### <a name="revoscalepy"></a>revoscalepy

이 시간 RevoScaleR에 대 한 것과 유사한 함수를 사용할 수 없습니다. 이후 버전에서 찾도록 **revoscalepy**합니다.

## <a name="get-library-location-and-version"></a>가져오기 라이브러리 위치 및 버전

실행 중인 코드에 사용 하는 올바른 환경, Python 또는 올바른 작업 영역에서 r을 확인 하는 경우가 때 사용 하는 여러 환경 또는 설치 된 R, Python, 있습니다.

예를 들어 기계 학습 바인딩을 사용 하 여 구성 요소를 업그레이드 한 경우 R 라이브러리 경로 기본값과 다른 폴더에 수 있습니다. 또한, R 클라이언트나의 독립 실행형 서버 인스턴스를 설치한 경우 컴퓨터에 여러 개의 R 라이브러리 될 수 있습니다.

이 예제에서는 경로 및 버전의 SQL Server에서 사용 되 고 라이브러리를 가져오는 방법을 보여 줍니다.

### <a name="r"></a>R

이 저장된 프로시저 인스턴스 라이브러리의 경로 및 버전의 SQL Server에서 사용 하는 RevoScaleR 패키지를 반환 합니다.

```sql
EXEC sp_execute_external_script
  @language =N'R',
  @script=N'
  sql_r_path <- rxSqlLibPaths("local")
  print(sql_r_path)
  version_info <-packageVersion("RevoScaleR")
  print(version_info)'
```

> [!NOTE]
> [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 함수는 대상 컴퓨터에만 실행할 수 있습니다. 함수는 원격 연결에 대 한 라이브러리 경로 반환할 수 없습니다.

**결과**

```text
STDOUT message(s) from external script: 
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER1000/R_SERVICES/library"
[1] '9.2.1'
```

### <a name="python"></a>Python

이 예제는 Python에 포함 된 폴더의 목록을 반환 `sys.path` 변수입니다. 현재 디렉터리 및 표준 라이브러리 경로 목록에 포함 됩니다.

```sql
EXEC sp_execute_external_script
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

