---
title: Python 데이터 과학 클라이언트 설정
description: Python을 사용하여 SQL Server Machine Learning Services에 원격으로 연결할 수 있도록 Python 로컬 환경(Jupyter Notebook 또는 PyCharm)을 설정합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/04/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15'
ms.openlocfilehash: 690955608e705ff61cadd15730ff12fb05780fee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470924"
---
# <a name="set-up-a-data-science-client-for-python-development-on-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services에서 Python 개발을 위한 데이터 과학 클라이언트 설정
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

Python 통합은 [Machine Learning Services(데이터베이스 내) 설치](../install/sql-machine-learning-services-windows-install.md)에 Python 옵션을 포함하는 경우 SQL Server 2017 이상에서 사용할 수 있습니다. 

SQL Server에 대한 Python 솔루션을 개발하고 배포하려면 Microsoft의 [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package) 및 기타 Python 라이브러리를 개발 워크스테이션에 설치합니다. 원격 SQL Server 인스턴스에도 있는 revoscalepy 라이브러리는 두 시스템 간의 컴퓨팅 요청을 조정합니다. 

이 문서에서는 기계 학습 및 Python 통합에 사용하도록 설정된 원격 SQL Server와 상호 작용할 수 있도록 Python 개발 워크스테이션을 구성하는 방법에 대해 알아봅니다. 이 문서의 단계를 완료하면 SQL Server에 있는 것과 동일한 Python 라이브러리가 만들어집니다. 또한 SQL Server의 로컬 Python 세션에서 원격 Python 세션으로 계산을 푸시하는 방법도 알아봅니다.

![클라이언트-서버 구성 요소](media/sqlmls-python-client-revo.png "로컬 및 원격 Python 세션 및 라이브러리")

