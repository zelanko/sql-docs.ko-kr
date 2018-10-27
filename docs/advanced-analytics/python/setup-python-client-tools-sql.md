---
title: SQL Server Machine Learning 사용에 대 한 Python 클라이언트 설정 | Microsoft Docs
description: Python 사용 하 여 SQL Server Machine Learning Services에 대 한 원격 연결에 대 한 로컬 Python 환경을 설정 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/25/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 326676d1be684b90784351de316590ebdb1ff29f
ms.sourcegitcommit: 182d77997133a6e4ee71e7a64b4eed6609da0fba
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/25/2018
ms.locfileid: "50051155"
---
# <a name="set-up-a-python-client-for-use-with-sql-server-machine-learning"></a>SQL Server Machine Learning 사용에 대 한 Python 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 통합은 Machine Learning Services (In-database) 설치에서 Python 옵션을 포함 하는 경우 SQL Server 2017 이상부터 사용할 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md)합니다.

이 문서에서는 기계 학습 및 Python 통합에 사용할 원격 SQL Server에 연결할 수 있도록 클라이언트 개발 워크스테이션을 구성 하는 방법에 알아봅니다. 끝으로 해야 동일한 Python 라이브러리와 SQL Server의 기능 푸시 계산을 SQL Server에 원격 세션에 대 한 로컬 세션에서 합니다.

> [!Tip]
> 비디오 데모를 참조 하세요 [R 실행 및 Jupyter Notebook에서 SQL Server의 원격 Python](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/)합니다.

> [!Note]
> 클라이언트 라이브러리만 설치 하는 대신은 독립 실행형 서버를 사용 합니다. 독립 실행형을 사용 하 여 다양 한 클라이언트와 서버는 더 많은 종단 간 시나리오 작업에 대 한 일부 고객은 선호 하는 옵션입니다. 있는 경우는 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md) SQL Server 데이터베이스 엔진 인스턴스를 완전히 분리 된 Python 서버가 있는 SQL Server 설치 프로그램에서 제공 합니다. Standalon 서버 Anaconda 및 Microsoft 전용 라이브러리의 오픈 소스 기본 배포를 포함합니다. 이 위치에서 Python 실행 파일을 찾을 수 있습니다: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`합니다. 리치 클라이언트 설치 유효성 검사를 열고을 [Jupyter notebook](#python-tools) 는 Python.exe를 사용 하 여 서버에서 명령을 실행 합니다.

## <a name="1---install-python-packages"></a>1-Python 패키지를 설치 합니다.

로컬 워크스테이션에는 기본 배포 및 Microsoft 전용 패키지를 포함 하 여 SQL Server에 있는 것과 동일한 Python 패키지 버전 있어야 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 하 고 [microsftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package)합니다. 합니다 [azureml 모델 관리](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) 패키지도 설치 되어 있지만 독립 실행형 (인스턴스가 아닌) Machine Learning Server 컨텍스트와 연결 된 운영 화 작업에 적용 됩니다. SQL Server 인스턴스에서 데이터베이스 내 분석을 위한 저장된 프로시저를 통해 운영 화는 합니다.

1. 4.2.0 Anaconda Python 3.5.2 사용 하 여 설치 하는 설치 스크립트를 다운로드 하 고 세 가지 이전에 Microsoft 패키지를 나열 합니다.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) SQL Server 2017에는 없는 경우 (일반적인 경우)에 바인딩됩니다. 확실 하지 않은 경우이 스크립트를 선택 합니다.

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) 원격 SQL Server 인스턴스가 [Machine Learning Server 9.3에 바인딩된](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

2. 관리자 권한으로 PowerShell 창을 열고 (마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행**).

3. 설치 관리자를 다운로드 하는 폴더로 이동한 스크립트를 실행 합니다. 추가 된 `-InstallFolder` 명령줄 인수를 라이브러리에 대 한 폴더 위치를 지정 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다. 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

설치 폴더를 생략 하면 기본값은 C:\Program Files\Microsoft\PyForMLS 합니다.

설치를 완료 하려면 시간이 소요 됩니다. PowerShell 창에서 진행률을 모니터링할 수 있습니다. 설치가 완료 되 면 전체 집합을 패키지 해야 합니다. 

> [!Tip] 
> 권장 합니다 [Python에 대 한 Windows FAQ](https://docs.python.org/3/faq/windows.html) 일반 purppose에 대 한 내용은 Windows에서 Python 프로그램을 실행 합니다.

## <a name="2---locate-executables"></a>2-실행 파일 찾기

PowerShell에서 여전히는 Python.exe, 스크립트 및 다른 패키지의 위치를 확인 하려면 설치 폴더로 이동 합니다. 

1. 입력 `cd \` 루트 드라이브를 이동한 다음에 대 한 지정 된 경로 입력 하려면 `-InstallFolder` 이전 단계에서 합니다. 기본값은 설치 하는 동안이 매개 변수를 생략 하는 경우 `cd C:\Program Files\Microsoft\PyForMLS`합니다.

2. 입력 `dir *.exe` 실행 파일을 나열 합니다. 나타납니다 **python.exe**를 **pythonw.exe**, 및 **제거 anaconda.exe**합니다.

  ![Python 실행 파일의 목록](media/powershell-python-exe.png)
   
시스템에서 여러 버전의 Python 사용 해야이 특정 Python.exe 로드 하려는 경우 **revoscalepy** 및 기타 Microsoft 패키지 있습니다.

> [!Note] 
> 설치 스크립트는 새 python 인터프리터 및 방금 설치한 모듈을 자동으로 제공 해야 하는 다른 도구는 컴퓨터에서 경로 환경 변수를 수정 하지 않습니다. 도구에는 Python 인터프리터 및 라이브러리를 연결에 대 한 도움말을 참조 하세요 [IDE 설치](#install-ide)합니다.

<a name="python-tool"></a>

## <a name="3---open-jupyter-notebooks"></a>3-열기 Jupyter Notebook

Anaconda는 Jupyter 노트북을 포함 합니다. 다음 단계로, 노트북을 만들고 방금 설치한 라이브러리를 포함 하는 몇 가지 Python 코드를 실행 합니다.

1. Powershell 프롬프트에서 Jupyter Notebook을 열려는 스크립트 폴더로 이동 합니다.

   ```powershell
   .\Scripts\jupyter-notebook
   ```

  기본 브라우저에서 노트북을 열어야 `http://localhost:8889/tree`합니다.

