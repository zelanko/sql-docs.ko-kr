---
title: "SQL Server R Services에 대한 R 패키지 관리 | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 98c14b05-750e-44f9-8531-1298bf51e8d2
caps.latest.revision: 7
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 7
---
# SQL Server R Services에 대한 R 패키지 관리
SQL Server 인스턴스에서 실행되는 R 패키지 관리를 더 수월하게 하기 위해 이제 **RevoScaleR** 패키지에 R 패키지의 설치 및 관리를 지원하는 함수가 포함됩니다. 

이러한 새 기능은 여러 가지 시나리오를 지원합니다.

- 데이터 과학자가 SQL Server 컴퓨터에 대한 관리자 권한이 없어도 SQL Server에 필요한 R 패키지를 설치할 수 있습니다. 패키지는 데이터베이스 단위로 설치됩니다.
- 패키지를 다른 사용자와 공유하기가 쉽습니다. 로컬 패키지 리포지토리만 설정하면 각 데이터 과학자가 개별 데이터베이스에 패키지를 설치합니다.
- 데이터베이스 관리자가 R 명령 실행 방법을 배우거나 패키지 종속성을 이해할 필요가 없습니다. DBA는 데이터베이스 역할을 사용하여 패키지를 설치, 제거 또는 사용할 수 있는 SQL Server 사용자를 제어합니다.
 
**작동 방식**

* 데이터베이스 관리자는 역할을 설정하고 해당 역할에 사용자를 추가하여 SQL Server 환경에서 R 패키지를 추가하거나 제거할 수 있는 권한이 있는 사용자를 제어하는 역할을 담당합니다.
* 패키지를 설치할 수 있는 권한이 있으면 R 코드에서 패키지 관리 함수 중 하나를 실행하고 패키지를 추가하거나 제거할 계산 컨텍스트를 지정합니다. 계산 컨텍스트는 로컬 컴퓨터 또는 SQL Server 인스턴스의 데이터베이스일 수 있습니다. 
* 패키지를 설치하는 호출이 SQL Server에서 실행되면 자격 증명이 서버에서 작업을 완료할 수 있는지 여부를 결정합니다. 
- 패키지 설치 함수는 종속성을 확인하고 로컬 계산 컨텍스트의 R 패키지 설치와 마찬가지로 SQL Server에 관련 패키지를 설치할 수 있는지 확인합니다.
- 패키지를 제거하는 함수도 종속성을 계산하고 SQL Server의 다른 패키지에서 더 이상 사용되지 않는 패키지를 제거하여 리소스를 확보하도록 합니다.
- 각 데이터 과학자는 다른 사용자에게 표시되지 않는 개인 패키지를 설치하여 고유한 R 패키지에서 작동하는 격리된 샌드박스를 제공할 수 있습니다.
-  패키지 범위를 데이터베이스로 지정할 수 있고 각 사용자는 각 데이터베이스에서 격리된 패키지 샌드박스를 가져오므로 동일한 R 패키지의 다른 버전을 사용하여 더 쉽게 설치할 수 있습니다. 

> [!NOTE]
> 현재 이 기능은 [!INCLUDE[ssSQLv14_md](../../includes/sssqlv14-md.md)]에서만 사용하도록 릴리스됩니다. 

## <a name="database-roles-and-database-scoping"></a>데이터베이스 역할 및 데이터베이스 범위 지정

새 패키지 관리 함수는 SQL Server의 특정 데이터베이스에 패키지를 설치하고 사용하는 데 두 가지 범위를 제공합니다.

- **공유 범위**

  *공유 범위*는 공유 범위 역할(**rpkgs-shared**)에 대한 사용 권한이 부여된 사용자가 지정된 데이터베이스에서 패키지를 설치하고 제거할 수 있음을 의미합니다. 공유 범위 라이브러리에 설치된 패키지는 SQL Server의 다른 데이터베이스 사용자가 설치된 R 패키지를 사용할 수 있는 경우 사용할 수 있습니다. 

- **전용 범위** 

  *전용 범위*는 전용 범위 역할(**rpkgs-private**)에서 멤버 권한이 부여된 사용자가 사용자 단위로 정의된 개인 라이브러리 위치에서 패키지를 설치하거나 제거할 수 있음을 의미합니다. 따라서 전용 범위에 설치된 모든 패키지는 해당 패키지를 설치한 사용자만 사용할 수 있습니다. 즉, SQL Server의 사용자는 다른 사용자가 설치한 개인 패키지를 사용할 수 없습니다. 

*공유* 및 *전용* 범위에 대한 이러한 모델을 결합하여 SQL Server에서 패키지를 배포하고 관리하기 위한 사용자 지정 보안 시스템을 개발할 수 있습니다. 

