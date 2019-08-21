---
title: Python 개발을 위한 데이터 과학 클라이언트 설정
description: Python을 사용 하 여 SQL Server Machine Learning Services에 대 한 원격 연결을 위해 Python 로컬 환경 (Jupyter Notebook 또는 PyCharm)을 설정 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 6f40f04d677d5dcfa758a13321009da3e535c5d4
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634536"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 Python 개발을 위한 데이터 과학 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Python 통합은 [Machine Learning Services (데이터베이스 내) 설치](../install/sql-machine-learning-services-windows-install.md)에 python 옵션을 포함 하는 경우 SQL Server 2017 이상 버전부터 사용할 수 있습니다. 

SQL Server에 대 한 Python 솔루션을 개발 하 고 배포 하려면 Microsoft의 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 및 다른 python 라이브러리를 개발 워크스테이션에 설치 합니다. 원격 SQL Server 인스턴스에도 있는 revoscalepy 라이브러리는 두 시스템 간의 컴퓨팅 요청을 조정 합니다. 

이 문서에서는 기계 학습 및 Python 통합에 사용 하도록 설정 된 원격 SQL Server와 상호 작용할 수 있도록 Python 개발 워크스테이션을 구성 하는 방법에 대해 알아봅니다. 이 문서의 단계를 완료 하면 SQL Server에 있는 것과 동일한 Python 라이브러리가 만들어집니다. 또한 SQL Server의 로컬 Python 세션에서 원격 Python 세션으로 계산을 푸시하는 방법도 알아봅니다.

![클라이언트-서버 구성 요소](media/sqlmls-python-client-revo.png "로컬 및 원격 Python 세션 및 라이브러리")

설치의 유효성을 검사 하기 위해이 문서에 설명 된 대로 기본 제공 Jupyter 노트북을 사용 하거나 [라이브러리](#install-ide) 를 PyCharm 또는 일반적으로 사용 하는 다른 IDE에 연결할 수 있습니다.

> [!Tip]
> 이러한 연습에 대 한 비디오 데모를 보려면 [Jupyter 노트북에서 SQL Server에서 원격으로 R 및 Python 실행](https://youtu.be/D5erljpJDjE)을 참조 하세요.

> [!Note]
> 클라이언트 라이브러리 설치에 대 한 대안은 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md) 를 리치 클라이언트로 사용 하는 것입니다 .이는 일부 고객이 더 심층적인 시나리오 작업을 선호 합니다. 독립 실행형 서버는 SQL Server에서 완전히 분리 되지만 Python 라이브러리가 동일 하기 때문에 SQL Server 데이터베이스 내 분석을 위해 클라이언트로 사용할 수 있습니다. 다른 데이터 플랫폼의 데이터를 가져오고 모델링 하는 기능을 포함 하 여 SQL 관련 없는 작업에도 사용할 수 있습니다. 독립 실행형 서버를 설치 하는 경우이 위치 `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`에서 Python 실행 파일을 찾을 수 있습니다. 설치의 유효성을 검사 하려면 [Jupyter 노트북을 열어](#python-tools) 해당 위치에서 Python을 사용 하 여 명령을 실행 합니다.

## <a name="commonly-used-tools"></a>일반적으로 사용 되는 도구

SQL에 대 한 Python 개발자 이거나 Python 및 데이터베이스 내 분석을 위한 SQL 개발자 인 경우에는 Python 개발 도구와 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 와 같은 t-sql 쿼리 편집기를 모두 실행 하 여의 모든 기능을 실행 해야 합니다. 데이터베이스 내 분석

Python 개발의 경우 SQL Server에 의해 설치 된 Anaconda 배포에 번들로 제공 되는 Jupyter 노트북을 사용할 수 있습니다. 이 문서에서는 Python 코드를 로컬로 실행 하 고 SQL Server에서 원격으로 실행할 수 있도록 Jupyter 노트북을 시작 하는 방법을 설명 합니다.

SSMS는 Python 코드를 포함 하는 저장 프로시저를 포함 하 여 SQL Server에서 저장 프로시저를 만들고 실행 하는 데 도움이 되는 별도의 다운로드입니다. Jupyter 노트북에서 작성 하는 거의 모든 Python 코드는 저장 프로시저에 포함 될 수 있습니다. 다른 빠른 시작을 단계별로 실행 하 여 [SSMS 및 포함 된 Python](../tutorials/quickstart-python-verify.md)에 대해 알아볼 수 있습니다.

## <a name="1---install-python-packages"></a>1-Python 패키지 설치

로컬 워크스테이션에는 Python 3.5.2 배포를 사용 하는 기본 Anaconda 4.2.0 및 Microsoft 관련 패키지를 비롯 하 여 SQL Server에 있는 Python 패키지 버전이 동일 해야 합니다.

설치 스크립트는 Python 클라이언트에 세 개의 Microsoft 관련 라이브러리를 추가 합니다. 이 스크립트는 데이터 원본 개체 및 계산 컨텍스트를 정의 하는 데 사용 되는 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)를 설치 합니다. 기계 학습 알고리즘을 제공 하는 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 을 설치 합니다. 또한 [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) 패키지는 설치 되어 있지만 독립 실행형 (비 인스턴스) Machine Learning Server 컨텍스트와 연결 된 운영 화 작업에 적용 되며 데이터베이스 내 분석에 대해 사용이 제한 될 수 있습니다.

1. 설치 스크립트를 다운로드 합니다.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py)Microsoft Python 패키지의 버전 9.2.1을 설치 합니다. 이 버전은 기본 SQL Server 인스턴스에 해당 합니다. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)Microsoft Python 패키지 버전 9.3을 설치 합니다. 원격 SQL Server 인스턴스가 [Machine Learning Server 9.3에 바인딩되](../install/upgrade-r-and-python.md)는 경우이 버전을 선택 하는 것이 좋습니다.