2. 클릭 **새로 만들기** 을 클릭 한 다음 **Python 3**합니다.

  ![Python 3를 새 선택 영역을 사용 하 여 jupyter notebook](media/jupyter-notebook-new-p3.png)

3. 입력 `import revoscalepy` Microsoft 전용 라이브러리 중 하나를 로드 하 고 명령을 실행 합니다.

4. 더 복잡 한 일련의 문 입력 합니다. 이 예제에서는 사용 하 여 요약 통계를 생성 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 로컬 데이터 집합에 대해 합니다. 다른 함수 샘플 데이터의 위치를 가져옵니다 하 고 로컬.xdf 파일에 대 한 데이터 원본 개체를 만듭니다.

  ```Python
  import os
  from revoscalepy import rx_summary
  from revoscalepy import RxXdfData
  from revoscalepy import RxOptions
  sample_data_path = RxOptions.get_option("sampleDataDir")
  print(sample_data_path)
  ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
  summary = rx_summary("ArrDelay+DayOfWeek", ds)
  print(summary)
  ```

다음 스크린샷에서 입력 및 간단한 설명을 위해 잘립니다 출력의 일부를 보여 줍니다.

  ![revoscalepy 입력 및 출력을 표시 하는 jupyter notebook](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-SQL 권한 가져오기

스크립트를 실행 하 여 데이터를 업로드 하는 SQL Server 인스턴스에 연결할 데이터베이스 서버의 유효한 로그인을 해야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합된 인증을 사용 하면 이지만 SQL 로그인을 사용 하 여 몇 가지 시나리오에 대 한 간단한 스크립트 외부 데이터 연결 문자열을 포함 하는 경우에 특히 권장 합니다.

최소한 코드를 실행 하는 데 사용 된 계정, 사용 중인와 특별 한 사용 권한을 모든 외부 스크립트를 실행 합니다. 데이터베이스에서 읽을 수 있는 권한이 있어야 합니다. 대부분의 개발자는 또한 저장된 프로시저를 만들고 학습 데이터가 포함 된 테이블에 데이터를 쓸 권한이 필요 하거나 데이터의 점수를 매긴 합니다. 

Python을 사용 하는 데이터베이스의 계정에 대해 다음 권한을 구성 하려면 데이터베이스 관리자에 게 문의 합니다.

+ **EXECUTE ANY EXTERNAL SCRIPT** 서버에서 Python을 실행 합니다.
+ **db_datareader** 모델 학습에 사용 되는 쿼리를 실행 하는 권한입니다.
+ **db_datawriter** 점수가 매겨진된 데이터 또는 학습 데이터를 쓸 수 있습니다.
+ **db_owner** 저장된 프로시저와 같은 개체를 만들 테이블을 함수입니다. 
  해야 **db_owner** 샘플 및 테스트 데이터베이스를 만들 수 있습니다. 

코드에서 SQL Server를 사용 하 여 기본적으로 설치 되지 않은 패키지에 필요한 경우 데이터베이스 관리자의 인스턴스와 함께 설치 된 패키지에 정렬 합니다. SQL Server는 보안된 환경 및 패키지를 설치할 수 있습니다에 제한이 있습니다. 코드의 일부로 임시 설치 패키지의 권한이 있는 경우에 권장 되지 않습니다. 또한 보안 관련 문제를 것이 좋습니다 server 라이브러리에서 새 패키지를 설치 하기 전에 항상 신중 하 게 합니다.

## <a name="5---test-remote-connection"></a>5--원격 연결을 테스트 하는 중

다음 단계를 시도 하기 전에 SQL Server 인스턴스에 대 한 연결 문자열에 있는 사용 권한이 있는지 확인 합니다 [아이리스 샘플 데이터베이스](../tutorials/demo-data-iris-in-sql.md)합니다. 데이터베이스가 없습니다. 충분 한 권한이 할 수 있습니다 [인라인 참조 하 여 데이터베이스를 만들](#create-iris-remotely)합니다.

연결 문자열을 유효한 값으로 바꿉니다. 샘플 코드를 사용 하 여 `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` 코드 해야 원격 서버를 지정 수 있는 인스턴스 이름을 사용 하지만 합니다.

### <a name="define-a-function"></a>함수 정의

다음 코드는 이후 단계에서 SQL Server로 전송할 함수를 정의 합니다. 를 실행 하면 사용 하 여 데이터 및 라이브러리 (revoscalepy, pandas, matplotlib) 원격 서버의 iris 데이터 집합의 산 점도 만듭니다. Bytestream는.png의 브라우저에서 렌더링할 Jupyter Notebook에 다시 반환 합니다.

```python
def send_this_func_to_sql():
    from revoscalepy import RxSqlServerData, rx_import
    from pandas.tools.plotting import scatter_matrix
    import matplotlib.pyplot as plt
    import io
    
    # remember the scope of the variables in this func are within our SQL Server Python Runtime
    connection_string = "Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"
    
    # specify a query and load into pandas dataframe df
    sql_query = RxSqlServerData(connection_string=connection_string, sql_query = "select * from iris_data")
    df = rx_import(sql_query)
    
    scatter_matrix(df)
    
    # return bytestream of image created by scatter_matrix
    buf = io.BytesIO()
    plt.savefig(buf, format="png")
    buf.seek(0)
    
    return buf.getvalue()
```

### <a name="send-the-function-to-sql-server"></a>SQL Server는 보내기

이 예제에서는 원격 계산 컨텍스트를 만들어 SQL server로 함수 실행을 보내려면 [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)합니다. 합니다 **rx_exec** 함수는 인수로 계산 컨텍스트를 수락 하기 때문에 유용 합니다. 원격으로 실행 하려는 모든 함수에는 계산 컨텍스트 인수가 있어야 합니다. 와 같은 일부 함수 [rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) 이 인수를 직접 지원 합니다. 하지 않는 작업에 사용할 수 있습니다 **rx_exec** 원격 계산 컨텍스트에서 코드를 제공 합니다.

이 예제에서는 원시 데이터가 없는 Jupyter 노트북에 SQL Server에서 전송 해야 했습니다. 모든 계산이 아이리스 데이터베이스 내에서 발생 하 고 이미지 파일에만 클라이언트에 반환 됩니다.

```python
from IPython import display
import matplotlib.pyplot as plt 
from revoscalepy import RxInSqlServer, rx_exec

# create a remote compute context with connection to SQL Server
sql_compute_context = RxInSqlServer(connection_string=connection_string.format(new_db_name))

# use rx_exec to send the function execution to SQL Server
image = rx_exec(send_this_func_to_sql, compute_context=sql_compute_context)[0]

# only an image was returned to my jupyter client. All data remained secure and was manipulated in my db.
display.Image(data=image)
```

다음 스크린 샷에서 입력과 산 점도 출력을 보여줍니다.

  ![산 점도 출력을 표시 하는 jupyter notebook](media/jupyter-notebook-scatterplot.png)

## <a name="6---link-ide-to-pythonexe"></a>6-링크 python.exe IDE

명령줄에서 스크립트를 간단히 디버깅 하는 경우 표준 Python tools를 사용 하 여 가져올 수 있습니다. 그러나 새 솔루션을 개발 하는 경우에 완전 한 Python IDE를 필요할 수 있습니다. 인기 있는 옵션이 있습니다.

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) Python을 사용 하 여
+ [Visual Studio 용 AI 도구](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Visual Studio Code에서 Python](https://code.visualstudio.com/docs/languages/python)
+ PyCharm, Spyder를 및 Eclipse와 같은 인기 있는 타사 도구

Machine learning 프로젝트 뿐만 아니라 데이터베이스 프로젝트를 지원 하기 때문에 Visual Studio 좋습니다. Python 환경을 구성 하는 도움말을 참조 하세요 [Visual Studio에서 Python 환경 관리](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)합니다.

자주 개발자가 여러 버전의 Python 사용 하므로 설치 프로그램은 Python 경로에 추가 되지 않습니다. Python 실행 파일 및 설치 프로그램에서 설치 된 라이브러리를 사용 하려면 IDE에 연결 **Python.exe** 도 제공 하는 경로의 **revoscalepy** 하 고 **microsoftml**합니다. 

Visual Studio에서 Python 프로젝트를 사용자 지정 환경의 기본 설치 가정 하 고 다음 값을 지정 합니다.

| 구성 설정 | value |
|-----------------------|-------|
| **접두사 경로** | C:\Program Files\Microsoft\PyForMLS |
| **인터프리터 경로** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **창 인터프리터** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

<a name="create-iris-remotely"></a>

## <a name="optional-create-the-iris-database-remotely"></a>선택 사항: 데이터베이스를 만들 아이리스 원격으로

원격 서버의 데이터베이스를 만들 수 있는 권한이 있으면이 문서의 예제에 사용 되는 아이리스 데모 데이터베이스를 만드는 다음 코드를 실행할 수 있습니다.

### <a name="1---create-the-irissql-database"></a>1-irissql 데이터베이스 만들기

```Python
import pyodbc

# creating a new db to load Iris sample in
new_db_name = "irissql"
connection_string = "Driver=SQL Server;Server=localhost;Database={0};Trusted_Connection=Yes;" 
                        # you can also swap Trusted_Connection for UID={your username};PWD={your password}
cnxn = pyodbc.connect(connection_string.format("master"), autocommit=True)
cnxn.cursor().execute("IF EXISTS(SELECT * FROM sys.databases WHERE [name] = '{0}') DROP DATABASE {0}".format(new_db_name))
cnxn.cursor().execute("CREATE DATABASE " + new_db_name)
cnxn.close()

print("Database created")
```

### <a name="2---import-iris-sample-from-sklearn"></a>2-SkLearn에서 아이리스 샘플 가져오기

```Python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-recoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-테이블을 만들고 아이리스 데이터를 로드 하려면 RecoscalePy Api를 사용 합니다.

```Python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

<a name="install-ide"></a>

## <a name="next-steps"></a>다음 단계

SQL Server 작업 연결 및 도구를가지고 revoscalepy 함수 및 계산 컨텍스트를 전환 좀 더 자세히 살펴보려면 대 한 자습서를 단계별로 실행 합니다.

> [!div class="nextstepaction"]
> [Revoscalepy 및 원격 계산 컨텍스트를 사용 하 여 모델 만들기](../tutorials/use-python-revoscalepy-to-create-model.md)