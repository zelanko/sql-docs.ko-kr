---
title: R 개발-SQL Server Machine Learning Services에 대 한 데이터 과학 클라이언트 설정
description: SQL Server에 대 한 원격 연결에 대 한 개발 워크스테이션에 로컬 R 라이브러리 및 도구를 설치 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b46ce112af08fca4c8986be51ba11a15d277fb4f
ms.sourcegitcommit: c60784d1099875a865fd37af2fb9b0414a8c9550
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2019
ms.locfileid: "58645535"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>SQL Server에서 R 개발에 대 한 데이터 과학 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

R 언어 옵션을 포함 하는 경우 이상 SQL Server 2016에서 사용할 수 있는 R 통합은는 [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md) 하거나 [SQL Server 2017 Machine Learning Services (In-database)](../install/sql-machine-learning-services-windows-install.md) 설치 합니다. 

설치를 개발 및 SQL Server에 대 한 R 솔루션을 배포 하려면 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 가져오려는 개발용 워크스테이션에서 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 및 기타 R 라이브러리입니다. 원격 SQL Server 인스턴스에서 필요한 또한, RevoScaleR 라이브러리는 두 시스템 간의 컴퓨팅 요청을 조정 합니다. 

이 문서에서는 기계 학습 및 R 통합에 사용할 원격 SQL Server를 사용 하 여 상호 작용할 수 있도록 R 클라이언트 개발 워크스테이션을 구성 하는 방법에 알아봅니다. 이 문서의 단계를 완료 한 후 SQL Server에 있는 것과 동일한 R 라이브러리를 해야 합니다. 또한 SQL Server에서 원격 R 세션에 로컬 R 세션에서 계산을 푸시하는 방법을 알 수 있습니다.

![클라이언트-서버 구성 요소](media/sqlmls-r-client-revo.png "로컬 및 원격 R 세션 및 라이브러리")

