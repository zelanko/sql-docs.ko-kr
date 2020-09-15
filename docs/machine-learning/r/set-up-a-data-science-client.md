---
title: R 데이터 과학 클라이언트 설정
description: SQL Server에 대한 원격 연결을 위해 개발 워크스테이션에 로컬 R 라이브러리 및 도구를 설치합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 06/13/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 95390a1eb5418a43883a9605c7498e6a86876e7e
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178900"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>SQL Server에서 R 개발을 위한 데이터 과학 클라이언트 설정
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

R 통합은 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 또는 [SQL Server Machine Learning Services(데이터베이스 내)](../install/sql-machine-learning-services-windows-install.md) 설치에 R 언어 옵션을 포함하는 경우 SQL Server 2016 이상에서 사용할 수 있습니다. 

SQL Server에 대한 R 솔루션을 개발하고 배포하려면 개발 워크스테이션에 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)를 설치하여 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 및 기타 R 라이브러리를 가져옵니다. 원격 SQL Server 인스턴스에도 필요한 RevoScaleR 라이브러리는 두 시스템 간에 컴퓨팅 요청을 조정합니다. 

이 문서에서는 기계 학습 및 R 통합에 사용하도록 설정된 원격 SQL Server와 상호 작용할 수 있도록 R 클라이언트 개발 워크스테이션을 구성하는 방법에 대해 알아봅니다. 이 문서의 단계를 완료하면 SQL Server에 있는 것과 동일한 R 라이브러리가 만들어집니다. 또한 SQL Server의 로컬 R 세션에서 원격 R 세션으로 계산을 푸시하는 방법도 알아봅니다.

![클라이언트-서버 구성 요소](media/sqlmls-r-client-revo.png "로컬 및 원격 R 세션 및 라이브러리")

