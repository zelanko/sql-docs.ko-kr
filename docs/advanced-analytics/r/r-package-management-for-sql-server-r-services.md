---
title: "SQL Server에 대 한 R 패키지 관리 | Microsoft Docs"
ms.custom: 
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f19982251b629d12215595685c0633b4c6b61c98
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="r-package-management-for-sql-server"></a>SQL Server에 대 한 R 패키지 관리

이 항목에서는 SQL Server의 인스턴스에서 실행 되는 R 패키지를 관리 하는 데 사용할 수 있는 패키지 관리 기능에 설명 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="package-management-using-t-sql"></a>T-SQL을 사용 하 여 패키지 관리

서버를 사용 하 여 컴퓨터 학습 작업에 대 한 유일한 사용자 하는 경우 및 해당 권한이 있는 경우 컴퓨터에서 관리자 권한으로 R 패키지 설치 계속 수 있습니다.

그러나 다른 사용자와 패키지를 공유 해야 할 경우 또는 여러 사용자를 서버에 컴퓨터 학습 작업을 실행 해야 할 경우 공유 패키지 라이브러리를 설정 하 더 효율적입니다. SQL Server 데이터베이스 역할을 통해이 지원합니다.

데이터베이스 관리자는 역할을 설정 하 고 역할에 사용자를 추가 하는 일을 담당 합니다. 역할을 통해 데이터베이스 관리자는 추가 하거나 SQL Server 환경에서 R 패키지를 제거할 수 있는 권한이 사용자 및 패키지 설치를 감사할 수를 제어할 수 있습니다.

### <a name="database-roles-for-package-management"></a>패키지 관리에 대한 데이터베이스 역할

다음 새 데이터베이스 역할 SQL Server의 보안 설치 및 R 패키지 관리를 지원합니다.

- `rpkgs-users`: 사용자가의 구성원으로 설치 된 모든 공유 패키지를 사용할 수 있도록는 `rpkgs-shared` 역할입니다.

- `rpkgs-private`:와 같은 권한으로 패키지 공유에 대 한 액세스를 제공 합니다.는 `rpkgs-users` 역할입니다. 이 역할의 멤버는 비공개로 범위가 지정된 패키지를 설치, 제거 및 사용할 수도 있습니다.

-  `rpkgs-shared`: 동일한 권한으로 제공 된 `rpkgs-private` 역할입니다. 이 역할의 멤버인 사용자는 공유 패키지를 설치하거나 제거할 수도 있습니다.

- `db_owner`:와 같은 권한을 사용에는 `rpkgs-shared` 역할입니다. 공유 패키지와 개인 패키지를 모두 설치하거나 제거할 수 있는 권한을 사용자에게 부여할 수도 있습니다.

### <a name="creating-an-external-package-library-using-t-sql"></a>T-SQL을 사용 하 여 외부 패키지 라이브러리 만들기

또한 SQL Server 2017 지원 T-SQL 문을 **외부 라이브러리 만들기**, 외부 라이브러리의 데이터베이스 관리자가 관리를 지원 합니다. 현재 라이브러리를 만드는 Windows 기반 이후 Python 패키지에 대 한 및 Linux 등 다른 플랫폼에서 실행 용으로 작성 된 패키지에 대 한 지원이 예정 되어 오른쪽 추가 대 한이 문을 사용할 수 있습니다.

자세한 내용은 참조 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)합니다.

## <a name="package-management-using-r"></a>R을 사용 하는 패키지 관리

**RevoScaleR** 패키지에는 이제을 쉽게 설치 및 R 패키지의 관리를 지 원하는 함수가 포함 됩니다. 패키지 관리에 대 한 데이터베이스 역할을 함께 이러한 새로운 작업을 지 원하는이 시나리오:

- 데이터 과학자는 SQL Server 컴퓨터에 관리자 권한이 필요 없이 SQL Server에 필요한 R 패키지를 설치할 수 있습니다.
- 데이터베이스 단위로에 패키지도 설치 하 고 데이터베이스를 이동한 패키지 함께 이동 합니다.
- 패키지를 다른 사용자와 공유 하는 것이 쉽습니다. 로컬 패키지 저장소를 설정 하면 각 데이터 과학자 저장소를 사용 하 여 자신의 데이터베이스에 패키지를 설치 하 수 있습니다.
- 데이터베이스 관리자는 R 명령을 실행 하는 방법을 알아보려면 하지 않아도 하 고 복잡 한 패키지 종속성을 추적할 필요가 없습니다.
- DBA는 친숙 한 데이터베이스 역할을 설치, 제거 또는 패키지를 사용할 권한이 있는 SQL Server 사용자 컨트롤을 사용할 수 있습니다.

### <a name="r-package-management-functions"></a>R 패키지 관리 기능

다음 패키지 관리 기능, RevoScaleR 패키지는 지정 된 계산 컨텍스트에서 설치 및 제거에 대 한 다음과 같이 제공 됩니다.

+ [rxInstalledPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstalledpackages): 지정 된 계산 컨텍스트에서 설치 된 패키지에 대 한 정보입니다.

