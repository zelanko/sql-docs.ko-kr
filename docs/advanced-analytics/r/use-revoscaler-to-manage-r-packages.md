---
title: RevoScaleR 함수를 사용 하 여 찾거나 R 패키지-SQL Server Machine Learning Services를 설치 하는 방법
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/31/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 7eed38e54b0c4e77af8f7b3ede0af2d98b9c58b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62642332"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>RevoScaleR 함수를 사용 하 여 찾거나 SQL Server에 R 패키지를 설치 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

RevoScaleR 9.0.1 나중에 SQL Server 계산 컨텍스트에서 R 패키지 관리에 대 한 함수를 포함 합니다. 이러한 함수는 서버에 직접 액세스 하지 않고도 SQL Server에서 패키지를 설치 하려면 원격 비관리자가 사용할 수 있습니다.

SQL Server 2017의 Machine Learning Services RevoScaleR의 최신 버전을 이미 포함 되어 있습니다. SQL Server 2016 R Services 고객이 수행 해야 합니다는 [구성 요소 업그레이드](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md) RevoScaleR 패키지 관리 함수를 가져오려고 합니다. 버전 및 콘텐츠를 검색 하는 방법에 대 한 지침 패키지 참조 [패키지 정보를 가져올](determine-which-packages-are-installed-on-sql-server.md)합니다.

## <a name="revoscaler-functions-for-package-management"></a>패키지 관리를 위한 RevoScaleR 함수

다음 표에서 R 패키지 설치 및 관리에 사용 되는 함수를 설명 합니다.

| 기능 | Description |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | 원격 SQL Server의 인스턴스 라이브러리의 경로 확인 합니다. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | 원격 SQL Server에서 하나 이상의 패키지에 대 한 경로 가져옵니다. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | SQL Server 계산 컨텍스트에서 패키지를 설치 하기 위해 원격 R 클라이언트에서이 함수를 호출, 지정 된 리포지토리에서 또는 참조 하 여 압축 된 패키지를 로컬로 저장 합니다. 이 함수 종속성 확인 하 고 로컬 계산 컨텍스트에서 R 패키지 설치와 마찬가지로 SQL server와 관련 된 모든 패키지를 설치할 수 있도록 보장 합니다. 이 옵션을 사용 하려면 서버 및 데이터베이스에서 패키지 관리를 활성화 합니다. 클라이언트와 서버 환경에 동일한 버전의 RevoScaleR 있어야 합니다. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 지정 된 계산 컨텍스트에서 설치 된 패키지 목록을 가져옵니다. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | 파일 시스템 및 지정 된 계산 컨텍스트에 대 한 데이터베이스 간의 패키지 라이브러리에 대 한 정보를 복사 합니다. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | 지정 된 계산 컨텍스트에서 패키지를 제거합니다. 또한 종속성을 계산 하 고 리소스 확보 하기 위해 더 이상 SQL Server에서 다른 패키지에서 사용 되는 패키지 제거를 확인 합니다. |

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server에서 원격 R 패키지 관리](r-package-how-to-enable-or-disable.md)

+ RevoScaleR 버전 클라이언트와 서버 환경에서 동일 해야 합니다. 자세한 내용은 [패키지 정보를 가져올](determine-which-packages-are-installed-on-sql-server.md)합니다.

+ 서버 및 데이터베이스에 연결 하 고 R 명령을 실행할 수 있는 권한입니다. 지정 된 인스턴스 및 데이터베이스에 패키지를 설치할 수 있도록 데이터베이스 역할의 멤버 여야 합니다.

+ 패키지 **공유 범위** 에 속한 사용자가 설치할 수는 `rpkgs-shared` 지정된 된 데이터베이스의 역할입니다. 이 역할의 모든 사용자는 공유 패키지를 제거할 수 있습니다.

+ 패키지 **전용 범위** 에 속하는 모든 사용자가 설치할 수는 `rpkgs-private` 데이터베이스의 역할입니다. 그러나 사용자가 보고 자신의 패키지만 제거 수 있습니다.

+ 데이터베이스 소유자는 공유 또는 전용 패키지를 사용 하 여 작업할 수 있습니다.

## <a name="client-connections"></a>클라이언트 연결

클라이언트 워크스테이션 될 수 있습니다 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) 또는 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (데이터 과학자는 대개 사용 무료 개발자 버전) 동일한 네트워크에 있습니다.

원격 R 클라이언트에서 패키지 관리 함수를 호출할 때 계산 컨텍스트 개체를 먼저 만들어야 합니다를 사용 하 여 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수입니다. 그런 다음 사용 하는 각 패키지 관리 함수에 대 한 계산 컨텍스트를 인수로 전달 합니다.

사용자 id는 계산 컨텍스트를 설정 하는 경우에 일반적으로 지정 됩니다. 사용자 이름 및 암호를 계산 컨텍스트를 만들 때 지정 않으면, R 코드를 실행 하는 사용자의 id가 사용 됩니다.

