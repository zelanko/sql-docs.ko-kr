---
title: "SQL Server에서 패키지를 찾거나 R 설치 RevoScaleR 함수를 사용 하는 방법 | Microsoft Docs"
ms.custom: 
ms.date: 01/08/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: R
ms.assetid: 
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.openlocfilehash: 1cc59cad6bfb95ee0981604d336087809f9cb932
ms.sourcegitcommit: 60d0c9415630094a49d4ca9e4e18c3faa694f034
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2018
---
# <a name="how-to-use-revoscaler-functions-to-find-or-install-r-packages-on-sql-server"></a>RevoScaleR 함수를 사용 하 여 찾거나 SQL Server에서 R 패키지를 설치 하는 방법

Microsoft R Server 릴리스 9.0.1 작업에 사용할 SQL Server 계산 컨텍스트에서의 패키지를 설치 하는 새로운 RevoScaleR 함수를 도입 합니다. 이러한 새 함수는 데이터 과학자가 서버에 대 한 직접 액세스 하지 않고 SQL Server에서 R 코드 실행을 쉽게 있습니다.

각 데이터 과학자는 다른 사용자에 게 표시 되지 않는 개인 패키지를 설치할 수 있습니다. 패키지는 데이터베이스에 범위를 지정할 수 때문에 각 사용자는 각 데이터베이스에 격리 패키지 샌드박스 가져옵니다 동일한 R 패키지의 다른 버전을 설치할 쉽습니다.

새 서버에 작업 데이터베이스를 마이그레이션하는 경우에 모든 패키지의 목록을 읽고 데이터베이스에 새 서버에 설치할 패키지 동기화 함수를 사용할 수 있습니다.

이 문서는 이러한 함수에 설명 하 고 함수 사용 예제를 제공 합니다.

## <a name="requirements"></a>요구 사항

+ 이러한 함수를 실행 하려면 인스턴스에서 R 명령을 실행할 수 있는 권한이 있어야 합니다.

+ 지정 하지 않으면 사용자 이름 및 암호 계산 컨텍스트를 만들 때, 하는 경우에 R 코드를 실행 하는 사용자의 id가 사용 됩니다.

+ R 원격 클라이언트에서 이러한 함수를 사용할 때는 계산 컨텍스트 개체를 먼저 만들어야를 사용 하 여는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 함수입니다. 그 후 사용 하는 각 패키지 관리 기능에 대 한 계산 컨텍스트를 인수로 전달 합니다.

+ 패키지 관리 기능을 사용 하 여를 실행할 수는 `sp_execute_external_script`합니다. 이렇게 하면 함수는 저장된 프로시저 호출자의 보안 컨텍스트를 사용 하 여 실행 합니다.

## <a name="list-of-package-management-functions"></a>패키지 관리 기능 목록

다음 패키지 관리 기능, RevoScaleR 패키지는 지정 된 계산 컨텍스트에서 설치 및 제거에 대 한 다음과 같이 제공 됩니다.

+ [rxInstalledPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstalledpackages): 지정 된 계산 컨텍스트에서 설치 된 패키지에 대 한 정보입니다.

+ [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages): 패키지를 압축 한 계산 컨텍스트를 지정 된 저장소 또는 로컬에 저장 한 읽어에 패키지를 설치 합니다.

+ [rxRemovePackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxremovepackages): 계산 컨텍스트에서 설치 된 패키지를 제거 합니다.

+ [rxFindPackage](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxfindpackage): 지정 된 계산 컨텍스트에서 하나 이상의 패키지에 대 한 경로 가져옵니다.

+ [rxSyncPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsyncpackages): 지정 된 계산 컨텍스트에서 파일 시스템과 데이터베이스 사이의 패키지 라이브러리를 복사 합니다.

