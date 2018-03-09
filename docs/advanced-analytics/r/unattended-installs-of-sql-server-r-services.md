---
title: "컴퓨터 학습 서비스의 무인된 설치 | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: f1c7aaf35c0c58e9a7aab3c5b31725f586ffd2ac
ms.sourcegitcommit: 4edac878b4751efa57601fe263c6b787b391bc7c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/19/2018
---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>시스템 학습 services (In-database) 무인된 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 기계 학습 구성 요소를 설치 하려면 SQL Server 설치 프로그램을 명령줄 인수를 사용 하는 방법을 설명 합니다.

수행 하지 설치 마법사의 대화형 기능을 사용 하는 대신에 라이선스 계약 하 고 컴퓨터 학습 구성 요소에 대 한 SQL Server에 대 한 포함 하 여 전체 설치 하는 데 필요한 모든 인수를 제공 의미 무인 설치는 명령줄 또는 다른 이름으로 자동 모드에서 일반적으로 스크립트의 일부입니다.

+ [SQL Server 2016 R Services](#bkmk_OldInstall)
+ [SQL Server 2017 컴퓨터 학습 서비스](#bkmk_NewInstall) Python 또는 R
+ [Microsoft R 서버 또는 서버를 학습 하는 컴퓨터](../r/install-microsoft-r-server-from-the-command-line.md)

**적용 대상: SQL Server 2017 기계 학습 Services (In-database) SQL Server 2016 R Services**

## <a name="prerequisites"></a>필수 구성 요소

+ 기계 학습 사용할지 각 인스턴스에서 데이터베이스 엔진을 설치 해야 합니다.

+ 컴퓨터에 인터넷에 액세스 하는 경우에 구성 요소를 미리 학습 하는 컴퓨터에 대 한 설치 관리자를 다운로드 해야 합니다. 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](../r/installing-ml-components-without-internet-access.md)합니다.

+ 별도 R 및 Python에 대 한 매개 변수는 오픈 소스 구성 요소 각각에 대 한 라이선스. SQL Server 2016은만 R; SQL Server 2017 R 및 Python 모두 지원합니다. 설치 하는 각 언어에 대 한 사용 조건에 동의 해야 합니다. 명령줄에이 매개 변수를 포함 하지 않으면 설치에 실패 합니다.

+ 프롬프트에 응답 하지 않고 설치를 완료 하려면 라이선스에 대 한 기타 기능을 설치 하려는 경우도 포함 한 모든 필수 인수를 식별 해야 합니다.

+ **혼합** 초기 릴리스에서 지 원하는 SQL 로그인 보안 모드는 필요 합니다. 필요 하지 않더라도 SQL 로그인을 사용 하는 데이터 과학자 하 여 솔루션 개발을 지 원하는 혼합 모드 인증을 사용 하도록 설정 하는 것이 좋습니다.

> [!IMPORTANT]
> 
> 기능을 사용 하려면 설치가 완료 된 후에 추가 단계가 필요 합니다. 및이 포함 다시 구성 하는 인스턴스를 다시 시작 합니다. 에 섹션에 있는 모든 항목을 검토 하십시오 [사후 설치 단계](#bkmk_PostInstall) 설치가 완료 된 후 필요한 조치를 결정 합니다.

## <a name="bkmk_NewInstall"></a>  SQL Server 2017에 대 한 명령줄 설치

다음 예에 포함 된 **최소** 기능 필요 합니다.

> [!IMPORTANT]
> 관리자 권한 명령 프롬프트에서 모든 명령을 실행 해야 합니다.
> 
> 설치가 완료 된 후에 몇 가지 추가 단계가 필요 합니다. 참조 [이 여기서](#bkmk_PostInstall)합니다. 
> 구성이 완료 된 후에 SQL Server 서비스의 다른 다시 시작 해야 합니다.

### <a name="install-r-only"></a>R 설치만

다음 예제에서는 자동, 무인 모드로 수행 하는 데 필요한 인수 추가 R 언어와 SQL Server 2017 컴퓨터 services (In-database) 설치 합니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

SQL Server 2017에 R에 대 한 필요한 플래그 note:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MR`
+ `IACCEPTROPENLICENSETERMS`을 참조하세요.

### <a name="install-python-only"></a>Python 설치만

다음 예제에서는 자동, 무인 모드로 수행 하는 데 필요한 인수 추가 Python 언어와 함께 SQL Server 2017 컴퓨터 services (In-database) 설치 합니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

SQL Server 2017에 Python에 대 한 필요한 플래그 note:

+ `ADVANCEDANALYTICS`
+ `SQL_INST_MPY`
+ `IACCEPTPYTHONOPENLICENSETERMS`

### <a name="install-both-r-and-python-on-a-named-instance"></a>명명 된 인스턴스에 R와 Python 설치

다음 예제에서는 명명 된 인스턴스에서 SQL Server 2017 컴퓨터 services (In-database) 설치는 자동, 무인 모드로 수행 하는 데 필요한 인수를 보여 줍니다. R 및 Python 모두 언어 추가 됩니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER.ServerName /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS /IACCEPTPYTHONOPENLICENSETERMS
```

## <a name="OldInstall"></a> SQL Server 2016에 대 한 명령줄 설치
 
다음 예제에서는 자동, 무인 모드로 수행 하는 데 필요한 인수 추가 R 언어와 SQL Server 2016 설치를 보여 줍니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
```

R Services 2016에 대 한 필요한 플래그 note:

+ `ADVANCEDANALYTICS`
+ `IACCEPTROPENLICENSETERMS`

## <a name = "bkmk_PostInstall"></a>설치 후 추가 단계

SQL Server 설치 프로그램을 설치한 버전에 관계 없이 완료 된 후 다음 단계를 수행 해야 합니다. 컴퓨터 학습 기능 기본으로 사용 되지 않습니다 및 명시적으로 설정 해야 합니다.

1.  설치가 완료 된 후에 새 열 **쿼리** 창을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 기능을 설정 하려면 다음 명령을 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  기능을 명시적으로 설정 해야 하 고 다시 구성 합니다. 그렇지 않으면 것 됩니다는 기능을 설치 하는 경우에 외부 스크립트를 호출할 수 있습니다.
  
2.  다시 구성 된 인스턴스에 대 한 SQL Server 서비스를 다시 시작 합니다. 이렇게 자동으로 다시 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스 뿐입니다.

> [!IMPORTANT]
> 
> 사용자 지정 보안 구성이 있는 경우 또는 사용 하려는 SQL Server 계산 컨텍스트로 원격 클라이언트에서 Python 또는 R 코드를 실행 하는 경우 몇 가지 추가 단계가 필요할 수도 있습니다. 
> 
> 자세한 내용은 참조 [업그레이드 및 설치 FAQ](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.
