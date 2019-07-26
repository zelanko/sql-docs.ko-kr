---
title: MiniCRAN를 사용 하 여 로컬 R 패키지 리포지토리 만들기
description: MiniCran를 사용 하 여 R 패키지 종속성을 검색 하 고 조합 하며 단일 통합 패키지로 설치 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 06/13/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 34b7fee6b5eef1503f56dd72c6d8ff10911bbdc1
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470221"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>MiniCRAN를 사용 하 여 로컬 R 패키지 리포지토리 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)에서 만든 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 패키지는 패키지와 종속성을 식별 하 여 단일 폴더에 다운로드 합니다 .이 패키지는 오프 라인 R 패키지 설치를 위해 다른 컴퓨터에 복사할 수 있습니다.

입력으로 하나 이상의 패키지를 지정 합니다. **miniCRAN** 는 이러한 패키지에 대 한 종속성 트리를 재귀적으로 읽고 나열 된 패키지와 해당 종속성만 cran 또는 유사한 리포지토리에서 다운로드 합니다.

출력으로 **miniCRAN** 는 선택한 패키지 및 모든 필수 종속성으로 구성 된 내부적으로 일관 된 리포지토리를 만듭니다. 그런 다음이 로컬 리포지토리를 서버로 이동 하 고 인터넷에 연결 하지 않고 패키지 설치를 계속할 수 있습니다.

> [!NOTE]
> 숙련 된 R 사용자는 다운로드 한 패키지에 대 한 설명 파일에서 종속 패키지 목록을 검색 하는 경우가 많습니다. 그러나 **가져오기** 에 나열 된 패키지에는 두 번째 수준 종속성이 있을 수 있습니다. 따라서 필요한 패키지의 전체 컬렉션을 어셈블하는 데 **miniCRAN** 을 권장 합니다.

## <a name="why-create-a-local-repository"></a>로컬 리포지토리를 만드는 이유

로컬 패키지 리포지토리를 만드는 목적은 서버 관리자 또는 조직의 다른 사용자가 서버에 새 R 패키지를 설치 하는 데 사용할 수 있는 단일 위치를 제공 하는 것입니다. 특히 인터넷에 액세스할 수 없는 것입니다. 리포지토리를 만든 후에는 새 패키지를 추가 하거나 기존 패키지의 버전을 업그레이드 하 여 리포지토리를 수정할 수 있습니다.

패키지 리포지토리는 다음과 같은 시나리오에서 유용 합니다.

- **보안**: 많은 R 사용자는 새 R 패키지를 CRAN 또는 해당 미러 사이트 중 하나에서 다운로드 하 여 설치 하는 데 익숙할 것입니다. 그러나 보안상의 이유로 일반적으로 실행 되 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 프로덕션 서버는 인터넷에 연결 되어 있지 않습니다.

- **간편한 오프 라인 설치**: 오프 라인 서버에 패키지를 설치 하려면 miniCRAN를 사용 하 여 모든 종속성을 다운로드 하 여 올바른 형식으로 모든 종속성을 가져오기도 해야 합니다.

    MiniCRAN를 사용 하면 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문을 사용 하 여 설치할 패키지를 준비할 때 패키지 종속성 오류가 발생 하지 않도록 할 수 있습니다.

- **향상 된 버전 관리**: 다중 사용자 환경에서는 서버에서 여러 패키지 버전의 무제한 설치를 방지 해야 하는 좋은 이유가 있습니다. 로컬 리포지토리를 사용 하 여 분석가에서 사용할 일관 된 패키지 집합을 제공 합니다. 

