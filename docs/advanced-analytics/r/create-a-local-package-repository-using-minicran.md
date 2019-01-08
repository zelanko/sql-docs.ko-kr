---
title: MiniCRAN-SQL Server Machine Learning Services를 사용 하 여 로컬 R 패키지 리포지토리 만들기
description: MiniCran을 사용 하 여 감지, 어셈블 및 R 패키지 종속성을 하나의 통합 패키지로 설치 합니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/29/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7dc2e286e6eb80fe1eef3e8b86ed1002a6344cfb
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53431756"
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>MiniCRAN을 사용 하 여 로컬 R 패키지 리포지토리 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 패키지를 만들어 [Andre de Vries](https://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)하 게 식별 하 고 패키지 및 R 패키지를 오프 라인 설치에 대 한 다른 컴퓨터에 복사할 수 있는 단일 폴더에 종속성을 다운로드 합니다.

입력으로 하나 이상의 패키지를 지정 합니다. **miniCRAN** 재귀적으로 이러한 패키지에 대 한 종속성 트리를 읽고 CRAN 또는 유사한 저장소에서 나열된 된 패키지 및 해당 종속성을 다운로드 합니다.

출력으로 **miniCRAN** 선택한 패키지 및 모든 필수 종속성 구성 된 내부적으로 일관성이 리포지토리를 만듭니다. 그런 다음 서버에이 로컬 저장소를 이동 하 고 인터넷에 연결 하지 않고 패키지 설치를 계속할 수 있습니다.

> [!NOTE]
> 경험이 많은 R 사용자 종종 종속 패키지 다운로드 한 패키지의 DESCRIPTION 파일의 목록을 찾습니다. 패키지에 나열 되는 반면 **Imports** 두 번째 수준 종속성이 있을 수 있습니다. 따라서 것이 좋습니다 **miniCRAN** 필요한 패키지의 전체 컬렉션을 조합 합니다.

## <a name="why-create-a-local-repository"></a>로컬 리포지토리를 만드는 이유

로컬 패키지 리포지토리를 만들겠다는 목표 특히 다른 하나는 인터넷 액세스가 없는 서버에 새 R 패키지를 설치 하려면 서버 관리자 또는 조직의 다른 사용자가 사용할 수 있는 단일 위치를 제공 하는 것입니다. 리포지토리를 만든 후에 새 패키지를 추가 하거나 기존 패키지 버전을 업그레이드 하 여 수정할 수 있습니다.

패키지 리포지토리는 이러한 시나리오에서 유용 합니다.

- **보안**: 많은 R 사용자가 다운로드 및 CRAN 또는 미러 사이트 중 하나에서 부과 하는 새로운 R 패키지를 설치 하는 데 익숙한 합니다. 그러나 보안상의 이유로, 실행 하는 프로덕션 서버 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 일반적으로 인터넷에 연결 되어 있지 않습니다.

- **오프 라인 설치 쉽게**: 오프 라인 서버에 패키지를 설치 하는 모든 패키지 종속 파일을 다운로드할 수도, miniCRAN을 사용 하 여 더 쉽게 종속성을 가져오려면 모든 올바른 형식이 필요 합니다.

    MiniCRAN을 사용 하 여 방지할 수 패키지를 사용 하 여 설치를 준비 하는 경우 패키지 종속성 오류를 [CREATE EXTERNAL LIBRARY](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문입니다.

- **향상 된 버전 관리**: 다중 사용자 환경에서 제한 되지 않은 서버에서 여러 패키지 버전 설치를 방지 하려면 적절 한 이유가 있습니다. 로컬 리포지토리를 사용 하 여 프로그램 분석가가 사용에 대 한 일관 된 패키지 집합을 제공 합니다. 

> [!TIP]
> 또한 Azure Machine Learning에서 사용할 패키지를 준비 하려면 miniCRAN를 사용할 수 있습니다. 자세한 내용은이 블로그를 참조 하세요. [MiniCRAN을 사용 하 여 Michele Usuelli 하 여 Azure 기계 학습에서](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="install-minicran"></a>MiniCRAN 설치

**miniCRAN** 패키지 자체는 다른 18 CRAN 패키지와 종속 인 간에 **RCurl** 시스템 종속성 패키지를에 **curl 개발자** 패키지. 마찬가지로, 패키지 **XML** 종속성을 가진 **libxml2 개발자**합니다. 종속성을 해결 하려면 작성 하는 로컬 리포지토리에 처음에 전체 인터넷 액세스를 사용 하 여 컴퓨터에서 하는 것이 좋습니다. 

기본 R 사용 하는 컴퓨터에서 다음 명령을 실행 R 도구 및 인터넷에 연결 합니다. 이 가정 *되지* SQL Server 컴퓨터. 다음 명령을 설치 합니다 **miniCRAN** 패키지 및 필수 **igraph** 패키지 있습니다. 이 예제에서는 패키지가 이미 설치 여부를 확인 하지만 경우에는 무시할 수 있습니다 문 및 패키지를 직접 설치 합니다.

```R
if(!require("miniCRAN")) install.packages("miniCRAN") 
if(!require("igraph")) install.packages("igraph") 
library("miniCRAN")
```

## <a name="set-the-cran-mirror-and-mran-snapshot"></a>MRAN 스냅숏과 CRAN 미러를 설정 합니다.

패키지를 가져오는 데 미러 사이트를 지정 합니다. 예를 들어, 필요한 패키지를 포함 하는 지역의 MRAN 사이트 또는 다른 사이트를 사용할 수 있습니다. 다운로드가 실패할 경우 다른 미러 사이트를 시도 합니다.

```R
CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
```

## <a name="create-a-local-folder"></a>로컬 폴더를 만듭니다

와 같은 로컬 폴더를 만들 `C:\mylocalrepo` 수집 된 패키지를 저장 하는 합니다. 종종이 작업을 반복 하는 경우 아마도 "miniCRANZooPackages" 또는 "miniCRANMyRPackagev2"와 같은 보다 알기 쉬운 이름, 사용 해야 합니다.

로컬 리포지토리로 폴더를 지정 합니다. R 구문을 사용 하 여 슬래시 경로 이름에 대 한 반대 되는 Windows 규칙에서.

```R
local_repo <- "C:/mylocalrepo"
```

## <a name="add-packages-to-the-local-repo"></a>로컬 리포지토리 패키지에 추가

이후에 **miniCRAN** 설치 되 고 다운로드 하려면 추가 패키지를 지정 하는 목록을 만듭니다 로드 합니다.

수행할 **되지** 종속성이 초기 목록에 추가 합니다. 합니다 **igraph** 에서 사용 하는 패키지 **miniCRAN** 수에 대 한 종속성 목록을 생성 합니다. 생성 된 종속성 그래프를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [miniCRAN 패키지 종속성을 식별 하는를 사용 하 여](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)입니다.

1. "Zoo"와 "예측" 변수에 대상 패키지를 추가 합니다.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```

2. 필요에 따라 종속성 그래프를 그릴 수 있지만 하지 정보를 제공 합니다.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 로컬 리포지토리를 만듭니다. SQL Server 인스턴스에 설치 된 버전에 필요한 경우 R 버전을 변경 해야 합니다. 3.2.2 버전이 SQL Server 2016에서, SQL Server 2017에서 버전 3.3을 합니다. 구성 요소 업그레이드를 수행한 경우에 버전 새로운 버전일 수 있습니다. 자세한 내용은 [가져오려면 R 및 Python 패키지 정보](determine-which-packages-are-installed-on-sql-server.md)합니다.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

   이 정보를 miniCRAN 패키지는 패키지를 복사 해야 하는 폴더 구조를 만들기는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 나중입니다.

이 시점에 필요한 패키지가 포함 된 폴더가 있어야 하 고 필요 했습니다 추가 패키지 합니다. 경로이 예와 비슷해야 합니다. C:\mylocalrepo\bin\windows\contrib\3.3 하며 압축 된 패키지의 컬렉션을 포함 해야 합니다. 모든 파일을 바꾸거나 패키지의 압축을 풉니다 수행 합니다.

필요에 따라 로컬 miniCRAN 리포지토리에 포함 된 패키지를 나열 하려면 다음 코드를 실행 합니다.

```R
pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
head(pdb);
pdb$Package;
pdb[, c("Package", "Version", "License")]
```

## <a name="add-packages-to-the-instance-library"></a>인스턴스 라이브러리에 패키지를 추가 합니다.

필요한 패키지를 사용 하 여 로컬 리포지토리를 만든 후 SQL Server 컴퓨터에 패키지 리포지토리를 이동 합니다. 다음 절차에는 R 도구를 사용 하 여 패키지를 설치 하는 방법을 설명 합니다.

1. MiniCRAN 리포지토리 패키지를 설치 하려는 서버로 전체를 포함 하는 폴더를 복사 합니다. 폴더에 일반적으로이 구조가: miniCRAN 루트 > bin > windows > contrib > 버전 > 모든 패키지 있습니다. 다음 예제에서는 루트 드라이브 해제 폴더를 가정합니다. 

2. 인스턴스와 연결 된 R 도구를 엽니다 (예를 들어 사용할 수 있습니다 Rgui.exe). 마우스 오른쪽 단추로 클릭 **관리자 권한으로 실행** 도구 시스템에 업데이트를 허용 하도록 합니다.

    - SQL Server 2017에 대 한 파일 RGUI 위치가 `C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`합니다.

    - SQL Server 2016의 경우 그 파일 RGUI 위치가 `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`합니다.

3. 인스턴스 라이브러리에 대 한 경로 가져오고 라이브러리 경로 목록에 추가 합니다. SQL Server 2017의 경로 다음 예제와 비슷합니다.

    ```R
    outputlib <- "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library"
    ```

4. 복사한 서버의 새 위치를 지정 합니다 **miniCRAN** 리포지토리에으로 `server_repo`입니다.

    이 예제에서는 저장소 서버의 임시 폴더에 복사 하는 가정 합니다.

    ```R
    inputlib <- "C:/temp/mylocalrepo"
    ```

5. 서버에서 새 R 작업 영역에서 작업 하는 이후 설치할 패키지 목록을 제공도 해야 합니다.

    ```R
    mypackages <- c("zoo", "forecast")
    ```

6. MiniCRAN 리포지토리의 로컬 복사본에 경로 제공 하는 패키지를 설치 합니다.

    ```R
    install.packages(mypackages, repos = file.path("file://", normalizePath(inputlib, winslash = "/")), lib = outputlib, type = "win.binary", dependencies = TRUE);
    ```

7. 인스턴스 라이브러리에서 다음과 같은 명령을 사용 하 여 설치 된 패키지를 볼 수 있습니다.

    ```R
    installed.packages()
    ```

## <a name="see-also"></a>참고자료

+ [패키지 정보 가져오기](determine-which-packages-are-installed-on-sql-server.md)
+ [R 자습서](../tutorials/sql-server-r-tutorials.md)
+ [방법 가이드](sql-server-machine-learning-tasks.md)


