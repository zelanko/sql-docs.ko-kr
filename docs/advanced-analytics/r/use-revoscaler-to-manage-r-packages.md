---
title: RevoScaleR 함수를 사용 하 여 R 패키지를 찾거나 설치 하는 방법
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e5cd2f55559671b1e3f3d2004c4865b8bac8aa42
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469884"
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>RevoScaleR 함수를 사용 하 여 SQL Server에서 R 패키지를 찾거나 설치 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

RevoScaleR 9.0.1 이상에는 R 패키지 관리를 위한 함수 SQL Server 계산 컨텍스트가 포함 되어 있습니다. 이러한 함수는 원격 관리자가 아닌 원격 서버에 직접 액세스 하지 않고 SQL Server에 패키지를 설치 하는 데 사용할 수 있습니다.

SQL Server 2017 Machine Learning Services에 최신 버전의 RevoScaleR가 이미 포함 되어 있습니다. SQL Server 2016 R Services 고객은 [구성 요소 업그레이드](../install/upgrade-r-and-python.md) 를 수행 하 여 RevoScaleR 패키지 관리 기능을 가져와야 합니다. 패키지 버전 및 내용을 검색 하는 방법에 대 한 지침은 [패키지 정보 가져오기](../package-management/installed-package-information.md)를 참조 하세요.

## <a name="revoscaler-functions-for-package-management"></a>패키지 관리에 대 한 RevoScaleR 함수

다음 표에서는 R 패키지 설치 및 관리에 사용 되는 함수에 대해 설명 합니다.