> [!TIP]
> MiniCRAN를 사용 하 여 Azure Machine Learning에서 사용할 패키지를 준비할 수도 있습니다. 자세한 내용은 다음 블로그를 참조 하세요. [Michele Usuelli에서 Azure ML에서 miniCRAN 사용](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>MiniCRAN 설치

**MiniCRAN** 패키지 자체는 18vel 패키지에 대 한 시스템 종속성이 있는 **rcurl** 패키지에 해당 하는 18 **개의** 다른 cran 패키지에 종속 됩니다. 마찬가지로 패키지 **XML** 은 **libxml2-devel**에 종속 됩니다. 종속성을 해결 하려면 전체 인터넷에 액세스할 수 있는 컴퓨터에서 초기에 로컬 리포지토리를 빌드하는 것이 좋습니다. 

기본 R, R 도구 및 인터넷 연결을 사용 하는 컴퓨터에서 다음 명령을 실행 합니다. SQL Server 컴퓨터가 *아닌* 것으로 가정 합니다. 다음 명령은 **miniCRAN** 패키지 및 필수 **igraph** 패키지를 설치 합니다. 이 예에서는 패키지가 이미 설치 되어 있는지 여부를 확인 하지만 if 문을 무시 하 고 패키지를 직접 설치할 수 있습니다.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>CRAN 미러 및 MRAN 된 스냅숏 설정

패키지를 가져오는 데 사용할 미러 사이트를 지정 합니다. 예를 들어 MRAN 된 사이트나 사용자의 지역에서 필요한 패키지를 포함 하는 다른 사이트를 사용할 수 있습니다. 다운로드에 실패 하면 다른 미러 사이트를 시도 합니다.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>로컬 폴더 만들기

수집 된 패키지를 저장할와 `C:\mylocalrepo` 같은 로컬 폴더를 만듭니다. 이를 자주 반복 하는 경우 "miniCRANZooPackages" 또는 "miniCRANMyRPackagev2"와 같이 좀 더 설명적인 이름을 사용 해야 합니다.

로컬 리포지토리로 폴더를 지정 합니다. R 구문은 경로 이름에 슬래시를 사용 합니다 .이는 Windows 규칙과 반대입니다.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>로컬 리포지토리에 패키지 추가

**MiniCRAN** 를 설치 하 고 로드 한 후 다운로드 하려는 추가 패키지를 지정 하는 목록을 만듭니다.

이 초기 목록에 종속성을 추가 **하지** 마세요. **MiniCRAN** 에서 사용 하는 **igraph** 패키지는 종속성 목록을 생성 합니다. 생성 된 종속성 그래프를 사용 하는 방법에 대 한 자세한 내용은 [miniCRAN를 사용 하 여 패키지 종속성 식별](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)을 참조 하세요.

1. 변수에 대상 패키지, "zoo" 및 "예측"을 추가 합니다.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. 필요에 따라 종속성 그래프를 그리면 정보를 사용할 수 있습니다.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 로컬 리포지토리를 만듭니다. 필요한 경우 SQL Server 인스턴스에 설치 된 버전에 대 한 R 버전을 변경 해야 합니다. 버전 3.2.2 SQL Server 2016, 버전 3.3 SQL Server 2017에 있습니다. 구성 요소를 업그레이드 한 경우 버전이 최신 버전이 될 수 있습니다. 자세한 내용은 [R 및 Python 패키지 정보 가져오기](../package-management/installed-package-information.md)를 참조 하세요.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   이 정보를 통해 miniCRAN 패키지는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 나중에 패키지를 복사 하는 데 필요한 폴더 구조를 만듭니다.

이 시점에서 필요한 패키지 및 필요한 추가 패키지를 포함 하는 폴더가 있어야 합니다. 경로는 다음 예제와 유사 해야 합니다. C:\mylocalrepo\bin\windows\contrib\3.3 및 압축 된 패키지의 컬렉션을 포함 해야 합니다. 패키지의 압축을 풀고 파일의 이름을 바꾸지 마십시오.

필요에 따라 다음 코드를 실행 하 여 로컬 miniCRAN 리포지토리에 포함 된 패키지를 나열 합니다.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>인스턴스 라이브러리에 패키지 추가

필요한 패키지를 사용 하 여 로컬 리포지토리를 만든 후 패키지 리포지토리를 SQL Server 컴퓨터로 이동 합니다. 다음 절차에서는 R tools를 사용 하 여 패키지를 설치 하는 방법을 설명 합니다.

1. MiniCRAN 리포지토리를 포함 하는 폴더를 전체로 복사 하 여 패키지를 설치할 서버에 복사 합니다. 이 폴더에는 일반적으로 miniCRAN root > bin > windows > 모든 패키지 > > 버전이 포함 됩니다. 다음 예제에서는 루트 드라이브의 폴더를 가정 합니다. 

2. 인스턴스와 연결 된 R 도구를 엽니다 (예: Rgui .exe를 사용할 수 있음). **관리자 권한으로 실행** 을 마우스 오른쪽 단추로 클릭 하 여 도구에서 시스템에 대 한 업데이트를 수행할 수 있도록 합니다.

    - SQL Server 2017의 경우 RGUI `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`의 파일 위치는입니다.

    - SQL Server 2016의 경우 RGUI의 파일 위치는 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`입니다.

3. 인스턴스 라이브러리의 경로를 가져오고 라이브러리 경로 목록에 추가 합니다. SQL Server 2017에서 경로는 다음 예제와 유사 합니다.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. **MiniCRAN** 리포지토리를 복사한 서버에서로 `server_repo`새 위치를 지정 합니다.

    이 예에서는 서버의 임시 폴더에 리포지토리를 복사 했다고 가정 합니다.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
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

+ [패키지 정보 가져오기](../package-management/installed-package-information.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