설치의 유효성을 검사하기 위해 이 문서에 설명된 대로 기본 제공 **RGUI** 도구를 사용하거나, RStudio 또는 일반적으로 사용하는 다른 IDE에 [라이브러리를 연결](#install-ide)할 수 있습니다.

> [!Note]
> 클라이언트 라이브러리 설치에 대한 대안은 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md)를 사용하여 다양한 클라이언트를 사용하는 것입니다. 이 경우 일부 고객은 보다 심층적인 시나리오 작업을 선호합니다. 독립 실행형 서버는 SQL Server에서 완전히 분리되지만 R 라이브러리가 동일하기 때문에 SQL Server 데이터베이스 내 분석을 위해 클라이언트로 사용할 수 있습니다. 다른 데이터 플랫폼의 데이터를 가져오고 모델링하는 기능을 포함하여 SQL과 관련이 없는 작업에도 사용할 수 있습니다. 독립 실행형 서버를 설치하는 경우 다음 위치에서 R 실행 파일을 찾을 수 있습니다. `C:\Program Files\Microsoft SQL Server\140\R_SERVER`. 설치의 유효성을 검사하려면 [R 콘솔 앱을 열고](#R-tools) 해당 위치에서 R.exe를 사용하여 명령을 실행합니다.

## <a name="commonly-used-tools"></a>일반적으로 사용되는 도구

SQL에 익숙하지 않은 R 개발자이거나 R 및 데이터베이스 내 분석을 위한 SQL 개발자인 경우 데이터베이스 내 분석의 모든 기능을 실행하려면 R 개발 도구와 [SSMS(SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 같은 T-SQL 쿼리 편집기가 모두 필요합니다.

간단한 R 개발 시나리오의 경우 MRO 및 SQL Server의 기본 R 배포에 포함된 RGUI 실행 파일을 사용할 수 있습니다. 이 문서에서는 로컬 및 원격 R 세션에 모두 RGUI를 사용하는 방법을 설명합니다. 생산성 향상을 위해 [RStudio 또는 Visual Studio](#install-ide)와 같이 모든 기능을 갖춘 IDE를 사용해야 합니다.

SSMS는 R 코드를 포함하는 저장 프로시저를 포함하여 SQL Server에서 저장 프로시저를 만들고 실행하는 데 도움이 되는 별도의 다운로드입니다. 개발 환경에서 작성하는 거의 모든 R 코드는 저장 프로시저에 포함될 수 있습니다. 다른 자습서를 단계별로 실행하여 [SSMS 및 포함된 R](../tutorials/r-taxi-classification-introduction.md)에 대해 알아볼 수 있습니다.

## <a name="1---install-r-packages"></a>1 - R 패키지 설치

Microsoft의 R 패키지는 여러 제품 및 서비스에서 사용할 수 있습니다. 로컬 워크스테이션에 Microsoft R Client를 설치하는 것이 좋습니다. R Client는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils) 및 기타 R 패키지를 제공합니다.

1. [Microsoft R Client를 다운로드](https://aka.ms/rclient/download)합니다.

2. 설치 마법사에서 기본 설치 경로를 그대로 사용하거나 변경하고, 구성 요소 목록을 그대로 사용하거나 변경하고, Microsoft R Client 사용 조건에 동의합니다.

   설치가 완료되면 시작 화면에서 제품 및 설명서를 소개합니다.

3. MKL_CBWR 시스템 환경 변수를 설정하여 Intel MKL(Math Kernel Library) 계산에서 일관성 있는 출력을 보장합니다.

   + 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭합니다.
   + 값이 **AUTO**로 설정된 **MKL_CBWR**이라는 새 시스템 변수를 만듭니다.

## <a name="2---locate-executables"></a>2 - 실행 파일 찾기

설치 폴더의 내용을 찾고 나열하여 R.exe, RGUI 및 기타 패키지가 설치되었는지 확인합니다. 

1. 파일 탐색기에서 C:\Program Files\Microsoft\R Client\R_SERVER\bin 폴더를 열어 R.exe 위치를 확인합니다.

2. X64 하위 폴더를 열어 **RGUI**를 확인합니다. 다음 단계에서 이 도구를 사용합니다.

3. C:\Program Files\Microsoft\R Client\R_SERVER\library를 열어 RevoScaleR, MicrosoftML 등을 포함하여 R Client와 함께 설치된 패키지 목록을 검토합니다.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3 - RGUI 시작

SQL Server와 함께 R을 설치하는 경우 RGui, Rterm 등을 포함한 R의 기본 설치에 대한 표준인 동일한 R 도구가 제공됩니다. 이 도구는 간단하며 패키지 및 라이브러리 정보를 확인하거나, 임시 명령 또는 스크립트를 실행하거나, 자습서를 단계별로 실행하는 데 유용합니다. 이 도구를 사용하여 R 버전 정보를 가져오고 연결을 확인할 수 있습니다.

1. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64를 열고 **RGui**를 두 번 클릭하여 R 명령 프롬프트에서 R 세션을 시작합니다.

   Microsoft 프로그램 폴더에서 R 세션을 시작하면 RevoScaleR을 포함한 여러 패키지가 자동으로 로드됩니다. 

2. 명령 프롬프트에 `print(Revo.version)`를 입력하여 RevoScaleR 패키지 버전 정보를 반환합니다. RevoScaleR의 버전 9.2.1 또는 9.3.0이 있어야 합니다.

3. 설치된 패키지 목록을 확인하려면 R 프롬프트에서 **search()** 를 입력합니다.

   ![R 로드 시 버전 정보](../install/media/rclient-rgui-r-prompt.png "R 프롬프트 열기")


## <a name="4---get-sql-permissions"></a>4 - SQL 사용 권한 가져오기

R Client에서 R 프로세스는 스레드 두 개와 메모리 내 데이터로 제한됩니다. 여러 코어 및 큰 데이터 세트를 사용하는 확장성 있는 처리를 위해 원격 SQL Server 인스턴스의 데이터 세트 및 계산 기능으로 실행(‘컴퓨팅 컨텍스트’라고도 함)을 이동할 수 있습니다.  이 방법은 프로덕션 SQL Server 인스턴스와 클라이언트를 통합하는 경우 권장되며, 이 방법을 사용하려면 권한 및 연결 정보가 필요합니다.

SQL Server 인스턴스에 연결하여 스크립트를 실행하고 데이터를 업로드하려면 데이터베이스 서버에 유효한 로그인이 있어야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합 인증을 사용하는 것이 좋지만 특히 스크립트에 외부 데이터에 대한 연결 문자열이 포함된 경우에는 SQL 로그인을 사용하는 것이 더 간단합니다.

최소한, 코드를 실행하는 데 사용되는 계정에는 작업 중인 데이터베이스에서 읽을 수 있는 권한 및 특수 EXECUTE ANY EXTERNAL SCRIPT 권한이 있어야 합니다. 대부분의 개발자는 저장 프로시저를 만들고 학습 데이터나 점수가 매겨진 데이터를 포함하는 테이블에 데이터를 쓸 수 있는 권한도 필요합니다. 

데이터베이스 관리자에게 R을 사용하는 데이터베이스에서 [계정에 대한 다음 권한을 구성](../security/user-permission.md)하도록 요청합니다.

+ 서버에서 R 스크립트를 실행하는 **EXECUTE ANY EXTERNAL SCRIPT**.
+ 모델 학습에 사용되는 쿼리를 실행하는 **db_datareader** 권한.
+ 학습 데이터 또는 점수가 매겨진 데이터를 쓰는 **db_datawriter**.
+ 저장 프로시저, 테이블, 함수 등의 개체를 만드는 **db_owner**. 
  또한 샘플 및 테스트 데이터베이스를 만들기 위한 **db_owner**도 필요합니다. 

코드에 기본적으로 SQL Server와 함께 설치되지 않은 패키지가 필요한 경우 데이터베이스 관리자와 조정하여 패키지가 인스턴스와 함께 설치되도록 합니다. SQL Server는 보안 환경으로, 패키지를 설치할 수 있는 위치에 대한 제한 사항이 있습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../package-management/install-additional-r-packages-on-sql-server.md)를 참조하세요.

## <a name="5---test-connections"></a>5 - 연결 테스트

확인 단계로 **RGUI** 및 RevoScaleR을 사용하여 원격 서버에 대한 연결을 확인합니다. SQL Server에서 [원격 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server)을 사용하도록 설정해야 하며, 사용자 로그인 및 연결할 데이터베이스를 포함하여 권한이 있어야 합니다. 

다음 단계에서는 데모 데이터베이스 [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md) 및 Windows 인증을 가정합니다.

1. 클라이언트 워크스테이션에서 **RGUI**를 엽니다. 예를 들어 `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64`로 이동하고 **RGui.exe**를 두 번 클릭하여 시작합니다.

2. RevoScaleR이 자동으로 로드됩니다. `print(Revo.version)` 명령을 실행하여 RevoScaleR이 작동하는지 확인합니다.

3. 원격 서버에서 실행되는 데모 스크립트를 입력합니다. 원격 SQL Server 인스턴스의 유효한 이름을 포함하도록 다음 샘플 스크립트를 수정해야 합니다. 이 세션은 로컬 세션으로 시작되지만 **rxSummary** 함수는 원격 SQL Server 인스턴스에서 실행됩니다.

   ```R
   # Define a connection. Replace server with a valid server name.
   connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
  
   # Specify the input data in a SQL query.
   sampleQuery <-"SELECT DISTINCT TOP(100) tip_amount FROM [dbo].nyctaxi_sample ORDER BY tip_amount DESC;"
  
   # Define a remote compute context based on the remote server.
   cc <-RxInSqlServer(connectionString=connStr)

   # Execute the function using the remote compute context.
   rxSummary(formula = ~ ., data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr), computeContext=cc)
   ```

   **Results:**

   이 스크립트는 원격 서버의 데이터베이스에 연결되고, 쿼리를 제공하고, 원격 코드 실행에 대한 컴퓨팅 컨텍스트 `cc` 명령을 만든 다음, RevoScaleR 함수 **rxSummary**를 제공하여 쿼리 결과의 통계 요약을 반환합니다.

   ```R
     Call:
   rxSummary(formula = ~., data = RxSqlServerData(sqlQuery = sampleQuery, 
       connectionString = connStr), computeContext = cc)

   Summary Statistics Results for: ~.
   Data: RxSqlServerData(sqlQuery = sampleQuery, connectionString = connStr) (RxSqlServerData Data Source)
   Number of valid observations: 100 
  
   Name       Mean   StdDev   Min Max ValidObs MissingObs
   tip_amount 63.245 31.61087 36  180 100      0     
   ```

4. 컴퓨팅 컨텍스트를 가져오고 설정합니다. 컴퓨팅 컨텍스트를 설정하면 해당 컴퓨팅 컨텍스트는 세션 기간 동안 적용됩니다. 계산이 로컬 또는 원격인지 확실하지 않으면 다음 명령을 실행하여 확인합니다. 연결 문자열을 지정하는 결과는 원격 컴퓨팅 컨텍스트를 나타냅니다.

   ```R
   # Return the current compute context.
   rxGetComputeContext()

   # Revert to a local compute context.
   rxSetComputeContext("local")
   rxGetComputeContext()

   # Switch back to remote.
   connStr <- "Driver=SQL Server;Server=<your-server-name>;Database=NYCTaxi_Sample;Trusted_Connection=true"
   cc <-RxInSqlServer(connectionString=connStr)
   rxSetComputeContext(cc)
   rxGetComputeContext()
   ```  

5. 이름 및 형식을 포함하여 데이터 원본의 변수 관련 정보를 반환합니다.

   ```R
   rxGetVarInfo(data = inDataSource)
   ```
   결과에는 변수 23개가 포함됩니다.


6. 산점도를 생성하여 두 변수 간에 종속성이 있는지 여부를 살펴봅니다. 

   ```R
   # Set the connection string. Substitute a valid server name for the placeholder.
   connStr <- "Driver=SQL Server;Server=<your database name>;Database=NYCTaxi_Sample;Trusted_Connection=true"

   # Specify a query on the nyctaxi_sample table.
   # For variables on each axis, remove nulls. Use a WHERE clause and <> to do this.
   sampleQuery <-"SELECT DISTINCT TOP 100 * from [dbo].[nyctaxi_sample] WHERE fare_amount <> '' AND  tip_amount <> ''"
   cc <-RxInSqlServer(connectionString=connStr)

   # Generate a scatter plot.
   rxLinePlot(fare_amount ~ tip_amount, data = RxSqlServerData(sqlQuery=sampleQuery, connectionString=connStr, computeContext=cc), type="p")
   ```

   다음 스크린샷은 입력 및 산점도 출력을 보여 줍니다.

   ![RGUI의 산점도](media/rclient-setup-scatterplot.png "NYC Taxi 데모 데이터의 산점도")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6 - R.exe에 도구 연결

지속적이고 중대한 개발 프로젝트의 경우 IDE(통합 개발 환경)를 설치해야 합니다. SQL Server 도구와 기본 제공 R 도구는 대규모 R 개발용으로 제공되는 것이 아닙니다. 작업 코드가 준비되면 SQL Server에서 실행할 저장 프로시저로 배포할 수 있습니다.

IDE로 로컬 R 라이브러리인 기본 R, RevoScaleR 등을 가리킵니다. 원격 SQL Server에서 워크로드를 실행하는 작업은 스크립트가 SQL Server에서 원격 컴퓨팅 컨텍스트를 호출하여 해당 서버의 데이터와 작업에 액세스하는 스크립트 실행 중에 수행됩니다.

### <a name="rstudio"></a>RStudio

[RStudio](https://www.rstudio.com/)를 사용하는 경우 원격 SQL Server에 해당하는 R 라이브러리 및 실행 파일을 사용하도록 환경을 구성할 수 있습니다.

1. SQL Server에 설치된 R 패키지 버전을 확인합니다. 자세한 내용은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조하세요.

1. Microsoft R Client 또는 독립 실행형 서버 옵션 중 하나를 설치하여 SQL Server 인스턴스에서 사용하는 기본 R 배포를 포함하여 RevoScaleR 및 기타 R 패키지를 추가합니다. 서버와 동일한 패키지 버전을 제공하는 동일하거나 더 낮은 버전을 선택합니다(패키지가 이전 버전과 호환됨). 버전 정보는 이 문서의 버전 맵을 참조하세요. [R 및 Python 구성 요소 업그레이드](../install/upgrade-r-and-python.md)

1. RStudio에서 RevoScaleR, Microsoft R Open 및 기타 Microsoft 패키지를 제공하는 R 환경을 가리키도록 [R 경로를 업데이트](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R)합니다. 

   + R Client 설치의 경우 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 검색
   + 독립 실행형 서버의 경우 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 또는 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library 검색

1. RStudio를 닫은 후 엽니다.

RStudio를 다시 열면 R Client(또는 독립 실행형 서버)의 R 실행 파일이 기본 R 엔진이 됩니다.


### <a name="r-tools-for-visual-studio-rtvs"></a>RTVS(Visual Studio용 R 도구)

R의 기본 설정 IDE가 아직 없는 경우 **Visual Studio용 R 도구**를 추천합니다.

+ [RTVS(Visual Studio용 R 도구) 다운로드](https://marketplace.visualstudio.com/items?itemName=MikhailArkhipov007.RTVS2019)
+ [설치 지침](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) - RTVS는 여러 버전의 Visual Studio에서 사용할 수 있습니다.
+ [Visual Studio용 R 도구 시작](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>RTVS에서 SQL Server에 연결

이 예제에서는 데이터 과학 워크로드가 설치된 Visual Studio 2017 Community Edition을 사용합니다.

1. **파일** 메뉴에서 **새로 만들기**를 선택한 후 **프로젝트**를 선택합니다.

2. 왼쪽 창에는 미리 설치된 템플릿 목록이 포함됩니다. **R**을 클릭하고 **R 프로젝트**를 선택합니다. **이름** 상자에 `dbtest`를 입력하고 **확인**을 클릭합니다. 

   Visual Studio에서 새 프로젝트 폴더 및 기본 스크립트 파일 `Script.R`을 만듭니다. 

3. 스크립트 파일의 첫 번째 줄에 `.libPaths()`를 입력한 후 CTRL+ENTER를 누릅니다.

   현재 R 라이브러리 경로는 **R 대화형** 창에 표시되어야 합니다. 

4. **R 도구** 메뉴를 클릭하고 **Windows**를 선택하여 작업 영역에 표시할 수 있는 다른 R 관련 창 목록을 확인합니다.
 
   + CTRL+3을 눌러 현재 라이브러리의 패키지에 대한 도움말을 확인합니다.
   + CTRL+8을 눌러 **변수 탐색기**에서 R 변수를 확인합니다.

## <a name="next-steps"></a>다음 단계

두 가지 자습서에는 컴퓨팅 컨텍스트를 로컬에서 원격 SQL Server 인스턴스로 전환할 수 있는 연습이 포함됩니다.

+ [자습서: RevoScaleR R 함수를 SQL Server 데이터와 함께 사용](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [데이터 과학 엔드투엔드 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)
