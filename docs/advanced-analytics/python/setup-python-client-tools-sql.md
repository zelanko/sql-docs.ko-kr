---
title: Python 개발-SQL Server Machine Learning을 위한 데이터 과학 클라이언트 설정
description: Python 사용 하 여 SQL Server Machine Learning Services에 대 한 원격 연결에 대 한 Python 로컬 환경 (Jupyter Notebook 또는 PyCharm)를 설정 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 448322fc79f4a85256b1d0b5b682fcc5147263c5
ms.sourcegitcommit: a91c3f4fe2587d474cd4d470bda93239ba2693bb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67140641"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services의 Python 개발을 위한 데이터 과학 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 통합은 Python 옵션을 포함 하는 경우 SQL Server 2017 이상부터 사용할 수 있습니다는 [Machine Learning Services (In-database) 설치](../install/sql-machine-learning-services-windows-install.md)합니다. 

를 개발 및 SQL Server에 대 한 Python 솔루션을 배포 하려면 Microsoft의를 설치 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 및 다른 Python 라이브러리 개발 워크스테이션입니다. Revoscalepy 라이브러리에도 있는 원격 SQL Server 인스턴스를 두 시스템 간의 컴퓨팅 요청을 조정 합니다. 

이 문서에서는 machine learning 및 Python 통합에 사용 되는 원격 SQL Server를 사용 하 여 상호 작용할 수 있도록 Python 개발 워크스테이션을 구성 하는 방법에 알아봅니다. 이 문서의 단계를 완료 한 후 SQL Server에 있는 것과 동일한 Python 라이브러리를 해야 합니다. 또한 SQL Server에서 Python의 원격 세션 로컬 Python 세션에서 계산을 푸시하는 방법을 알 수 있습니다.

![클라이언트-서버 구성 요소](media/sqlmls-python-client-revo.png "로컬 및 원격 Python 세션 및 라이브러리")

