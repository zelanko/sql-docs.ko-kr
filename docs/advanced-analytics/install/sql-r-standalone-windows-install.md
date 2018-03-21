---
title: "SQL Server 2016 R Server (독립 실행형) 설치 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2018
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
ms.workload: On Demand
ms.openlocfilehash: 48f28b7a8d357e80e7defb6d6a8d446041380fbf
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/21/2018
---
# <a name="install-sql-server-2016-r-server-standalone"></a>SQL Server 2016 R Server (독립 실행형) 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 독립 실행형 버전을 설치 하려면 SQL Server 2016 설치 프로그램을 사용 하는 방법을 설명 **SQL Server 2016 R 서버**합니다. Enterprise Edition 또는 Software Assurance, 있는 경우 프로덕션 서버에 설치 하는 독립 실행형 R Server는 무료입니다.

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

SQL Server 2016가 필요 합니다. SQL Server 2017를 설정한 경우 설치 하십시오 [SQL Server 2017 컴퓨터 학습 서버 (독립 실행형)](sql-machine-learning-standalone-windows-install.md) 대신 합니다.

모든 이전 버전의 Revolution Analytics 도구 또는 패키지를 설치한 경우에 먼저 제거 해야 있습니다. 

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 패치 설치 요구 사항 

Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2016에 대 한 설치 마법사를 시작 합니다. 서비스 팩 1 이상을 설치 하는 것이 좋습니다.

2. 에 **설치** 탭을 클릭 **새 R Server (독립 실행형) 설치**합니다.
    
     ![R 서버 독립 실행형의 설치 프로그램을 시작](media/2016-setup-installation-rsvr.png "R 서버 독립 실행형의 설치를 시작 합니다.")
    
3.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
    **R 서버(독립 실행형)**  
    
    ![기능 선택 R Server 독립 실행형에 대 한](media/2016setup-rserver-features.png "기능 서버 독립 실행형 R에 대 한 선택")
    
    기타 모든 옵션은 무시해도 됩니다. 
    
    > [!NOTE]
    > 설치 하지 않습니다는 **공유 기능** R Services 이미 설치 되어 있는 SQL Server 데이터베이스에서 분석에 대 한 컴퓨터에서 설치를 실행 하는 경우. 중복 된 라이브러리를 만듭니다.
    > 
    > SQL Server에서 실행 되는 R 스크립트를 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리와 충돌 하 여 관리 하는 반면 독립 실행형 R 서버에는 이러한 제한이 응용 프로그램과 다른 데이터베이스 작업을 방해할 수 있습니다.
    > 
    > 일반적으로 권장 R Server (독립 실행형) 설치 하는 다른 컴퓨터에 SQL Server R Services (In-database)에서.

4.  Microsoft R Open을 다운로드 및 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다.
    
    이러한 구성 요소 및 해야, 모든 필수 구성 요소 설치에는 시간이 걸릴 수 있습니다.
    
5.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

## <a name="default-installation-folders"></a>기본 설치 폴더

SQL Server 설치 프로그램을 사용 하 여 R Server를 설치 하면 R 라이브러리 설치에 사용 된 SQL Server 버전에 연결 하는 폴더에 설치 됩니다. 이 폴더에 샘플 데이터, R 기본 패키지에 대 한 설명서 및 R 도구 및 런타임의 설명서도 찾을 수 있습니다.

그러나 별도 Windows installer (하지 SQL 설치 프로그램)를 사용 하 여 Microsoft R Server를 설치 하거나 별도 Windows installer를 사용 하 여 업그레이드 하는 경우 R 라이브러리는 다른 폴더에 설치 됩니다.

하지만 동일한 컴퓨터에도 SQL Server R services (In-database)의 인스턴스를 설치한 경우에 대해 권장, R 라이브러리 및 도구의 두 번째 복사본을 다른 폴더에 설치 됩니다.

다음 표에서 각 설치에 대 한 경로 나열합니다.

|버전| 설치 방법 | 기본 폴더|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |독립 실행형 응용 프로그램|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning Server(독립 실행형) |  SQL Server 2017 설치 마법사에서 R 언어 옵션 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning Server(독립 실행형) |  Python 언어 옵션으로 SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning Server(독립 실행형) |  독립 실행형 응용 프로그램 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services(In-Database) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning Services(데이터베이스 내) |SQL Server 2017 설치 마법사에서 R 언어 옵션|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning Services(데이터베이스 내) |Python 언어 옵션으로 SQL Server 2017 설치 마법사| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>개발 도구

개발 IDE 설정의 일부분으로 설치 되지 않았습니다. 추가 도구 필요 하지 않은, 포함 된 모든 표준 도구와는 제공 되는 R, Python의 배포와 함께 합니다.

새 릴리스를 시도 하는 것이 좋습니다 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 또는 [Visual Studio 용 Python](https://docs.microsoft.com/en-us/visualstudio/python/installing-python-support-in-visual-studio)합니다. Visual Studio 모두 R 및 Python으로 데이터베이스 개발 도구, SQL Server와의 연결 및 BI 도구를 지원합니다. 그러나 RStudio를 포함 하 여 모든 기본 설정된 개발 환경에 사용할 수 있습니다.
  
## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드로 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자 몇 가지 간단한 예제 차별화할 수 및 R SQL Server와 함께 작동 하는 방법에 대 한 기본 사항을 설명 합니다. 다음 단계에서는 다음 링크 참조:

+ [자습서: T-SQL에서 R을 실행할](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.
+ [R 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.