예를 들어 공유 범위를 사용하여 데이터 과학자 그룹의 리더나 관리자에게 패키지를 설치할 수 있는 권한을 부여하면 동일한 SQL Server 인스턴스에서 다른 모든 사용자나 데이터 과학자가 해당 패키지를 사용할 수 있습니다. 

또 다른 시나리오에서는 사용자 간에 더 큰 격리가 필요하거나 다른 버전의 패키지를 사용할 수 있습니다. 이런 경우 전용 범위를 사용하여 데이터 과학자에게 개별 권한을 부여하면 필요한 패키지만 설치하고 사용하도록 할 수 있습니다. 패키지는 사용자 단위로 설치되므로 한 사용자가 설치한 패키지는 동일한 SQL Server 데이터베이스를 사용하는 다른 사용자의 작업에 영향을 주지 않습니다. 

### <a name="database-roles-for-package-management"></a>패키지 관리에 대한 데이터베이스 역할

다음과 같은 새 데이터베이스 역할이 SQL R Services의 보안 설치 및 패키지 관리를 지원합니다. 

- **rpkgs-users** 사용자가 **rpkgs-shared** 역할의 멤버가 설치한 모든 공유 패키지를 사용하도록 허용합니다.

- **rpkgs-private** **rpkgs-users** 역할과 동일한 권한으로 공유 패키지에 액세스할 수 있습니다. 이 역할의 멤버는 비공개로 범위가 지정된 패키지를 설치, 제거 및 사용할 수도 있습니다.

-  **rpkgs-shared** **rpkgs-private** 역할과 동일한 권한을 제공합니다. 이 역할의 멤버인 사용자는 공유 패키지를 설치하거나 제거할 수도 있습니다. 
 
- **db_owner** - **rpkgs-shared** 역할과 동일한 권한을 갖습니다. 공유 패키지와 개인 패키지를 모두 설치하거나 제거할 수 있는 권한을 사용자에게 부여할 수도 있습니다.



## <a name="new-package-management-functions"></a>새 패키지 관리 함수


+ `rxInstalledPackages`: 지정된 계산 컨텍스트에서 설치된 패키지에 대한 정보를 찾습니다.

+ `rxInstallPackages`: 지정된 리포지토리에서 또는 로컬에 저장된 압축된 패키지를 읽어 계산 컨텍스트에 패키지를 설치합니다.

+ `rxRemovePackages`: 계산 컨텍스트에서 설치된 패키지를 제거합니다.

+ `rxFindPackage`: 지정된 계산 컨텍스트에서 하나 이상의 패키지에 대한 경로를 가져옵니다.

+ `rxSqlLibPaths`: SQL Server 내부에서 실행되는 동안 패키지에 대한 라이브러리 트리의 검색 경로를 가져옵니다.

## <a name="examples"></a>예

### <a name="get-package-location-on-sql-server-compute-context"></a>SQL Server 계산 컨텍스트에서 패키지 위치 가져오기

이 예제에서는 계산 컨텍스트 *sqlServer*에서 **RevoScaleR** 패키지의 경로를 가져옵니다.

  ```R
  sqlPackagePaths <- rxFindPackage(package = "RevoScaleR", computeContext = sqlServerL)
  ```
  
  ### <a name="get-locations-for-multiple-packages"></a>여러 패키지의 위치 가져오기

다음 예제에서는 계산 컨텍스트 *sqlServer*에서 **RevoScaleR** 및 **lattice** 패키지의 경로를 가져옵니다. 여러 패키지에 대한 정보를 찾을 때 패키지 이름을 포함하는 문자열 벡터를 전달합니다.

  ```R
  packagePaths <- rxFindPackage(package = c("RevoScaleR", "lattice"), computeContext = sqlServer)
  ```



### <a name="list-packages-in-specified-compute-context"></a>지정된 계산 컨텍스트에서 패키지 나열

이 예제에서는 계산 컨텍스트 *sqlServer*에 설치된 모든 패키지를 나열한 다음 콘솔에 표시합니다.

  ```R
  myPackages <- rxInstalledPackages(computeContext = sqlServer) 
  myPackages
  ```

### <a name="get-package-versions"></a>패키지 버전 가져오기

이 예제에서는 계산 컨텍스트 *sqlServer*에 설치된 패키지의 빌드 번호 및 버전 번호를 가져옵니다.

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

## <a name="see-also"></a>참고 항목

[R 패키지 관리를 사용하거나 사용하지 않도록 설정하는 방법](../../advanced-analytics/r-services/how-to-enable-or-disable-r-package-management.md)