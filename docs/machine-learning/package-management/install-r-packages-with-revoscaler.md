---
title: RevoScaleR을 사용하여 R 패키지 설치
description: RevoScaleR 함수를 사용하여 Machine Learning Services 또는 R Services를 통해 SQL Server에 R 패키지를 설치하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/20/2019
ms.topic: how-to
author: garyericson
ms.author: garye
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 1526f1c9eaaf4924ec248b523bd44148398e031b
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94870118"
---
# <a name="use-revoscaler-to-install-r-packages"></a>RevoScaleR을 사용하여 R 패키지 설치

[!INCLUDE [SQL Server 2016 and 2017 only](../../includes/applies-to-version/sqlserver2016-2017-only.md)]

이 문서에서는 [RevoScaleR](../r/ref-r-revoscaler.md)(버전 9.0.1 이상) 함수를 사용하여 Machine Learning Services 또는 R Services를 통해 SQL Server에 R 패키지를 설치하는 방법에 대해 설명합니다. RevoScaleR 함수는 서버에 직접 액세스하지 않고도 관리자가 아닌 원격 위치에서 SQL Server에 패키지를 설치하는 데 사용할 수 있습니다.

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
> [!NOTE]
> SQL Server R Services 고객은 RevoScaleR 패키지 관리 함수를 얻으려면 [구성 요소 업그레이드](../install/upgrade-r-and-python.md)를 수행해야 합니다. 패키지 버전 및 콘텐츠를 검색하는 방법에 대한 지침은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조하세요.
::: moniker-end

## <a name="revoscaler-functions-for-package-management"></a>R 패키지 관리를 위한 RevoScaleR 함수

다음 표에서는 R 패키지 설치 및 관리에 사용되는 함수에 대해 설명합니다.

| 함수 | Description |
|----------|-------------|
| [rxSqlLibPaths](/machine-learning-server/r-reference/revoscaler/rxsqllibpaths) | 원격 SQL Server의 인스턴스 라이브러리 경로를 확인합니다. |
| [rxFindPackage](/machine-learning-server/r-reference/revoscaler/rxfindpackage) | 원격 SQL Server에 있는 하나 이상의 패키지에 대한 경로를 가져옵니다. |
| [rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages) | 원격 R 클라이언트에서 이 함수를 호출하여 지정된 리포지토리에서 또는 로컬로 저장된 압축 패키지를 읽어 SQL Server 컴퓨팅 컨텍스트에 패키지를 설치합니다. 이 함수는 종속성을 확인하고 로컬 컴퓨팅 컨텍스트의 R 패키지 설치와 마찬가지로 SQL Server에 관련 패키지를 설치할 수 있는지 확인합니다. 이 옵션을 사용하려면 서버 및 데이터베이스에서 패키지 관리를 사용하도록 설정해야 합니다. 클라이언트 환경과 서버 환경의 RevoScaleR 버전이 동일해야 합니다. |
| [rxInstalledPackages](/machine-learning-server/r-reference/revoscaler/rxinstalledpackages) | 지정된 컴퓨팅 컨텍스트에서 설치된 패키지 목록을 가져옵니다. |
| [rxSyncPackages](/machine-learning-server/r-reference/revoscaler/rxsyncpackages) | 지정된 컴퓨팅 컨텍스트에 대한 패키지 라이브러리 정보를 파일 시스템과 데이터베이스 사이에 복사합니다. |
| [rxRemovePackages](/machine-learning-server/r-reference/revoscaler/rxremovepackages) | 지정된 컴퓨팅 컨텍스트에서 패키지를 제거합니다. 또한 종속성을 계산하고 SQL Server의 다른 패키지에서 더 이상 사용되지 않는 패키지를 제거하여 리소스를 확보하도록 합니다. |

## <a name="prerequisites"></a>사전 요구 사항

+ SQL Server에서 원격 관리를 사용하도록 설정했습니다. 자세한 내용은 [SQL Server에서 R 패키지 관리 사용](r-package-how-to-enable-or-disable.md)을 참조하세요.

+ RevoScaleR 버전이 클라이언트 및 서버 환경에서 동일합니다. 자세한 내용은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조하세요.

