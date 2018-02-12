---
title: "SQL Server와 함께 사용 하기 위해 데이터 과학 클라이언트 설정 | Microsoft Docs"
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
ms.assetid: d15ee956-918f-40e0-b986-2bf929ef303a
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 80b4898397cd0cb6460b379d91be81eb28cd9b87
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="set-up-a-data-science-client-for-use-with-sql-server"></a>SQL Server와 함께 사용 하기 위해 데이터 과학 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

인스턴스를 구성 하 고 나면 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기계 학습을 지원 하려면 원격 실행 및 배포에 대 한 서버에 연결할 수 있는 개발 환경을 설정 해야 합니다.

이 문서에서는 SQL Server에서 R 코드를 실행 하는 무료 Visual Studio Community 버전의 구성을 비롯 한 몇 가지 일반적인 클라이언트 시나리오를 설명 합니다.

## <a name="install-r-libraries-on-the-client"></a>클라이언트에서 R 라이브러리를 설치 합니다.

클라이언트 환경에는 SQL Server에서 R의 분산 실행을 지원하는 추가 RevoScaleR 패키지 및 Microsoft R Open이 포함되어 있어야 합니다. R의 표준 배포에 원격 계산 컨텍스트 또는 R 작업의 병렬 실행을 지 원하는 패키지를 사용할 필요가 없습니다.

이러한 라이브러리를 가져오려면 다음 중 하나를 설치 합니다.
  
+ [Microsoft R Client](http://aka.ms/rclient/download)

+ Microsoft R Server (SQL Server 2016) 용

    - SQL Server 설치 프로그램에서 설치 하려면 참조 [독립 실행형 R Server 만들기](../../advanced-analytics/r/create-a-standalone-r-server.md)

    - 별도 Windows 기반 설치 관리자를 사용 하려면 참조 [Windows 용 컴퓨터 학습 서버 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ (SQL Server 2017) 용 서버를 학습 하는 컴퓨터

    - SQL Server 설치 프로그램에서 설치 하려면 참조 [독립 실행형 R Server 만들기](../../advanced-analytics/r/create-a-standalone-r-server.md)

    - 별도 Windows 기반 설치 관리자를 사용 하려면 참조 [Windows 용 R 서버 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="install-a-development-environment"></a>개발 환경 설치

기본 R 개발 환경이 없는 경우 다음 중 하나를 권장 합니다.

+ R Tools for Visual Studio

    Visual Studio 2015와 함께 작동 합니다.

    설치 정보를 참조 하십시오. [Visual Studio에 대 한 R 도구를 설치 하는 방법을](https://docs.microsoft.com/visualstudio/rtvs/installation)합니다.
 
    RTVS Microsoft R 클라이언트 라이브러리를 사용 하도록 구성 하려면 참조 [Microsoft R Client에 대 한](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

+ Visual Studio 2017

    무료 Community Edition도 R, Python 및 F #에 대 한 프로젝트 템플릿을 설치 하는 데이터 과학 작업을 포함 합니다.

    Visual Studio 다운로드 [이 사이트](https://www.visualstudio.com/vs/)합니다. 

+ RStudio

    RStudio를 사용하려면 RevoScaleR 라이브러리를 사용하기 위한 몇 가지 추가 단계가 필요합니다.

    - Microsoft R Client 필요한 패키지 및 라이브러리를 설치 합니다.
    - Microsoft R 런타임을 사용 하기 위해 R 경로 업데이트 합니다.

    자세한 내용은 참조 [R 클라이언트-IDE 구성](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client#step-2-configure-your-ide)합니다.

## <a name="configure-your-ide"></a>IDE 구성

+ R Tools for Visual Studio

    참조 [이 사이트](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r) R 도구를 사용 하 여 Visual Studio에 대 한 프로젝트 빌드 및 R을 디버그 하는 방법의 몇 가지 예제입니다. 

+ Visual Studio 2017

    Microsoft R 클라이언트나 R Server를 설치 하는 경우 **전에** Visual Studio를 설치, R 서버 라이브러리를 자동으로 감지 하 고 라이브러리 경로에 사용 합니다. RevoScaleR 라이브러리를 설치 하지 않은에서 **R 도구** 메뉴 선택 **R 클라이언트 설치**합니다.

## <a name="run-r-in-sql-server"></a>SQL Server에서 R 실행

이 예제에서는 설치 된 데이터 과학 작업의 Visual Studio 2017 Community Edition을 사용 합니다.

1. **파일** 메뉴 선택 **새로** 선택한 후 **프로젝트**합니다.

2. -손 창에 미리 설치 된 템플릿 목록이 포함 되어 있습니다. 클릭 **R**를 선택 하 고 **R 프로젝트**합니다. 에 **이름** 상자에 입력 합니다 `dbtest` 클릭 **확인**합니다.

3. Visual Studio 새 프로젝트 폴더와 기본 스크립트 파일을 만듭니다 `Script.R`합니다. 

4. 형식 `.libPaths()` 스크립트의 첫 번째 줄에 파일을 선택한 다음 CTRL + ENTER를 누릅니다.

5. 에 현재 R 라이브러리 경로 표시 해야는 **R 대화형** 창. 

6. 클릭는 **R 도구** 메뉴와 선택 **Windows** 작업 영역에 표시할 수 있는 다른 R 관련 창의 목록을 볼 수 있습니다.
 
    + CTRL + 3 현재 라이브러리의 패키지에서 도움말을 봅니다.
    + R 변수 참조는 **변수 탐색기**, CTRL + 8입니다.

7. SQL Server 인스턴스에 대 한 연결 문자열을 만들고 SQL Server 데이터 원본 개체를 만들 RxInSqlServer 생성자에서 연결 문자열을 사용 합니다. 

    ```r
    connStr <- "Driver=SQL Server;Server=MyServer;Database=MyTestDB;Uid=;Pwd="
    sqlShareDir <- paste("C:\\AllShare\\", Sys.getenv("USERNAME"), sep = "")
    sqlWait <- TRUE
    sqlConsoleOutput <- FALSE
    cc <- RxInSqlServer(connectionString = connStr, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    sampleDataQuery <- "SELECT TOP 100 * from [dbo].[MyTestTable]"
    inDataSource <- RxSqlServerData(sqlQuery = sampleDataQuery, connectionString = connStr, rowsPerRead = 500)
    ```

    > [!TIP]
    > 일괄 처리를 실행 하려면 실행 하 고 CTRL + ENTER를 눌러 줄을 선택 합니다.

8. 계산 컨텍스트는 서버를 설정 하 고 데이터에 몇 가지 간단한 R 코드를 실행 하십시오.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    결과에 반환 되는 **R 대화형** 창.
    
    코드는 SQL Server 인스턴스에서 실행 되 고 있음을 사용자가 직접 보장 하려는 경우 프로파일러 추적을 만드는 데 사용할 수 있습니다.