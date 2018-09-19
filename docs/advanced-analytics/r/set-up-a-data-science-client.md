---
title: SQL Server에서 R 개발에 대 한 데이터 과학 클라이언트 설정 | Microsoft Docs
description: SQL Server에 대 한 원격 연결에 대 한 개발 워크스테이션에 로컬 R 라이브러리 및 도구를 설치 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 309a78a2195f55a3ec39604b0c2bd385bb06a271
ms.sourcegitcommit: 9d0ff4f3e40db48fc01788684d34719065d159b6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/12/2018
ms.locfileid: "44724317"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>SQL Server에서 R 개발에 대 한 데이터 과학 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

인스턴스를 구성한 후 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 기계 학습을 지원 하려면 원격 실행 및 배포에 대 한 서버에 연결할 수 있는 R 개발 환경을 설정 해야 합니다.

### <a name="evaluation-and-independent-development"></a>평가 및 독립 개발
 
Developer edition 및 SQL Server로 이동 하려는 R 스크립트를 로컬로 작업할 계획 있다면 있습니다 수 건너 뛰 세요 [IDE 설치](#install-ide) SQL Server에서 사용 되는 로컬 R 라이브러리 도구를 가리킵니다.

> [!Tip]
> 데모 및 비디오 연습을 참조 하세요 [실행 R 및 Python 원격으로 원하는 IDE 또는 Jupyter Notebook에서 SQL server에서](https://blogs.msdn.microsoft.com/mlserver/2018/07/10/run-r-and-python-remotely-in-sql-server-from-jupyter-notebooks-or-any-ide/) 이 [YouTube 비디오](https://youtu.be/D5erljpJDjE)합니다.

## <a name="1---install-r-packages"></a>1-R 패키지를 설치 합니다.

Microsoft 제품의 R 기능은 다중 계층입니다. Microsoft의 오픈 소스 기본 R 배포를 시작 하지만 같은 제품 관련 패키지를 사용 하 여 확장 한 다음 됩니다 [RevoScaleR](revoscaler-overview.md), 원격 계산 컨텍스트 및 병렬 R 작업 실행 수 있도록 합니다.

클라이언트와 원격 서버 간에 조정 된 작업에는 동일한 패키지가 포함 된 두 시스템 필요 합니다. 클라이언트 워크스테이션에서 라이브러리의 완전 한 보완을 가져오려면 다음 표에 소프트웨어 패키지 중 하나를 설치 합니다. 

| 라이브러리 공급자 | 사용법  |
|------------------|--------------------------------|
| [Microsoft R Client](http://aka.ms/rclient/download) |  이 무료 다운로드는 RevoScaleR 및 MicrosoftML, 다른 R 패키지를 제공 하지만 두 스레드 및 메모리 내 데이터 제한 됩니다. 그러나 수 여전히 로컬로 시작 하는 R 솔루션을 만드는 앤 시프트 할 실행 (이라고 *계산 컨텍스트*) 데이터 액세스 및 원격 SQL Server 인스턴스를 계산 기능을 합니다. 이 방법은 프로덕션 SQL Server 인스턴스와 클라이언트 통합에 대 한 권장 합니다. 이 도구에 대 한 자세한 내용은 참조 하세요. [Microsoft R Client 란](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)합니다.|
| 독립 실행형 서버 | 아래 **공유 기능**, SQL Server 설치 프로그램이 SQL Server 2016 R Services 및 SQL Server 2017의 machine learning 위한 독립 실행형 서버 설치 옵션을 포함 합니다. 이들은 모든 기능을 갖춘 서버에 연결 하 고 여러 개의 데이터 플랫폼에서 데이터를 사용 하는 기능을 사용 하 여 SQL Server에서 완전히 분리입니다. 하지만 R 및 Python 작업을 실행 하는 SQL Server 데이터베이스 엔진 인스턴스에 액세스 하려면 클라이언트 소속의 소프트웨어를 잠재적으로 사용할 수 있습니다. [SQL Server 2017 Machine Learning Server (독립 실행형)](../install/sql-machine-learning-standalone-windows-install.md) SQL Server 2017 machine learning 인스턴스로 동일한 라이브러리에 있습니다. [SQL Server 2016 R Server (독립 실행형)](../install/sql-r-standalone-windows-install.md) SQL Server 2016 R Services와 동일한 라이브러리에 있습니다. |


<a name="r-tool"></a>
 
## <a name="2---open-an-r-prompt"></a>2-R 프롬프트를 열으십시오

SQL Server를 사용 하 여 R을 설치할 때 동일한 R 도구 등, RGui 및 Rterm과 등 R의 기본 설치에 표준인를 얻게 됩니다. 이러한 도구는 경량, 라이브러리 및 패키지 정보를 확인, 임시 명령 또는 스크립트를 실행 하거나 자습서를 단계별로 실행 하면 유용 합니다. R 버전 정보를 가져오고 연결을 확인 하려면 이러한 도구를 사용할 수 있습니다.

SQL Server 또는 R Client와 함께 설치 된 r 버전을 사용 하려면 SQL Server 또는 R 클라이언트 프로그램 폴더에서 R 프롬프트를 엽니다. 다음 단계를 R Client 및 RGui.exe 됩니다.

1. R Client에 대 한 이동 `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64`합니다.
2. 두 번 클릭 **RGui.exe** R 명령 프롬프트를 사용 하 여 R 세션을 시작할 수 있습니다.

Microsoft 프로그램 폴더에서 R 세션을 시작할 때 RevoScaleR의 경우를 비롯 한 여러 패키지를 자동으로 로드 합니다. 입력 **찾으며** 확인에 대 한 R 프롬프트에서.

   ![R을 로드할 때 버전 정보](../install/media/rclient-rgui-r-prompt.png "R 프롬프트를 엽니다.")

### <a name="tool-list-and-location"></a>도구 목록 및 위치

| 도구 | Description | 
|------|-------------|
| **RTerm**: | R 스크립트를 실행 하기 위한 명령줄 터미널 | 
| **RGui.exe** | R 간단한 대화형 편집기 명령줄 인수를 RGui.exe 및 RTerm에 대 한 동일합니다. |
| **RScript** | 일괄 처리 모드에서 R 스크립트를 실행 하기 위한 명령줄 도구입니다. |

도구에 위치한 **bin** 설치 된 SQL Server와 기본 R 또는 R 클라이언트에 대 한 폴더입니다. 다음 경로 제품 버전 및 기능에 따라 설치 된 도구에 대 한 유효한 위치가 같습니다.

| Microsoft 제품 | R 도구 위치 |
|-------------------|-----------------|
| Microsoft R Client | `~\Program Files\Microsoft\R Client\R_SERVER\bin\x64` |
| Microsoft Machine Learning (R) 서버 | `~\Program Files\Microsoft\R_SERVER\bin\x64`
| SQL Server 2016 R Services | `~\Program Files\Microsoft SQL Server\MSSQL13.<instancename>\R_SERVICES\bin\x64`|
| SQL Server 2016 R 독립 실행형 서버 | `~\Program Files\Microsoft SQL Server\130\R_SERVER\bin\x64` 
| SQL Server 2017 Machine Learning 서비스 (R) | `~\Program Files\Microsoft SQL Server\MSSQL14.<instancename>\R_SERVICES\bin\x64`|
| SQL Server 2017 Machine Learning (R) 독립 실행형 서버 | `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` |

## <a name="3---permissions"></a>3-사용 권한

스크립트를 실행 하 여 데이터를 업로드 하는 SQL Server 인스턴스에 연결할 데이터베이스 서버의 유효한 로그인을 해야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합된 인증을 사용 하지만 일부 시나리오에 대 한 간단 SQL 로그인을 사용 하 여 권장 합니다.

최소한 코드를 실행 하는 데 사용 된 계정, 사용 중인와 특별 한 사용 권한을 모든 외부 스크립트를 실행 합니다. 데이터베이스에서 읽을 수 있는 권한이 있어야 합니다. 대부분의 개발자도 스크립트를 포함 하는 저장된 프로시저의 형태로 새 개체를 만들 수 있는 권한이 필요할 및 학습 데이터를 포함 하는 테이블에 데이터를 쓸 또는 데이터의 점수를 매긴 합니다. 

R을 사용할 데이터베이스 계정에 다음 권한을 구성하도록 데이터베이스 관리자에게 요청하십시오.

+ **EXECUTE ANY EXTERNAL SCRIPT** 서버에서 R을 실행 합니다.
+ **db_datareader** 모델 학습에 사용 되는 쿼리를 실행 하는 권한입니다.
+ **db_datawriter** 점수가 매겨진된 데이터 또는 학습 데이터를 쓸 수 있습니다.
+ **db_owner** 저장된 프로시저와 같은 개체를 만들 테이블을 함수입니다. 
  해야 **db_owner** 샘플 및 테스트 데이터베이스를 만들 수 있습니다. 

코드에서 SQL Server를 사용 하 여 기본적으로 설치 되지 않은 패키지에 필요한 경우 데이터베이스 관리자의 인스턴스와 함께 설치 된 패키지에 정렬 합니다. SQL Server는 보안된 환경 및 패키지를 설치할 수 있습니다에 제한이 있습니다. 코드의 일부로 임시 설치 패키지의 권한이 있는 경우에 권장 되지 않습니다. 또한 보안 관련 문제를 것이 좋습니다 server 라이브러리에서 새 패키지를 설치 하기 전에 항상 신중 하 게 합니다.

> [!Tip]
> SQL Server와 로컬 개발 환경에서 작업을 사용 하 여 잘 모르는 경우에 로그인 및 사용 권한을 설정 하는 방법에 대 한 알아보려면이 자습서를 단계별로 실행할 수 있습니다: [RevoScaleR 심층 분석](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)

## <a name="4---test-connections"></a>4-테스트 연결

에 대 한 SQL Server를 사용할 수 있어야 합니다 [원격 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server.md) 하며 사용자 로그인 등 데이터베이스에 연결할 권한이 있어야 합니다. 다음 단계는 데모 데이터베이스를 전제로 [NYCTaxi_Sample](../tutorials/sqldev-download-the-sample-data.md) 및 Windows 인증입니다.

 확인 단계에서는 원격 서버에 대 한 연결을 확인 하려면 RevoScaleR을 기본 제공 도구를 사용 합니다.

1. 먼저 [R 도구를 열고](#r-tool) 클라이언트 워크스테이션에 있습니다. RevoScaleR을 자동으로 로드합니다. 예를 들어, 이동할 `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` 를 두 번 클릭 **RGui.exe** 시작 합니다.

2. RevoScaleR가 데모 데이터 집합에 통계 요약을 반환 하는이 명령을 실행 하 여 작동을 확인 합니다. SQL Server 데이터베이스 엔진 인스턴스에 대 한 올바른 서버 이름을 제공 했는지 확인 합니다.

```r
connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
testQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
cc <-RxInSqlServer(connectionString=connStr)
rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=testQuery, connectionString=connStr), computeContext=cc)
```
이 스크립트 원격 서버의 데이터베이스에 연결 하는 쿼리를 제공, 계산 컨텍스트를 만듭니다 `cc` 원격 코드 실행에 대 한 지침 제공 RevoScaleR 함수 **rxSummary** 통계 반환 쿼리 결과의 요약입니다.

<a name="install-ide"></a>

## <a name="5---install-an-ide"></a>5-IDE를 설치 합니다.

지속적인 및 심각한 개발 프로젝트용 통합된 개발 환경 (IDE)를 설치 해야 합니다. SQL Server 도구 및 기본 제공 R 도구는 많은 R 개발에 대 한 장착 없습니다. 작업 코드를 만든 후에 SQL Server에서 실행 하기 위해 저장 프로시저로 배포할 수 있습니다.

로컬 R 라이브러리를 IDE 가리켜야: 기본 R, RevoScaleR 및 등입니다. 원격 SQL Server에서 실행 중인 작업 스크립트를 해당 서버에서 데이터 및 작업에 액세스 하는 SQL server에서 원격 계산 컨텍스트를 호출 하는 경우 스크립트를 실행 하는 동안 발생 합니다.

### <a name="rstudio"></a>RStudio

사용 하는 경우 [RStudio](https://www.rstudio.com/), R 라이브러리 및 해당 원격 SQL Server에 해당 하는 실행 파일을 사용 하도록 환경을 구성할 수 있습니다.

1. SQL Server에 설치 된 R 패키지 버전을 확인 합니다. 자세한 내용은 [가져오려면 R 패키지 정보](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)합니다.

1. Microsoft R Client 또는 RevoScaleR 및 SQL Server 인스턴스에서 사용 되는 기본 R 배포를 포함 하 여 다른 R 패키지를 추가 하는 독립 실행형 서버 옵션 중 하나를 설치 합니다. 수준 이하로 동시 버전을 선택 (패키지는 이전 버전과 호환 됨) 서버에 있는 것과 동일한 패키지 버전을 제공 합니다. 버전 정보를 매핑할이 문서의 버전을 참조 하세요. [업그레이드 하는 R 및 Python 구성 요소](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

1. RStudio에 [R 경로 업데이트](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) RevoScaleR, Microsoft R Open 및 기타 Microsoft 패키지를 제공 하 여 R 환경을 가리키도록 합니다. 구입한 방법 RevoScaleR 및 다른 라이브러리에 따라 다음 경로 중 하나를 가장 가능성이 높은 것:

  + C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library
  + C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library
  + C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64

### <a name="r-tools-for-visual-studio-rtvs"></a>R Tools for Visual Studio (RTVS)

아직 없는 경우 기본 IDE를 R에 대 한, 것이 좋습니다 **R Tools for Visual Studio**합니다.

+ [R Tools for Visual Studio (RTVS) 다운로드](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [설치 지침](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) -RTVS가 Visual Studio의 여러 버전에서 사용할 수 있습니다.
+ [Visual Studio 용 R 도구를 사용 하 여 시작](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>RTVS에서 SQL Server에 연결

이 예제에서는 데이터 과학 워크 로드가 설치 된 Visual Studio 2017 Community Edition을 사용 합니다.

1. **파일** 메뉴에서 **새로 만들기** 선택한 후 **프로젝트**합니다.

2. 왼쪽 창에는 미리 설치 된 템플릿 목록을 포함합니다. 클릭 **R**, 선택한 **R 프로젝트**합니다. 에 **이름을** 상자에 입력 `dbtest` 클릭 **확인**합니다. 

  Visual Studio 새 프로젝트 폴더를 만들고 기본 스크립트 파일을 `Script.R`입니다. 

3. 형식 `.libPaths()` 스크립트의 첫 번째 줄에 파일 및 CTRL + ENTER를 누릅니다.

  현재 R 라이브러리 경로 표시 해야 합니다 **R 대화형** 창입니다. 

4. 클릭 합니다 **R 도구** 선택한 메뉴 **Windows** 작업 영역에 표시할 수 있는 다른 R 관련 창의 목록을 보려면.
 
    + CTRL + 3 현재 라이브러리의 패키지에서 도움말을 봅니다.
    + R 변수 참조를 **변수 탐색기**, CTRL + 8입니다.

5. 연결 문자열을 SQL Server 인스턴스를 만들고 SQL Server 데이터 원본 개체를 만들려면 RxInSqlServer 생성자에서 연결 문자열을 사용 합니다. 

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

6. 계산 컨텍스트를 서버로 설정 하 고 데이터에 몇 가지 간단한 R 코드를 실행 합니다.

    ```r
    rxSetComputeContext(cc)
    rxGetVarInfo(data = inDataSource)
    ```

    결과가 반환 되는 **R 대화형** 창입니다.
    
    직접 코드를 SQL Server 인스턴스에서 실행 될 것임을 보장 하려는 경우에 추적을 만드는 Profiler를 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

원격 SQL Server 인스턴스로 로컬 계산 컨텍스트를 전환한 연습해 볼 수 있도록 두 개의 다른 자습서 연습을 포함 합니다.

+ [SQL Server 데이터를 사용 하 여 자습서: 사용 하 여 RevoScaleR R 함수](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)