---
title: R 및 Python 구성 요소에 대 한 명령 프롬프트 설치
description: SQL Server 명령줄 설치 프로그램을 실행 하 여 SQL Server 데이터베이스 엔진 인스턴스에 R 언어 및 Python 통합을 추가 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 07/30/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: f60aa3684778a7347b1ffd613a924c3bf0b7b94a
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271941"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>명령줄에서 SQL Server machine learning R 및 Python 구성 요소를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 명령줄에서 SQL Server machine learning 구성 요소를 설치 하는 방법에 대 한 지침을 제공 합니다.

+ [새 데이터베이스 내 인스턴스](#indb)
+ [기존 데이터베이스 엔진 인스턴스에 추가](#add-existing)
+ [자동 설치](#silent)
+ [새 독립 실행형 서버](#shared-feature)

설치 사용자 인터페이스를 사용 하 여 자동, 기본 또는 전체 상호 작용을 지정할 수 있습니다. 이 문서에서는 R 및 Python machine learning 구성 요소에 고유한 매개 변수를 포함 하 여 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)를 보완 합니다.

## <a name="pre-install-checklist"></a>사전 설치 검사 목록

+ 관리자 권한 명령 프롬프트에서 명령을 실행 합니다. 

+ 데이터베이스 내 설치에는 데이터베이스 엔진 인스턴스가 필요 합니다. [기존 인스턴스에 점진적으로 추가할](#add-existing)수는 있지만 R 또는 Python 기능만 설치할 수는 없습니다. 데이터베이스 엔진 없이 R 및 Python을 사용 하려는 경우 [독립 실행형 서버](#shared-feature)를 설치 합니다.

+ 장애 조치 (failover) 클러스터에를 설치 하지 않습니다. R 및 Python 프로세스를 격리 하는 데 사용 되는 보안 메커니즘은 Windows Server 장애 조치 (failover) 클러스터 환경과 호환 되지 않습니다.

+ 도메인 컨트롤러에를 설치 하지 마십시오. 설치 프로그램의 Machine Learning Services 일부가 실패 하 게 됩니다.

+ 동일한 컴퓨터에 독립 실행형 및 데이터베이스 내 인스턴스를 설치 하지 마십시오. 독립 실행형 서버는 동일한 리소스에 대해 경쟁 하며 두 설치의 성능을 모두 마이닝 합니다.


## <a name="command-line-arguments"></a>명령줄 인수

기능 인수는 라이선스 용어 계약과 마찬가지로 필수입니다. 

명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다. /QS 스위치를 사용하면 진행률만 표시되고 입력이 허용되지 않으므로 오류가 발생해도 오류 메시지가 표시되지 않습니다. /QS 매개 변수는 /Action=install이 지정된 경우에만 지원됩니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
| 인수 | 설명 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 데이터베이스 내 버전을 설치 합니다. SQL Server R Services (데이터베이스 내).  |
| /FEATURES = SQL_SHARED_MR | 독립 실행형 버전에 대 한 R 기능을 설치 합니다. R Server (독립 실행형)를 SQL Server 합니다. 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소를 사용 하기 위한 사용 조건에 동의 했음을 나타냅니다. |
| /IACCEPTPYTHONLICENSETERMS | Python 구성 요소 사용에 대 한 사용 조건에 동의 했음을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server 사용 조건에 동의 했음을 나타냅니다.|
| /MRCACHEDIRECTORY | 오프 라인 설치의 경우 R 구성 요소 CAB 파일이 포함 된 폴더를 설정 합니다. |
::: moniker-end

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
| 인수 | 설명 |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 데이터베이스 내 버전을 설치 합니다. Machine Learning Services (데이터베이스 내)를 SQL Server 합니다.  |
| /FEATURES = SQL_INST_MR | AdvancedAnalytics를 사용 하 여이를 페어링 합니다. Microsoft R Open 및 독점 R 패키지를 포함 하 여 (데이터베이스 내) R 기능을 설치 합니다. |
| /FEATURES = SQL_INST_MPY | AdvancedAnalytics를 사용 하 여이를 페어링 합니다. Anaconda 및 독점 Python 패키지를 포함 하 여 (데이터베이스 내) Python 기능을 설치 합니다. |
| /FEATURES = SQL_SHARED_MR | 독립 실행형 버전에 대 한 R 기능을 설치 합니다. SQL Server Machine Learning Server (독립 실행형). 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /FEATURES = SQL_SHARED_MPY | 독립 실행형 버전에 대 한 Python 기능을 설치 합니다. SQL Server Machine Learning Server (독립 실행형). 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소를 사용 하기 위한 사용 조건에 동의 했음을 나타냅니다. |
| /IACCEPTPYTHONLICENSETERMS | Python 구성 요소 사용에 대 한 사용 조건에 동의 했음을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server 사용 조건에 동의 했음을 나타냅니다.|
| /MRCACHEDIRECTORY | 오프 라인 설치의 경우 R 구성 요소 CAB 파일이 포함 된 폴더를 설정 합니다. |
| /MPYCACHEDIRECTORY | 나중에 사용하기 위해 예약되어 있습니다. 인터넷에 연결 되지 않은 컴퓨터에 설치할 Python 구성 요소 CAB 파일을 저장 하려면% TEMP%를 사용 합니다. |
::: moniker-end

## <a name="indb"></a>데이터베이스 내 인스턴스 설치

데이터베이스 내 분석은 **AdvancedAnalytics** 기능을 설치에 추가 하는 데 필요한 데이터베이스 엔진 인스턴스에 사용할 수 있습니다. 고급 분석이 포함 된 데이터베이스 엔진 인스턴스를 설치 하거나 [기존 인스턴스에 추가할](#add-existing)수 있습니다. 

대화형 화면 프롬프트 없이 진행률 정보를 보려면/qs 인수를 사용 합니다.

> [!IMPORTANT]
> 설치 후에는 두 개의 추가 구성 단계가 남아 있습니다. 이러한 작업을 수행 하기 전에는 통합이 완료 되지 않습니다. 지침은 [설치 후 작업](#post-install) 을 참조 하세요.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
### <a name="sql-server-machine-learning-services-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server Machine Learning Services: 데이터베이스 엔진, Python 및 R을 사용한 고급 분석

데이터베이스 엔진 인스턴스의 동시 설치를 위해 인스턴스 이름 및 관리자 (Windows) 로그인을 제공 합니다. 핵심 및 언어 구성 요소를 설치 하는 기능 뿐만 아니라 모든 사용 조건에 대 한 동의를 포함 합니다.

```cmd
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이와 동일한 명령 이지만 혼합 인증을 사용 하 여 데이터베이스 엔진에 대 한 SQL Server 로그인이 있습니다.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이 예제는 Python 전용 이며 기능을 생략 하 여 언어를 하나 추가할 수 있음을 보여 줍니다.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
### <a name="sql-server-r-services-database-engine-and-advanced-analytics-with-r"></a>SQL Server R Services: R을 사용 하 여 데이터베이스 엔진 및 고급 분석

데이터베이스 엔진 인스턴스의 동시 설치를 위해 인스턴스 이름 및 관리자 (Windows) 로그인을 제공 합니다. 핵심 및 언어 구성 요소를 설치 하는 기능 뿐만 아니라 모든 사용 조건에 대 한 동의를 포함 합니다.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```
::: moniker-end

## <a name="post-install"></a>설치 후 구성 (필수)

데이터베이스 내 설치에만 적용 됩니다.

설치가 완료 되 면 R 및 Python을 포함 하는 데이터베이스 엔진 인스턴스, Microsoft R 및 Python 패키지, Microsoft R Open, Anaconda, 도구, 샘플 및 배포의 일부인 스크립트를 사용할 수 있습니다. 

설치를 완료 하려면 다음 두 가지 작업을 더 수행 해야 합니다.


::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
1. 데이터베이스 엔진 서비스를 다시 시작 합니다.

1. SQL Server Machine Learning Services: 기능을 사용 하려면 외부 스크립트를 사용 하도록 설정 합니다. 다음 단계로 [SQL Server Machine Learning Services (데이터베이스 내) 설치](sql-machine-learning-services-windows-install.md) 의 지침을 따르세요. 
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
1. 데이터베이스 엔진 서비스를 다시 시작 합니다.

1. SQL Server R Services: 기능을 사용 하려면 외부 스크립트를 사용 하도록 설정 합니다. 다음 단계로 [SQL Server R Services 설치 (데이터베이스 내)](sql-r-services-windows-install.md) 의 지침을 따릅니다. 
::: moniker-end

## <a name="add-existing"></a>기존 데이터베이스 엔진 인스턴스에 고급 분석 추가

데이터베이스 내 고급 분석을 기존 데이터베이스 엔진 인스턴스에 추가할 때 인스턴스 이름을 제공 합니다. 예를 들어 이전에 SQL Server 2017 데이터베이스 엔진과 Python을 설치한 경우이 명령을 사용 하 여 R을 추가할 수 있습니다.

```cmd  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```

## <a name="silent"></a>자동 설치

자동 설치는 .cab 파일 위치에 대 한 검사를 표시 하지 않습니다. 따라서 .cab 파일의 압축을 풀 위치를 지정 해야 합니다. Python의 경우 CAB 파일은% TEMP *에 위치 해야 합니다. R의 경우이에 대 한 임시 디렉터리를 사용 하 여 폴더 경로를 설정할 수 있습니다.
 
```cmd  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% 
```

## <a name="shared-feature"></a>독립 실행형 서버 설치

독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되지 않은 "공유 기능"입니다. 다음 예에서는 독립 실행형 서버를 설치 하기 위한 올바른 구문을 보여 줍니다.

::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
SQL Server Machine Learning Server는 독립 실행형 서버에서 Python 및 R을 지원 합니다.

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end
::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
R Server SQL Server R 전용:

```cmd
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```
::: moniker-end

설치가 완료 되 면 배포에 포함 된 서버, Microsoft 패키지, R의 오픈 소스 배포와 Python, 도구, 샘플 및 스크립트를 사용할 수 있습니다. 

R 콘솔 창을 열려면로 `\Program files\Microsoft SQL Server\150 (or 140/130)\R_SERVER\bin\x64` 이동 하 고 **rgui**를 두 번 클릭 합니다. R을 처음 사용하세요? 이 자습서를 사용해 보세요. [기본 R 명령 및 RevoScaleR 함수: 25 개의 일반적인](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)예입니다.

Python 명령을 열려면로 `\Program files\Microsoft SQL Server\150 (or 140)\PYTHON_SERVER\bin\x64` 이동 하 여 **python**을 두 번 클릭 합니다.

## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드에 대 한 도움이 필요 하세요? 일반적인 질문과 알려진 문제에 대 한 답변은 다음 문서를 참조 하세요.

* [업그레이드 및 설치 FAQ-Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 실행 합니다.

* [SQL Server에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [자습서: T-SQL에서 R 사용](../tutorials/quickstart-r-create-script.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [자습서: Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)를 참조하세요.