+ [rxInstallPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxinstallpackages): 패키지를 압축 한 계산 컨텍스트를 지정 된 저장소 또는 로컬에 저장 한 읽어에 패키지를 설치 합니다.

+ [rxRemovePackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxremovepackages): 계산 컨텍스트에서 설치 된 패키지를 제거 합니다.

+ [rxFindPackage](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxfindpackage): 지정 된 계산 컨텍스트에서 하나 이상의 패키지에 대 한 경로 가져옵니다.

+ [rxSyncPackages](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsyncpackages): 지정 된 계산 컨텍스트에서 파일 시스템과 데이터베이스 사이의 패키지 라이브러리를 복사 합니다.

+ [rxSqlLibPaths](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxsqllibpaths): SQL Server 내에서 실행 하는 동안 패키지에 대 한 라이브러리 트리에 대 한 검색 경로 가져옵니다.

이러한 패키지는 SQL Server 2017에서 기본적으로도 포함 됩니다. 이상에서 사용할 인스턴스를 업그레이드 하는 경우 SQL Server 2016 인스턴스에 패키지를 추가할 수 있습니다 Microsoft R 9.0.1 합니다. 자세한 내용은 참조 [R 업그레이드를 사용 하 여 SqlBindR.exe](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

이러한 함수에 대 한 정보, RevoScaleR 함수 참조 페이지를 참조 하십시오.: (https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler)

## <a name="how-package-management-works"></a>패키지 관리의 작동 원리

패키지를 설치할 수 있는 권한이 있으면 R 코드에서 패키지 관리 함수 중 하나를 실행하고 패키지를 추가하거나 제거할 계산 컨텍스트를 지정합니다. 계산 컨텍스트는 로컬 컴퓨터 또는 SQL Server 인스턴스의 데이터베이스일 수 있습니다. 패키지를 설치하는 호출이 SQL Server에서 실행되면 자격 증명이 서버에서 작업을 완료할 수 있는지 여부를 결정합니다. 패키지 설치 함수는 종속성을 확인하고 로컬 계산 컨텍스트의 R 패키지 설치와 마찬가지로 SQL Server에 관련 패키지를 설치할 수 있는지 확인합니다. 패키지를 제거하는 함수도 종속성을 계산하고 SQL Server의 다른 패키지에서 더 이상 사용되지 않는 패키지를 제거하여 리소스를 확보하도록 합니다.

각 데이터 과학자 R 패키지에 대 한 개인 샌드박스를 만드는 다른 사람에 게 표시 되지 않는 개인 패키지를 설치할 수 있습니다. 패키지는 데이터베이스에 범위를 지정할 수 때문에 각 사용자는 각 데이터베이스에 격리 패키지 샌드박스 가져옵니다 동일한 R 패키지의 다른 버전을 설치할 쉽습니다.

새 서버에 작업 데이터베이스를 마이그레이션하는 경우에 모든 패키지의 목록을 읽고 데이터베이스에 새 서버에 설치할 패키지 동기화 함수를 사용할 수 있습니다.

> [!NOTE]
> 
> Microsoft R Server 9.0.1 부터는 패키지 관리에 대 한 R 기능 제공 됩니다. RevoScaleR 함수를 찾을 수 없으면, 최신 버전으로 업그레이드 해야 하는 것입니다.

### <a name="bkmk_scope"></a>역할별 패키지의 범위 지정

새 패키지 관리 함수는 SQL Server의 특정 데이터베이스에 패키지를 설치하고 사용하는 데 두 가지 범위를 제공합니다.

- **공유 범위**

  *공유 범위* 의미 공유 범위 역할에 사용 권한 부여 된 사용자 (`rpkgs-shared`) 설치 하 고 지정된 된 데이터베이스에 패키지를 제거할 수 있습니다. 공유 범위 라이브러리에 설치된 패키지는 SQL Server의 다른 데이터베이스 사용자가 설치된 R 패키지를 사용할 수 있는 경우 사용할 수 있습니다.

- **전용 범위**

  *개인 범위* 의미 개인 범위 역할의 멤버 자격이 부여 된 사용자 (`rpkgs-private`)을 설치 또는 사용자 당 정의 된 개인 라이브러리 위치에 패키지를 제거 합니다. 따라서 전용 범위에 설치된 모든 패키지는 해당 패키지를 설치한 사용자만 사용할 수 있습니다. 즉, SQL Server의 사용자는 다른 사용자가 설치한 개인 패키지를 사용할 수 없습니다.

*공유* 및 *전용* 범위에 대한 이러한 모델을 결합하여 SQL Server에서 패키지를 배포하고 관리하기 위한 사용자 지정 보안 시스템을 개발할 수 있습니다.

예를 들어 공유 범위를 사용하여 데이터 과학자 그룹의 리더나 관리자에게 패키지를 설치할 수 있는 권한을 부여하면 동일한 SQL Server 인스턴스에서 다른 모든 사용자나 데이터 과학자가 해당 패키지를 사용할 수 있습니다.

또 다른 시나리오에서는 사용자 간에 더 큰 격리가 필요하거나 다른 버전의 패키지를 사용할 수 있습니다. 이런 경우 전용 범위를 사용하여 데이터 과학자에게 개별 권한을 부여하면 필요한 패키지만 설치하고 사용하도록 할 수 있습니다. 패키지는 사용자 단위로 설치되므로 한 사용자가 설치한 패키지는 동일한 SQL Server 데이터베이스를 사용하는 다른 사용자의 작업에 영향을 주지 않습니다.

### <a name="synchronizing-r-package-libraries"></a>R 패키지 라이브러리를 동기화합니다.

에 대 한 새로운 R 함수를 포함 하는 SQL Server 2017 (및 Microsoft R server 2017 년 4 월 릴리스) CTP 2.0 릴리스 *패키지 동기화*합니다.

패키지 동기화 데이터베이스 엔진 추적에서 특정 소유자 및 그룹을 사용 하 고 필요한 경우 파일 시스템에 이러한 패키지를 작성할 수 있는 패키지 함을 의미 합니다. 이러한 시나리오에서 패키지 동기화를 사용할 수 있습니다.

+ SQL Server 인스턴스 간에 R 패키지를 이동.
+ 특정 사용자에 대 한 패키지를 다시 설치 하거나 데이터베이스가 복원 된 후 그룹

자세한 내용은 참조 [rxSyncPackages](../r/package-install-uninstall-and-sync.md)합니다.

## <a name="examples"></a>예

이러한 예제 패키지 관리 기능에 대 한 기본 사용법을 보여 줍니다. 이러한 명령을 실행 하려면 인스턴스에서 R 명령을 실행할 수 있는 권한이 필요 합니다.

+ 원격 R 터미널를 실행할 때 SQL Server 인스턴스를 지정 하는 계산 컨텍스트 개체를 만들 하 고 계산 컨텍스트를 인수로 전달 되는 함수를 실행 하십시오.

+ 저장된 프로시저에서 패키지 관리 기능을 실행 하려면 래핑해야 해당 호출에서 `sp_execute_external_script`합니다.

### <a name="package-scoping"></a>패키지 범위 지정

이 예에서는 인스턴스에 설치 된 패키지에 대 한 확인 `myServer`, 데이터베이스에서 `TestDB`합니다. 패키지 관리를 특정 데이터베이스 및 사용자 범위가 지정 됩니다. 사용자를 지정 하지 않으면 계산 컨텍스트 호출을 실행 하는 사용자 가정 합니다. 자세한 내용은 참조 [역할별 패키지의 Scoping](#bkmk_scope)합니다.

```R
sqlServerCompute <- RxInSqlServer(connectionString = "Driver=SQL Server;Server=myServer;Database=TestDB;Uid=myID;Pwd=myPwd;");
sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerCompute);
```

### <a name="get-package-location-on-a-remote-sql-server-compute-context"></a>패키지 위치를에 원격 SQL Server 계산 컨텍스트를 가져옵니다.

이 예제에서는 계산 컨텍스트 **sqlServer** 에서 *RevoScaleR*패키지의 경로를 가져옵니다.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```

### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예제에서는 계산 컨텍스트 **sqlServer** 에서 **RevoScaleR** 및 *lattice*패키지의 경로를 가져옵니다. 여러 패키지에 대 한 정보를 얻으려면 패키지 이름을 포함 하는 문자열 벡터를 전달 합니다.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```

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

### <a name="get-package-versions-on-a-remote-compute-context"></a>패키지 버전에는 원격 계산 컨텍스트 가져오기

계산 컨텍스트를에 설치 된 패키지에 대 한 빌드 번호 및 버전 번호를 가져오려는 R 콘솔에서이 명령을 실행 *sqlServer*합니다.

  ```R
  sqlPackages <- rxInstalledPackages(fields = c("Package", "Version", "Built"), computeContext = sqlServer)
```

### <a name="install-a-package-on-sql-server"></a>SQL Server에 패키지 설치

이 예제에서는 **ggplot2** 패키지 및 해당 종속성을 계산 컨텍스트 *sqlServer*에 설치합니다.

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

### <a name="package-synchronization"></a>패키지 동기화

다음 예에서는 데이터베이스에서 관리 되는 패키지의 목록으로 파일 시스템에 설치 된 패키지를 동기화 합니다. 일부 패키지가 없는 경우 파일 시스템에 설치 됩니다.

```R
# Instantiate the compute context
connectionString <- "Driver=SQL Server;Server=myServer;Database=TestDB;Trusted_Connection=True;"
computeContext <- RxInSqlServer(connectionString = connectionString )

# Synchronize the packages in the file system for all scopes and users
rxSyncPackages(computeContext=computeContext, verbose=TRUE)
```

## <a name="next-steps"></a>다음 단계

[사용 하도록 설정 하거나 R 패키지 관리를 사용 하지 않도록 설정 하는 방법](../r/r-package-how-to-enable-or-disable.md)

