---
title: "명령 프롬프트의 SQL Server 컴퓨터에 대 한 학습 구성 요소 설치 | Microsoft Docs"
ms.custom: 
ms.date: 03/15/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.workload: Inactive
ms.openlocfilehash: c51d8299837f0eda02a07afe1ea4d34d3ecd5e31
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-machine-learning-components-from-the-command-line"></a>명령줄에서 SQL Server 컴퓨터에 대 한 학습 구성 요소를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는 명령줄에서 구성 요소를 학습 intalling SQL Server 컴퓨터에 대 한 지침을 제공 합니다.

+ [데이터베이스에서 인스턴스](#indb)
+ [기존 데이터베이스 엔진 인스턴스 추가](#add-existing)
+ [자동 설치](#silent)
+ [독립 실행형 서버](#shared-feature)

설치 사용자 인터페이스와의 상호 작용 자동, 기본, 또는 전체를 지정할 수 있습니다. 이 문서를 보완 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md), R 및 Python 컴퓨터 학습 구성 요소에 고유한 매개 변수를 포함 합니다.

## <a name="pre-install-checklist"></a>설치 전 검사 목록

+ 관리자 권한 명령 프롬프트에서 명령이 실행된 합니다. 

+ 데이터베이스 엔진 인스턴스는 데이터베이스에 설치 필요 합니다. 수 있지만 단지 Python 또는 R 기능을 설치할 수 없습니다 [기존 인스턴스에 증분식으로 추가](#add-existing)합니다. 데이터베이스 엔진 없이 R 및 Python만 하려는 경우 설치는 [독립 실행형 서버](#shared-feature)합니다.

+ 장애 조치 클러스터에 설치 하지 마십시오. R 및 Python 프로세스를 격리 하기 위해 사용 되는 보안 메커니즘 Windows Server 장애 조치 클러스터 환경와 호환 되지 않습니다.

+ 도메인 컨트롤러에 설치 하지 마십시오. 설치 프로그램의 시스템 학습 서비스 부분 실패 합니다.

+ 동일한 컴퓨터에 독립 실행형 및 데이터베이스의 인스턴스를 설치 하지 않습니다. 독립 실행형 서버 두 설치의 성능을 저해 하면서 동일한 리소스를 경합 합니다.


## <a name="command-line-arguments"></a>명령줄 인수

기능 인수가 용어 계약을 라이선스 하는 대로 필요 합니다. 

명령 프롬프트에서 설치할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 /Q 매개 변수를 사용하는 완전 자동 모드 또는 /QS 매개 변수를 사용하는 단순 자동 모드를 지원합니다. /QS 스위치를 사용하면 진행률만 표시되고 입력이 허용되지 않으므로 오류가 발생해도 오류 메시지가 표시되지 않습니다. /QS 매개 변수는 /Action=install이 지정된 경우에만 지원됩니다.

| 인수 | Description |
|-----------|-------------|
| /FEATURES = AdvancedAnalytics | 데이터베이스의 버전을 설치: SQL Server 2017 컴퓨터 학습 Services (In-database) 또는 SQL Server 2016 R Services (In-database).  |
| /FEATURES = SQL_INST_MR | SQL Server 2017만 적용 됩니다. 쌍으로 연결 AdvancedAnalytics 합니다. Microsoft R Open 및 독점 R 패키지를 포함 하 여 (In-database) R 기능을 설치 합니다. SQL Server 2016 R Services 기능은 R 전용 이므로 릴리스에 대 한 매개 변수가 없습니다.|
| / 기능 SQL_INST_MPY = | SQL Server 2017만 적용 됩니다. 쌍으로 연결 AdvancedAnalytics 합니다. Anaconda 및 소유 Python 패키지를 포함 하 여 Python (In-database) 기능을 설치 합니다. |
| / 기능 SQL_SHARED_MR = | 독립 실행형 버전에 대 한 R 기능을 설치: SQL Server 2017 컴퓨터 학습 Server (독립 실행형) 또는 SQL Server 2016 R 서버 (독립 실행형). 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되어 있지 "공유 기능"입니다.|
| / 기능 SQL_SHARED_MPY = | SQL Server 2017만 적용 됩니다. 독립 실행형 버전에 대 한 Python 기능을 설치: SQL Server 2017 컴퓨터 학습 서버 (독립 실행형). 독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되어 있지 "공유 기능"입니다.|
| /IACCEPTROPENLICENSETERMS  | 오픈 소스 R 구성 요소를 사용 하기 위한 사용 조건에 동의한 것을 나타냅니다. |
| / IACCEPTPYTHONLICENSETERMS | Python 구성 요소를 사용 하기 위한 사용 조건에 동의한 것을 나타냅니다. |
| /IACCEPTSQLSERVERLICENSETERMS | SQL Server를 사용 하기 위한 사용 조건에 동의한 것을 나타냅니다.|
| / MRCACHEDIRECTORY | 오프 라인 설치에 대 한 R 구성 요소 CAB 파일을 포함 하는 폴더를 설정 합니다. |
| / MPYCACHEDIRECTORY | 오프 라인 설치에 대 한 Python 구성 요소 CAB 파일을 포함 하는 폴더를 설정 합니다. |


## <a name="indb"></a> 데이터베이스 인스턴스 설치

데이터베이스에서 분석 데이터베이스 엔진 인스턴스를 추가 하는 데 필요한에 사용할 수 있는 **AdvancedAnalytics** 기능을 설치 합니다. 고급 분석에는 데이터베이스 엔진 인스턴스를 설치할 수 있습니다 또는 [기존 인스턴스 추가](#add-existing)합니다. 

대화형 없이 진행 상황 정보 화면에 나타나는 표시 되는 메시지를 보려면 /qs 인수를 사용 합니다.

> [!Important]
> 설치 후 두 개의 추가 구성 단계가 남아 있습니다. 이러한 작업은 수행 될 때까지 통합을 완전 하지 않습니다. 참조 [사후 설치 작업](#post-install) 지침에 대 한 합니다.

### <a name="sql-server-2017-database-engine-advanced-analytics-with-python-and-r"></a>SQL Server 2017: 데이터베이스 엔진, 고급 Python 및 R 분석

데이터베이스 엔진 인스턴스를 설치 하는 동시에 대 한 인스턴스 이름 및 관리자 (Windows) 로그인을 제공 합니다. 코어 및 언어 구성 요소 뿐 아니라 모든 라이선스 조건에 대 한 동의 설치 하기 위한 기능이 포함 됩니다.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이 같은 명령을 사용 하 여 데이터베이스 엔진에서 SQL Server 로그인을 사용 하지만 혼합 인증 합니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY
/INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<sql-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS
```

이 예제는 Python만 표시 기능을 생략 하 여 한 언어를 추가할 수 있습니다.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTPYTHONLICENSETERMS
```

### <a name="sql-server-2016-database-engine-and-advanced-analytics-with-r"></a>SQL Server 2016: 데이터베이스 엔진 및 R 사용 하는 고급 분석

이 명령은 같습니다. SQL Server 2017 아니라 Python 요소 없이에서 사용할 수 없는 SQL Server 2016 설치 합니다.

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<Windows-username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS 
```

## <a name="post-install"></a> 설치 후 구성 (필수)

데이터베이스 설치에만 해당에 적용 됩니다.

설치가 완료 되 면 R 및 Python, Microsoft R 및 Python 패키지, Microsoft R Open, Anaconda, 도구, 샘플 및 스크립트는 배포의 일부인 사용 하는 데이터베이스 엔진 인스턴스를 수 있습니다. 

두 개 더 많은 작업 함께 설치를 완료 해야 합니다.

1. 데이터베이스 엔진 서비스를 다시 시작 합니다.

1. 외부 스크립트 사용 하도록 설정 기능을 사용할 수 있습니다. 지침에 따라 [설치할 SQL Server 2017 컴퓨터 학습 Services (In-database)](sql-machine-learning-services-windows-install.md) 다음 단계로 합니다. 

SQL Server 2016에 대 한이 항목을 대신 사용 [설치할 SQL Server 2016 R Services (In-database)](sql-r-services-windows-install.md)합니다.

## <a name="add-existing"></a> 기존 데이터베이스 엔진 인스턴스에 고급 분석을 추가 합니다.

고급 분석 데이터베이스에서 기존 데이터베이스 엔진 인스턴스를 추가할 때 인스턴스 이름을 제공 합니다. 예를 들어 SQL Server 2017 데이터베이스 엔진 및 Python, 이전에 설치한 경우이 명령을 사용할 수 있습니다이 오른쪽을 추가 하려면

```  
Setup.exe /qs /ACTION=Install /FEATURES=SQL_INST_MR /INSTANCENAME=MSSQLSERVER 
/IACCEPTSQLSERVERLICENSETERMS  /IACCEPTROPENLICENSETERMS
```



## <a name="silent"></a> 자동 설치

자동 설치.cab 파일 위치를 확인을 하지 않습니다. 이러한 이유로.cab 파일 압축 풀기을 저장할 위치를 지정 해야 합니다. 이 대 한 임시 디렉터리를 수 있습니다.
 
```  
Setup.exe /q /ACTION=Install /FEATURES=SQLEngine,ADVANCEDANALYTICS,SQL_INST_MR,SQL_INST_MPY 
/INSTANCENAME=MSSQLSERVER /SQLSYSADMINACCOUNTS="<username>" 
/IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS 
/MRCACHEDIRECTORY=%temp% /MPYCACHEDIRECTORY=%temp%
```

## <a name="shared-feature"></a> 독립 실행형 서버 설치

독립 실행형 서버는 데이터베이스 엔진 인스턴스에 바인딩되어 있지 "공유 기능"입니다. 다음 예에서는 두 릴리스에 대 한 올바른 구문을 보여 줍니다.

SQL Server 2017 독립 실행형 서버에서 Python 및 R을 지원합니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR,SQL_SHARED_MPY  
/IACCEPTROPENLICENSETERMS /IACCEPTPYTHONLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

SQL Server 2016은 R 전용:

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR 
/IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

설치가 완료 되는 서버, Microsoft 패키지, R 및 Python, 도구, 샘플 및 스크립트는 배포의 일부인의 오픈 소스 배포 하는 것이 해야 합니다. 

Files\microsoft SQL Server\140 (또는 130)으로 서 \R_SERVER\bin\x64는 R 콘솔 창을 열고 다음을 두 번 클릭을 **RGui.exe**합니다. R을 처음 사용하세요? 다음 자습서: [기본 R 명령과 RevoScaleR 함수: 25는 일반적인 예제](https://docs.microsoft.com/en-us/machine-learning-server/r/tutorial-r-to-revoscaler)합니다.

Python 명령, a m files\microsoft SQL Server\140\PYTHON_SERVER\bin\x64 이동을 열려면 두 번 클릭 **python.exe**합니다.

## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드로 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자 몇 가지 간단한 예제 차별화할 수 및 R SQL Server와 함께 작동 하는 방법에 대 한 기본 사항을 설명 합니다. 다음 단계에서는 다음 링크 참조:

+ [자습서: T-SQL에서 R을 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는이 자습서를 수행 하 여 SQL Server와 함께 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.