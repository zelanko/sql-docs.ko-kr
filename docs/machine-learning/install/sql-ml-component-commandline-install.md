---
title: 명령 프롬프트에서 설치
description: SQL Server 명령줄 설치 프로그램을 실행하여 Python 및 R이 포함된 Machine Learning Services를 SQL Server 데이터베이스 엔진 인스턴스에 추가합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/25/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 8e32b14682c7813dd911b52e80249cf6af7ebaac
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96122757"
---
# <a name="install-sql-server-machine-learning-services-with-r-and-python-from-the-command-line"></a>명령줄에서 R 및 Python을 사용하여 SQL Server Machine Learning Services 설치
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

이 문서에서는 명령줄에서 Python 및 R이 포함된 [SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)를 설치하는 방법에 대한 지침을 제공합니다.

자동, 기본, 전체 상호 작용 등 설치 프로그램 사용자 인터페이스 사용 방식을 지정할 수 있습니다. 이 문서에서는 R 및 Python 기계 학습 구성 요소에 고유한 매개 변수를 포함하여 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 보완합니다.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

+ 관리자 권한 명령 프롬프트에서 명령을 실행합니다. 

+ 데이터베이스 내 설치에는 데이터베이스 엔진 인스턴스가 필요합니다. [기존 인스턴스에 증분식으로 추가](#add-existing)할 수 있지만 R 또는 Python 기능만 설치할 수는 없습니다. 데이터베이스 엔진 없이 R 및 Python을 사용하려면 [독립 실행형 서버](#shared-feature)를 설치합니다.

+ 장애 조치(Failover) 클러스터에는 설치할 수 없습니다. R 및 Python 프로세스 격리에 사용되는 보안 메커니즘이 Windows Server 장애 조치(failover) 클러스터 환경과 호환되지 않기 때문입니다.

+ 도메인 컨트롤러에는 설치하지 마세요. 설치 시 Machine Learning Services 부분이 실패하게 됩니다.

+ 동일한 컴퓨터에 독립 실행형 인스턴스와 데이터베이스 내 인스턴스를 함께 설치하지 마세요. 독립 실행형 서버가 동일한 리소스에 대해 경합하여 두 설치 모두 성능이 저하됩니다.

## <a name="command-line-arguments"></a>명령줄 인수

**/FEATURES** 인수는 사용 약관과 마찬가지로 필수입니다. 

명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 **/Q** 매개 변수를 사용하는 완전 자동 모드 또는 **/QS** 매개 변수를 사용하는 단순 자동 모드를 지원합니다. **/QS** 스위치를 사용하면 진행률만 표시되고 입력이 허용되지 않으므로 오류가 발생해도 오류 메시지가 표시되지 않습니다. **/QS** 매개 변수는 **/Action=install** 이 지정된 경우에만 지원됩니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| 인수 | Description |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 데이터베이스 내 버전을 설치합니다. (SQL Server R Services(데이터베이스 내))  |
| /FEATURES = SQL_SHARED_MR | 독립 실행형 버전용 R 기능을 설치합니다. (SQL Server R Server(독립 실행형)) 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소의 사용 약관에 동의했음을 나타냅니다. |
| /IACCEPTPYTHONLICENSETERMS | Python 구성 요소의 사용 약관에 동의했음을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server 사용 약관에 동의했음을 나타냅니다.|
| /MRCACHEDIRECTORY | 오프라인 설치의 경우 R 구성 요소 CAB 파일이 포함된 폴더를 설정합니다. |
::: moniker-end

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
| 인수 | Description |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 데이터베이스 내 버전을 설치합니다. (SQL Server Machine Learning Services(데이터베이스 내))  |
| /FEATURES = SQL_INST_MR | AdvancedAnalytics와 페어링합니다. Microsoft R Open 및 전용 R 패키지를 포함하여 R 기능(데이터베이스 내)을 설치합니다. |
| /FEATURES = SQL_INST_MPY | AdvancedAnalytics와 페어링합니다. Anaconda 및 전용 Python 패키지를 포함하여 Python 기능(데이터베이스 내)을 설치합니다. |
| /FEATURES = SQL_SHARED_MR | 독립 실행형 버전용 R 기능을 설치합니다. (SQL Server Machine Learning Server(독립 실행형)) 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /FEATURES = SQL_SHARED_MPY | 독립 실행형 버전용 Python 기능을 설치합니다. (SQL Server Machine Learning Server(독립 실행형)) 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소의 사용 약관에 동의했음을 나타냅니다. |
| /IACCEPTPYTHONLICENSETERMS | Python 구성 요소의 사용 약관에 동의했음을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server 사용 약관에 동의했음을 나타냅니다.|
| /MRCACHEDIRECTORY | 오프라인 설치의 경우 R 구성 요소 CAB 파일이 포함된 폴더를 설정합니다. |
| /MPYCACHEDIRECTORY | 다음에 사용하도록 예약됩니다. %TEMP%를 사용하여 인터넷이 연결되지 않은 컴퓨터에 설치할 Python 구성 요소 CAB 파일을 저장합니다. |
::: moniker-end

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
| 인수 | Description |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 데이터베이스 내 버전을 설치합니다. (SQL Server Machine Learning Services(데이터베이스 내))  |
| /FEATURES = SQL_INST_MR | AdvancedAnalytics와 페어링합니다. Microsoft R Open 및 전용 R 패키지를 포함하여 R 기능(데이터베이스 내)을 설치합니다. |
| /FEATURES = SQL_INST_MPY | AdvancedAnalytics와 페어링합니다. Anaconda 및 전용 Python 패키지를 포함하여 Python 기능(데이터베이스 내)을 설치합니다. |
| /FEATURES = SQL_INST_MJAVA | AdvancedAnalytics와 페어링합니다. Open JRE를 포함하여 Java 기능(데이터베이스 내)을 설치합니다. |
| /FEATURES = SQL_SHARED_MR | 독립 실행형 버전용 R 기능을 설치합니다. (SQL Server Machine Learning Server(독립 실행형)) 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /FEATURES = SQL_SHARED_MPY | 독립 실행형 버전용 Python 기능을 설치합니다. (SQL Server Machine Learning Server(독립 실행형)) 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소의 사용 약관에 동의했음을 나타냅니다. |
| /IACCEPTPYTHONLICENSETERMS | Python 구성 요소의 사용 약관에 동의했음을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server 사용 약관에 동의했음을 나타냅니다.|
| /MRCACHEDIRECTORY | 오프라인 설치의 경우 R 구성 요소 CAB 파일이 포함된 폴더를 설정합니다. |
| /MPYCACHEDIRECTORY | 다음에 사용하도록 예약됩니다. %TEMP%를 사용하여 인터넷이 연결되지 않은 컴퓨터에 설치할 Python 구성 요소 CAB 파일을 저장합니다. |
::: moniker-end

## <a name="in-database-instance-installations"></a><a name="indb"></a> 데이터베이스 내 인스턴스 설치

데이터베이스 내 분석은 데이터베이스 엔진 인스턴스에 사용할 수 있으며, 설치에 **AdvancedAnalytics** 기능을 추가하는 데 필요합니다. 고급 분석이 포함된 데이터베이스 엔진 인스턴스를 설치하거나 [기존 인스턴스에 추가](#add-existing)할 수 있습니다. 

대화형 화면 프롬프트 없이 진행률 정보를 보려면 /qs 인수를 사용합니다.

> [!IMPORTANT]
> 설치 후에는 두 개의 추가 구성 단계가 남습니다. 이러한 작업을 수행하기 전에는 통합이 완료되지 않습니다. 지침은 [설치 후 작업](#post-install)을 참조하세요.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server Machine Learning Services: 데이터베이스 엔진, Python 및 R을 사용한 고급 분석

데이터베이스 엔진 인스턴스의 동시 설치를 위해 인스턴스 이름 및 관리자(Windows) 로그인을 제공합니다. 코어 및 언어 구성 요소를 설치하는 기능뿐만 아니라 모든 사용 약관에 대한 동의를 포함합니다.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이는 동일한 명령이지만 혼합 인증을 사용하여 데이터베이스 엔진에 로그인하는 SQL Server 로그인이 포함되어 있습니다.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이 예제는 Python 전용이며 기능 하나를 생략하여 언어를 하나 추가할 수 있음을 보여 줍니다.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services: 데이터베이스 엔진, R을 사용한 고급 분석

데이터베이스 엔진 인스턴스의 동시 설치를 위해 인스턴스 이름 및 관리자(Windows) 로그인을 제공합니다. 코어 및 언어 구성 요소를 설치하는 기능뿐만 아니라 모든 사용 약관에 대한 동의를 포함합니다.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install-configuration-required"></a><a name="post-install"></a> 설치 후 구성(필수)

데이터베이스 내 설치에만 적용됩니다.

설치가 완료되면 R 및 Python을 포함하는 데이터베이스 엔진 인스턴스, Microsoft R 및 Python 패키지, Microsoft R Open, Anaconda, 도구, 샘플 및 스크립트를 배포의 일부로 사용할 수 있습니다. 

설치를 완료하려면 다음 두 가지 작업을 더 수행해야 합니다.


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. 데이터베이스 엔진 서비스를 다시 시작합니다.

1. SQL Server Machine Learning Services: 기능을 사용하려면 외부 스크립트를 사용하도록 설정합니다. 다음 단계로 [SQL Server Machine Learning Services(데이터베이스 내) 설치](sql-machine-learning-services-windows-install.md)의 지침을 수행합니다. 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. 데이터베이스 엔진 서비스를 다시 시작합니다.

1. SQL Server R Services: 기능을 사용하려면 외부 스크립트를 사용하도록 설정합니다. 다음 단계로 [SQL Server R Services(데이터베이스 내) 설치](sql-r-services-windows-install.md)의 지침을 수행합니다. 
::: moniker-end

## <a name="add-advanced-analytics-to-an-existing-database-engine-instance"></a><a name="add-existing"></a> 기존 데이터베이스 엔진 인스턴스에 고급 분석 추가

기존 데이터베이스 엔진 인스턴스에 데이터베이스 내 고급 분석을 추가할 때 인스턴스 이름을 제공합니다. 예를 들어 이전에 SQL Server 2017 이상 데이터베이스 엔진과 Python을 설치한 경우 이 명령을 사용하여 R을 추가할 수 있습니다.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent-install"></a><a name="silent"></a> 자동 설치

자동 설치는 .cab 파일 위치 확인을 표시하지 않습니다. 따라서 .cab 파일의 압축을 풀 위치를 지정해야 합니다. Python의 경우 CAB 파일은 %TEMP*에 위치해야 합니다. R의 경우 이를 위한 임시 디렉터리를 사용하여 폴더 경로를 설정할 수 있습니다.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="standalone-server-installations"></a><a name="shared-feature"></a> 독립 실행형 서버 설치

독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다. 다음 예제에서는 독립 실행형 서버를 설치하기 위한 올바른 구문을 보여 줍니다.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Server는 독립 실행형 서버에서 Python 및 R을 지원합니다.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
SQL Server R Server는 R 전용입니다.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

설치가 완료되면 서버, Microsoft 패키지, R 및 Python의 오픈 소스 배포, 도구, 샘플 및 스크립트를 배포의 일부로 사용할 수 있습니다. 

R 콘솔 창을 열려면 `\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64`로 이동하고 **RGui.exe** 를 두 번 클릭합니다. R을 처음 사용하세요? 다음 자습서를 사용해 보세요. [기본 R 명령 및 RevoScaleR 함수: 25개 공통 예제](/machine-learning-server/r/tutorial-r-to-revoscaler).

Python 명령을 열려면 `\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64`로 이동하고 **python.exe** 를 두 번 클릭합니다.

## <a name="next-steps"></a>다음 단계

Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [Python 자습서: SQL Server Machine Learning Services에서 선형 회귀를 사용하여 스키 대여 예측](../tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python 자습서: Categorizing customers using k-means clustering with SQL Server Machine Learning Services](../tutorials/python-clustering-model.md)(SQL Server Machine Learning Services에서 k-평균 클러스터링을 사용하여 고객 분류)

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [빠른 시작: T-SQL에서 R 사용](../tutorials/quickstart-r-create-script.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/r-taxi-classification-introduction.md)