+ [rxSqlLibPaths](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 내에서 실행 하는 동안 패키지에 대 한 라이브러리 트리에 대 한 검색 경로 가져옵니다.

이러한 패키지는 SQL Server 2017에 기본적으로 포함 됩니다. 이러한 함수에 대 한 정보, RevoScaleR 함수 참조 페이지를 참조 하십시오.: (https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)

> [!NOTE]
> 패키지 관리에 대 한 R 함수에는 Microsoft R Server 9.0.1부터 사용할 수는 있습니다. RevoScaleR 함수를 찾을 수 없으면, 최신 버전으로 업그레이드 해야 하는 것입니다. 

## <a name="examples"></a>예

이 섹션에는 SQL Server 인스턴스 또는 데이터베이스에서 패키지 관리 기능을 사용 하는 방법 예제가 포함 되어 있습니다. 

+ 패키지 설치 함수는 종속성을 확인하고 로컬 계산 컨텍스트의 R 패키지 설치와 마찬가지로 SQL Server에 관련 패키지를 설치할 수 있는지 확인합니다.

+ 함수는 _제거_ 패키지도 종속성을 계산 하 고 리소스를 더 이상 SQL Server에서 다른 패키지에서 사용 되는 패키지 제거를 보장 합니다.

+ 특정 데이터베이스에 패키지를 추가 하거나 패키지를 찾을 수는 사용자와 범위를 사용할 수 있습니다.

    + 패키지를 **공유 범위** 에 속한 사용자가 설치할 수는 `rpkgs-shared` 지정된 된 데이터베이스의 역할입니다. 이 역할의 모든 사용자가 공유 하는 패키지를 제거할 수 있습니다.
    + 패키지를 **개인 범위** 에 속하는 모든 사용자가 설치할 수는 `rpkgs-private` 는 데이터베이스 역할에에서 지정 합니다. 그러나 사용자가 보고 자신의 패키지만 제거 수입니다.
    + 데이터베이스 소유자 공유 또는 전용으로 패키지를 사용할 수 있습니다.

**R 코드에서**

패키지를 설치할 수 있는 권한이 있는 경우 패키지 중 하나 R 클라이언트에서 관리 기능의 실행 하 고 패키지 추가 되거나 제거 될 수 있는 계산 컨텍스트를 지정 합니다.  계산 컨텍스트는 로컬 컴퓨터 또는 SQL Server 인스턴스의 데이터베이스일 수 있습니다. 자격 증명 서버에서 작업을 완료할 수 있는지 여부를 결정 합니다.

**Transact SQL에서**

에 대 한 호출에 래핑한 저장된 프로시저에서 패키지 관리 기능을 실행 하려면 `sp_execute_external_script`합니다.

### <a name="get-list-of-packages-in-a-sql-server-compute-context"></a>SQL Server 계산 컨텍스트에서 패키지 목록 가져오기

이 예에서는 인스턴스에 설치 된 패키지에 대 한 확인 `myServer`, 데이터베이스에서 `TestDB`합니다. 패키지 관리를 특정 데이터베이스 및 사용자 범위가 지정 됩니다. 사용자를 지정 하지 않으면 계산 컨텍스트 호출을 실행 하는 사용자 가정 합니다. 자세한 내용은 참조 [역할별 패키지의 Scoping](#bkmk_scope)합니다.

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-path-on-a-remote-sql-server-compute-context"></a>원격 SQL Server 계산 컨텍스트에서에서 패키지 경로를 가져옵니다

이 예제에서는 계산 컨텍스트 **sqlServer** 에서 *RevoScaleR*패키지의 경로를 가져옵니다.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예제에서는 계산 컨텍스트 **sqlServer** 에서 **RevoScaleR** 및 *lattice*패키지의 경로를 가져옵니다. 여러 패키지에 대 한 정보를 얻으려면 패키지 이름을 포함 하는 문자열 벡터를 전달 합니다.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```


### <a name="get-package-versions-on-a-remote-compute-context"></a>패키지 버전에는 원격 계산 컨텍스트 가져오기

계산 컨텍스트를에 설치 된 패키지에 대 한 빌드 번호 및 버전 번호를 가져오려는 R 콘솔에서이 명령을 실행 *sqlServer*합니다.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>SQL Server에 패키지 설치

이 예에서는 설치는 **예측** 패키지 및 해당 종속성을 계산 컨텍스트 *sqlServer*합니다.

  ```R
  pkgs <- c("ggplot2")
  rxInstallPackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
  ```

### <a name="remove-a-package-from-sql-server"></a>SQL Server에서 패키지 제거

이 예제에서는 **ggplot2** 패키지 및 해당 종속성을 계산 컨텍스트 *sqlServer*에서 제거합니다.

  ```R
  pkgs <- c("ggplot2")
  rxRemovePackages(pkgs = pkgs, verbose = TRUE, scope = "private", computeContext = sqlServer)
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
