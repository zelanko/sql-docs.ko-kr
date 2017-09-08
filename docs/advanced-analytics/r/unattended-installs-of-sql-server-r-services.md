---
title: "컴퓨터 학습 서비스의 무인된 설치 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 77e92b2d-5777-4c31-bf02-f931ed54a247
caps.latest.revision: 18
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: babb74aa866404853cfef83e1d30159354f385e7
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="unattended-installation-of-machine-learning-services-in-database"></a>시스템 학습 services (In-database) 무인된 설치

이 항목에서는 자동 모드에서 데이터베이스 엔진의 인스턴스에 기계 학습을 설치 하려면 SQL Server 설치 프로그램을 명령줄 인수를 사용 하는 방법을 설명 합니다. 무인된 설치에서 설치 마법사의 대화형 기능을 사용 하지 않는 한 라이선스 컴퓨터 학습 구성 요소 및 SQL Server에 대 한 계약을 포함 하 여 전체 설치 하는 데 필요한 모든 인수를 제공 해야 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 Services (In-database)

> [!IMPORTANT]
> 
> SQL Server 2016 및 SQL Server 2017에서 기능을 사용 하려면 설치가 완료 된 후 추가 단계는 필요 합니다. 및이 포함 다시 구성 하는 인스턴스를 다시 시작 합니다. 모든 단계를 검토 해야 합니다.

## <a name="prerequisites"></a>필수 구성 요소

+ 기계 학습 사용할지 각 인스턴스에서 데이터베이스 엔진을 설치 해야 합니다.

+ 컴퓨터에 인터넷에 액세스 하는 경우에 구성 요소를 미리 학습 하는 컴퓨터에 대 한 설치 관리자를 설치 해야 합니다. 다운로드 위치에 대 한 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](../../advanced-analytics/r/installing-ml-components-without-internet-access.md)합니다.

+ R 및 Python에 대 한 오픈 소스 구성 요소에 관련 된 매개 변수를 라이선스 새 가지가 있습니다. 설치 하는 각 언어에 대 한 별도 인수로 사용 조건에 동의 해야 합니다. 명령줄에 이 매개 변수를 포함하지 않으면 설치가 실패합니다.

+ 프롬프트에 응답 하지 않고 설치를 완료 하려면 라이선스에 대 한 기타 기능을 설치 하려는 경우도 포함 한 모든 필수 인수를 식별 해야 합니다.

> [!NOTE] 
> 초기 릴리스는 혼합된 보안 모드를 지 원하는 SQL 로그인 해야 했습니다. 그러나 데이터 과학자 SQL 로그인을 사용 하 여 솔루션 개발을 지 원하는 혼합 모드 인증을 사용 하도록 설정 하는 것이 좋습니다.

## <a name="bkmk_NewInstall"></a>R 통한 학습 서비스 컴퓨터의 무인된 설치

다음 예제와 **최소** 자동, 무인된 수행할 때 명령줄에 지정 하려면 필요한 기능을 SQL Server 2017 컴퓨터 services (In-database) 설치 합니다.

1. 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 합니다.

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQLENGINE,ADVANCEDANALYTICS, SQL_INST_MR /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    
    참고 SQL Server 2017에 R에 대 한 필요한 플래그: `ADVANCEDANALYTICS`, `SQL_INST_MR`, 및 `IACCEPTROPENLICENSETERMS`합니다.
2. 서버를 다시 시작합니다.
3. 에 설명 된 대로 설치 후 구성 단계를 수행 [이 여기서](#bkmk_PostInstall)합니다. SQL Server 서비스의 또 다른 다시 시작 해야 합니다.

## <a name="OldInstall"></a>R Services (In-database) 무인된 설치.
 
 다음 예제와 **최소** SQL Server 2016 R 서비스의 자동, 무인된 수행할 때 명령줄에 지정 하려면 필요한 기능을 설치 합니다.

1. 관리자 권한 명령 프롬프트를 열고 다음 명령을 실행 합니다.

    ```  
    Setup.exe /q /ACTION=Install /FEATURES=SQL,ADVANCEDANALYTICS /INSTANCENAME=MSSQLSERVER /SECURITYMODE=SQL /SAPWD="%password%" /SQLSYSADMINACCOUNTS="<username>" /IACCEPTSQLSERVERLICENSETERMS /IACCEPTROPENLICENSETERMS
    ```
    R SERVICES 2016에 대 한 필요한 플래그 참고: `ADVANCEDANALYTICS` 및 `IACCEPTROPENLICENSETERMS`합니다.
2. 서버를 다시 시작합니다.
3. 에 설명 된 대로 설치 후 구성 단계를 수행 [이 여기서](#bkmk_PostInstall)합니다. SQL Server 서비스의 또 다른 다시 시작 해야 합니다.

## <a name = "bkmk_PostInstall"></a>설치 후 추가 단계

1.  설치가 완료 된 후에 새 열 **쿼리** 창을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 기능을 설정 하려면 다음 명령을 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
    > [!NOTE]
    >  기능을 명시적으로 설정 해야 하 고 다시 구성 합니다. 그렇지 않으면 것 됩니다는 기능을 설치 하는 경우에 외부 스크립트를 호출할 수 있습니다.
  
2.  다시 구성 된 인스턴스에 대 한 SQL Server 서비스를 다시 시작 합니다. 이렇게 자동으로 다시 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스 뿐입니다.

3. 사용자 지정 보안 구성이 있거나 SQL Server를 사용하여 원격 계산 컨텍스트를 지원할 경우 추가 단계가 필요할 수 있습니다. 자세한 내용은 [업그레이드 및 설치 FAQ](../../advanced-analytics/r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조하세요.

