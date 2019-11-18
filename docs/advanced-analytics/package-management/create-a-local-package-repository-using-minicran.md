---
title: miniCRAN을 사용하여 리포지토리 만들기
description: miniCRAN 패키지를 사용하여 오프라인으로 R 패키지를 설치하고 패키지 및 종속성의 로컬 리포지토리를 만드는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9b83a0c016cf16e4df8ef7fcb90b3711eabe4933
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727574"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>miniCRAN을 사용하여 로컬 R 패키지 리포지토리 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html)을 사용하여 오프라인으로 R 패키지를 설치하고 패키지 및 종속성의 로컬 리포지토리를 만드는 방법을 설명합니다. **miniCRAN**은 패키지 및 종속성을 식별하여 단일 폴더에 다운로드합니다. 이것을 다른 컴퓨터에 복사하여 오프라인으로 R 패키지를 설치할 수 있습니다.

하나 이상의 패키지를 지정할 수 있으며, **miniCRAN**은 이러한 패키지에 대한 종속성 트리를 재귀적으로 읽습니다. 그런 다음, 나열된 패키지와 CRAN 또는 유사한 리포지토리의 해당 종속성만 다운로드합니다.

여기까지 완료되면 **miniCRAN**은 선택한 패키지와 모든 필수 종속성으로 구성된 내부적으로 일관적인 리포지토리를 만듭니다. 이 로컬 리포지토리를 서버로 이동하고, 인터넷에 연결하지 않고 패키지를 계속 설치할 수 있습니다.

숙련된 R 사용자는 다운로드한 패키지의 DESCRIPTION 파일에서 종속 패키지 목록을 검색하는 경우가 자주 있습니다. 그러나 **가져오기**에 나열된 패키지에 두 번째 수준의 종속성이 있을 가능성도 있습니다. 이러한 이유로 필수 패키지의 전체 컬렉션을 어셈블하는 데 **miniCRAN**을 사용할 것을 권장합니다.

## <a name="why-create-a-local-repository"></a>로컬 리포지토리를 만드는 이유

로컬 패키지 리포지토리를 만드는 목적은 서버 관리자 또는 조직 내 다른 사용자가 서버에 새 R 패키지, 특히 인터넷에 액세스할 수 없는 패키지를 설치하는 데 사용할 수 있는 단일 위치를 제공하는 것입니다. 리포지토리를 만든 후에는 새 패키지를 추가하거나 기존 패키지의 버전을 업그레이드하여 리포지토리를 수정할 수 있습니다.

패키지 리포지토리는 다음과 같은 시나리오에 유용합니다.

- **보안**: 많은 R 사용자는 CRAN 또는 미러 사이트 중 하나에서 새 R 패키지를 다운로드하여 설치하는 데 익숙합니다. 그러나 보안상의 이유로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]를 실행하는 프로덕션 서버는 일반적으로 인터넷에 연결되지 않습니다.

- **간편한 오프라인 설치**: 오프라인 서버에 패키지를 설치하려면 모든 패키지 종속 요소도 다운로드해야 합니다. miniCRAN을 사용하면 모든 종속 요소를 올바른 형식으로 보다 쉽게 가져올 수 있습니다. miniCRAN을 사용하면 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문을 사용하여 설치할 패키지를 준비할 때 패키지 종속성 오류를 방지할 수 있습니다.

- **개선된 버전 관리**: 다중 사용자 환경에서는 서버에 여러 패키지 버전을 무제한으로 설치하지 않는 것이 좋습니다. 로컬 리포지토리를 사용하여 사용자에게 일관적인 패키지 세트를 제공하세요.

## <a name="install-minicran"></a>miniCRAN 설치

**miniCRAN** 패키지 자체는 18개의 다른 CRAN 패키지에 종속되어 있으며, 그 중 하나인 **RCurl**은 **curl-devel** 패키지에 시스템이 종속되어 있습니다. 마찬가지로, **XML** 패키지는 **libxml2-devel**에 종속되어 있습니다. 종속성을 해결하려면 처음에는 인터넷에 완전히 액세스할 수 있는 머신에서 로컬 리포지토리를 빌드하는 것이 좋습니다.

기본 R, R 도구 및 인터넷 연결을 사용하는 컴퓨터에서 다음 명령을 실행합니다. 이 컴퓨터는 SQL Server 컴퓨터가 아닌 것으로 가정합니다. 다음 명령은 **miniCRAN** 패키지와 **igraph** 패키지를 설치합니다. 이 예제에서는 패키지가 이미 설치되어 있는지 여부를 확인하지만, `if` 문을 무시하고 패키지를 직접 설치할 수 있습니다.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>CRAN 미러 및 MRAN 스냅샷 설정

