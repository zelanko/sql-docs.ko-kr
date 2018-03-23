---
title: SQL Server와 함께 사용 하기 위해 Python 클라이언트 도구 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2018
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.service: ''
ms.component: python
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d81c3db5c1d1f4658ff9490316fe2311ba96c66f
ms.sourcegitcommit: 34766933e3832ca36181641db4493a0d2f4d05c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2018
---
# <a name="set-up-python-client-tools-for-use-with-sql-server"></a>Python SQL Server와 함께 사용 하기 위해 클라이언트 도구 설정 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에는 SQL Server에서 Python 코드를 실행을 지원 하도록 Windows 컴퓨터에서 Python 환경을 구성 하는 방법을 설명 합니다. 다음과 같은 시나리오는 다음과 같습니다.

+ 원격 Python 워크스테이션에서 솔루션을 개발 및 SQL Server 계산 컨텍스트에서 실행을 위해 SQL Server에 코드를 보내 테스트 합니다. 

    일반적으로 모든 기능을 갖춘 Python 개발 환경을 설치 하려고 합니다. 
    
    로컬 Python 환경 해야 SQL Server 인스턴스에서 Python 환경과 호환 되며 원격 계산 컨텍스트를 지 원하는 라이브러리를 설치 해야 합니다.

+ 하면 개발 및 전용된 Python 도구를 사용 하 여 코드를 테스트 한 후 저장된 프로시저에서 실행 되도록 SQL Server에 코드를 마이그레이션하십시오.

    모든 기능을 갖춘 인 Python IDE를 사용 하 여 개발 하는 경우에 서버. 그러나 코드를 배포 하기 전에 SQL Server 환경을 에뮬레이션 하는 환경에서 테스트 것입니다.

+ 주로 SQL Server에서 저장된 프로시저에서 Python 코드를 실행 하 고 Python 코드를 개발 하지 않습니다. 코드 테스트 되 고 저장된 프로시저에서 래핑하기 전에 디버깅을 예상 합니다. 그러나 경우에 따라 문제의 원인을 확인 하려면 SQL Server 외부 코드를 실행 하려면 할 수 있습니다.

    모든 Python 도구는 서버에 설치 하지 않으려면 및 분포와 함께 설치 하는 기본 도구만 사용 합니다. 저장된 프로시저 외부의 코드 작동 하는지 확인 하려면 인스턴스 라이브러리를 사용 하는 Python 환경을 구성할 수도 있습니다.

## <a name="requirements"></a>요구 사항

Python 코드를 개발 하는 데 어떤 도구에 관계 없이 다음 요구 사항을 SQL Server에서 Python 코드를 실행 하거나 SQL Server 데이터를 사용할 때마다 적용 됩니다.

