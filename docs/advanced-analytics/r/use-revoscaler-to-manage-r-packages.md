---
title: SQL Server에서 패키지를 찾거나 R 설치 RevoScaleR 함수를 사용 하는 방법 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c872a945388696a75a07116c0a84a64d64d668d4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>RevoScaleR 함수를 사용 하 여 찾거나 SQL Server에서 R 패키지를 설치 하는 방법
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Microsoft R Server 릴리스 9.0.1 작업에 사용할 SQL Server 계산 컨텍스트에서의 패키지를 설치 하는 새로운 RevoScaleR 함수를 도입 합니다. 이러한 새 함수 R 코드를 실행 하는 서버에 직접 액세스 하지 않고 SQL Server에 패키지를 설치 하는 데이터 과학자 쉽게 있습니다.

## <a name="how-does-it-work"></a>어떻게 작동 합니까

이상 버전에서는 사용할 수 있습니다 또는 R Server 9.0.1 있는 경우는 [rxInstallPackages](https://docs.microsoft.com/en-us/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 패키지를 설치할 SQL Server 계산 컨텍스트에서 R 원격 클라이언트에서 함수입니다. 이 옵션을 사용 하려면 패키지 관리 서버 및 데이터베이스에 설정 해야 합니다. 이 기능에서 해당 버전의 R 서비스 또는 컴퓨터 학습 서비스 서버에 설치할 수 있도록 해야 합니다.

RevoScaleR의 새 버전에는 이러한 함수가 포함 됩니다. 

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage) 함수는 지정 된 계산 컨텍스트에서 하나 이상의 패키지에 대 한 경로 가져옵니다.

    특정 데이터베이스에 패키지를 추가 하거나 패키지를 찾을 수는 사용자와 범위를 사용할 수 있습니다.

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) 함수는 지정 된 계산 컨텍스트에서 설치 된 패키지 목록을 가져옵니다.

+ [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 계산 컨텍스트로 패키지를 설치 하는 함수, 지정 된 저장소에서 또는 로컬로 저장 된 참조 하 여 패키지를 압축 합니다.

    이 함수 종속성에 대 한 확인 하 고 로컬 계산 컨텍스트에서 R 패키지 설치와 마찬가지로 SQL server에 모든 관련된 패키지를 설치할 수 있도록 합니다.

+ [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages) 함수는 지정 된 계산 컨텍스트에서에서 패키지를 제거 합니다.

    또한 종속성을 계산 하 고 리소스를 더 이상 SQL Server에서 다른 패키지에서 사용 되는 패키지 제거를 보장 합니다.

+ 사용 하 여는 [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages) 함수 사이 파일 시스템 및 데이터베이스를 지정 된 계산 컨텍스트에 대 한 패키지 라이브러리에 대 한 정보를 복사 합니다.

+ 사용 하 여는 [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) 계산 컨텍스트는 SQL Server에 인스턴스 라이브러리 경로 확인 하는 함수입니다.

**적용 대상:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]합니다. 에서도 지원 [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)] 이상 R 서버 9.0으로 업그레이드 합니다. 다른 제한이 적용 됩니다.

## <a name="requirements"></a>요구 사항

+ 이러한 함수를 실행 하려면 서버와 데이터베이스에 연결 하 고 R 명령을 실행 하는 권한이 있어야 합니다.

+ R 원격 클라이언트에서 이러한 함수를 사용할 때는 계산 컨텍스트 개체를 먼저 만들어야를 사용 하 여는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수입니다. 그 후 사용 하는 각 패키지 관리 기능에 대 한 계산 컨텍스트를 인수로 전달 합니다.

+ 지정 하지 않으면 사용자 이름 및 암호 계산 컨텍스트를 만들 때, 하는 경우에 R 코드를 실행 하는 사용자의 id가 사용 됩니다.

+ 내 패키지 관리 기능을 실행할 수 이기도 `sp_execute_external_script`합니다. 이렇게 하면 함수는 저장된 프로시저 호출자의 보안 컨텍스트를 사용 하 여 실행 합니다.

+ 패키지를 **공유 범위** 에 속한 사용자가 설치할 수는 `rpkgs-shared` 지정된 된 데이터베이스의 역할입니다. 이 역할의 모든 사용자가 공유 하는 패키지를 제거할 수 있습니다.

+ 패키지를 **개인 범위** 에 속하는 모든 사용자가 설치할 수는 `rpkgs-private` 는 데이터베이스 역할에에서 지정 합니다. 그러나 사용자가 보고 자신의 패키지만 제거 수입니다.

+ 데이터베이스 소유자 공유 또는 전용으로 패키지를 사용할 수 있습니다.

## <a name="package-installation-from-machine-learning-server-or-remote-r-client"></a>학습 서버나 원격 R 클라이언트 컴퓨터에서 패키지 설치

시작 하기 전에 이러한 조건이 충족 되어 있는지 확인 합니다.

