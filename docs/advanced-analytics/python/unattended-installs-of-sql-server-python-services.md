---
title: "Python 컴퓨터 학습 services (In-database) 무인된 설치 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: r-services
ms.component: python
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: ec10bd25b3709a578ea5dee6c109da69ff7d3327
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="unattended-installation-of-python-machine-learning-services-in-database"></a>Python 컴퓨터 학습 services (In-database) 무인된 설치

이 항목에서는 컴퓨터 학습 서비스 및 자동 모드를 사용 하 여 Python을 사용 하 여 SQL Server 데이터베이스 엔진을 설치 하려면 SQL Server 2017 설치 프로그램에서 명령줄 인수를 사용 하는 방법에 설명 합니다.

> [!NOTE]
> 반드시의 사용권 계약, Python 및 SQL server에 대 한 명령줄 인수를 포함 합니다.

## <a name="prerequisites"></a>필수 구성 요소

설치 프로세스를 시작하기 전에 다음 요구 사항을 확인하세요.

+ Python 서비스는 SQL Server 2017 데이터베이스 엔진 독립적으로 설치할 수 없습니다. SQL 데이터베이스 엔진 기능을 포함 해야 합니다.
+ 오프 라인 설치를 수행 하는 경우에 필요한 Python 구성 요소를 사전에 다운로드 하 고 로컬 폴더를 복사 해야 합니다. 다운로드 위치에 대 한 참조 [컴퓨터 학습 구성 요소 설치 인터넷 연결 되지 않은](../../advanced-analytics/r-services/installing-ml-components-without-internet-access.md)합니다.
+ 새 매개 변수는 */IACCEPTPYTHONLICENSETERMS*, 나타내는 Continuum Analytics에서 제공 하는 Python 구성 요소를 사용 하 여에 대 한 사용 약관을 수락 했습니다. 명령줄에 이 매개 변수를 포함하지 않으면 설치가 실패합니다.
+ 프롬프트에 응답 하지 않고 설치를 완료 하려면 SQL Server 라이선스, 및 Python 및 설치 하려는 경우 다른 기능에 대 한 포함 한 모든 필수 인수를 식별 해야 합니다.
+  혼합된 모드 인증을 SQL Server 2016의 몇 가지 시험판 버전에서 필요 합니다. 데이터 과학자는 개발 하 고 원격으로 SQL 로그인을 사용 하 여 솔루션을 테스트 시나리오에서 유용할 수 있지만는 필요한 경우 더 이상.

## <a name="perform-an-unattended-installation-of-python-machine-learning-services-in-database"></a>Python 컴퓨터 학습 services (In-database) 무인된 설치 수행

다음 예제와 **최소** 기본 인스턴스에서 Python 및 데이터베이스 엔진의 자동, 무인 설치를 수행 하는 경우 명령줄에서 지정 하는 기능 필요 합니다.

> [!NOTE]
> 이 기능은 SQL Server 2017 필요합니다. Python은 SQL Server의 이전 버전에서 지원 되지 않습니다.

1. 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 합니다.

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS, SQL_INST_MPY /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTPYTHONLICENSETERMS
    ```

    > [!NOTE]
    > 
    > Python에 대 한 새 설치 플래그는: `SQL_INST_MPY` 및`IACCEPTPYTHONLICENSETERMS`

2. 지정 된 대로 서버를 다시 시작 합니다.
3. 에 설명 된 대로 설치 후 구성 단계를 수행 [이 여기서](#bkmk_PostInstall)합니다. SQL Server 서비스의 또 다른 다시 시작 해야 합니다.

## <a name = "bkmk_PostInstall"></a>설치 후 단계

1.  설치가 완료 된 후에 새 열 **쿼리** 창을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 기능을 설정 하려면 다음 명령을 실행 합니다.

    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  기능을 명시적으로 설정 해야 하 고 다시 구성 합니다. 그렇지 않으면 것 됩니다는 기능을 설치 하는 경우에 외부 스크립트를 호출할 수 있습니다.
  
3.  다시 구성 된 인스턴스에 대 한 SQL Server 서비스를 다시 시작 합니다. 이렇게 자동으로 다시 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스 뿐입니다.

3. 사용자 지정 보안 구성이 있거나 SQL Server를 사용하여 원격 계산 컨텍스트를 지원할 경우 추가 단계가 필요할 수 있습니다. 자세한 내용은 참조 [컴퓨터 학습 설치 문제 해결](../machine-learning-troubleshooting-faq.md)합니다.
