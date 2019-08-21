---
title: MiniCRAN를 사용 하 여 로컬 R 패키지 리포지토리 만들기
description: MiniCRAN 패키지를 사용 하 여 패키지 및 종속성의 로컬 리포지토리를 만드는 방법으로 R 패키지를 오프 라인으로 설치 하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 68f86d673b944a029c7bd0f74c9594692bd579f4
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69634171"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>MiniCRAN를 사용 하 여 로컬 R 패키지 리포지토리 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 를 사용 하 여 패키지 및 종속성의 로컬 리포지토리를 만드는 방법으로 R 패키지를 오프 라인으로 설치 하는 방법을 설명 합니다. **miniCRAN** 는 오프 라인 R 패키지 설치를 위해 다른 컴퓨터에 복사 하는 단일 폴더에 패키지 및 종속성을 식별 하 고 다운로드 합니다.

하나 이상의 패키지를 지정할 수 있으며, **miniCRAN** 는 이러한 패키지에 대 한 종속성 트리를 재귀적으로 읽습니다. 그런 다음 나열 된 패키지와 해당 종속성을 CRAN 또는 유사한 리포지토리에서 다운로드 합니다.

작업이 완료 되 면 **miniCRAN** 는 선택한 패키지 및 모든 필수 종속성으로 구성 된 내부적으로 일관 된 리포지토리를 만듭니다. 이 로컬 리포지토리를 서버로 이동 하 고 인터넷에 연결 하지 않고 패키지를 계속 설치할 수 있습니다.

숙련 된 R 사용자는 다운로드 한 패키지의 설명 파일에서 종속 패키지 목록을 검색 하는 경우가 많습니다. 그러나 **가져오기** 에 나열 된 패키지에는 두 번째 수준 종속성이 있을 수 있습니다. 따라서 필요한 패키지의 전체 컬렉션을 어셈블하는 데 **miniCRAN** 을 권장 합니다.

## <a name="why-create-a-local-repository"></a>로컬 리포지토리를 만드는 이유

로컬 패키지 리포지토리를 만드는 목적은 서버 관리자 또는 조직의 다른 사용자가 서버에 새 R 패키지를 설치 하는 데 사용할 수 있는 단일 위치를 제공 하는 것입니다. 특히 인터넷에 액세스할 수 없는 것입니다. 리포지토리를 만든 후에는 새 패키지를 추가 하거나 기존 패키지의 버전을 업그레이드 하 여 리포지토리를 수정할 수 있습니다.

패키지 리포지토리는 다음과 같은 시나리오에서 유용 합니다.

- **보안**: 많은 R 사용자는 새 R 패키지를 CRAN 또는 해당 미러 사이트 중 하나에서 다운로드 하 여 설치 하는 데 익숙할 것입니다. 그러나 보안상의 이유로 일반적으로 실행 되 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 프로덕션 서버는 인터넷에 연결 되어 있지 않습니다.

- **간편한 오프 라인 설치**: 오프 라인 서버에 패키지를 설치 하려면 패키지 종속성도 모두 다운로드 해야 합니다. MiniCRAN를 사용 하면 모든 종속성을 올바른 형식으로 보다 쉽게 가져올 수 있습니다. MiniCRAN를 사용 하면 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문을 사용 하 여 설치할 패키지를 준비할 때 패키지 종속성 오류가 발생 하지 않도록 할 수 있습니다.

- **향상 된 버전 관리**: 다중 사용자 환경에서는 서버에 여러 패키지 버전을 무제한으로 설치 하지 않는 것이 좋습니다. 로컬 리포지토리를 사용 하 여 사용자에 게 일관 된 패키지 집합을 제공 합니다.

## <a name="install-minicran"></a>MiniCRAN 설치

**MiniCRAN** 패키지 자체는 18vel 패키지에 대 한 시스템 종속성이 있는 **rcurl** 패키지에 해당 하는 18 **개의** 다른 cran 패키지에 종속 됩니다. 마찬가지로 패키지 **XML** 은 **libxml2-devel**에 종속 됩니다. 종속성을 해결 하려면 전체 인터넷에 액세스할 수 있는 컴퓨터에서 초기에 로컬 리포지토리를 빌드하는 것이 좋습니다.

기본 R, R 도구 및 인터넷 연결을 사용 하는 컴퓨터에서 다음 명령을 실행 합니다. SQL Server 컴퓨터가 아닌 것으로 가정 합니다. 다음 명령은 **miniCRAN** 패키지 및 **igraph** 패키지를 설치 합니다. 이 예에서는 패키지가 이미 설치 되어 있는지 여부를 확인 하지만 `if` 문을 무시 하 고 패키지를 직접 설치할 수 있습니다.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>CRAN 미러 및 MRAN 된 스냅숏 설정