2. 관리자 권한으로 PowerShell 창을 엽니다 ( **관리자 권한으로 실행**을 마우스 오른쪽 단추로 클릭).

3. 설치 관리자를 다운로드 한 폴더로 이동 하 여 스크립트를 실행 합니다. `-InstallFolder` 명령줄 인수를 추가 하 여 라이브러리의 폴더 위치를 지정 합니다. 예를 들어 다음과 같은 가치를 제공해야 합니다. 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

설치 폴더를 생략 하는 경우 기본값은 C:\Program Files\Microsoft\PyForMLS.입니다.

설치를 완료 하는 데 다소 시간이 걸립니다. PowerShell 창에서 진행률을 모니터링할 수 있습니다. 설치가 완료 되 면 전체 패키지 집합이 있습니다. 

> [!Tip] 
> Windows에서 Python 프로그램을 실행 하는 방법에 대 한 일반적인 purppose 정보는 [python For WINDOWS FAQ](https://docs.python.org/3/faq/windows.html) 를 권장 합니다.

## <a name="2---locate-executables"></a>2-실행 파일 찾기

PowerShell에서 설치 폴더의 내용을 나열 하 여 Python .exe, 스크립트 및 기타 패키지가 설치 되었는지 확인 합니다. 

1. 을 `cd \` 입력 하 여 루트 드라이브로 이동한 다음, 이전 단계에서에 `-InstallFolder` 지정한 경로를 입력 합니다. 설치 하는 동안이 매개 변수를 생략 한 경우 `cd C:\Program Files\Microsoft\PyForMLS`기본값은입니다.

2. 을 `dir *.exe` 입력 하 여 실행 파일을 나열 합니다. **Python**, **pythonw**및 **uninstall-anaconda**가 표시 되어야 합니다.

  ![Python 실행 파일 목록](media/powershell-python-exe.png)
   
여러 버전의 Python이 있는 시스템에서는 **revoscalepy** 및 기타 Microsoft 패키지를 로드 하려는 경우이 특정 Python을 사용 해야 합니다.

> [!Note] 
> 설치 스크립트는 컴퓨터의 PATH 환경 변수를 수정 하지 않습니다. 즉, 방금 설치한 새 python 인터프리터 및 모듈을 다른 도구에서 자동으로 사용할 수 없습니다. Python 인터프리터 및 라이브러리를 도구에 연결 하는 방법에 대 한 도움말은 [IDE 설치](#install-ide)를 참조 하세요.

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-Jupyter 노트북을 엽니다.

Anaconda에는 Jupyter 노트북이 포함 되어 있습니다. 다음 단계로, 노트북을 만들고 방금 설치한 라이브러리를 포함 하는 Python 코드를 실행 합니다.

1. 여전히 C:\Program Files\Microsoft\PyForMLS 디렉터리에 있는 Powershell 프롬프트에서 Scripts 폴더의 Jupyter 노트북을 엽니다.

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  의 기본 브라우저 `https://localhost:8889/tree`에서 노트북이 열립니다.

  **Jupyter-notebook**를 두 번 클릭 하 여 시작할 수도 있습니다. 

2. **새로 만들기** 를 클릭 한 다음 **Python 3**을 클릭 합니다.

  ![새 Python 3을 선택 하는 jupyter 노트북](media/jupyter-notebook-new-p3.png)

3. 명령을 `import revoscalepy` 입력 하 고 실행 하 여 Microsoft 전용 라이브러리 중 하나를 로드 합니다.

4. 을 입력 하 `print(revoscalepy.__version__)` 고을 실행 하 여 버전 정보를 반환 합니다. 9\.2.1 또는 9.3.0가 표시 되어야 합니다. [서버에서 revoscalepy](../package-management/r-package-information.md)를 사용 하 여 이러한 버전 중 하나를 사용할 수 있습니다.

4. 더 복잡 한 일련의 문을 입력 합니다. 이 예에서는 로컬 데이터 집합에 대해 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 를 사용 하 여 요약 통계를 생성 합니다. 다른 함수는 샘플 데이터의 위치를 가져오고 로컬 .xdf 파일에 대 한 데이터 원본 개체를 만듭니다.

  ```python
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

다음 스크린샷에서는 간단 하 게 나타내기 위해 잘린 출력의 입력 및 부분을 보여 줍니다.

  ![revoscalepy 입력 및 출력을 보여 주는 jupyter 노트북](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-SQL 사용 권한 가져오기

SQL Server 인스턴스에 연결 하 여 스크립트를 실행 하 고 데이터를 업로드 하려면 데이터베이스 서버에 유효한 로그인이 있어야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합 인증을 사용 하는 것이 좋지만 특히 스크립트에 외부 데이터에 대 한 연결 문자열이 포함 된 경우에는 SQL 로그인을 사용 하는 것이 더 간단 합니다.

최소한 코드를 실행 하는 데 사용 되는 계정에는 작업 중인 데이터베이스에서 읽을 수 있는 권한이 있어야 하며 특수 사용 권한은 외부 스크립트를 실행 합니다. 대부분의 개발자는 저장 프로시저를 만들고 학습 데이터 나 점수가 매겨진 데이터를 포함 하는 테이블에 데이터를 쓸 수 있는 권한도 필요 합니다. 

데이터베이스 관리자에 게 Python을 사용 하는 데이터베이스에서 [계정에 대 한 다음 권한을 구성](../security/user-permission.md)하도록 요청 합니다.

+ **외부 스크립트를 실행** 하 여 서버에서 Python을 실행 합니다.
+ 모델 학습에 사용 되는 쿼리를 실행할 수 있는 권한을 **db_datareader** 합니다.
+ 학습 데이터 또는 점수가 매겨진 데이터를 **db_datawriter** 합니다.
+ 저장 프로시저, 테이블, 함수 등의 개체를 만드는 **db_owner** 
  또한 샘플 및 테스트 데이터베이스를 만들려면 **db_owner** 가 필요 합니다. 

코드에 기본적으로 SQL Server와 함께 설치 되지 않은 패키지가 필요한 경우 데이터베이스 관리자를 사용 하 여 패키지를 인스턴스와 함께 설치 되도록 정렬 합니다. SQL Server은 보안 환경으로, 패키지를 설치할 수 있는 위치에 대 한 제한 사항이 있습니다. 권한이 있는 경우에도 패키지를 코드의 일부로 임시 설치 하지 않는 것이 좋습니다. 또한 서버 라이브러리에 새 패키지를 설치 하기 전에 항상 보안 문제를 신중 하 게 고려해 야 합니다.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-테스트 데이터 만들기

원격 서버에서 데이터베이스를 만들 수 있는 권한이 있는 경우 다음 코드를 실행 하 여이 문서의 나머지 단계에 사용 되는 Iri demo 데이터베이스를 만들 수 있습니다.

### <a name="1---create-the-irissql-database-remotely"></a>1-원격으로 irissql 데이터베이스 만들기

```python
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

### <a name="2---import-iris-sample-from-sklearn"></a>2-샘플에서 조리개 샘플 가져오기

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-Revoscalepy Api를 사용 하 여 테이블을 만들고 Iri 데이터 로드

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6-원격 연결 테스트

다음 단계를 시도 하기 전에 SQL Server 인스턴스에 대 한 사용 권한과 [iri 샘플 데이터베이스](../tutorials/demo-data-iris-in-sql.md)에 대 한 연결 문자열이 있는지 확인 합니다. 데이터베이스가 존재 하지 않고 충분 한 사용 권한이 있는 경우 [이러한 인라인 지침을 사용 하 여 데이터베이스를 만들](#create-iris-remotely)수 있습니다.

연결 문자열을 유효한 값으로 바꿉니다. 예제 코드에서는를 `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` 사용 하지만 코드에서 인스턴스 이름과 데이터베이스 사용자 로그인에 매핑되는 자격 증명 옵션을 사용 하 여 원격 서버를 지정 해야 합니다.

### <a name="define-a-function"></a>함수 정의

다음 코드는 이후 단계에서 SQL Server 하기 위해 전송 하는 함수를 정의 합니다. 실행 될 때 원격 서버의 데이터 및 라이브러리 (revoscalepy, pandas, matplotlib)를 사용 하 여 조리개 데이터 집합의 산 점도를 만듭니다. 브라우저에서 렌더링 하기 위해 bytestream의 파일을 Jupyter 노트북에 다시 반환 합니다.

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

### <a name="send-the-function-to-sql-server"></a>함수를 SQL Server 보냅니다.

이 예제에서는 원격 계산 컨텍스트를 만든 다음 [rx_exec](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-exec)를 사용 하 여 SQL Server 함수 실행을 보냅니다. **Rx_exec** 함수는 계산 컨텍스트를 인수로 허용 하므로 유용 합니다. 원격으로 실행 하려는 모든 함수에는 계산 컨텍스트 인수가 있어야 합니다. [Rx_lin_mod](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-lin-mod) 와 같은 일부 함수는이 인수를 직접 지원 합니다. 사용 하지 않는 작업의 경우 **rx_exec** 를 사용 하 여 원격 계산 컨텍스트에서 코드를 배달할 수 있습니다.

이 예제에서는 SQL Server에서 Jupyter Notebook 원시 데이터를 전송 하지 않았습니다. 모든 계산은 Iri 데이터베이스 내에서 발생 하며 이미지 파일만 클라이언트에 반환 됩니다.

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

다음 스크린샷은 입력 및 산 점도 출력을 보여 줍니다.

  ![산 점도 출력을 표시 하는 jupyter 노트북](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-도구에서 Python 시작

개발자가 여러 버전의 Python에서 자주 작업 하므로 설치 프로그램이 Python을 경로에 추가 하지 않습니다. 설치 프로그램에서 설치 하는 Python 실행 파일 및 라이브러리를 사용 하려면 **revoscalepy** 및 **microsoftml**도 제공 하는 경로에서 **python** 에 IDE를 연결 합니다. 

### <a name="command-line"></a>패키지 실행 유틸리티

C:\Program Files\Microsoft\PyForMLS (또는 Python 클라이언트 라이브러리 설치를 위해 지정한 위치)에서 **python** 을 실행 하는 경우 전체 Anaconda 배포에 대 한 액세스 권한 및 Microsoft python 모듈, revoscalepy에 액세스할 수 있습니다.및 **microsoftml**.

1. C:\Program Files\Microsoft\PyForMLS로 이동 하 고 **Python**을 두 번 클릭 합니다.
2. 대화형 도움말을 엽니다.`help()`
3. 도움말 프롬프트 `help> revoscalepy`에 모듈 이름을 입력 합니다. 도움말은 이름, 패키지 내용, 버전 및 파일 위치를 반환 합니다.
4. **도움말 >** 프롬프트 `revoscalepy`에서 버전 및 패키지 정보를 반환 합니다. Enter 키를 눌러 도움말을 종료 합니다.
5. 모듈 가져오기:`import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter 노트북

이 문서에서는 기본 제공 Jupyter 노트북을 사용 하 여 **revoscalepy**에 대 한 함수 호출을 보여 줍니다. 이 도구를 처음 접하는 경우 다음 스크린샷에서는 해당 부분이 함께 표시 되는 방식과 "작동" 하는 이유를 보여 줍니다. 

C:\Program Files\Microsoft\PyForMLS 부모 폴더에는 Anaconda와 Microsoft 패키지가 포함 됩니다. Jupyter 노트북은 Anaconda의 Scripts 폴더 아래에 포함 되어 있으며 Python 실행 파일은 Jupyter 노트북에 자동으로 등록 됩니다. 데이터 과학 및 기계 학습에 사용 되는 세 가지 Microsoft 패키지를 포함 하 여 사이트에서 찾은 패키지를 노트북으로 가져올 수 있습니다.

  ![실행 파일 및 라이브러리](media/jupyter-notebook-python-registration.png)

다른 IDE를 사용 하는 경우 도구에 Python 실행 파일 및 함수 라이브러리를 연결 해야 합니다. 다음 섹션에서는 일반적으로 사용 되는 도구에 대 한 지침을 제공 합니다.

### <a name="visual-studio"></a>Visual Studio

[Visual Studio에서 python](https://code.visualstudio.com/docs/languages/python)을 사용 하는 경우 다음 구성 옵션을 사용 하 여 Microsoft python 패키지를 포함 하는 python 환경을 만듭니다.

| 구성 설정 | value |
|-----------------------|-------|
| **접두사 경로** | C:\Program Files\Microsoft\PyForMLS |
| **인터프리터 경로** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **창 인터프리터** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

Python 환경을 구성 하는 데 도움이 필요한 경우 [Visual Studio에서 python 환경 관리](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)를 참조 하세요.

### <a name="pycharm"></a>PyCharm

PyCharm에서 인터프리터를 Machine Learning Server에 의해 설치 된 Python 실행 파일에 설정 합니다.

1. 새 프로젝트의 설정에서 **로컬 추가**를 클릭 합니다.

2. `C:\Program Files\Microsoft\PyForMLS\` 을 입력합니다.

이제 **revoscalepy**, **microsoftml**또는 **azureml** 모듈을 가져올 수 있습니다. **도구** > **Python 콘솔** 을 선택 하 여 대화형 창을 열 수도 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server에 대 한 도구 및 작업 연결이 있으므로 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 사용 하 여 Python 빠른 시작을 통해 실행 하 여 기술을 확장 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server에 Python이 있는지 확인](../tutorials/quickstart-python-verify.md)