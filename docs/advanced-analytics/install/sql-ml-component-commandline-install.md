---
title: R 및 Python 구성 요소를 학습 하는 SQL Server 컴퓨터의 설치 명령 프롬프트 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/21/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 77b68c6206e069a29821549998714a671239ca56
ms.sourcegitcommit: 9528843359cc43b9c66afac363f542ae343266e9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/22/2018
ms.locfileid: "40434873"
---
# <a name="install-sql-server-machine-learning-r-and-python-components-from-the-command-line"></a>SQL Server machine learning 명령줄에서 R 및 Python 구성 요소 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 intalling SQL Server machine learning 명령줄에서 구성 요소에 대 한 지침을 제공 합니다.

+ [새 데이터베이스 인스턴스](#indb)
+ [기존 데이터베이스 엔진 인스턴스에 추가 합니다.](#add-existing)
+ [자동 설치](#silent)
+ [새 독립 실행형 서버](#shared-feature)

설치 사용자 인터페이스를 사용 하 여 자동, 기본 또는 전체 상호 작용을 지정할 수 있습니다. 이 문서를 보완 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), R 및 Python 기계 학습 구성 요소에 고유한 매개 변수를 포함 합니다.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

+ 관리자 권한 명령 프롬프트에서 명령이 실행된 합니다. 

+ 데이터베이스 엔진 인스턴스를이 데이터베이스의 설치 필요 합니다. 수 있지만 단지 R 또는 Python 기능을 설치할 수 없습니다 [기존 인스턴스를 증분 방식으로 추가할](#add-existing)합니다. 데이터베이스 엔진 없이 R 및 Python만 하려는 경우 설치 합니다 [독립 실행형 서버](#shared-feature)합니다.

+ 장애 조치 클러스터에 설치 하지 마세요. R 및 Python 프로세스 격리에 사용 되는 보안 메커니즘을 Windows Server 장애 조치 클러스터 환경과 호환 되지 않습니다.

+ 도메인 컨트롤러에 설치 하지 마세요. Machine Learning 서비스에 대 한 부분 설치 하지 못합니다.

+ 동일한 컴퓨터에 독립 실행형 응용 프로그램과 데이터베이스 인스턴스를 설치 하지 마세요. 독립 실행형 서버 설치 둘 다의 성능을 저해 하면서 같은 리소스를 경합 합니다.


## <a name="command-line-arguments"></a>명령줄 인수

기능 인수가 용어 계약을 라이선싱 하는 대로 필요 합니다. 

명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다. /QS 스위치를 사용하면 진행률만 표시되고 입력이 허용되지 않으므로 오류가 발생해도 오류 메시지가 표시되지 않습니다. /QS 매개 변수는 /Action=install이 지정된 경우에만 지원됩니다.

| 인수 | Description |
|-----------|-------------|
| / 기능 AdvancedAnalytics = | 데이터베이스의 버전을 설치 합니다: SQL Server 2017 Machine Learning Services (In-database) 또는 SQL Server 2016 R Services (In-database).  |
| / 기능 SQL_INST_MR = | SQL Server 2017만 적용 됩니다. AdvancedAnalytics를이 쌍으로 연결 합니다. Microsoft R Open 및 전용 R 패키지를 포함 하 여 (데이터베이스 내) R 기능을 설치 합니다. SQL Server 2016 R Services 기능은 R 전용 이므로 해당 릴리스에 대 한 매개 변수가 있습니다.|
| / 기능 SQL_INST_MPY = | SQL Server 2017만 적용 됩니다. AdvancedAnalytics를이 쌍으로 연결 합니다. Anaconda 및 전용 Python 패키지를 포함 하 여 (In-database) Python 기능을 설치 합니다. |
| / 기능 = SQL_SHARED_MR | 독립 실행형 버전에 대 한 R 기능을 설치 합니다: SQL Server 2017 Machine Learning Server (독립 실행형) 또는 SQL Server 2016 R Server (독립 실행형). 독립 실행형 서버는 "공유 기능" 데이터베이스 엔진 인스턴스에 바인딩되지 않습니다.|
| / 기능 SQL_SHARED_MPY = | SQL Server 2017만 적용 됩니다. 독립 실행형 버전에 대 한 Python 기능을 설치 합니다: SQL Server 2017 Machine Learning Server (독립 실행형). 독립 실행형 서버는 "공유 기능" 데이터베이스 엔진 인스턴스에 바인딩되지 않습니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소를 사용 하 여에 대 한 사용 약관에 동의한 것을 나타냅니다. |
| /IACCEPTPYTHONLICENSETERMS | Python 구성 요소를 사용 하 여에 대 한 사용 약관에 동의한 것을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server를 사용 하 여에 대 한 사용 약관에 동의한 것을 나타냅니다.|
| /MRCACHEDIRECTORY | 오프 라인 설치에 대 한 R 구성 요소 CAB 파일이 포함 된 폴더를 설정 합니다. |
| / MPYCACHEDIRECTORY | 오프 라인 설치에 대 한 Python 구성 요소 CAB 파일이 포함 된 폴더를 설정 합니다. |


## <a name="indb"></a> 데이터베이스 인스턴스 설치

데이터베이스 내 분석을 추가 하는 데 필요한 데이터베이스 엔진 인스턴스를 사용할 수는 **AdvancedAnalytics** 기능을 설치 합니다. 고급 분석을 사용 하 여 데이터베이스 엔진 인스턴스를 설치할 수 있습니다 또는 [기존 인스턴스에 추가](#add-existing)합니다. 

진행률 정보 없이 대화형 화면의 프롬프트를 보려면 /qs 인수를 사용 합니다.

> [!IMPORTANT]
> 설치 후 두 개의 추가 구성 단계가 남아 있습니다. 이러한 작업 수행 될 때까지 통합을 완전 하지 않습니다. 참조 [post-installation tasks](#post-install) 지침에 대 한 합니다.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: 데이터베이스 엔진, Python 및 R을 사용한 고급 분석

데이터베이스 엔진 인스턴스를 설치 하는 동시에 대 한 인스턴스 이름 및 관리자 (Windows) 로그인을 제공 합니다. 모든 라이선스 약관에 동의 뿐만 아니라 핵심 언어 구성 요소를 설치 하기 위한 기능이 포함 됩니다.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이 같은 명령을 사용 하 여 데이터베이스 엔진에서 SQL Server 로그인을 사용 하 여 하지만 혼합 인증 합니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이 예제에서는 Python 전용 이며, 표시 언어 기능을 생략 하 여 추가할 수 있습니다.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: 데이터베이스 엔진 및 R 사용 하 여 고급 분석

이 명령은 SQL Server 2017로 하지만 Python 요소 없이 되지 않는 SQL Server 2016 설치 프로그램에서 사용할 수 있습니다.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> 설치 후 구성 (필수)

데이터베이스 설치에만 적용 됩니다.

설치가 완료 되 면 R 및 Python, Microsoft R 및 Python 패키지, Microsoft R Open, Anaconda, 도구, 샘플 및 배포의 일부인 스크립트를 사용 하 여 데이터베이스 엔진 인스턴스를 해야 합니다. 

설치를 완료 하려면 두 개 더 많은 작업이 필요 합니다.

1. 데이터베이스 엔진 서비스를 다시 시작 합니다.

1. 기능을 사용 하기 전에 외부 스크립트를 사용 합니다. 지침을 따릅니다 [설치 SQL Server 2017 Machine Learning Services (In-database)](sql-machine-learning-services-windows-install.md) 다음 단계로 합니다. 

SQL Server 2016의 경우 대신이 문서 [설치할 SQL Server 2016 R Services (In-database)](sql-r-services-windows-install.md)합니다.

## <a name="add-existing"></a> 기존 데이터베이스 엔진 인스턴스에 고급 분석을 추가 합니다.

데이터베이스 내 고급 분석에 기존 데이터베이스 엔진 인스턴스를 추가할 때 인스턴스 이름을 제공 합니다. 예를 들어, SQL Server 2017 데이터베이스 엔진 및 Python을 이전에 설치한 경우이 명령을 사용할 수 있습니다이 R.를 추가 하려면

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> 자동 설치

자동 설치를.cab 파일 위치에 대 한 검사를 하지 않습니다. 이 따라서가에 대 한.cab 파일 압축을 풀 수를 저장할 위치를 지정 해야 합니다. 이 대 한 임시 디렉터리를 수 있습니다.
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> 독립 실행형 서버 설치

독립 실행형 서버는 "공유 기능" 데이터베이스 엔진 인스턴스에 바인딩되지 않습니다. 다음 예제에서는 두 릴리스에 대 한 올바른 구문을 보여 줍니다.

SQL Server 2017에서는 독립 실행형 서버에 Python 및 R을 지원합니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016은 R 전용:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

설치가 완료 되는 서버, Microsoft 패키지, R 및 Python, 도구, 샘플 및 배포의 일부인 스크립트의 오픈 소스 배포 하는 것이 있습니다. 

SQL Server\140 \Program files\Microsoft (또는 130)로 이동 \R_SERVER\bin\x64 R 콘솔 창을 열고를 두 번 클릭 **RGui.exe**합니다. R을 처음 사용하세요? 이 자습서 학습 해 보기: [기본 R 명령 및 RevoScaleR 함수: 25 일반적인 예로](https://docs.microsoft.com/machine-learning-server/r/tutorial-r-to-revoscaler)합니다.

Python 명령을 열려면 a m files\microsoft SQL Server\140\PYTHON_SERVER\bin\x64 이동 하 고 두 번 클릭 **python.exe**합니다.

## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드를 사용 하 여 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대 한 답변을 다음 문서를 참조 하세요.

* [업그레이드 및 설치 FAQ-Machine Learning 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 R을 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: T-SQL에서 R 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 이러한 자습서를 수행 하 여 SQL Server를 사용 하 여 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: t-sql로 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.