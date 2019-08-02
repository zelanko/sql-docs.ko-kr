---
title: R 개발용 데이터 과학 클라이언트 설정
description: SQL Server에 대 한 원격 연결을 위해 개발 워크스테이션에 로컬 R 라이브러리 및 도구를 설치 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: e87770447c371f46ad384daffa3c7bc40b836904
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715601"
---
# <a name="set-up-a-data-science-client-for-r-development-on-sql-server"></a>SQL Server에서 R 개발용 데이터 과학 클라이언트 설정
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

R 통합은 [SQL Server 2016 r Services](../install/sql-r-services-windows-install.md) 또는 [SQL Server Machine Learning Services (데이터베이스 내)](../install/sql-machine-learning-services-windows-install.md) 설치에 r 언어 옵션을 포함 하는 경우 SQL Server 2016 이상에서 사용할 수 있습니다. 

SQL Server 용 R 솔루션을 개발 하 고 배포 하려면 개발 워크스테이션에 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client) 를 설치 하 여 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) 및 기타 r 라이브러리를 가져옵니다. RevoScaleR 라이브러리는 원격 SQL Server 인스턴스에도 필요 하며 두 시스템 간의 컴퓨팅 요청을 조정 합니다. 

이 문서에서는 machine learning 및 R 통합을 위해 사용 하도록 설정 된 원격 SQL Server와 상호 작용할 수 있도록 R 클라이언트 개발 워크스테이션을 구성 하는 방법에 대해 알아봅니다. 이 문서의 단계를 완료 하면 SQL Server에 있는 것과 동일한 R 라이브러리가 만들어집니다. SQL Server에서 로컬 R 세션에서 원격 R 세션으로 계산을 푸시하는 방법도 알아봅니다.

![클라이언트-서버 구성 요소](media/sqlmls-r-client-revo.png "로컬 및 원격 R 세션 및 라이브러리")