+ 서버와 데이터베이스에 연결하고 R 명령을 실행할 수 있는 권한이 있습니다. 지정된 인스턴스 및 데이터베이스에 패키지를 설치할 수 있도록 하는 데이터베이스 역할의 멤버여야 합니다.

  + 지정된 데이터베이스에서 **역할에 속하는 사용자가** 공유 범위`rpkgs-shared`의 패키지를 설치할 수 있습니다. 이 역할의 모든 사용자는 공유 패키지를 제거할 수 있습니다.

  + 데이터베이스에서 **역할에 속하는 사용자가** 프라이빗 범위`rpkgs-private`의 패키지를 설치할 수 있습니다. 그러나 사용자는 자신의 패키지만 확인하고 제거할 수 있습니다.

  + 데이터베이스 소유자는 공유 또는 프라이빗 패키지를 사용할 수 있습니다.

## <a name="client-connections"></a>클라이언트 연결

클라이언트 워크스테이션은 동일한 네트워크에서 [Microsoft R Client](/machine-learning-server/r-client/install-on-windows) 또는 [Microsoft Machine Learning Server](/machine-learning-server/install/machine-learning-server-windows-install)(데이터 과학자는 일반적으로 무료 개발자 버전 사용)일 수 있습니다.

원격 R 클라이언트에서 패키지 관리 함수를 호출하는 경우 [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수를 사용하여 컴퓨팅 컨텍스트 개체를 먼저 만들어야 합니다. 그런 다음 사용하는 각 패키지 관리 함수에 대해 컴퓨팅 컨텍스트를 인수로 전달합니다.

사용자 ID는 일반적으로 컴퓨팅 컨텍스트를 설정할 때 지정됩니다. 컴퓨팅 컨텍스트를 만들 때 사용자 이름 및 암호를 지정하지 않으면 R 코드를 실행하는 사용자의 ID가 사용됩니다.

1. R 명령줄에서 인스턴스 및 데이터베이스에 대한 연결 문자열을 정의합니다.
2. [RxInSqlServer](/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 생성자를 사용하여 연결 문자열로 SQL Server 컴퓨팅 컨텍스트를 정의합니다.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 설치하려는 패키지 목록을 만들고 이 목록을 문자열 변수에 저장합니다.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. [rxInstallPackages](/machine-learning-server/r-reference/revoscaler/rxinstallpackages)를 호출하고, 컴퓨팅 컨텍스트와 패키지 이름을 포함하는 문자열 변수를 전달합니다.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    종속 패키지가 필요한 경우 클라이언트에서 인터넷 연결을 사용할 수 있다고 가정하여 설치됩니다.
    
    패키지는 해당 사용자의 기본 범위에서 연결하는 사용자의 자격 증명을 사용하여 설치됩니다.

## <a name="call-package-management-functions-in-stored-procedures"></a>저장 프로시저에서 패키지 관리 함수 호출

`sp_execute_external_script`에서 패키지 관리 함수를 실행할 수 있습니다. 이렇게 하면 저장 프로시저 호출자의 보안 컨텍스트를 사용하여 함수가 실행됩니다.

## <a name="examples"></a>예

이 섹션에서는 컴퓨팅 컨텍스트로 SQL Server 인스턴스 또는 데이터베이스에 연결할 때 원격 클라이언트에서 이러한 함수를 사용하는 방법에 대한 예를 제공합니다.

모든 예를 보려면 연결 문자열 또는 연결 문자열이 필요한 컴퓨팅 컨텍스트를 제공해야 합니다. 이 예에서는 SQL Server에 대한 컴퓨팅 컨텍스트를 만드는 한 가지 방법을 제공합니다.

```R
instance_name <- "computer-name/instance-name";
database_name <- "TestDB";
sqlWait= TRUE;
sqlConsoleOutput <- TRUE;
connString <- paste("Driver=SQL Server;Server=", instance_name, ";Database=", database_name, ";Trusted_Connection=true;", sep="");
sqlcc <- RxInSqlServer(connectionString = connString, wait = sqlWait, consoleOutput = sqlConsoleOutput, numTasks = 4);
```

서버 위치 및 보안 모델에 따라 연결 문자열에 도메인 및 서브넷 사양을 제공하거나 SQL 로그인을 사용해야 할 수 있습니다. 다음은 그 예입니다.

```R
connStr <- "Driver=SQL Server;Server=myserver.financeweb.contoso.com;Database=Finance;Uid=RUser1;Pwd=RUserPassword"
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>원격 SQL Server 컴퓨팅 컨텍스트에 대한 패키지 경로 가져오기

이 예에서는 컴퓨팅 컨텍스트 **에서** RevoScaleR`sqlcc` 패키지의 경로를 가져옵니다.

```R
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlcc)
print(sqlPackagePaths)
```

**결과**

"C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library/RevoScaleR"

> [!TIP]
> SQL 콘솔 출력을 표시하는 옵션을 사용하도록 설정한 경우 `print` 문 앞에 오는 함수에서 상태 메시지를 가져올 수 있습니다. 코드 테스트를 마친 후에는 컴퓨팅 컨텍스트 생성자에서 `consoleOutput`을 FALSE로 설정하여 메시지를 제거합니다.

### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예제에서는 컴퓨팅 컨텍스트 **에서** RevoScaleR **및** lattice`sqlcc`패키지의 경로를 가져옵니다. 여러 패키지에 대한 정보를 가져오려면 패키지 이름을 포함하는 문자열 벡터를 전달합니다.

```R
packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlcc)
print(packagePaths)
```

### <a name="get-package-versions-on-a-remote-compute-context"></a>원격 컴퓨팅 컨텍스트에 대한 패키지 버전 가져오기

R 콘솔의 이 명령을 실행하여 컴퓨팅 컨텍스트 *sqlServer* 에 설치된 패키지의 빌드 번호 및 버전 번호를 가져옵니다.

```R
sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>SQL Server에 패키지 설치