1. R 명령줄에서 인스턴스 및 데이터베이스에 연결 문자열을 정의 합니다.
2. 사용 된 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 연결 문자열을 사용 하 여 SQL Server 계산 컨텍스트를 정의 하는 생성자입니다.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 설치 하 고 문자열 변수에 목록을 저장 하려면 패키지의 목록을 만듭니다.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 호출 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 계산 컨텍스트 및 패키지 이름이 포함 된 문자열 변수를 전달 합니다.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    종속 패키지가 필요한 경우 설치 된, 인터넷 연결이 클라이언트에서 사용할 수 있는 것으로 가정 합니다.
    
    패키지는 해당 사용자에 대 한 기본 범위에서 연결을 수행한 사용자의 자격 증명을 사용 하 여 설치 됩니다.

## <a name="call-package-management-functions-in-stored-procedures"></a>저장된 프로시저에서 패키지 관리 함수를 호출 합니다.

캠 내 패키지 관리 함수를 실행 `sp_execute_external_script`합니다. 이렇게 하면 함수는 저장된 프로시저 호출자의 보안 컨텍스트를 사용 하 여 실행 됩니다.

## <a name="examples"></a>예

이 섹션에서는 SQL Server 인스턴스 또는 데이터베이스를 계산 컨텍스트로 연결할 때 원격 클라이언트에서 이러한 함수를 사용 하는 방법의 예제를 제공 합니다.

모든 예제에 대 한 연결 문자열 또는 연결 문자열을 해야 하는 계산 컨텍스트를 제공 해야 합니다. 이 예제에서는 SQL Server에 대 한 계산 컨텍스트를 만드는 한 가지 방법은 제공 합니다.

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

서버가 위치한 및 보안 모델에 따라 연결 문자열에서 도메인 및 서브넷 사양을 제공 하 여 SQL 로그인을 사용 해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>원격 SQL Server 계산 컨텍스트에서 패키지 경로를 가져옵니다.

이 예제에 대 한 경로 가져옵니다 합니다 **RevoScaleR** 계산 컨텍스트에서 패키지 `sqlcc`합니다.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**결과**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> SQL 콘솔 출력을 참조 하는 옵션을 설정한 경우 앞에 오는 함수에서 상태 메시지를 발생할 수 있습니다는 `print` 문입니다. 코드 테스트를 마친 후 설정 `consoleOutput` 메시지를 제거 하기 위해 계산 컨텍스트 생성자에 FALSE로 합니다.

### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예제에 대 한 경로 가져옵니다 합니다 **RevoScaleR** 하 고 **격자** 계산 컨텍스트에서 패키지 `sqlcc`합니다. 여러 패키지에 대 한 정보를 가져오려는 패키지 이름을 포함 하는 문자열 벡터를 전달 합니다.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>원격 계산 컨텍스트에서 패키지 버전 가져오기

계산 컨텍스트에서 설치 된 패키지에 대 한 빌드 번호 및 버전 번호를 가져오려면 R 콘솔에서이 명령을 실행 *sqlServer*합니다.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**결과**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>SQL Server에 패키지 설치

이 예제에서는 설치를 **예측** 패키지 및 해당 종속성을 계산 컨텍스트.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>SQL Server에서 패키지 제거

이 예제는 **예측** 패키지 및 해당 종속성 계산 컨텍스트에서 합니다.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>데이터베이스 및 파일 시스템 간에 패키지를 동기화 합니다.

다음 예에서는 데이터베이스를 검사 **TestDB**, 모든 패키지를 파일 시스템에 설치 되어 있는지 확인 합니다. 일부 패키지가 누락 된 경우 파일 시스템에 설치 됩니다.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

패키지 동기화가 작동 한 데이터베이스 및 사용자 단위로 합니다. 자세한 내용은 [SQL Server에 대 한 R 패키지 동기화](../r/package-install-uninstall-and-sync.md)합니다.

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>SQL Server에서 패키지를 나열 하는 저장된 프로시저 사용

Management Studio 또는 T-SQL을 현재 인스턴스에 설치 된 패키지의 목록을 가져오려면를 지 원하는 다른 도구에서이 명령을 사용 하 여 `rxInstalledPackages` 저장된 프로시저에서 합니다.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths` SQL Server Machine Learning Services에서 사용 하는 액티브 라이브러리를 확인 하려면 함수를 사용할 수 있습니다. 이 스크립트는 현재 서버에 대 한 라이브러리 경로 반환할 수 있습니다. 

```sql
declare @instance_name nvarchar(100) = @@SERVERNAME, @database_name nvarchar(128) = db_name();
exec sp_execute_external_script 
  @language = N'R',
  @script = N'
    connStr <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
    .libPaths(rxSqlLibPaths(connStr));
    print(.libPaths());
  ', 
  @input_data_1 = N'', 
  @params = N'@instance_name nvarchar(100), @database_name nvarchar(128)',
  @instance_name = @instance_name, 
  @database_name = @database_name;
```

## <a name="see-also"></a>참고자료

+ [원격 R 패키지 관리 사용](r-package-how-to-enable-or-disable.md)
+ [R 패키지 동기화](package-install-uninstall-and-sync.md)
+ [R 패키지를 설치 하기 위한 팁](packages-installed-in-user-libraries.md)
+ [기본 패키지](installing-and-managing-r-packages.md)