설치의 유효성을 검사 하기 위해이 문서에 설명 된 대로 기본 제공 **Rgui** 도구를 사용 하거나 [라이브러리](#install-ide) 를 rgui 또는 일반적으로 사용 하는 다른 IDE에 연결할 수 있습니다.

> [!Note]
> 클라이언트 라이브러리 설치에 대 한 대안은 [독립 실행형 서버](../install/sql-machine-learning-standalone-windows-install.md) 를 리치 클라이언트로 사용 하는 것입니다 .이는 일부 고객이 더 심층적인 시나리오 작업을 선호 합니다. 독립 실행형 서버는 SQL Server에서 완전히 분리 되지만 R 라이브러리가 동일 하기 때문에 SQL Server 데이터베이스 내 분석을 위해 클라이언트로 사용할 수 있습니다. 다른 데이터 플랫폼의 데이터를 가져오고 모델링 하는 기능을 포함 하 여 SQL 관련 없는 작업에도 사용할 수 있습니다. 독립 실행형 서버를 설치 하는 경우이 위치 `C:\Program Files\Microsoft SQL Server\140\R_SERVER`에서 R 실행 파일을 찾을 수 있습니다. 설치의 유효성을 검사 하려면 [r 콘솔 앱을 열어](#R-tools) 해당 위치에서 setup.exe를 사용 하 여 명령을 실행 합니다.

## <a name="commonly-used-tools"></a>일반적으로 사용 되는 도구

SQL에 대 한 새로운 R 개발자 이거나 R 및 데이터베이스 내 분석의 새로운 SQL 개발자 인 경우에는 R 개발 도구와 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 와 같은 t-sql 쿼리 편집기를 모두 실행 하 여 데이터베이스 내 기능을 모두 실행 해야 합니다. analytics.

간단한 R 개발 시나리오의 경우 MRO 및 SQL Server의 기본 R 배포에 번들로 제공 되는 RGUI 실행 파일을 사용할 수 있습니다. 이 문서에서는 로컬 및 원격 R 세션 모두에 RGUI를 사용 하는 방법을 설명 합니다. 생산성 향상을 위해 [Rstudio 또는 Visual Studio](#install-ide)와 같은 완전 한 기능을 갖춘 IDE를 사용 해야 합니다.

SSMS는 R 코드를 포함 하는 저장 프로시저를 포함 하 여 SQL Server에서 저장 프로시저를 만들고 실행 하는 데 유용 하 고 별도의 다운로드입니다. 개발 환경에서 작성 하는 거의 모든 R 코드는 저장 프로시저에 포함 될 수 있습니다. 다른 자습서를 단계별로 실행 하 여 [SSMS 및 Embedded R](../tutorials/sqldev-in-database-r-for-sql-developers.md)에 대해 알아볼 수 있습니다.

## <a name="1---install-r-packages"></a>1-R 패키지 설치

Microsoft의 R 패키지는 여러 제품 및 서비스에서 사용할 수 있습니다. 로컬 워크스테이션에서 Microsoft R Client 설치 하는 것이 좋습니다. R 클라이언트는 [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler), [MicrosoftML](https://docs.microsoft.com/machine-learning-server/r-reference/microsoftml/microsoftml-package), [SQLRUtils](https://docs.microsoft.com/machine-learning-server/r-reference/sqlrutils/sqlrutils)및 기타 r 패키지를 제공 합니다.

1. [Microsoft R Client를 다운로드](https://aka.ms/rclient/download)합니다.

2. 설치 마법사에서 기본 설치 경로를 그대로 적용 하거나 변경 하 고, 구성 요소 목록을 수락 하거나 변경 하 고, Microsoft R Client 사용 조건에 동의 합니다.

  설치가 완료 되 면 시작 화면에서 제품 및 설명서를 소개 합니다.

3. MKL_CBWR 시스템 환경 변수를 만들어 Intel MKL (Math Kernel Library) 계산에 일관 된 출력이 있는지 확인 합니다.

  + 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭 합니다.
  + 값이 **AUTO**로 설정 된 **MKL_CBWR**이라는 새 시스템 변수를 만듭니다.

## <a name="2---locate-executables"></a>2-실행 파일 찾기

설치 폴더의 내용을 찾아서 나열 하 여 R .exe, RGUI 및 기타 패키지가 설치 되었는지 확인 합니다. 

1. 파일 탐색기에서 C:\Program Files\Microsoft\R Client\R_SERVER\bin 폴더를 열어 R .exe의 위치를 확인 합니다.

2. X64 하위 폴더를 열어서 **Rgui**를 확인 합니다. 다음 단계에서이 도구를 사용 합니다.

3. C:\Program Files\Microsoft\R Client\R_SERVER\library를 열어 RevoScaleR, MicrosoftML 등을 비롯 한 R 클라이언트와 함께 설치 된 패키지 목록을 검토 합니다.


<a name="R-tools"></a>
 
## <a name="3---start-rgui"></a>3-RGUI 시작

SQL Server를 사용 하 여 R을 설치 하는 경우 RGui, Rgui 등과 같은 R의 기본 설치와 동일한 R 도구를 사용할 수 있습니다. 이러한 도구는 간단 하 고 패키지 및 라이브러리 정보를 확인 하거나 임시 명령 또는 스크립트를 실행 하거나 자습서를 단계별로 실행 하는 데 유용 합니다. 이러한 도구를 사용 하 여 R 버전 정보를 가져오고 연결을 확인할 수 있습니다.

1. C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64를 열고 **Rgui** 를 두 번 클릭 하 여 r 명령 프롬프트를 사용 하 여 r 세션을 시작 합니다.

  Microsoft program 폴더에서 R 세션을 시작 하면 RevoScaleR를 비롯 한 여러 패키지가 자동으로 로드 됩니다. 

2. 명령 `print(Revo.version)` 프롬프트에서를 입력 하 여 RevoScaleR 패키지 버전 정보를 반환 합니다. 9\.2.1 또는 9.3.0 for RevoScaleR가 있어야 합니다.

3. R 프롬프트에서 **search ()** 를 입력 하 여 설치 된 패키지 목록을 확인 합니다.

   ![R 로드 시 버전 정보](../install/media/rclient-rgui-r-prompt.png "R 프롬프트 열기")


## <a name="4---get-sql-permissions"></a>4-SQL 사용 권한 가져오기

R 클라이언트에서 R 처리는 두 개의 스레드와 메모리 내 데이터로 구분 됩니다. 다중 코어 및 큰 데이터 집합을 사용 하는 확장 가능한 처리를 위해 실행 ( *계산 컨텍스트*)을 데이터 집합으로 이동 하 고 원격 SQL Server 인스턴스의 계산 능력을 높일 수 있습니다. 이는 프로덕션 SQL Server 인스턴스와 클라이언트를 통합 하는 데 권장 되는 방법 이며, 작동 하려면 권한 및 연결 정보가 필요 합니다.

SQL Server 인스턴스에 연결 하 여 스크립트를 실행 하 고 데이터를 업로드 하려면 데이터베이스 서버에 유효한 로그인이 있어야 합니다. SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다. 일반적으로 Windows 통합 인증을 사용 하는 것이 좋지만 특히 스크립트에 외부 데이터에 대 한 연결 문자열이 포함 된 경우에는 SQL 로그인을 사용 하는 것이 더 간단 합니다.

최소한 코드를 실행 하는 데 사용 되는 계정에는 작업 중인 데이터베이스에서 읽을 수 있는 권한이 있어야 하며 특수 사용 권한은 외부 스크립트를 실행 합니다. 대부분의 개발자는 저장 프로시저를 만들고 학습 데이터 나 점수가 매겨진 데이터를 포함 하는 테이블에 데이터를 쓸 수 있는 권한도 필요 합니다. 

R을 사용 하는 데이터베이스에서 데이터베이스 관리자에 게 [계정에 대 한 다음 권한을 구성](../security/user-permission.md)하도록 요청 합니다.

+ **외부 스크립트를 실행** 하 여 서버에서 R 스크립트를 실행 합니다.
+ 모델 학습에 사용 되는 쿼리를 실행할 수 있는 권한을 **db_datareader** 합니다.
+ 학습 데이터 또는 점수가 매겨진 데이터를 **db_datawriter** 합니다.
+ 저장 프로시저, 테이블, 함수 등의 개체를 만드는 **db_owner** 
  또한 샘플 및 테스트 데이터베이스를 만들려면 **db_owner** 가 필요 합니다. 

코드에 기본적으로 SQL Server와 함께 설치 되지 않은 패키지가 필요한 경우 데이터베이스 관리자를 사용 하 여 패키지를 인스턴스와 함께 설치 되도록 정렬 합니다. SQL Server은 보안 환경으로, 패키지를 설치할 수 있는 위치에 대 한 제한 사항이 있습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](install-additional-r-packages-on-sql-server.md)를 참조 하세요.

## <a name="5---test-connections"></a>5-연결 테스트

 확인 단계로 **Rgui** 및 RevoScaleR를 사용 하 여 원격 서버에 대 한 연결을 확인 합니다. [원격 연결](https://docs.microsoft.com/sql/database-engine/configure-windows/view-or-configure-remote-server-connection-options-sql-server) 에 대해 SQL Server를 사용 하도록 설정 해야 하며 사용자 로그인 및 연결할 데이터베이스를 비롯 한 권한이 있어야 합니다. 

다음 단계에서는 데모 데이터베이스, [NYCTaxi_Sample](../tutorials/demo-data-nyctaxi-in-sql.md)및 Windows 인증을 가정 합니다.

1. 클라이언트 워크스테이션에서 **Rgui** 를 엽니다. 예를 들어로 `~\Program Files\Microsoft SQL Server\140\R_SERVER\bin\x64` 이동 하 여 **rgui .exe** 를 두 번 클릭 하 여 시작 합니다.

2. RevoScaleR가 자동으로 로드 됩니다. 다음 명령을 실행 하 여 RevoScaleR가 작동 하는지 확인 합니다.`print(Revo.version)`

3. 원격 서버에서 실행 되는 데모 스크립트를 입력 합니다. 원격 SQL Server 인스턴스에 대 한 올바른 이름을 포함 하도록 다음 샘플 스크립트를 수정 해야 합니다. 이 세션은 로컬 세션으로 시작 되지만 **Rxsummary** 함수는 원격 SQL Server 인스턴스에서 실행 됩니다.

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

  이 스크립트는 원격 서버의 데이터베이스에 연결 하 고, 쿼리를 제공 하 고, 원격 코드 `cc` 실행에 대 한 계산 컨텍스트 명령을 만든 다음, RevoScaleR 함수 **rxsummary** 를 제공 하 여 쿼리의 통계 요약을 반환 합니다. 검색.

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

4. 계산 컨텍스트를 가져오고 설정 합니다. 계산 컨텍스트를 설정 하면 세션 기간 동안 적용 됩니다. 계산이 로컬 또는 원격 인지 확실 하지 않은 경우 다음 명령을 실행 하 여 확인 합니다. 연결 문자열을 지정 하는 결과는 원격 계산 컨텍스트를 의미 합니다.

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

5. 이름 및 유형을 포함 하 여 데이터 소스의 변수에 대 한 정보를 반환 합니다.

  ```R
  rxGetVarInfo(data = inDataSource)
  ```
  결과에는 23 개의 변수가 포함 됩니다.


6. 두 변수 간에 종속성이 있는지 여부를 탐색 하기 위해 산 점도를 생성 합니다. 

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

  다음 스크린샷은 입력 및 산 점도 출력을 보여 줍니다.

   ![RGUI의 산 점도](media/rclient-setup-scatterplot.png "NYC Taxi demo 데이터의 산 점도")

<a name="install-ide"></a>

## <a name="6---link-tools-to-rexe"></a>6-setup.exe에 도구 연결

지속적이 고 심각한 개발 프로젝트의 경우 IDE (통합 개발 환경)를 설치 해야 합니다. SQL Server 도구와 기본 제공 R 도구는 R 개발에 많은 기능을 제공 하지 않습니다. 작업 코드를 만든 후에는 SQL Server에서 실행 하기 위한 저장 프로시저로 배포할 수 있습니다.

IDE에서 로컬 R 라이브러리: 기본 R, RevoScaleR 등을 가리킵니다. 원격 SQL Server에서 작업을 실행 하는 작업은 스크립트를 실행 하는 동안 발생 합니다. 스크립트는 SQL Server에서 원격 계산 컨텍스트를 호출 하 여 해당 서버의 데이터 및 작업에 액세스할 때 발생 합니다.

### <a name="rstudio"></a>RStudio

[Rstudio](https://www.rstudio.com/)를 사용 하는 경우 원격 SQL Server에 해당 하는 R 라이브러리 및 실행 파일을 사용 하도록 환경을 구성할 수 있습니다.

1. SQL Server에 설치 된 R 패키지 버전을 확인 합니다. 자세한 내용은 [R 패키지 정보 가져오기](../package-management/installed-package-information.md)를 참조 하세요.

1. Microsoft R Client 또는 독립 실행형 서버 옵션 중 하나를 설치 하 여 SQL Server 인스턴스에서 사용 하는 기본 R 배포를 비롯 하 여 RevoScaleR 및 기타 R 패키지를 추가 합니다. 서버와 동일한 패키지 버전을 제공 하는 동일한 수준 또는 더 낮은 버전 (패키지가 이전 버전과 호환 됨)을 선택 합니다. 버전 정보는이 문서의 버전 맵을 참조 하세요. [R 및 Python 구성 요소를 업그레이드](../install/upgrade-r-and-python.md)합니다.

1. RStudio에서 RevoScaleR, Microsoft R Open 및 기타 Microsoft 패키지를 제공 하는 R 환경을 가리키도록 [r 경로를 업데이트](https://support.rstudio.com/hc/articles/200486138-Using-Different-Versions-of-R) 합니다. 

  + R 클라이언트 설치의 경우 C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64를 찾습니다.
  + 독립 실행형 서버의 경우 C:\Program Files\Microsoft SQL Server\140\R_SERVER\Library 또는 C:\Program Files\Microsoft SQL Server\130\R_SERVER\Library를 찾습니다.

2. RStudio를 닫은 다음 엽니다.

RStudio를 다시 열 때 R 클라이언트 (또는 독립 실행형 서버)의 R 실행 파일이 기본 R 엔진입니다.


### <a name="r-tools-for-visual-studio-rtvs"></a>Visual Studio용 R 도구 (RTVS)

R에 대해 선호 하는 IDE가 아직 없는 경우 **Visual Studio용 R 도구**하는 것이 좋습니다.

+ [다운로드 Visual Studio용 R 도구 (RTVS)](https://visualstudio.microsoft.com/vs/features/rtvs/)
+ [설치 지침](https://docs.microsoft.com/visualstudio/rtvs/installing-r-tools-for-visual-studio) -rtvs는 여러 버전의 Visual Studio에서 사용할 수 있습니다.
+ [Visual Studio용 R 도구 시작](https://docs.microsoft.com/visualstudio/rtvs/getting-started-with-r)

### <a name="connect-to-sql-server-from-rtvs"></a>RTVS에서 SQL Server에 연결

이 예제에서는 데이터 과학 워크 로드가 설치 된 Visual Studio 2017 Community Edition을 사용 합니다.

1. **파일** 메뉴에서 **새로 만들기** 를 선택한 다음 **프로젝트**를 선택 합니다.

2. 왼쪽 창에는 미리 설치 된 템플릿 목록이 있습니다. **R**을 클릭 하 고 **r 프로젝트**를 선택 합니다. **이름** 상자에를 입력 `dbtest` 하 고 **확인**을 클릭 합니다. 

  Visual Studio에서 새 프로젝트 폴더와 기본 스크립트 파일 ( `Script.R`)을 만듭니다. 

3. 스크립트 `.libPaths()` 파일의 첫 번째 줄에를 입력 한 다음 ctrl + enter를 누릅니다.

  현재 R 라이브러리 경로는 **R 대화형** 창에 표시 되어야 합니다. 

4. **R 도구** 메뉴를 클릭 하 고 **Windows** 를 선택 하 여 작업 영역에 표시할 수 있는 다른 r 특정 창 목록을 표시 합니다.
 
  + CTRL + 3을 눌러 현재 라이브러리의 패키지에 대 한 도움말을 봅니다.
  + CTRL + 8을 눌러 **변수 탐색기**에서 R 변수를 확인 합니다.

## <a name="next-steps"></a>다음 단계

계산 컨텍스트를 로컬에서 원격 SQL Server 인스턴스로 전환할 수 있는 연습이 포함 된 두 가지 자습서가 있습니다.

+ [자습서: SQL Server 데이터에 RevoScaleR R 함수 사용](../tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)
+ [데이터 과학 종단 간 연습](../tutorials/walkthrough-data-science-end-to-end-walkthrough.md)