+ 클라이언트에 RevoScale 9.0.1 이상.
+ SQL Server 인스턴스에서 RevoScaleR의 해당 버전을 설치한 합니다.
+ [패키지 관리 기능](..\r\r-package-how-to-enable-or-disable.md) 인스턴스에서 사용 되었습니다.
+ 지정 된 인스턴스 및 데이터베이스에 패키지를 설치할 수 있도록 하는 데이터베이스 역할의 멤버인 사용자가 있습니다. 나중에 역할 설치 패키지를 공유 또는 전용 위치를 지원 합니다. 지금은 데이터베이스 소유자 인 경우 패키지를 설치할 수 있습니다.

1. R 명령줄에서 인스턴스 및 데이터베이스에 대 한 연결 문자열을 정의 합니다.
2. 사용 하 여는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 연결 문자열을 사용 하 여 SQL Server 계산 컨텍스트를 정의 하는 생성자입니다.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 설치 하 여 문자열 변수에 목록을 저장 제거할 패키지의 목록을 만듭니다.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 호출 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 계산 컨텍스트 및 패키지 이름이 포함 된 문자열 변수를 전달 합니다.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    종속 패키지 필요한 경우 또한 설치 하기 인터넷 연결을 클라이언트에서 사용할 수 있는 것으로 가정 합니다.
    
    패키지는 해당 사용자의 기본 범위에 연결 하는 사용자의 자격 증명을 사용 하 여 설치 됩니다.

## <a name="examples"></a>예

이 섹션에서는 SQL Server 인스턴스 또는 계산 컨텍스트로 써 데이터베이스에 연결할 때 원격 클라이언트에서 이러한 기능을 사용 하는 방법의 예제를 제공 합니다.

모든 예에 대 한 연결 문자열 또는 연결 문자열을 필요로 하는 계산 컨텍스트를 제공 해야 합니다. 이 예에서는 SQL Server에 대 한 계산 컨텍스트를 만드는 한 가지 방법은 제공 합니다.

```R
instance_name <- "Machine name/Instance name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

서버를 찾으면 및 보안 모델에 따라 SQL 로그인을 사용 하거나 연결 문자열에 도메인 및 서브넷 사양을 제공 할 수 있습니다. 예를 들어:

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"


### Get package path on a remote SQL Server compute context

This example gets the path for the **RevoScaleR** package on the compute context, `sqlcc`.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**결과**

"C: / Program 파일/Microsoft SQL Server/MSSQL14 합니다. MSSQLSERVER/R_SERVICES/라이브러리/RevoScaleR "

> [!TIP]
> 앞에 오는 함수에서 상태 메시지 SQL 콘솔 출력을 참조 하는 옵션을 사용 하는 경우 발생할 수 있습니다는 `print` 문. 코드 테스트를 완료 한 후 설정 `consoleOutput` 메시지를 제거 하기 위해 계산 컨텍스트 생성자에서 FALSE로 합니다.

### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예제에 대 한 경로 가져옵니다는 **RevoScaleR** 및 **격자** 계산 컨텍스트에서 패키지 `sqlcc`합니다. 여러 패키지에 대 한 정보를 얻으려면 패키지 이름을 포함 하는 문자열 벡터를 전달 합니다.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>패키지 버전에는 원격 계산 컨텍스트 가져오기

계산 컨텍스트를에 설치 된 패키지에 대 한 빌드 번호 및 버전 번호를 가져오려는 R 콘솔에서이 명령을 실행 *sqlServer*합니다.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

**결과**

```text
[1] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

[2] "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/lattice"
```

### <a name="install-a-package-on-sql-server"></a>SQL Server에 패키지 설치

이 예에서는 설치는 **예측** 패키지 및 해당 종속성을 계산 컨텍스트.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>SQL Server에서 패키지 제거

이 예에서는 제거 된 **예측** 패키지 및 해당 종속성 계산 컨텍스트를 합니다.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>데이터베이스 및 파일 시스템 간에 패키지를 동기화 합니다.

다음 예제에서는 데이터베이스를 검사 **TestDB**, 파일 시스템에 설치 된 모든 패키지가 있는지 여부를 결정 합니다. 일부 패키지가 없는 경우 파일 시스템에 설치 됩니다.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

패키지 동기화가 작동 하는 데이터베이스 및 사용자 단위 단위로. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 동기화](../r/package-install-uninstall-and-sync.md)합니다.

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>SQL Server에서 패키지를 나열할 저장된 프로시저를 사용 합니다.

Management Studio 또는 원하는 T-SQL, 현재 인스턴스에 설치 된 패키지 목록을 가져올 수 있는 다른 도구에서이 명령을 실행를 사용 하 여 `rxInstalledPackages` 저장된 프로시저에서 합니다.

```SQL
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths` SQL Server 컴퓨터 학습 서비스에서 사용 하는 액티브 라이브러리를 확인 하는 함수를 사용할 수 있습니다. 이 스크립트의 라이브러리 경로를 현재 서버를 반환할 수 있습니다. 

```SQL
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