설치 유효성 검사를 사용할 수 있습니다 기본 제공 Jupyter Notebook이이 문서에 설명 된 대로 또는 [라이브러리를 링크](#install-ide) PyCharm 또는 일반적으로 사용 하는 모든 다른 IDE.

> [!Tip]
> 이러한 실습 비디오 데모를 참조 하세요 [실행할 R 및 Python Jupyter Notebook에서 SQL Server에서 원격으로](https://youtu.be/D5erljpJDjE)입니다.

> [!Note]
> 클라이언트 라이브러리 설치 하는 대신 사용 하는 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md) 심층 시나리오 작업에 대 한 일부 고객은 선호 하는 풍부한 클라이언트로 합니다. 독립 실행형 서버는 SQL Server에서 완전히 분리 되지만 동일한 Python 라이브러리를 있기 때문에 사용할 수 있습니다 클라이언트로 SQL Server 데이터베이스 내 분석에 대 한 합니다. 가져오기 및 다른 데이터 플랫폼에서 데이터를 모델링 하는 기능을 포함 하 여 비 SQL 관련 작업에 사용할 수 있습니다. 독립 실행형 서버를 설치한 경우에이 위치에서 Python 실행 파일을 찾을 수 있습니다: `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`합니다. 설치 유효성을 검사 하 [Jupyter notebook을 엽니다](#python-tools) 는 Python.exe를 사용 하 여 해당 위치에서 명령을 실행 합니다.

## <a name="commonly-used-tools"></a>일반적으로 도구 사용

해야 하는지 여부를 sql에 새 Python 개발자 또는 Python 및 데이터베이스 내 분석에 새 SQL 개발자가 Python 개발 도구 및 T-SQL 쿼리 편집기와 같은 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 모든 실행 하려면 데이터베이스 내 분석의 기능입니다.

Python 개발을 위한 SQL Server가 설치 된 Anaconda 배포에 번들로 제공 되는 Jupyter Notebook을 사용할 수 있습니다. 이 문서에서는 로컬 및 원격으로 SQL Server에서 Python 코드를 실행할 수 있도록 Jupyter 노트북을 시작 하는 방법에 설명 합니다.

SSMS는 만들기 및 Python 코드를 포함 하는 등 SQL Server에서 저장된 프로시저를 실행 하는 데 별도 다운로드입니다. 저장된 프로시저에서 Jupyter Notebook에서 작성 하는 거의 모든 Python 코드를 포함할 수 있습니다. 다른 빠른 시작에 대해 자세히 알아보려면 단계별로 실행할 수 있습니다 [SSMS 및 포함 된 Python](../tutorials/quickstart-python-verify.md)합니다.

## <a name="1---install-python-packages"></a>1-Python 패키지를 설치 합니다.

로컬 워크스테이션에는 동일한 Python 패키지 버전으로 Python 3.5.2 배포 및 Microsoft 전용 패키지를 사용 하 여 기본 Anaconda 4.2.0를 비롯 한 SQL Server에 있어야 합니다.

설치 스크립트를 Python 클라이언트를 세 가지 Microsoft 전용 라이브러리를 추가합니다. 스크립트 설치 [revoscalepy](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/revoscalepy-package), 데이터 원본 개체 및 계산 컨텍스트를 정의 하는 데 사용 합니다. 설치할 [microsoftml](https://docs.microsoft.com/machine-learning-server/python-reference/microsoftml/microsoftml-package) 기계 학습 알고리즘을 제공 합니다. 합니다 [azureml](https://docs.microsoft.com/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) 패키지도 설치 되어 있지만-인스턴스가 아닌 독립 실행형 Machine Learning Server 컨텍스트와 연결 된 운영 화 작업에 적용 되 고 데이터베이스 내 분석에 대 한 사용이 제한 될 수 있습니다.

1. 설치 스크립트를 다운로드 합니다.

  + [https://aka.ms/mls-py](https://aka.ms/mls-py) 9.2.1 Microsoft Python 패키지의 버전을 설치합니다. 이 버전을 기본 SQL Server 2017 인스턴스에 해당합니다. 

  + [https://aka.ms/mls93-py](https://aka.ms/mls93-py) 버전 9.3의 Microsoft Python 패키지를 설치합니다. 원격 SQL Server 2017 인스턴스에 있으면이 버전 보다 적합 [Machine Learning Server 9.3에 바인딩된](../install/upgrade-r-and-python.md)합니다.

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

PowerShell에서 여전히 Python.exe, 스크립트 및 다른 패키지를 설치 했는지 확인 하려면 설치 폴더의 내용을 나열 합니다. 

1. 입력 `cd \` 루트 드라이브를 이동한 다음에 대 한 지정 된 경로 입력 하려면 `-InstallFolder` 이전 단계에서 합니다. 기본값은 설치 하는 동안이 매개 변수를 생략 하는 경우 `cd C:\Program Files\Microsoft\PyForMLS`합니다.

2. 입력 `dir *.exe` 실행 파일을 나열 합니다. 나타납니다 **python.exe**를 **pythonw.exe**, 및 **제거 anaconda.exe**합니다.

  ![Python 실행 파일의 목록](media/powershell-python-exe.png)
   
시스템에서 여러 버전의 Python 사용 해야이 특정 Python.exe 로드 하려는 경우 **revoscalepy** 및 기타 Microsoft 패키지 있습니다.

> [!Note] 
> 설치 스크립트는 새 python 인터프리터 및 방금 설치한 모듈을 자동으로 제공 해야 하는 다른 도구는 컴퓨터에서 경로 환경 변수를 수정 하지 않습니다. 도구에는 Python 인터프리터 및 라이브러리를 연결에 대 한 도움말을 참조 하세요 [IDE 설치](#install-ide)합니다.

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3-열기 Jupyter Notebook

Anaconda는 Jupyter 노트북을 포함 합니다. 다음 단계로, 노트북을 만들고 방금 설치한 라이브러리를 포함 하는 몇 가지 Python 코드를 실행 합니다.

1. Powershell 프롬프트에서 C:\Program Files\Microsoft\PyForMLS 디렉터리에 여전히 스크립트 폴더에서 Jupyter Notebook을 엽니다.

  ```powershell
  .\Scripts\jupyter-notebook
  ```

  기본 브라우저에서 노트북을 열어야 `https://localhost:8889/tree`합니다.

  시작 하는 또 다른 방법은 것을 두 번 클릭 **jupyter notebook.exe**합니다. 

2. 클릭 **새로 만들기** 을 클릭 한 다음 **Python 3**합니다.

  ![Python 3를 새 선택 영역을 사용 하 여 jupyter notebook](media/jupyter-notebook-new-p3.png)

3. 입력 `import revoscalepy` Microsoft 전용 라이브러리 중 하나를 로드 하 고 명령을 실행 합니다.

4. 입력 하 고 실행 `print(revoscalepy.__version__)` 버전 정보를 반환 합니다. 9\.2.1 또는 9.3.0 표시 됩니다. 사용 하 여 이러한 버전 중 하나를 사용할 수 있습니다 [서버의 revoscalepy](../package-management/installed-package-information.md)합니다. 

4. 더 복잡 한 일련의 문 입력 합니다. 이 예제에서는 사용 하 여 요약 통계를 생성 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary) 로컬 데이터 집합에 대해 합니다. 다른 함수 샘플 데이터의 위치를 가져옵니다 하 고 로컬.xdf 파일에 대 한 데이터 원본 개체를 만듭니다.

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

다음 스크린샷에서 입력 및 간단한 설명을 위해 잘립니다 출력의 일부를 보여 줍니다.

  ![revoscalepy 입력 및 출력을 표시 하는 jupyter notebook](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4-SQL 권한 가져오기

스크립트를 실행 하 여 데이터를 업로드 하는 SQL Server 인스턴스에 연결할 데이터베이스 서버의 유효한 로그인을 해야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합된 인증을 사용 하면 이지만 SQL 로그인을 사용 하 여 몇 가지 시나리오에 대 한 간단한 스크립트 외부 데이터 연결 문자열을 포함 하는 경우에 특히 권장 합니다.

최소한 코드를 실행 하는 데 사용 된 계정, 사용 중인와 특별 한 사용 권한을 모든 외부 스크립트를 실행 합니다. 데이터베이스에서 읽을 수 있는 권한이 있어야 합니다. 대부분의 개발자는 또한 저장된 프로시저를 만들고 학습 데이터가 포함 된 테이블에 데이터를 쓸 권한이 필요 하거나 데이터의 점수를 매긴 합니다. 

데이터베이스 관리자에 게 [계정에 대해 다음 권한을 구성](../security/user-permission.md), Python을 사용 하는 데이터베이스에서:

+ **EXECUTE ANY EXTERNAL SCRIPT** 서버에서 Python을 실행 합니다.
+ **db_datareader** 모델 학습에 사용 되는 쿼리를 실행 하는 권한입니다.
+ **db_datawriter** 점수가 매겨진된 데이터 또는 학습 데이터를 쓸 수 있습니다.
+ **db_owner** 저장된 프로시저와 같은 개체를 만들 테이블을 함수입니다. 
  해야 **db_owner** 샘플 및 테스트 데이터베이스를 만들 수 있습니다. 

코드에서 SQL Server를 사용 하 여 기본적으로 설치 되지 않은 패키지에 필요한 경우 데이터베이스 관리자의 인스턴스와 함께 설치 된 패키지에 정렬 합니다. SQL Server는 보안된 환경 및 패키지를 설치할 수 있습니다에 제한이 있습니다. 코드의 일부로 임시 설치 패키지의 권한이 있는 경우에 권장 되지 않습니다. 또한 보안 관련 문제를 것이 좋습니다 server 라이브러리에서 새 패키지를 설치 하기 전에 항상 신중 하 게 합니다.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5-테스트 데이터를 생성 합니다.

원격 서버의 데이터베이스를 만들 수 있는 권한이 있으면이 문서의 나머지 단계에 사용 되는 아이리스 데모 데이터베이스를 만드는 다음 코드를 실행할 수 있습니다.

### <a name="1---create-the-irissql-database-remotely"></a>1-irissql 데이터베이스를 원격으로 만들기

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

### <a name="2---import-iris-sample-from-sklearn"></a>2-SkLearn에서 아이리스 샘플 가져오기

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3-테이블을 만들고 아이리스 데이터를 로드 하려면 Revoscalepy Api를 사용 합니다.

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6--원격 연결을 테스트 하는 중

다음 단계를 시도 하기 전에 SQL Server 인스턴스에 대 한 연결 문자열에 있는 사용 권한이 있는지 확인 합니다 [아이리스 샘플 데이터베이스](../tutorials/demo-data-iris-in-sql.md)합니다. 데이터베이스가 없습니다. 충분 한 권한이 할 수 있습니다 [인라인 참조 하 여 데이터베이스를 만들](#create-iris-remotely)합니다.

연결 문자열을 유효한 값으로 바꿉니다. 샘플 코드를 사용 하 여 `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"` 코드 해야 원격 서버를 지정할 수 있습니다는 인스턴스 이름과 데이터베이스 사용자 로그인에 매핑되는 자격 증명 옵션을 사용 하 여 있지만.

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


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7-도구에서 Python을 시작 합니다.

자주 개발자가 여러 버전의 Python 사용 하므로 설치 프로그램은 Python 경로에 추가 되지 않습니다. Python 실행 파일 및 설치 프로그램에서 설치 된 라이브러리를 사용 하려면 IDE에 연결 **Python.exe** 도 제공 하는 경로의 **revoscalepy** 하 고 **microsoftml**합니다. 

### <a name="command-line"></a>패키지 실행 유틸리티

실행할 때 **Python.exe** C:\Program Files\Microsoft\PyForMLS에서 (또는 Python 클라이언트 라이브러리 설치에 대 한 지정 된 모든 위치) 전체 Anaconda 배포와 Microsoft Python에 액세스할 수 있습니다 모듈 **revoscalepy** 하 고 **microsoftml**합니다.

1. C:\Program Files\Microsoft\PyForMLS로 이동한 후 두 번 클릭 **Python.exe**합니다.
2. 대화형 도움말을 엽니다. `help()`
3. 프롬프트에서 도움말 모듈의 이름 입력: `help> revoscalepy`합니다. 도움말 이름, 패키지 콘텐츠, 버전 및 파일 위치를 반환합니다.
4. 패키지 및 버전 정보를 반환 합니다 **도움말 >** 프롬프트: `revoscalepy`합니다. Enter 키를 몇 번 도움말을 종료 합니다.
5. 모듈을 가져옵니다. `import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter Notebook

이 문서에서는 함수 호출을 보여 줍니다. 기본 제공 Jupyter Notebook **revoscalepy**합니다. 이 도구를 처음 이라면 다음 스크린 샷에서 퍼즐 조각을 방식 및 모든 "잘 작동" 하는 이유 보여 줍니다. 

부모 폴더 C:\Program Files\Microsoft\PyForMLS Anaconda Microsoft 패키지를 포함 합니다. Jupyter Notebook Scripts 폴더에서 Anaconda에 포함 되어 및 Python 실행 파일은 Jupyter Notebook과 함께 자동 등록 합니다. 사이트 패키지에서 찾은 패키지는 데이터 과학 및 기계 학습에 사용 되는 세 가지 Microsoft 패키지를 포함 하 여 notebook을로 가져올 수 있습니다.

  ![실행 파일 및 라이브러리](media/jupyter-notebook-python-registration.png)

다른 IDE를 사용 하는 경우에 도구에는 Python 실행 파일 및 함수 라이브러리를 연결 해야 합니다. 다음 섹션에서는 자주 사용 되는 도구에 대 한 지침을 제공합니다.

### <a name="visual-studio"></a>Visual Studio

있다면 [Visual Studio에서 Python](https://code.visualstudio.com/docs/languages/python), Microsoft Python 패키지가 포함 된 Python 환경을 만들려면 다음 구성 옵션을 사용 합니다.

| 구성 설정 | value |
|-----------------------|-------|
| **접두사 경로** | C:\Program Files\Microsoft\PyForMLS |
| **인터프리터 경로** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **창 인터프리터** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

Python 환경을 구성 하는 도움말을 참조 하세요 [Visual Studio에서 Python 환경 관리](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)합니다.

### <a name="pycharm"></a>PyCharm

PyCharm의 Machine Learning Server 설치 실행 python 인터프리터를 설정 합니다.

1. 설정에서 새 프로젝트를 클릭 **로컬 추가**합니다.

2. `C:\Program Files\Microsoft\PyForMLS\` 을 입력합니다.

이제 가져올 수 있습니다 **revoscalepy**하십시오 **microsoftml**, 또는 **azureml** 모듈입니다. 선택할 수도 있습니다 **도구가** > **Python 콘솔** 는 대화형 창을 엽니다.

## <a name="next-steps"></a>다음 단계

SQL Server 작업 연결 및 도구를가지고 기술을 사용 하 여 Python 빠른 시작을 통해 실행 하 여 확장 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.

> [!div class="nextstepaction"]
> [빠른 시작: Python SQL Server에 있는지 확인](../tutorials/quickstart-python-verify.md)