설치의 유효성을 검사 하려면 기본 제공을 사용할 수 있습니다 **RGUI** 이 문서에 설명 된 대로 도구 또는 [라이브러리를 링크](#install-ide) RStudio 또는 일반적으로 사용 하는 모든 다른 IDE.

> [!Note]
> 클라이언트 라이브러리 설치 하는 대신 사용 하는 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md) 심층 시나리오 작업에 대 한 일부 고객은 선호 하는 풍부한 클라이언트로 합니다. 독립 실행형 서버는 SQL Server에서 완전히 분리 되어 있지만 동일한 R 라이브러리에 있기 때문에 사용할 수 있습니다 클라이언트로 SQL Server 데이터베이스 내 분석에 대 한 합니다. 가져오기 및 다른 데이터 플랫폼에서 데이터를 모델링 하는 기능을 포함 하 여 비 SQL 관련 작업에 사용할 수 있습니다. 독립 실행형 서버를 설치한 경우에이 위치에서 R 실행 파일을 찾을 수 있습니다: `C:\Program Files\Microsoft SQL Server\140\R_SERVER`합니다. 설치 유효성을 검사 하 [R 콘솔 앱을 열고](#R-tools) 는 R.exe를 사용 하 여 해당 위치에서 명령을 실행 합니다.

## <a name="commonly-used-tools"></a>일반적으로 도구 사용

새 sql을 R 개발자 또는 R과 데이터베이스 내 분석에 새 SQL 개발자 인 경우 해야 하는지는 R 개발 도구 및 T-SQL 쿼리 편집기와 같은 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 모든 연습에 데이터베이스 내 분석의 기능입니다.

간단한 R 개발 시나리오에 대 한 실행 파일, RGUI MRO 및 SQL Server의 기본 R 배포에 번들로 사용할 수 있습니다. 이 문서에는 로컬 및 원격 R 세션에 대해 RGUI를 사용 하는 방법을 설명 합니다. 향상 된 생산성을 사용 해야 모든 기능을 갖춘 IDE와 같은 [RStudio 또는 Visual Studio](#install-ide)합니다.

SSMS는 만들기 및 SQL server에서 R 코드를 포함 하는 포함 하 여 저장된 프로시저를 실행 하는 데 별도 다운로드입니다. 저장된 프로시저에서 개발 환경에서 작성 하는 거의 모든 R 코드를 포함할 수 있습니다. 에 대해 자세히 알아보려면 다른 자습서를 단계별로 실행할 수 있습니다 [SSMS 및 포함 된 R](../tutorials/sqldev-in-database-r-for-sql-developers.md)합니다.

## <a name="1---install-r-packages"></a>1-R 패키지를 설치 합니다.

Microsoft의 R 패키지를 여러 제품 및 서비스에서 사용할 수 있습니다. 로컬 워크스테이션에서 Microsoft R Client를 설치 하는 것이 좋습니다. R Client 제공 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package)를 [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils), 및 기타 R 패키지입니다.

1. [Microsoft R Client 다운로드](https://aka.ms/rclient/download)합니다.

2. 설치 마법사에서 또는 기본 설치 경로 변경 허용 또는 구성 요소 목록에서 변경 하며 Microsoft R Client 사용 조건에 동의 합니다.

  설치가 완료 되 면 시작 화면 제품 및 문서를 소개 합니다.

3. Intel 라이브러리 MKL (Math Kernel) 계산에 일관 된 출력을 확인 하는 MKL_CBWR 시스템 환경 변수를 만듭니다.

  + 제어판에서 클릭 **시스템 및 보안** > **System** > **고급 시스템 설정**  >   **환경 변수**합니다.
  + 라는 새 시스템 변수를 만듭니다 **MKL_CBWR**로 설정 된 값을 사용 하 여 **자동**합니다.

## <a name="2---locate-executables"></a>2-실행 파일 찾기

찾은 R.exe, RGUI, 및 기타 패키지를 설치 했는지 확인 하려면 설치 폴더의 내용을 나열 합니다. 

1. 파일 탐색기에서 R.exe의 위치를 확인 하려면 C:\Program Files\Microsoft\R Client\R_SERVER\bin 폴더를 엽니다.

2. 확인에 오픈 x64 하위 폴더로 **RGUI**합니다. 다음 단계에서이 도구를 사용 합니다.

3. RevoScaleR, MicrosoftML, 등 R Client를 사용 하 여 설치 된 패키지 목록을 검토 하려면 C:\Program Files\Microsoft\R Client\R_SERVER\library를 엽니다.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-RGUI를 시작 합니다.

SQL Server를 사용 하 여 R을 설치할 때 동일한 R 도구 등, RGui 및 Rterm과 등 R의 기본 설치에 표준인를 얻게 됩니다. 이러한 도구는 경량, 라이브러리 및 패키지 정보를 확인, 임시 명령 또는 스크립트를 실행 하거나 자습서를 단계별로 실행 하면 유용 합니다. R 버전 정보를 가져오고 연결을 확인 하려면 이러한 도구를 사용할 수 있습니다.

1. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 열고 두 번 클릭 **RGui** R 명령 프롬프트를 사용 하 여 R 세션을 시작할 수 있습니다.

  Microsoft 프로그램 폴더에서 R 세션을 시작할 때 RevoScaleR의 경우를 비롯 한 여러 패키지를 자동으로 로드 합니다. 

2. 입력 `print(Revo.version)` RevoScaleR 반환할 명령 프롬프트에서 버전 정보를 패키지 합니다. RevoScaleR에 대 한 버전 9.2.1 또는 9.3.0 해야 합니다.

3. 입력 **찾으며** 설치 된 패키지 목록에 대 한 R 프롬프트에서.

   ![R을 로드할 때 버전 정보](../install/media/rclient-rgui-r-prompt.png "R 프롬프트를 엽니다.")


## <a name="4---get-sql-permissions"></a>4-SQL 권한 가져오기

R 클라이언트에서 R 처리 스레드 및 메모리 내 데이터 제한 됩니다. 다중 코어 및 큰 데이터 집합을 사용 하 여 확장 가능한 처리에 대 한 실행을 이동할 수 있습니다 (이라고 *계산 컨텍스트*) 데이터 집합 및 계산 원격 SQL Server 인스턴스를 활용 합니다. 프로덕션 SQL Server 인스턴스와 클라이언트 통합에 대 한 권장 되는 방법 이며 작동 하도록 하는 권한과 연결 정보를 사용 하도록 해야 합니다.

스크립트를 실행 하 여 데이터를 업로드 하는 SQL Server 인스턴스에 연결할 데이터베이스 서버의 유효한 로그인을 해야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합된 인증을 사용 하면 이지만 SQL 로그인을 사용 하 여 몇 가지 시나리오에 대 한 간단한 스크립트 외부 데이터 연결 문자열을 포함 하는 경우에 특히 권장 합니다.

최소한 코드를 실행 하는 데 사용 된 계정, 사용 중인와 특별 한 사용 권한을 모든 외부 스크립트를 실행 합니다. 데이터베이스에서 읽을 수 있는 권한이 있어야 합니다. 대부분의 개발자는 또한 저장된 프로시저를 만들고 학습 데이터가 포함 된 테이블에 데이터를 쓸 권한이 필요 하거나 데이터의 점수를 매긴 합니다. 

데이터베이스 관리자에 게 [계정에 대해 다음 권한을 구성](../security/user-permission.md), r:를 사용 하는 데이터베이스에서

+ **EXECUTE ANY EXTERNAL SCRIPT** 서버에서 R 스크립트를 실행 합니다.
+ **db_datareader** 모델 학습에 사용 되는 쿼리를 실행 하는 권한입니다.
+ **db_datawriter** 점수가 매겨진된 데이터 또는 학습 데이터를 쓸 수 있습니다.
+ **db_owner** 저장된 프로시저와 같은 개체를 만들 테이블을 함수입니다. 
  해야 **db_owner** 샘플 및 테스트 데이터베이스를 만들 수 있습니다. 

코드에서 SQL Server를 사용 하 여 기본적으로 설치 되지 않은 패키지에 필요한 경우 데이터베이스 관리자의 인스턴스와 함께 설치 된 패키지에 정렬 합니다. SQL Server는 보안된 환경 및 패키지를 설치할 수 있습니다에 제한이 있습니다. 자세한 내용은 [SQL Server에 새로운 R 패키지 설치](install-additional-r-packages-on-sql-server.md)합니다.

## <a name="5---test-connections"></a>5-연결을 테스트 합니다.

 확인 단계를 사용 하 여 **RGUI** 및 RevoScaleR 원격 서버 연결을 확인 합니다. 에 대 한 SQL Server를 사용할 수 있어야 합니다 [원격 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) 하며 사용자 로그인 등 데이터베이스에 연결할 권한이 있어야 합니다. 

다음 단계는 데모 데이터베이스를 전제로 [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md), 및 Windows 인증입니다.

1. 오픈 **RGUI** 클라이언트 워크스테이션에 있습니다. 예를 들어, 이동할 `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` 를 두 번 클릭 **RGui.exe** 시작 합니다.

2. RevoScaleR을 자동으로 로드합니다. 이 명령을 실행 하 여 RevoScaleR가 작동을 확인 합니다. `print(Revo.version)`

3. 원격 서버에서 실행 되는 데모 스크립트를 입력 합니다. 원격 SQL Server 인스턴스에 대 한 올바른 이름을 포함 하려면 다음 샘플 스크립트를 수정 해야 합니다. 이 세션 로컬 세션으로 시작 되지만 **rxSummary** 함수를 원격 SQL Server 인스턴스에서 실행 합니다.

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

  이 스크립트 원격 서버의 데이터베이스에 연결 하는 쿼리를 제공, 계산 컨텍스트를 만듭니다 `cc` 원격 코드 실행에 대 한 지침 제공 RevoScaleR 함수 **rxSummary** 통계 반환 쿼리 결과의 요약입니다.

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

4. Get 및 계산 컨텍스트를 설정 합니다. 계산 컨텍스트를 설정 하면 세션의 기간에 대 한 적용 남아 있습니다. 모르는 경우 계산 로컬 또는 원격 인지를 확인 하려면 다음 명령을 실행 합니다. 연결 문자열을 지정 하는 결과는 원격 계산 컨텍스트를 나타냅니다.

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

5. 이름 및 형식을 포함 하 여 데이터 원본에서 변수에 대 한 정보를 반환 합니다.

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  결과 23 변수를 포함 합니다.


6. 두 개의 변수 간의 종속성이 있는지 여부를 나타내는 탐색 산 점도 생성 합니다. 

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

  다음 스크린 샷에서 입력과 산 점도 출력을 보여줍니다.

   ![RGUI의 산 점도](media/rclient-setup-scatterplot.png "NYC Taxi 데이터에 대 한 산 점도")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-링크 R.exe 도구

지속적인 및 심각한 개발 프로젝트용 통합된 개발 환경 (IDE)를 설치 해야 합니다. SQL Server 도구 및 기본 제공 R 도구는 많은 R 개발에 대 한 장착 없습니다. 작업 코드를 만든 후에 SQL Server에서 실행 하기 위해 저장 프로시저로 배포할 수 있습니다.

IDE를 로컬 R 라이브러리를 가리키도록: 기본 R, RevoScaleR 및 등입니다. 원격 SQL Server에서 실행 중인 작업 스크립트를 해당 서버에서 데이터 및 작업에 액세스 하는 SQL server에서 원격 계산 컨텍스트를 호출 하는 경우 스크립트를 실행 하는 동안 발생 합니다.

### <a name="rstudio"></a>RStudio

사용 하는 경우 [RStudio](https://www.rstudio.com/), R 라이브러리 및 해당 원격 SQL Server에 해당 하는 실행 파일을 사용 하도록 환경을 구성할 수 있습니다.

1. SQL Server에 설치 된 R 패키지 버전을 확인 합니다. 자세한 내용은 [가져오려면 R 패키지 정보](determine-which-packages-are-installed-on-sql-server.md#get-the-r-library-location)합니다.

1. Microsoft R Client 또는 RevoScaleR 및 SQL Server 인스턴스에서 사용 되는 기본 R 배포를 포함 하 여 다른 R 패키지를 추가 하는 독립 실행형 서버 옵션 중 하나를 설치 합니다. 수준 이하로 동시 버전을 선택 (패키지는 이전 버전과 호환 됨) 서버에서와 동일한 패키지 버전을 제공 합니다. 버전 정보에 대 한이 문서의 매핑 버전을 보려면 [R 및 Python 구성 요소를 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

1. RStudio에 [R 경로 업데이트](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) RevoScaleR, Microsoft R Open 및 기타 Microsoft 패키지를 제공 하 여 R 환경을 가리키도록 합니다. 

  + R Client 설치의 경우 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 찾습니다
  + 독립 실행형 서버에서 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 또는 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library 확인

2. 페이지를 닫은 다음 RStudio를 엽니다.

RStudio를 다시 열 때 R 클라이언트 (또는 독립 실행형 서버)에서 실행할 R 기본 R 엔진입니다.


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

## <a name="next-steps"></a>다음 단계

원격 SQL Server 인스턴스로 로컬 계산 컨텍스트를 전환한 연습해 볼 수 있도록 두 개의 다른 자습서 연습을 포함 합니다.

+ [자습서: RevoScaleR R 함수를 사용 하 여 SQL Server 데이터를 사용 하 여](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)