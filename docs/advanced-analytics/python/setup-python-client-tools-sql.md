---
title: SQL Server Machine Learning 사용에 대 한 Python 클라이언트 도구 설정 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 6f6823870060992586756dffa93aac6937d27d65
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40401303"
---
# <a name="set-up-python-client-tools-for-use-with-sql-server-machine-learning"></a>Python을 사용 하 여 SQL Server Machine Learning을 사용 하 여에 대 한 클라이언트 도구 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Python 통합은 SQL Server 2017 이상 버전에서는 Machine Learning Services (In-database)에 Python 지원을 추가할 때부터 사용할 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md)합니다.

이 문서에서는 Python에 사용할 수 있도록 원격 SQL Server에 연결할 수 있도록 개발 워크스테이션을 구성 하는 방법에 알아봅니다.

### <a name="evaluation-and-independent-development"></a>평가 및 독립 개발
 
Developer edition 및 SQL Server로 이동 하려는 Python 스크립트를 로컬로 작업할 계획 있다면 있습니다 수 건너 뛰 세요 [IDE 설치](#install-ide) SQL Server에서 사용 되는 로컬 Python 라이브러리 도구를 가리킵니다.

> [!Tip]
> 데모 및 비디오 연습을 참조 하세요 [실행 R 및 Python 원격으로 원하는 IDE 또는 Jupyter Notebook에서 SQL server에서](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/) 이 [YouTube 비디오](https://youtu.be/D5erljpJDjE)합니다.

## <a name="1---install-python-packages"></a>1-Python 패키지를 설치 합니다.

로컬 워크스테이션에는 SQL Server에 있는 것과 동일한 Python 패키지 버전을 있어야 합니다.: revoscalepy 및 microsftml 합니다. 추가 Python 패키지를 사용할 수 있지만-인스턴스가 아닌 독립 실행형 Machine Learning Server 컨텍스트에서 다른 시나리오를 사용 하 여 더 일반적으로 사용 됩니다. 

1. 설치 셸 스크립트를 다운로드 [ https://aka.ms/mls93-py ](https://aka.ms/mls93-py) (사용할지 [ https://aka.ms/mls-py ](https://aka.ms/mls-py) 의 9.2에 대 한 합니다. 릴리스)입니다. 스크립트 앞에 나열 된 모든 패키지와 함께 Python 3.5.2를 포함 하는 Anaconda 4.2.0을 설치 합니다.

  Python 구성 요소를 통해 제공 됩니다 [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033)합니다. 다른 버전에 필요한 경우 참조 [CAB 다운로드](../install/sql-ml-cab-downloads.md)

2. 관리자 권한으로 PowerShell 창을 엽니다 (마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행**).

3. 설치 관리자를 다운로드 하는 폴더로 이동한 스크립트를 실행 합니다. 추가 된 `-InstallFolder` 명령줄 인수를 라이브러리에 대 한 폴더 위치를 지정 합니다. 예를 들어: 

   ```python
   cd {{download-directory}}
   .\Install-PyForMLS.ps1 -InstallFolder "C:\path-to-python-for-mls")
   ```

   설치를 완료 하려면 시간이 소요 됩니다. PowerShell 창에서 진행률을 모니터링할 수 있습니다. 설치가 완료 되 면 전체 집합을 패키지 해야 합니다. 예를 들어 지정한 `C:\mspythonlibs` 에서 패키지를 찾습니다는 폴더 이름으로 `C:\mspythonlibs\Lib\site-packages`입니다. 그렇지 않은 경우 기본 폴더는 `C:\Program Files\Microsoft\PyForMLS1`합니다.

새 python 인터프리터 및 방금 설치한 모듈을 도구에 자동으로 제공 되므로 설치 스크립트를 컴퓨터에 PATH 환경 변수를 수정 하지 않습니다. 도구에는 Python 인터프리터 및 라이브러리를 연결에 대 한 도움말을 참조 하세요 [IDE를 설치 하는 5-](#install-ide)합니다.

<a name="python-tool"></a>
 
## <a name="2---open-a-python-prompt"></a>2-Python 프롬프트를 열으십시오

기본 제공 도구 및 revoscalepy 등 microsoftml 제품별 라이브러리 외에도 데이터를 포함 하는 Microsoft에서 Python 통합 합니다. 다음 항목은 설치가 완료 되 면 클라이언트와 서버 인스턴스에서 사용할 수 있습니다.

+ Python 샘플 데이터
+ 4.2 anaconda 배포 
+ Python 실행 파일 python.exe 및 pythonw.exe

> [!Tip] 
> 권장 합니다 [Python에 대 한 Windows FAQ](https://docs.python.org/3/faq/windows.html) 일반 purppose에 대 한 내용은 Windows에서 Python 프로그램을 실행 합니다.

### <a name="on-client-workstations"></a>클라이언트 워크스테이션에서

사용 하 여 설치 스크립트에 의해 설치 된 Python 실행 파일:

1. 로 `C:\Program Files\Microsoft\PyForMLS\python.exe` 설치 경로 대해 선택한 모든 위치 또는 합니다.

2. 마우스 오른쪽 단추로 클릭 **Python.exe** 선택한 **관리자 권한으로 실행** 는 대화형 명령줄 창을 엽니다.

### <a name="on-sql-server"></a>SQL server

SQL Server 설치 프로그램을 서버 인스턴스에 표준 Python 도구 및 리소스를 추가합니다. Developer edition을 사용 하는 Python 버전을 확인 하거나 임시 명령을 실행 하려는 경우:

1. 로 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`합니다.

2. 마우스 오른쪽 단추로 클릭 **Python.exe** 선택한 **관리자 권한으로 실행** 는 대화형 명령줄 창을 엽니다.

> [!Note]
> 일반적으로 리소스 경합을 방지 하려면 좋습니다 있습니다 **하지** 수 있다면 인스턴스 라이브러리에서 Python을 서버에서 실행할 SQL Server 인스턴스가 실행 되 고 Python 코드입니다. 그러나 인스턴스 라이브러리의 도구를 사용 하 여 SQL Server에서 실행 하는 경우에 발생 하는 문제를 디버그 및 자세한 오류 메시지를 보거나 모든 필수 패키지가 설치 되어 있는지 확인 하려는 경우에 중요 한 수 있습니다.

## <a name="3---permissions"></a>3-사용 권한

스크립트를 실행 하 여 데이터를 업로드 하는 SQL Server 인스턴스에 연결할 데이터베이스 서버의 유효한 로그인을 해야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합된 인증을 사용 하지만 일부 시나리오에 대 한 간단 SQL 로그인을 사용 하 여 권장 합니다.

최소한 코드를 실행 하는 데 사용 된 계정, 사용 중인와 특별 한 사용 권한을 모든 외부 스크립트를 실행 합니다. 데이터베이스에서 읽을 수 있는 권한이 있어야 합니다. 대부분의 개발자도 스크립트를 포함 하는 저장된 프로시저의 형태로 새 개체를 만들 수 있는 권한이 필요할 및 학습 데이터를 포함 하는 테이블에 데이터를 쓸 또는 데이터의 점수를 매긴 합니다. 

Python을 사용 하는 데이터베이스의 계정에 대해 다음 권한을 구성 하려면 데이터베이스 관리자에 게 문의 합니다.

+ **EXECUTE ANY EXTERNAL SCRIPT** 서버에서 Python을 실행 합니다.
+ **db_datareader** 모델 학습에 사용 되는 쿼리를 실행 하는 권한입니다.
+ **db_datawriter** 점수가 매겨진된 데이터 또는 학습 데이터를 쓸 수 있습니다.
+ **db_owner** 저장된 프로시저와 같은 개체를 만들 테이블을 함수입니다. 
  해야 **db_owner** 샘플 및 테스트 데이터베이스를 만들 수 있습니다. 

코드에서 SQL Server를 사용 하 여 기본적으로 설치 되지 않은 패키지에 필요한 경우 데이터베이스 관리자의 인스턴스와 함께 설치 된 패키지에 정렬 합니다. SQL Server는 보안된 환경 및 패키지를 설치할 수 있습니다에 제한이 있습니다. 코드의 일부로 임시 설치 패키지의 권한이 있는 경우에 권장 되지 않습니다. 또한 보안 관련 문제를 것이 좋습니다 server 라이브러리에서 새 패키지를 설치 하기 전에 항상 신중 하 게 합니다.

## <a name="4---test-connections"></a>4-테스트 연결

모든 도구 및 라이브러리를 설치한 후 서버에 연결 및 계산 컨텍스트를 만들 수 있습니다 또는 Python SQL Server와 통신할 수 있는지 확인 됩니다.

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>Python 명령줄에서 해당 revoscalepy 작동 확인

확인 합니다 **revoscalepy** 모듈을 로드할 수 있는 Python 대화형 명령 프롬프트에서 다음 샘플 코드를 실행 합니다. Python 샘플 데이터를 사용 하는 데이터 요약을 생성 하는 코드와 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)합니다. 

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

호출 되 고 Python의 인스턴스를 확인할 수 있도록 샘플 데이터 경로가 인쇄 됩니다.

### <a name="verify-that-python-can-be-called-from-a-local-sql-server"></a>로컬 SQL Server에서 Python을 호출할 수 있는지 확인 합니다.

로컬 개발 환경에서 Python 통신 하 고 있는 로컬을 사용 하 여 확인 [외부 스크립트에 대해 구성 된 SQL Server 인스턴스](../install/sql-machine-learning-services-windows-install.md)합니다. SQL Server Management Studio를 사용 하 여 새 열려는 **쿼리** 저장된 프로시저의 컨텍스트에서 모든 간단한 Python 명령 창과 실행:

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

처음으로 Python 런타임 시작 하는 데 걸릴 수 있습니다는 몰라도 오류가 없는 경우 SQL Server 실행 패드를 작동 하 고 SQL Server에서 Python을 시작할 수 있습니다.

확인 하려면 **revoscalepy** 바탕으로 스크립트를 실행 하는 SQL Server 인스턴스 라이브러리는 사용할 수 있습니다 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary), SQL Server와 호환 되는 결과를 생성할 일부 약간의 수정. 

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'
import os
from pandas import DataFrame
from revoscalepy import rx_summary
from revoscalepy import RxXdfData
from revoscalepy import RxOptions

sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay + DayOfWeek", ds)
print(summary)
dfsummary = summary.summary_data_frame
OutputDataSet = dfsummary
'
WITH RESULT SETS  ((ColName nvarchar(25) , ColMean float, ColStdDev  float, ColMin  float,   ColMax  float, Col_ValidObs  float, Col_MissingObs int))
```

Rx_summary 형식의 개체를 반환 하므로 `class revoscalepy.functions.RxSummary.RxSummaryResults`, SQL Server에서 결과 처리 하도록 여러 요소를 포함 하는, 테이블 형식으로 데이터 프레임에만 추출할 수 있습니다.

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>SQL Server의 원격 계산 컨텍스트로 Python 실행 확인

설치한 후 **revoscalepy** 로컬 Python 개발 환경에서 Python에 사용 되는 SQL Server 2017의 원격 인스턴스에 연결할 수 있습니다 및 서버를 사용 하 여 비슷한 코드 샘플을 실행 해야 합니다 컨텍스트를 계산 합니다. 

이 스크립트를 실행 하는 유효한 서버 이름 및 기존 데이터베이스를 지정 합니다. 이 스크립트는 데이터베이스를 사용 하지 않습니다 하지만 연결 문자열을 필요로 합니다.

```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=<server-name>;Database=TestDB;Trusted_Connection=True"
sqlcc = RxInSqlServer(
    connection_string = sql_conn_string,
    num_tasks = 1,
    auto_cleanup = False,
    console_output = True,
    execution_timeout_seconds = 0,
    wait = True
    )
rx_set_compute_context(sqlcc)

# get sample data and path
sample_data_path = RxOptions.get_option("sampleDataDir")
print(sample_data_path)

# generate summary
ds = RxXdfData(os.path.join(sample_data_path, "AirlineDemoSmall.xdf"))
summary = rx_summary("ArrDelay+DayOfWeek", ds)
print(summary)
```

이 샘플에서는 요약 개체는 SQL Server로 제대로 구성 된 테이블 형식 데이터를 반환 하지 않고 콘솔에 반환 됩니다. 

또한 때문 [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 되었습니다 호출 샘플 데이터가 로드 되 고 로컬 samples 폴더 아닌 컴퓨터의 SQL Server samples 폴더에서.


<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5-IDE를 설치 합니다.

명령줄에서 스크립트를 간단히 디버깅 하는 경우 표준 Python tools를 사용 하 여 가져올 수 있습니다. 그러나 새 솔루션을 개발 하거나 원격 클라이언트에서 작업 하는 경우 좋습니다 완전 한 Python IDE를 사용을 합니다. 인기 있는 옵션이 있습니다.

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) Python을 사용 하 여
+ [Visual Studio 용 AI 도구](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Visual Studio Code에서 Python](https://code.visualstudio.com/docs/languages/python)
+ PyCharm, Spyder를 및 Eclipse와 같은 인기 있는 타사 도구

Machine learning 프로젝트 뿐만 아니라 데이터베이스 프로젝트를 지원 하기 때문에 Visual Studio 좋습니다. Python 환경을 구성 하는 도움말을 참조 하세요 [Visual Studio에서 Python 환경 관리](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)합니다.

자주 개발자가 여러 버전의 Python 사용 하므로 설치 프로그램은 Python 경로에 추가 되지 않습니다. Python 실행 파일 및 설치 프로그램에서 설치 된 라이브러리를 사용 하려면 IDE에 연결 **Python.exe** revoscalepy 및 microsoftml도 제공 하는 경로입니다. 예를 들어, Visual Studio에서 Python 프로젝트의 경우 사용자 지정 환경을 지정 `C:\Program Files\Microsoft\PyForMLS`, `C:\Program Files\Microsoft\PyForMLS\python.exe` 하 고 `C:\Program Files\Microsoft\PyForMLS\pythonw.exe` 에 대 한 **접두사 경로**를 **인터프리터 경로**, 및  **창 인터프리터**, 각각.

추가 지침을 참조 하세요 [링크 Python 도구 및 Ide](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)합니다. 문서는 Microsoft Machine Learning Server에 대 한 기록 되므로 Python 경로 서로 다르지만 다양 한 도구에서 Python 라이브러리에 연결 하는 방법을 보여줍니다.

## <a name="next-steps"></a>다음 단계

SQL Server 작업 연결 및 도구를가지고 revoscalepy 함수 및 계산 컨텍스트를 전환 좀 더 자세히 살펴보려면 대 한 자습서를 단계별로 실행 합니다.

> [!div class="nextstepaction"]
> [Revoscalepy 및 원격 계산 컨텍스트를 사용 하 여 모델 만들기](../tutorials/use-python-revoscalepy-to-create-model.md)