| 함수 | 설명 |
|----------|-------------|
| [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | 원격 SQL Server의 인스턴스 라이브러리 경로를 확인 합니다. |
| [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) | 원격 SQL Server에 있는 하나 이상의 패키지에 대 한 경로를 가져옵니다. |
| [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | 원격 R 클라이언트에서이 함수를 호출 하 여 지정 된 리포지토리에서 또는 로컬로 저장 된 압축 된 패키지를 읽어 SQL Server 계산 컨텍스트에 패키지를 설치 합니다. 이 함수는 종속성을 확인 하 고 로컬 계산 컨텍스트에서 R 패키지를 설치 하는 것 처럼 SQL Server에 모든 관련 패키지를 설치할 수 있는지 확인 합니다. 이 옵션을 사용 하려면 서버 및 데이터베이스에서 패키지 관리를 사용 하도록 설정 해야 합니다. 클라이언트 환경과 서버 환경의 RevoScaleR 버전이 동일 해야 합니다. |
| [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 지정 된 계산 컨텍스트에 설치 된 패키지 목록을 가져옵니다. |
| [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | 지정 된 계산 컨텍스트에 대 한 패키지 라이브러리 정보를 파일 시스템과 데이터베이스 사이에 복사 합니다. |
| [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) | 지정 된 계산 컨텍스트에서 패키지를 제거 합니다. 또한 종속성을 계산 하 고 SQL Server의 다른 패키지에서 더 이상 사용 되지 않는 패키지를 제거 하 여 리소스를 확보할 수 있도록 합니다. |

## <a name="prerequisites"></a>사전 요구 사항

+ [SQL Server에서 원격 R 패키지 관리를 사용 하도록 설정](r-package-how-to-enable-or-disable.md)

+ RevoScaleR 버전은 클라이언트 환경과 서버 환경에서 동일 해야 합니다. 자세한 내용은 [패키지 정보 가져오기](../package-management/installed-package-information.md)를 참조 하세요.

+ 서버와 데이터베이스에 연결 하 고 R 명령을 실행할 수 있는 권한입니다. 지정 된 인스턴스 및 데이터베이스에 패키지를 설치할 수 있도록 하는 데이터베이스 역할의 멤버 여야 합니다.

+ **공유 범위의** 패키지는 지정 된 데이터베이스의 `rpkgs-shared` 역할에 속하는 사용자가 설치할 수 있습니다. 이 역할의 모든 사용자는 공유 패키지를 제거할 수 있습니다.

+ **전용 범위의** 패키지는 데이터베이스의 `rpkgs-private` 역할에 속한 모든 사용자가 설치할 수 있습니다. 그러나 사용자는 자신의 패키지만 보고 제거할 수 있습니다.

+ 데이터베이스 소유자는 공유 또는 개인 패키지를 사용할 수 있습니다.

## <a name="client-connections"></a>클라이언트 연결

클라이언트 워크스테이션은 같은 네트워크에서 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/install-on-windows) 또는 [Microsoft Machine Learning Server](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install) (데이터 과학자 종종 무료 developer edition을 사용) 할 수 있습니다.

원격 R 클라이언트에서 패키지 관리 함수를 호출할 때 [Rxinsqlserver](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수를 사용 하 여 계산 컨텍스트 개체를 먼저 만들어야 합니다. 그런 다음 사용 하는 각 패키지 관리 함수에 대해 계산 컨텍스트를 인수로 전달 합니다.

사용자 id는 일반적으로 계산 컨텍스트를 설정할 때 지정 됩니다. 계산 컨텍스트를 만들 때 사용자 이름 및 암호를 지정 하지 않으면 R 코드를 실행 하는 사용자의 id가 사용 됩니다.

1. R 명령줄에서 인스턴스 및 데이터베이스에 대 한 연결 문자열을 정의 합니다.
2. [Rxinsqlserver](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 생성자를 사용 하 여 연결 문자열을 사용 하 여 SQL Server 계산 컨텍스트를 정의 합니다.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 설치 하려는 패키지 목록을 만들고이 목록을 문자열 변수에 저장 합니다.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. [Rxinstallpackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 를 호출 하 고 패키지 이름을 포함 하는 문자열 변수 및 계산 컨텍스트를 전달 합니다.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    종속 패키지가 필요한 경우 클라이언트에서 인터넷 연결을 사용할 수 있다고 가정 하 여 설치 됩니다.
    
    패키지는 해당 사용자의 기본 범위에서 연결 하는 사용자의 자격 증명을 사용 하 여 설치 됩니다.

## <a name="call-package-management-functions-in-stored-procedures"></a>저장 프로시저에서 패키지 관리 함수 호출

내 `sp_execute_external_script`에서 패키지 관리 함수를 실행 합니다. 이렇게 하면 저장 프로시저 호출자의 보안 컨텍스트를 사용 하 여 함수가 실행 됩니다.

## <a name="examples"></a>예

이 섹션에서는 SQL Server 인스턴스 또는 데이터베이스에 계산 컨텍스트로 연결할 때 원격 클라이언트에서 이러한 함수를 사용 하는 방법에 대 한 예를 제공 합니다.

모든 예를 보려면 연결 문자열 또는 연결 문자열이 필요한 계산 컨텍스트를 제공 해야 합니다. 이 예에서는 SQL Server에 대 한 계산 컨텍스트를 만드는 한 가지 방법을 제공 합니다.

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

서버 위치 및 보안 모델에 따라 연결 문자열에 도메인 및 서브넷 사양을 제공 하거나 SQL 로그인을 사용 해야 할 수 있습니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>원격 SQL Server 계산 컨텍스트에서 패키지 경로 가져오기

이 예제에서는 계산 컨텍스트의 `sqlcc` **RevoScaleR** 패키지에 대 한 경로를 가져옵니다.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**결과**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> SQL 콘솔 출력을 표시 하는 옵션을 사용 하도록 설정한 경우에는 `print` 문 앞에 오는 함수에서 상태 메시지를 가져올 수 있습니다. 코드 테스트를 마친 후에는 계산 컨텍스트 `consoleOutput` 생성자에서를 FALSE로 설정 하 여 메시지를 제거 합니다.

### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예에서는 `sqlcc`계산 컨텍스트에서 **RevoScaleR** 및 **격자** 패키지의 경로를 가져옵니다. 여러 패키지에 대 한 정보를 가져오려면 패키지 이름을 포함 하는 문자열 벡터를 전달 합니다.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>원격 계산 컨텍스트에서 패키지 버전 가져오기

R 콘솔에서이 명령을 실행 하 여 계산 컨텍스트 *sqlServer*에 설치 된 패키지의 빌드 번호 및 버전 번호를 가져옵니다.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**결과**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>SQL Server에 패키지 설치

이 예에서는 **예측** 패키지와 해당 종속성을 계산 컨텍스트에 설치 합니다.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>SQL Server에서 패키지 제거

이 예에서는 계산 컨텍스트에서 **예측** 패키지와 해당 종속성을 제거 합니다.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>데이터베이스와 파일 시스템 간에 패키지 동기화

다음 예에서는 **Testdb**데이터베이스를 확인 하 고 모든 패키지가 파일 시스템에 설치 되어 있는지 여부를 확인 합니다. 일부 패키지는 누락 된 경우 파일 시스템에 설치 됩니다.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

패키지 동기화는 데이터베이스당 및 사용자별로 작동 합니다. 자세한 내용은 [SQL Server에 대 한 R 패키지 동기화](../r/package-install-uninstall-and-sync.md)를 참조 하세요.

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>저장 프로시저를 사용 하 여 SQL Server에서 패키지 나열

저장 프로시저에서를 사용 하 여 `rxInstalledPackages` 현재 인스턴스에 설치 된 패키지 목록을 가져오려면 Management Studio 또는 t-sql을 지 원하는 다른 도구에서이 명령을 실행 합니다.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

함수 `rxSqlLibPaths` 는 SQL Server Machine Learning Services에서 사용 하는 활성 라이브러리를 확인 하는 데 사용할 수 있습니다. 이 스크립트는 현재 서버에 대 한 라이브러리 경로만 반환할 수 있습니다. 

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

## <a name="see-also"></a>참조

+ [원격 R 패키지 관리 사용](r-package-how-to-enable-or-disable.md)
+ [R 패키지 동기화](package-install-uninstall-and-sync.md)
+ [R 패키지를 설치 하기 위한 팁](packages-installed-in-user-libraries.md)
+ [기본 패키지](../package-management/default-packages.md)