이 예제에서는 **forecast** 패키지 및 해당 종속성을 컴퓨팅 컨텍스트에 설치합니다.

  ```R
  pkgs <- c("forecast")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="remove-a-package-from-sql-server"></a>SQL Server에서 패키지 제거

이 예제에서는 **forecast** 패키지 및 해당 종속성을 컴퓨팅 컨텍스트에서 제거합니다.

  ```R
  pkgs <- c("forecast")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlcc)
  ```

### <a name="synchronize-packages-between-database-and-file-system"></a>데이터베이스와 파일 시스템 간에 패키지 동기화

다음 예에서는 **TestDB** 데이터베이스를 확인하고 모든 패키지가 파일 시스템에 설치되었는지 여부를 확인합니다. 일부 패키지는 누락된 경우 파일 시스템에 설치됩니다.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

패키지 동기화는 데이터베이스당 및 사용자별로 작동합니다. 자세한 내용은 [SQL Server의 R 패키지 동기화](package-install-uninstall-and-sync.md)를 참조하세요.

### <a name="use-a-stored-procedure-to-list-packages-in-sql-server"></a>저장 프로시저를 사용하여 SQL Server에서 패키지 나열

저장 프로시저의 `rxInstalledPackages`를 사용하여 현재 인스턴스에 설치된 패키지 목록을 가져오려면 Management Studio 또는 T-SQL을 지원하는 다른 도구에서 이 명령을 실행합니다.

```sql
EXEC sp_execute_external_script 
  @language=N'R', 
  @script=N'
    myPackages <- rxInstalledPackages();
    OutputDataSet <- as.data.frame(myPackages);
    '
```

`rxSqlLibPaths` 함수를 사용하여 SQL Server Machine Learning Services에서 사용하는 활성 라이브러리를 확인할 수 있습니다. 이 스크립트는 현재 서버에 대한 라이브러리 경로만 반환할 수 있습니다. 

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

## <a name="see-also"></a>참고 항목

+ [원격 R 패키지 관리 사용](r-package-how-to-enable-or-disable.md)
+ [R 패키지 동기화](package-install-uninstall-and-sync.md)
+ [R 패키지 사용 팁](tips-for-using-r-packages.md)
+ [R 패키지 정보 가져오기](../package-management/r-package-information.md)