패키지를 가져오는 데 사용할 미러 사이트를 지정합니다. 예를 들어 MRAN 사이트 또는 해당 지역의 사이트 중에서 필요한 패키지를 포함하고 있는 다른 사이트를 사용할 수 있습니다. 다운로드가 실패하면 다른 미러 사이트를 시도합니다.

```R
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>로컬 폴더 만들기

수집한 패키지를 저장할 로컬 폴더를 만듭니다. 이 작업을 자주 반복하는 경우 "miniCRANZooPackages" 또는 "miniCRANMyRPackageV2"처럼 자세한 이름을 사용하는 것이 좋습니다.

폴더를 로컬 리포지토리로 지정합니다. R 구문은 Windows 규칙과 반대로 경로 이름에 슬래시를 사용합니다.

```R
local_repo <- "C:/miniCRANZooPackages"
```

## <a name="add-packages-to-the-local-repo"></a>로컬 리포지토리에 패키지 추가

**miniCRAN**을 설치하고 로드한 후에는 다운로드할 추가 패키지를 지정하는 목록을 만듭니다.

이 초기 목록에는 종속성을 추가하지 **마세요**. **miniCRAN**에서 사용하는 **igraph** 패키지는 종속성 목록을 자동으로 생성합니다. 생성된 종속성 그래프를 사용하는 방법에 대한 자세한 내용은 [miniCRAN을 사용하여 패키지 종속성을 식별하는 방법](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)을 참조하세요.

1. 대상 패키지 "zoo" 및 "forecast"를 변수에 추가합니다.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. 필요에 따라 종속성 그래프를 그립니다. 필수 사항은 아니지만 정보를 얻을 수 있습니다.

    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 로컬 리포지토리를 만듭니다. 필요한 경우 R 버전을 SQL Server 인스턴스에 설치된 버전으로 변경해야 합니다. 구성 요소를 업그레이드한 경우 현재 버전이 원래 버전보다 높을 수 있습니다. 자세한 내용은 [R 패키지 정보 가져오기](../package-management/r-package-information.md)를 참조하세요.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   이 정보를 통해 miniCRAN 패키지는 나중에 패키지를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 복사하는 데 필요한 폴더 구조를 만듭니다.

지금은 폴더에 필요한 패키지와 필요한 추가 패키지가 들어 있습니다. 이 폴더에는 압축된 패키지 컬렉션이 포함되어 있습니다. 패키지의 압축을 풀거나 파일 이름을 바꾸지 마세요.

필요에 따라 다음 코드를 실행하여 로컬 miniCRAN 리포지토리에 포함된 패키지를 나열합니다.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>인스턴스 라이브러리에 패키지 추가

필요한 패키지가 포함된 로컬 리포지토리를 만든 후에는 패키지 리포지토리를 SQL Server 컴퓨터로 이동합니다. 다음 절차에서는 R 도구를 사용하여 패키지를 설치하는 방법을 설명합니다.

1. miniCRAN 리포지토리가 포함된 폴더 전체를, 패키지를 설치할 서버에 복사합니다. 일반적으로 이 폴더의 구조는 다음과 같습니다. 

   `<miniCRAN root>/bin/windows/contrib/version/<all packages>`

   이 절차에서는 루트 드라이브의 폴더인 것으로 가정합니다.

2. 인스턴스와 연결된 R 도구를 엽니다(예를 들어 Rgui.exe를 사용할 수 있음). 마우스 오른쪽 단추를 클릭하고 **관리자 권한으로 실행**을 선택하여 도구에서 시스템을 업데이트할 수 있도록 허용합니다.

   ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
   - 예를 들어 RGUI의 기본 파일 위치는 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`입니다.
   ::: moniker-end

   ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
   - 예를 들어 RGUI의 파일 위치는 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`입니다.
   ::: moniker-end

   ::: moniker range=">sql-server-2017||=sqlallproducts-allversions"
   - 예를 들어 RGUI의 파일 위치는 `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\bin\x64`입니다.
   ::: moniker-end

3. 인스턴스 라이브러리의 경로를 가져와서 라이브러리 경로 목록에 추가합니다.

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

4. **miniCRAN** 리포지토리를 `server_repo`로 복사한 서버의 새 위치를 지정합니다.

    이 예제에서는 서버의 임시 폴더에 리포지토리를 복사했다고 가정합니다.

    ```R
    inputlib <- "C:/miniCRANZooPackages"
    ```

5. 서버의 새 R 작업 영역에서 작업 중이므로 설치할 패키지 목록도 제공해야 합니다.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. 패키지를 설치하고, miniCRAN 리포지토리의 로컬 복사본 경로를 제공합니다.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 인스턴스 라이브러리에서 다음과 같은 명령을 사용하여 설치된 패키지를 볼 수 있습니다.

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>관련 항목:

+ [R 패키지 정보 가져오기](../package-management/r-package-information.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