패키지를 가져오는 데 사용할 미러 사이트를 지정 합니다. 예를 들어 MRAN 된 사이트나 사용자의 지역에서 필요한 패키지를 포함 하는 다른 사이트를 사용할 수 있습니다. 다운로드에 실패 하면 다른 미러 사이트를 시도 합니다.

```R
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>로컬 폴더 만들기

수집 된 패키지를 저장할 로컬 폴더를 만듭니다. 자주 반복 하는 경우 "miniCRANZooPackages" 또는 "miniCRANMyRPackageV2"와 같이 설명이 포함 된 이름을 사용 하는 것이 좋습니다.

로컬 리포지토리로 폴더를 지정 합니다. R 구문은 경로 이름에 슬래시를 사용 합니다 .이는 Windows 규칙과 반대입니다.

```R
local_repo <- "C:/miniCRANZooPackages"
```

## <a name="add-packages-to-the-local-repo"></a>로컬 리포지토리에 패키지 추가

**MiniCRAN** 를 설치 하 고 로드 한 후 다운로드 하려는 추가 패키지를 지정 하는 목록을 만듭니다.

이 초기 목록에 종속성을 추가 **하지** 마세요. **MiniCRAN** 에서 사용 하는 **igraph** 패키지는 종속성 목록을 자동으로 생성 합니다. 생성 된 종속성 그래프를 사용 하는 방법에 대 한 자세한 내용은 [miniCRAN를 사용 하 여 패키지 종속성 식별](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)을 참조 하세요.

1. 변수에 "zoo" 및 "예측"을 추가 합니다.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. 필요에 따라 종속성 그래프를 그립니다. 이는 필수는 아니지만 정보를 받을 수 있습니다.

    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 로컬 리포지토리를 만듭니다. 필요한 경우 R 버전을 SQL Server 인스턴스에 설치 된 버전으로 변경 해야 합니다. 구성 요소를 업그레이드 한 경우 버전은 원래 버전 보다 최신인 것일 수 있습니다. 자세한 내용은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조 하세요.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   이 정보를 통해 miniCRAN 패키지는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 나중에 패키지를 복사 하는 데 필요한 폴더 구조를 만듭니다.

이 시점에서 필요한 패키지 및 필요한 추가 패키지를 포함 하는 폴더가 있어야 합니다. 폴더는 압축 된 패키지의 컬렉션을 포함 해야 합니다. 패키지의 압축을 풀고 파일의 이름을 바꾸지 마십시오.

필요에 따라 다음 코드를 실행 하 여 로컬 miniCRAN 리포지토리에 포함 된 패키지를 나열 합니다.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>인스턴스 라이브러리에 패키지 추가

필요한 패키지를 사용 하 여 로컬 리포지토리를 만든 후 패키지 리포지토리를 SQL Server 컴퓨터로 이동 합니다. 다음 절차에서는 R tools를 사용 하 여 패키지를 설치 하는 방법을 설명 합니다.

1. MiniCRAN 리포지토리를 포함 하는 폴더를 전체로 복사 하 여 패키지를 설치할 서버에 복사 합니다. 폴더에는 일반적으로 다음 구조가 있습니다. 

   `<miniCRAN root>/bin/windows/contrib/version/<all packages>`

   이 절차에서는 루트 드라이브의 폴더를 가정 합니다.

2. 인스턴스와 연결 된 R 도구를 엽니다 (예: Rgui .exe를 사용할 수 있음). 마우스 오른쪽 단추를 클릭 하 고 **관리자 권한으로 실행** 을 선택 하 여 도구에서 시스템에 대 한 업데이트를 수행할 수 있도록 합니다.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   - 예를 들어 RGUI `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`의 기본 파일 위치는입니다.
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   - 예를 들어 RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`의 파일 위치는입니다.
   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   - 예를 들어 RGUI `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64`의 파일 위치는입니다.
   ::: moniker-end

3. 인스턴스 라이브러리의 경로를 가져오고 라이브러리 경로 목록에 추가 합니다.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   예:

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   예:

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   예:

   ```R
   outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL15.MSSQLSERVER/R_SERVICES/library"
   ```

   ::: moniker-end

4. **MiniCRAN** 리포지토리 `server_repo`를 복사한 서버에서 새 위치를 지정 합니다.

    이 예에서는 서버의 임시 폴더에 리포지토리를 복사 했다고 가정 합니다.

    ```R
    inputlib <- "C:/miniCRANZooPackages"
    ```

5. 서버의 새 R 작업 영역에서 작업 하 고 있으므로 설치할 패키지의 목록도 표시 해야 합니다.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. MiniCRAN 리포지토리의 로컬 복사본에 대 한 경로를 제공 하 여 패키지를 설치 합니다.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 인스턴스 라이브러리에서 다음과 같은 명령을 사용 하 여 설치 된 패키지를 볼 수 있습니다.

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>참조

+ [R 패키지 정보 가져오기](../package-management/r-package-information.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