+ Python을 사용 하려면 2017 또는 그 이후 버전의 SQL Server가 필요 합니다. 또한 컴퓨터 학습 Services (In-database)를 지 원하는 기능을 설치 하 고 기능을 명시적으로 설정 해야 합니다. 자세한 내용은 참조 [SQL Server 2017 설정](../r/set-up-sql-server-r-services-in-database.md)합니다.

    SQL Server 2017의 초기 릴리스는를 설치한 경우이 명령줄 유틸리티에서 Python 명령을 실행 하려고 하면 오류가 발생할 수 있습니다. 하는 것이 좋습니다 있습니다 [최신 버전으로 업그레이드](#bkmk_update) 가능한 경우. 

+ Python 코드를 실행할 수 있는 권한을 데이터베이스에 연결 하는 데 사용 하 여 코드를 실행할 계정에 확인 해야 합니다. 특별 권한 `EXECUTE ANY EXTERNAL SCRIPT` Python 또는 R 스크립트를 사용 하는 모든 계정에 필요 합니다. 

+ 계정에 데이터를 읽거나 새 개체를 만들 필요할 수 있는 데이터베이스 권한이 있는지 확인 해야 합니다. 

+ 코드에 필요한 SQL Server와 함께 기본적으로 설치 되지 않은 패키지를 인스턴스에서 사용 하는 Python 환경에 설치 된 패키지가 있으면 데이터베이스 관리자와 함께 정렬 됩니다. SQL Server는 보안 된 환경 및 패키지를 설치할 수 있습니다에 대 한 제한이 있습니다. 

    코드의 일부로 임시 설치 패키지의 권한이 있는 경우에 권장 되지 않습니다. 또한 서버 라이브러리의 새 패키지를 설치 하기 전에 고려해 보안 관련 문제 항상 신중 하 게 합니다.

> [!NOTE]
> 하려는 경우 Python을 사용 하 여 Linux 또는 Spark 클러스터와 같은 추가 계산 컨텍스트를 지 원하는 컴퓨터 학습 서버와 이러한 문서를 참조 하십시오.
> 
> + [Windows에서 사용자 지정 Python 패키지 및 인터프리터를 로컬로 설치 하는 방법](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter)
> + [Python 도구 및 Ide 학습 서버 컴퓨터와 함께 설치 된 Python 인터프리터를 연결합니다](https://docs.microsoft.com/machine-learning-server/python/quickstart-python-tools)

## <a name="default-tools-included-with-standard-install"></a>표준 설치에 포함 된 기본 도구

SQL Server 2017 컴퓨터 학습 Services (in-database)와 Python의 기본 설치는 다음과 같은 표준 Python 도구와 리소스를 추가합니다.

+ Python 예제 데이터
+ 4.2 anaconda 배포 
+ 실행 파일 python.exe Python 및 pythonw.exe

기본적으로이 폴더에 설치는: `~\Program Files\Microsoft SQL Server\<instance_name>\PYTHON_SERVICES`합니다. 

## <a name="open-python-from-the-command-line"></a>명령줄에서 Python을 열려면 

인스턴스와 함께 설치 하는 Python 런타임의 사용 하려면 실행 Python 설치 경로에서 시작할 수 있습니다. 사용할 수 있는 기본 지침의 [Python에 대 한 Windows FAQ](https://docs.python.org/3/faq/windows.html)합니다.

> [!IMPORTANT]
> 일반적으로 리소스 경합을 방지 하려면 좋습니다 있습니다 **없는** 가능 하다 고 생각 하는 경우 인스턴스 라이브러리에서 Python을 서버에서 실행 된 SQL Server 인스턴스가 실행 되 고 Python 코드입니다. 그러나 인스턴스 라이브러리에는 도구를 사용 하 여 SQL Server에서 실행 하는 경우에 발생 하는 문제를 디버깅 하 고 보다 자세한 오류 메시지를 보거나 모든 필수 패키지가 설치 되어 있는지 확인 하려고 하는 경우 유용 수 있습니다.

1. 인스턴스 라이브러리를 설치한 폴더로 이동 합니다. 예를 들어 기본 설치에서 폴더는 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES`합니다.

2. Python.exe를 찾습니다. 

3. 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행** 를 대화형 명령줄 창을 엽니다.

## <a name="bkmk_update"></a> Python 구성 요소 업데이트

여기 설명 된 스크립트를 사용 하 여 다운로드 하 여 최신 버전을 설치 Python 구성 요소를 업데이트할 수 있습니다: [windows 설치 Python 클라이언트](https://docs.microsoft.com/machine-learning-server/install/python-libraries-interpreter#install-on-windows)
> 
> 스크립트에서 다운로드 한 설치 관리자는 [SPO_9.3.0.0_1033.cab](https://go.microsoft.com/fwlink/?LinkId=859054&clcid=1033)합니다. 다른 버전을 필요한 경우 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](http://bing.com)

## <a name="set-up-a-python-development-environment"></a>Python 개발 환경 설정

명령줄에서 스크립트 단순히 디버깅 하는 경우 텍스트 편집기를 사용 하 또는 컴퓨터 학습 서비스와 함께 설치 된 표준 Python 도구를 사용 하 여 얻을 수 있습니다. 그러나 새 솔루션을 개발 하거나 원격 클라이언트에서 작업 하는 경우 사용 하는 모든 기능을 갖춘 인 Python IDE 보세요. 인기 있는 옵션이 있습니다.

+ [Visual Studio 2017 Community Edition](https://www.visualstudio.com/vs/features/python/) python
+ [Visual Studio 용 AI 도구](https://docs.microsoft.com/visualstudio/ai/installation)
+ [Visual Studio Code에서 Python](https://code.visualstudio.com/docs/languages/python)
+ PyCharm, Spyder, 및 Eclipse와 같은 인기 있는 타사 도구

Visual Studio 컴퓨터 학습 프로젝트 뿐 아니라 데이터베이스 프로젝트를 지원 하기 때문에 권장 됩니다. Python 환경 구성 도움말을 참조 하세요. [Visual Studio에서 관리 하는 Python 환경](https://docs.microsoft.com/visualstudio/python/managing-python-environments-in-visual-studio)

## <a name="install-revoscalepy"></a>Revoscalepy 설치

로드 하려고 할 때 오류가 발생할 수 컴퓨터 학습 서비스를 성공적으로 설치한 경우에 **revoscalepy** Python 명령줄에서 함수입니다. 다음이 단계에 사용 하도록 설정에 대 한 업데이트를 설치 하는 방법을 설명 **revoscalepy**합니다.

1. 설치 셸 스크립트를 다운로드 https://aka.ms/mls93-py (사용 또는 https://aka.ms/mls-py 는 9.2에 대 한 합니다. 릴리스)입니다. 스크립트 앞에 나열 된 모든 패키지와 함께 3.5.2, Python을 포함 하는 Anaconda 4.2.0를 설치 합니다.

2. 관리자로 승격 된 권한으로 PowerShell 창을 새로 엽니다.

3. 폴더를 다운로드 한 설치 관리자를 열고 스크립트를 실행 합니다.

```ps1
cd {{download-directory}}
.\Install-PyForMLS.ps1
```

실행할 수도 있습니다는 `-InstallFolder` 명령줄 인수는 명령의 일부로 새 경로 지정 합니다. 예를 들어 

```ps1
.\Install-PyForMLS.ps1 -InstallFolder "<installation_path>")
```

오류가 발생 하는 경우 일시 중단 하는 특정 파일에 대 한 실행 정책을 세션 기간 동안 다음과 같이 해야 합니다. 

```ps1
powershell -ExecutionPolicy Bypass -File "C:\<installation_path>\Install-PyForMLS.ps1"
```

세션의 기간에 대 한 실행 정책을 일시 중지할 수 있습니다. 이 문을 사용 하 여 실행 정책 설정은 `Unrestricted` 세션의 기간에 대 한 구성을 변경 되거나 않는 한 변경 내용을 디스크에 기록 합니다.

```ps1
Set-ExecutionPolicy Bypass -Scope Process
```

## <a name="verify-that-python-and-revoscalepy-are-working"></a>Python 및 revoscalepy 작동 하는지 확인 하십시오.

모든 도구 및 라이브러리를 설치한 후 서버에 연결 하 고 계산 컨텍스트를 만들 수 있습니다 또는 Python SQL Server와 통신할 수 있는지 확인 해야 합니다.

### <a name="verify-that-revoscalepy-works-from-the-python-command-line"></a>Python 명령줄에서 해당 revoscalepy 작동 확인

되었는지 확인 하 고 **revoscalepy** 모듈을 로드할 수 있는 Python 대화형 명령 프롬프트에서 다음 샘플 코드를 실행 합니다. 코드에서 Python 샘플 데이터를 사용 하 여 데이터 요약을 생성 하 고 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary)합니다. 

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

Python의 인스턴스를 호출 하 고 확인할 수 있도록 샘플 데이터 경로가 인쇄 됩니다.

### <a name="verify-that-python-can-be-called-from-sql-server"></a>SQL Server에서 Python을 호출할 수 있는지 확인 하십시오.

Python SQL Server와 통신 하를 확인 하려면 SQL Server Management Studio를 엽니다. (등 다른 유사한 도구를 사용할 수 [SQL 작업 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is).) 새 **쿼리** 저장된 프로시저의 컨텍스트에서 모든 단순 Python 명령 창 및 실행 합니다.

```SQL
EXEC sp_execute_external_script @language = N'Python', 
@script = N'print(3+4)'
```

Python 런타임은 처음으로 실행 하려면 시간이 걸릴 수 있습니다는 몰라도 오류가 있을 경우 SQL Server 실행 패드를 작동 하 고 SQL Server에서 Python을 시작할 수 있습니다.

확인 하려면 **revoscalepy** 를 바탕으로 스크립트를 실행 하는 SQL Server 인스턴스 라이브러리에서 사용할 수 [rx_summary](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-summary), 몇 가지 약간의 수정이 SQL Server와 호환 되는 결과를 생성 합니다. 

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

Rx_summary 형식의 개체를 반환 하기 때문에 `class revoscalepy.functions.RxSummary.RxSummaryResults`, SQL Server에서 결과 처리 하도록 여러 요소를 포함 하, 테이블 형식으로 데이터 프레임에만 추출할 수 있습니다.

### <a name="verify-python-execution-in-sql-server-as-remote-compute-context"></a>SQL Server의 원격 연산 컨텍스트로 Python 실행 되었는지 확인

설치한 경우 **revoscalepy** 로컬 Python 개발 환경에서 여기서 Python을 사용 하는 SQL Server 2017의 인스턴스에 연결할 수 없고 compute로 서버를 사용 하 여 유사한 코드 샘플을 실행 해야 컨텍스트입니다. 


```Python
import os
from revoscalepy import rx_summary, RxOptions, RxXdfData, RxSqlServerData, RxInSqlServer

# define connection string and compute context
sql_conn_string="Driver=SQL Server;Server=;Database=TestDB;Trusted_Connection=True"
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

이 샘플에서는 요약 개체는 SQL Server에 올바른 형식의 테이블 형식 데이터를 반환 하지 않고 콘솔에 반환 됩니다. 

또한 때문에 [rx_set_compute_context](https://docs.microsoft.com/machine-learning-server/python-reference/revoscalepy/rx-set-compute-context) 되었습니다 호출 샘플 데이터가 로드 되 고 SQL Server 컴퓨터에서 샘플 폴더에서을 로컬 샘플 폴더에서가 아니라 합니다.