설치의 유효성을 검사하기 위해 이 문서에 설명된 대로 기본 제공 Jupyter Notebook을 사용하거나, PyCharm 또는 일반적으로 사용하는 다른 IDE에 [라이브러리를 연결](#install-ide)할 수 있습니다.

> [!Tip]
> 이러한 연습에 대한 비디오 데모를 보려면 [Jupyter Notebook의 SQL Server에서 R 및 Python을 원격으로 실행](https://youtu.be/D5erljpJDjE)을 참조하세요.

> [!Note]
> 클라이언트 라이브러리 설치에 대한 대안은 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md)를 사용하여 다양한 클라이언트를 사용하는 것입니다. 이 경우 일부 고객은 보다 심층적인 시나리오 작업을 선호합니다. 독립 실행형 서버는 SQL Server에서 완전히 분리되지만 Python 라이브러리가 동일하기 때문에 SQL Server 데이터베이스 내 분석을 위해 클라이언트로 사용할 수 있습니다. 다른 데이터 플랫폼의 데이터를 가져오고 모델링하는 기능을 포함하여 SQL과 관련이 없는 작업에도 사용할 수 있습니다. 독립 실행형 서버를 설치하는 경우 다음 위치에서 Python 실행 파일을 찾을 수 있습니다. `C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`. 설치의 유효성을 검사하려면 [Jupyter Notebook을 열고](#python-tools) 해당 위치에서 Python.exe를 사용하여 명령을 실행합니다.

## <a name="commonly-used-tools"></a>일반적으로 사용되는 도구

SQL에 익숙하지 않은 Python 개발자이거나 Python 및 데이터베이스 내 분석을 위한 SQL 개발자인 경우 데이터베이스 내 분석의 모든 기능을 실행하려면 Python 개발 도구와 [SQL Server Management Studio(SSMS)](../../ssms/download-sql-server-management-studio-ssms.md) 같은 T-SQL 쿼리 편집기가 모두 필요합니다.

Python 개발의 경우 SQL Server에 의해 설치된 Anaconda 배포에 번들로 제공되는 Jupyter Notebook을 사용할 수 있습니다. 이 문서에서는 SQL Server에서 Python 코드를 로컬 및 원격으로 실행할 수 있도록 Jupyter Notebook을 시작하는 방법을 설명합니다.

SSMS는 Python 코드를 포함하는 저장 프로시저를 포함하여 SQL Server에서 저장 프로시저를 만들고 실행하는 데 도움이 되는 별도의 다운로드입니다. Jupyter Notebook에서 작성하는 거의 모든 Python 코드는 저장 프로시저에 포함될 수 있습니다. 다른 빠른 시작을 단계별로 실행하여 [SSMS 및 포함된 Python](../tutorials/quickstart-python-create-script.md)에 대해 알아볼 수 있습니다.

## <a name="1---install-python-packages"></a>1 - Python 패키지 설치

로컬 워크스테이션에는 Python 3.5.2 배포를 사용하는 기본 Anaconda 4.2.0 및 Microsoft 관련 패키지를 비롯하여 SQL Server와 동일한 Python 패키지 버전이 있어야 합니다.

설치 스크립트는 Python 클라이언트에 세 개의 Microsoft 관련 라이브러리를 추가합니다. 이 스크립트는 데이터 원본 개체 및 컴퓨팅 컨텍스트를 정의하는 데 사용되는 [revoscalepy](/machine-learning-server/python-reference/revoscalepy/revoscalepy-package)를 설치합니다. 기계 학습 알고리즘을 제공하는 [microsoftml](/machine-learning-server/python-reference/microsoftml/microsoftml-package)을 설치합니다. [azureml](/machine-learning-server/python-reference/azureml-model-management-sdk/azureml-model-management-sdk) 패키지도 설치되지만 독립 실행형(비 인스턴스) Machine Learning Server 컨텍스트와 연결된 운영화 작업에 적용되며 데이터베이스 내 분석에 대해 사용이 제한될 수 있습니다.

1. 설치 스크립트를 다운로드합니다.

   + [https://aka.ms/mls-py](https://aka.ms/mls-py)에서는 Microsoft Python 패키지의 버전 9.2.1을 설치합니다. 이 버전은 기본 SQL Server 인스턴스에 해당합니다. 

   + [https://aka.ms/mls93-py](https://aka.ms/mls93-py)에서는 Microsoft Python 패키지의 버전 9.3을 설치합니다. 이 버전은 원격 SQL Server 인스턴스가 [Machine Learning Server 9.3에 바인딩](../install/upgrade-r-and-python.md)되는 경우에 더 적합합니다.

2. 관리자 권한으로 PowerShell 창을 엽니다(**관리자 권한으로 실행** 을 마우스 오른쪽 단추 클릭).

3. 설치 프로그램을 다운로드한 폴더로 이동하여 스크립트를 실행합니다. `-InstallFolder` 명령줄 인수를 추가하여 라이브러리의 폴더 위치를 지정합니다. 다음은 그 예입니다. 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls"
   ```

설치 폴더를 생략하는 경우 기본값은 C:\Program Files\Microsoft\PyForMLS입니다.

설치를 완료하는 데 다소 시간이 걸립니다. PowerShell 창에서 진행률을 모니터링할 수 있습니다. 설치가 완료되면 전체 패키지 집합을 갖게 됩니다. 

> [!Tip] 
> Windows에서 Python 프로그램을 실행하는 방법에 대한 일반적인 정보는 [Windows용 Python FAQ](https://docs.python.org/3/faq/windows.html)를 참조하는 것이 좋습니다.

## <a name="2---locate-executables"></a>2 - 실행 파일 찾기

PowerShell에서 설치 폴더의 내용을 나열하여 Python.exe, 스크립트 및 기타 패키지가 설치되었는지 확인합니다. 

1. `cd \`를 입력하여 루트 드라이브로 이동한 다음, 이전 단계에서 `-InstallFolder`에 대해 지정한 경로를 입력합니다. 설치하는 동안 이 매개 변수를 생략한 경우 기본값은 `cd C:\Program Files\Microsoft\PyForMLS`입니다.

2. `dir *.exe`를 입력하여 실행 파일을 나열합니다. **python.exe**, **pythonw.exe**, **uninstall-anaconda.exe** 가 표시됩니다.

   ![Python 실행 파일 목록](media/powershell-python-exe.png)
   
여러 버전의 Python을 포함하는 시스템에서는 **revoscalepy** 및 기타 Microsoft 패키지를 로드하려면 이 특정 Python.exe를 사용해야 합니다.

> [!Note] 
> 설치 스크립트는 컴퓨터의 PATH 환경 변수를 수정하지 않습니다. 즉, 방금 설치한 새 python 인터프리터 및 모듈을 다른 도구에서 자동으로 사용할 수 없습니다. Python 인터프리터 및 라이브러리를 도구에 연결하는 방법에 대한 도움말은 [IDE 설치](#install-ide)를 참조하세요.

<a name="python-tools"></a>

## <a name="3---open-jupyter-notebooks"></a>3 - Jupyter Notebook 열기

Anaconda에는 Jupyter Notebook이 포함되어 있습니다. 다음 단계로, 노트를 만들고 방금 설치한 라이브러리를 포함하는 Python 코드를 실행합니다.

1. C:\Program Files\Microsoft\PyForMLS 디렉터리에 있는 Powershell 프롬프트에서 Scripts 폴더의 Jupyter Notebook을 엽니다.

   ```powershell
   .\Scripts\jupyter-notebook
   ```

   `https://localhost:8889/tree`의 기본 브라우저에서 노트가 열립니다.

   **jupyter-notebook.exe** 를 두 번 클릭하여 시작할 수도 있습니다. 

2. **새로 만들기** 를 클릭한 다음 **Python 3** 를 클릭합니다.

   ![새 Python 3 선택 항목이 있는 Jupyter Notebook](media/jupyter-notebook-new-p3.png)

3. `import revoscalepy`를 입력하고 명령을 실행하여 Microsoft 전용 라이브러리 중 하나를 로드합니다.

4. `print(revoscalepy.__version__)`를 입력하고 실행하여 버전 정보를 반환합니다. 9\.2.1 또는 9.3.0이 표시됩니다. [서버에서 revoscalepy](../package-management/r-package-information.md)를 사용하여 이러한 버전 중 하나를 사용할 수 있습니다.

4. 더 복잡한 일련의 문을 입력합니다. 이 예에서는 로컬 데이터 집합에 대해 [rx_summary](/machine-learning-server/python-reference/revoscalepy/rx-summary)를 사용하여 요약 통계를 생성합니다. 다른 함수는 샘플 데이터의 위치를 가져오고 로컬 .xdf 파일에 대한 데이터 원본 개체를 만듭니다.

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

다음 스크린샷에서는 간단하게 나타난 입력 및 일부 출력을 보여 줍니다.

  ![revoscalepy 입력 및 출력을 보여 주는 Jupyter Notebook](media/jupyter-notebook-local-revo.png)

## <a name="4---get-sql-permissions"></a>4 - SQL 사용 권한 가져오기

SQL Server 인스턴스에 연결하여 스크립트를 실행하고 데이터를 업로드하려면 데이터베이스 서버에 유효한 로그인이 있어야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합 인증을 사용하는 것이 좋지만 특히 스크립트에 외부 데이터에 대한 연결 문자열이 포함된 경우에는 SQL 로그인을 사용하는 것이 더 간단합니다.

최소한, 코드를 실행하는 데 사용되는 계정에는 작업 중인 데이터베이스에서 읽을 수 있는 권한 및 특수 EXECUTE ANY EXTERNAL SCRIPT 권한이 있어야 합니다. 대부분의 개발자는 저장 프로시저를 만들고 학습 데이터나 점수가 매겨진 데이터를 포함하는 테이블에 데이터를 쓸 수 있는 권한도 필요합니다. 

데이터베이스 관리자에게 Python을 사용하는 데이터베이스에서 [계정에 대한 다음 권한을 구성](../security/user-permission.md)하도록 요청합니다.

+ 서버에서 Python을 실행하는 **EXECUTE ANY EXTERNAL SCRIPT**.
+ 모델 학습에 사용되는 쿼리를 실행하는 **db_datareader** 권한.
+ 학습 데이터 또는 점수가 매겨진 데이터를 쓰는 **db_datawriter**.
+ 저장 프로시저, 테이블, 함수 등의 개체를 만드는 **db_owner**. 
  또한 샘플 및 테스트 데이터베이스를 만들기 위한 **db_owner** 도 필요합니다. 

코드에 기본적으로 SQL Server와 함께 설치되지 않은 패키지가 필요한 경우 데이터베이스 관리자와 조정하여 패키지가 인스턴스와 함께 설치되도록 합니다. SQL Server는 보안 환경으로, 패키지를 설치할 수 있는 위치에 대한 제한 사항이 있습니다. 권한이 있는 경우에도 패키지를 코드의 일부로 임시 설치하지 않는 것이 좋습니다. 또한 서버 라이브러리에 새 패키지를 설치하기 전에 항상 보안 문제를 신중하게 고려해야 합니다.


<a name="create-iris-remotely"></a>

## <a name="5---create-test-data"></a>5 - 테스트 데이터 만들기

원격 서버에 데이터베이스를 만들 수 있는 권한이 있는 경우 다음 코드를 실행하여 이 문서의 나머지 단계에 사용되는 Iris 데모 데이터베이스를 만들 수 있습니다.

### <a name="1---create-the-irissql-database-remotely"></a>1 - 원격으로 irissql 데이터베이스 만들기

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

### <a name="2---import-iris-sample-from-sklearn"></a>2 - SkLearn에서 Iris 샘플 가져오기

```python
from sklearn import datasets
import pandas as pd

# SkLearn has the Iris sample dataset built in to the package
iris = datasets.load_iris()
df = pd.DataFrame(iris.data, columns=iris.feature_names)
```

### <a name="3---use-revoscalepy-apis-to-create-a-table-and-load-the-iris-data"></a>3 - Revoscalepy API를 사용하여 테이블을 만들고 Iris 데이터 로드

```python
from revoscalepy import RxSqlServerData, rx_data_step

# Example of using RX APIs to load data into SQL table. You can also do this with pyodbc
table_ref = RxSqlServerData(connection_string=connection_string.format(new_db_name), table="iris_data")
rx_data_step(input_data = df, output_file = table_ref, overwrite = True)

print("New Table Created: Iris")
print("Sklearn Iris sample loaded into Iris table")
```

## <a name="6---test-remote-connection"></a>6 - 원격 연결 테스트

다음 단계를 수행하기 전에 SQL Server 인스턴스에 대한 사용 권한과 [Iris 샘플 데이터베이스](../tutorials/demo-data-iris-in-sql.md)에 대한 연결 문자열이 있는지 확인합니다. 데이터베이스가 존재하지 않고 충분한 사용 권한이 있는 경우 [이러한 인라인 지침을 사용하여 데이터베이스를 만들 수](#create-iris-remotely) 있습니다.

연결 문자열을 유효한 값으로 바꿉니다. 샘플 코드는 `"Driver=SQL Server;Server=localhost;Database=irissql;Trusted_Connection=Yes;"`를 사용하지만 코드에서 인스턴스 이름과 데이터베이스 사용자 로그인에 매핑되는 자격 증명 옵션을 사용하여 원격 서버를 지정해야 합니다.

### <a name="define-a-function"></a>함수 정의

다음 코드는 이후 단계에서 SQL Server로 보내는 함수를 정의합니다. 실행되면 원격 서버에서 데이터 및 라이브러리(revoscalepy, pandas, matplotlib)를 사용하여 iris 데이터 세트의 산점도를 만듭니다. 브라우저에서 렌더링하기 위해 .png의 바이트 스트림을 Jupyter Notebook으로 다시 반환합니다.

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

### <a name="send-the-function-to-sql-server"></a>함수를 SQL Server로 보내기

이 예에서는 원격 컴퓨팅 컨텍스트를 만든 다음 [rx_exec](/machine-learning-server/python-reference/revoscalepy/rx-exec)를 사용하여 함수 실행을 SQL Server로 보냅니다. **rx_exec** 함수는 컴퓨팅 컨텍스트를 인수로 허용하므로 유용합니다. 원격으로 실행하려는 모든 함수에는 컴퓨팅 컨텍스트 인수가 있어야 합니다. [rx_lin_mod](/machine-learning-server/python-reference/revoscalepy/rx-lin-mod)와 같은 일부 함수는 이 인수를 직접 지원합니다. 지원하지 않는 작업의 경우 **rx_exec** 를 사용하여 원격 컴퓨팅 컨텍스트에서 코드를 전달할 수 있습니다.

이 예제에서는 SQL Server에서 Jupyter Notebook으로 원시 데이터를 전송할 필요가 없었습니다. 모든 계산은 Iris 데이터베이스 내에서 발생하며 이미지 파일만 클라이언트에 반환됩니다.

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

다음 스크린샷은 입력 및 산점도 출력을 보여 줍니다.

  ![산점도 출력을 보여 주는 Jupyter Notebook](media/jupyter-notebook-scatterplot.png)


<a name="install-ide"></a>

## <a name="7---start-python-from-tools"></a>7 - 도구에서 Python 시작

개발자가 여러 버전의 Python에서 자주 작업하므로 설치 프로그램은 Python을 경로에 추가하지 않습니다. 설치 프로그램에서 설치된 Python 실행 파일과 라이브러리를 사용하려면 IDE를 **revoscalepy** 및 **microsoftml** 을 제공하는 경로의 **Python.exe** 에 연결합니다. 

### <a name="command-line"></a>명령 줄

C:\Program Files\Microsoft\PyForMLS(또는 Python 클라이언트 라이브러리 설치에 지정한 위치)에서 **Python.exe** 를 실행하면 전체 Anaconda 배포 및 Microsoft Python 모듈인 **revoscalepy** 및 **microsoftml** 에 액세스할 수 있습니다.

1. C:\Program Files\Microsoft\PyForMLS로 이동한 다음 **Python.exe** 를 두 번 클릭합니다.
2. 대화형 도움말을 가져옵니다. `help()`
3. 도움말 프롬프트에 다음 모듈 이름을 입력합니다. `help> revoscalepy`. 도움말은 이름, 패키지 콘텐츠, 버전 및 파일 위치를 반환합니다.
4. **도움말>** 프롬프트: `revoscalepy`에서 버전 및 패키지 정보를 반환합니다. Enter 키를 몇 번 눌러 도움말을 종료합니다.
5. 모듈을 가져옵니다. `import revoscalepy`


### <a name="jupyter-notebooks"></a>Jupyter Notebook

이 문서에서는 기본 제공 Jupyter Notebook을 사용하여 **revoscalepy** 에 대한 함수 호출을 보여 줍니다. 이 도구를 처음 접하는 경우 다음 스크린샷에서는 해당 부분이 결합되는 방식과 함께 "작동"하는 이유를 보여 줍니다. 

C:\Program Files\Microsoft\PyForMLS 상위 폴더에는 Anaconda 및 Microsoft 패키지가 포함되어 있습니다. Jupyter Notebook은 Anaconda의 Scripts 폴더 아래에 포함되어 있으며 Python 실행 파일은 Jupyter Notebook에 자동으로 등록됩니다. 데이터 과학 및 기계 학습에 사용되는 세 가지 Microsoft 패키지를 포함하여 사이트 패키지에서 찾을 수 있는 패키지를 노트로 가져올 수 있습니다.

  ![실행 파일 및 라이브러리](media/jupyter-notebook-python-registration.png)

다른 IDE를 사용하는 경우 도구에 Python 실행 파일 및 함수 라이브러리를 연결해야 합니다. 다음 섹션에서는 일반적으로 사용되는 도구에 대한 지침을 제공합니다.

### <a name="visual-studio"></a>Visual Studio

[Visual Studio에 Python](https://code.visualstudio.com/docs/languages/python)이 있는 경우 다음 구성 옵션을 사용하여 Microsoft Python 패키지가 포함된 Python 환경을 만듭니다.

| 구성 설정 | 값 |
|-----------------------|-------|
| **접두사 경로** | C:\Program Files\Microsoft\PyForMLS |
| **인터프리터 경로** | C:\Program Files\Microsoft\PyForMLS\python.exe |
| **창 인터프리터** | C:\Program Files\Microsoft\PyForMLS\pythonw.exe |

Python 환경을 구성하는 방법에 대한 도움말은 [Visual Studio의 Python 환경 관리](/visualstudio/python/managing-python-environments-in-visual-studio)를 참조하세요.

### <a name="pycharm"></a>PyCharm

PyCharm에서 인터프리터를 Machine Learning Server가 설치한 Python 실행 파일로 설정합니다.

1. 새 프로젝트의 설정에서 **로컬 추가** 를 클릭합니다.

2. `C:\Program Files\Microsoft\PyForMLS\`를 입력합니다.

이제 **revoscalepy**, **microsoftml** 또는 **azureml** 모듈을 가져올 수 있습니다. **도구** > **Python 콘솔** 을 선택하여 대화형 창을 열 수도 있습니다.

## <a name="next-steps"></a>다음 단계

SQL Server에 대한 도구와 작업 연결이 있으므로 [SSMS(SQL Server Management Studio)](../../ssms/download-sql-server-management-studio-ssms.md)를 사용하여 Python 빠른 시작을 통해 기술을 확장합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server Machine Learning Services를 사용하여 간단한 Python 스크립트 만들기 및 실행](../tutorials/quickstart-python-create-script.md)