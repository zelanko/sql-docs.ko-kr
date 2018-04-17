---
title: MiniCRAN (SQL Server 기계 학습)를 사용 하 여 로컬 R 패키지 리포지토리 만들기 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4ce6479c0e7087e63271811abb47a2174747638e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="create-a-local-r-package-repository-using-minicran"></a>MiniCRAN를 사용 하 여 로컬 R 패키지 리포지토리 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) Andre de Vries 이러한 일반적인 시나리오를 지원 하 여 패키지가 생성 되었습니다. 

+ 단일 패키지 또는 패키지 집합에 대 한 패키지 종속성을 분석
+ R 패키지 집합이 인터넷 연결 되지 않은 서버에 설치를 준비 합니다.

사용자는 원하는 패키지 집합을 지정 하 여 miniCRAN 재귀적으로 이러한 패키지에 대 한 종속성 트리를 읽고 CRAN 또는 유사한 저장소에서 나열 된 패키지만 및 해당 종속성을 다운로드 합니다.

출력으로 miniCRAN에서 내부적으로 일관성이 저장소로 구성 된 선택한 패키지 및 모든 필수 종속성을 만듭니다. 그런 다음이 로컬 저장소를 서버에 이동한 인터넷을 사용 하지 않고 패키지 설치를 진행 합니다.

숙련 된 R 사용자가 다운로드 한 패키지에 대 한 설명 파일에서 종속 패키지 목록은 종종 찾습니다. 패키지에 나열 되는 반면 **Imports** 두 번째 수준 종속성이 있을 수 있습니다. 이러한 이유로 사용 좋습니다는 **miniCRAN** 메서드.

## <a name="what-is-a-package-repository"></a>패키지 저장소는 무엇입니까

로컬 패키지 리포지토리를 만드는의 목표는 서버 관리자 또는 조직의 다른 사용자가 인터넷에 연결 되지 않은 서버에 새 R 패키지를 설치 하는 데 사용할 수 있는 단일 위치를 제공 하는 것입니다. 저장소를 만든 후에 새 패키지를 추가 하거나 기존 패키지의 버전을 업그레이드 하 여 수정할 수 있습니다.

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 에 의해 작성 되었으므로 R에 대 한 패키지 [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) 를 일관 된 만드는 쉽게 수행할 수 있도록 조직에 대 한 R 패키지 집합을 관리 합니다. 

패키지 저장소는 이러한 시나리오에서 유용 합니다.

- **보안**: 많은 R 사용자는에서 다운로드 및 설치가 새 R 패키지 CRAN 또는 해당 미러 사이트의 사이트 중 하나에 익숙해져 있습니다. 그러나 보안상의 이유로 실행 하는 프로덕션 서버에 대 한 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 일반적으로 인터넷에 연결 되어 있지 않습니다.

- **오프 라인 설치 쉽게**: 오프 라인 서버에 패키지를 설치 하려면 모든 패키지 종속 파일을 다운로드할 수도, 사용 하 여 miniCRAN 더 쉽게 종속성을 가져오려면 모든 올바른 형식이 필요 합니다.

    MiniCRAN를 사용 하 여 방지할 수 패키지와 함께 설치를 준비 하는 경우 패키지 종속성 오류는 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문.

- **향상 된 버전 관리**: 다중 사용자 환경에는 제한 되지 않은 서버에 여러 패키지 버전 설치를 방지 하기 위해 경우가 있습니다. 분석가가에서 사용 하기 위해 패키지의 일관 된 집합을 제공 하는 로컬 저장소를 사용 합니다. 

> [!TIP]
> 또한 miniCRAN를 사용 하 여 Azure 기계 학습에서 사용 하기 위해 패키지를 준비 합니다. 자세한 내용은이 블로그를 참조 하십시오.: [miniCRAN 미셸 Usuelli 하 여 Azure 기계 학습에서 사용 하 여](https://www.r-bloggers.com/using-minicran-in-azure-ml/) 

## <a name="prepare-packages-using-minicran"></a>MiniCRAN를 사용 하 여 패키지 준비

**miniCRAN** 패키지 자체를 다른 18 CRAN 패키지에 종속 되어 있는 간에 **RCurl** 시스템 종속 되어 있는 패키지를에 **curl 개발자** 패키지 합니다. 마찬가지로, 패키지 **XML** 에 종속 **libxml2 개발자**합니다. 

이러한 이유로, 빌드하는 로컬 리포지토리 처음 전체 인터넷에 연결 된 컴퓨터에 있도록 좋습니다 이러한 모든 종속성을 쉽게 맞출 수 있습니다. 

리포지토리를 만든 후에 다른 위치에 저장소를 이동할 수 있습니다.

### <a name="step-1-install-the-minicran-package"></a>1단계. MiniCRAN 패키지 설치

만들어서 시작는 **miniCRAN** 저장소를 원본으로 사용 합니다. 인터넷에 연결 하는 컴퓨터에서이 리포지토리를 만들어야 합니다.

1. 설치는 **miniCRAN** 패키지와 필요한 **igraph** 패키지 합니다. 이 예제에서는 패키지가 이미 설치 여부 확인 하지만 if를 무시할 수 있습니다 문을 직접 패키지를 설치 하 고 있습니다.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") 
    if(!require("igraph")) install.packages("igraph") 
    library("miniCRAN")
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>2단계. 패키지 원본 정의: CRAN 미러 또는 MRAN 스냅숏

1. 패키지를 가져올 수 있는 사용 하도록 미러 사이트를 지정 합니다. 예를 들어 필요한 패키지를 포함 하는 해당 지역에서 MRAN 사이트 또는 다른 사이트를 사용할 수 있습니다. 다운로드가 실패 하면 다른 미러 사이트를 시도 하십시오.

    ```R
    CRAN_mirror <- c(CRAN = "https://mran.microsoft.com")
    CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
    ```

2. 수집 된 패키지를 저장할 로컬 폴더의 이름을 입력 합니다. 

    사전에 폴더를 만들 수 있어야 합니다. 오류가 발생 하는 경우는 `local_repo` 나중에 R 코드를 실행할 때 폴더가 존재 하지 않습니다.

    폴더 설명 하는 이름이 있어야 합니다. "MiniCRAN"을 사용 했습니다 여기 있지만 종종이 작업을 반복 하는 경우 아마도 "miniCRANZooPackages" 또는 "miniCRANMyRPackagev2" 같은 보다 설명적인 이름을 사용 해야 합니다.

    ```R
    local_repo <- "~/miniCRAN"
    ```

    결과 해당 하는 환경 변수를 반환 하는 물결표 확장 연산자 `Sys.getenv("R_USER")`합니다.

### <a name="step-3-add-packages-to-the-repository"></a>3단계. 패키지 저장소에 추가

1. 후 **miniCRAN** 가 다운로드 하려는 추가 패키지를 지정 하는 목록을 생성 설치 합니다.

    수행 **하지** 종속성이 초기 목록에 추가 합니다. **igraph** 패키지에서 사용 하는 **miniCRAN** 종속성 목록을 생성 합니다. 생성 된 종속성 그래프를 사용 하는 방법에 대 한 자세한 내용은 참조 [miniCRAN를 사용 하 여 패키지 종속성을 식별 하](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)합니다.

    다음 R 스크립트는 대상 패키지, "zoo"와 "예측" 변수에 추가합니다.

    ```R
    pkgs_needed <- c("zoo", "forecast")
    ```
2. 없는 필수 종속성 그래프를 표시 하지만 정보를 제공 없을 수 있습니다.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 로컬 리포지토리를 만듭니다. 필요한 경우 R 버전을 변경 해야 합니다.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3");
    ```

    이 정보를 miniCRAN 패키지에 패키지를 복사 해야 하는 폴더 구조를 만듭니다는 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 나중입니다.

4. 이 시점에서 패키지를 포함 하는 폴더 있어야 하 고 필요 했던 모든 추가 패키지 합니다.

    MiniCRAN 저장소에 포함 된 패키지를 나열 하려면 다음 코드를 실행할 수 있습니다.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE);
    head(pdb);
    pdb$Package;
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>4단계. R 패키지 라이브러리에 추가 하는 인스턴스 저장소를 사용 하 여

저장소를 만들어 있습니다 필요한 패키지를 추가한 후에 서버 컴퓨터에 패키지 리포지토리를 이동 하 고 SQL Server에서 사용 하기 위해 올바른 라이브러리에 R 패키지가 설치 되어 있는지 확인 해야 합니다.

다음 절차에는 R 도구를 사용 하 여 패키지를 설치 하는 방법을 설명 합니다.

1. MiniCRAN 리포지토리 패키지를 설치 하려는 서버에 전체를 포함 하는 폴더를 복사 합니다. 폴더에는 일반적으로이 구조에: miniCRAN 루트 > bin->-> windows-contrib > 버전을 더-> 모든 패키지->.

2. 인스턴스와 연결 된 R 도구를 사용 하 여 R 명령 프롬프트를 엽니다.

    - SQL Server 2017 년에 대 한 기본 폴더는 `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`합니다.

    - SQL Server 2016의 경우 기본 폴더는 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`입니다.

    - 명명 된 인스턴스의 경우 기본 경로 것과 같이 설정 해야: `<instance_path>.RTEST/R_SERVICES/library`합니다.

    -  다른 드라이브에 SQL Server를 설치했거나 설치 경로에서 다른 변경을 수행한 경우 해당 변경도 수행해야 합니다.

3. 인스턴스 라이브러리에 대 한 경로 가져오고 라이브러리 경로 목록에 추가 합니다.

    ```R
    .libPaths()[1];
    lib <- .libPaths()[1]
    ```

    이 명령은 SQL Server에서와 같은 인스턴스와 연결 된 라이브러리 경로 반환 해야: "c: / Program 파일/Microsoft SQL Server/MSSQL14 합니다. MSSQLSERVER/R_SERVICES/라이브러리 "

4. 복사 했던 서버에서 새 위치를 지정 된 **miniCRAN** 저장소로 `server_repo`합니다.

    이 예제에서는 저장소 서버에 임시 폴더에 복사한 가정 합니다.

    ```R
    source_repo <- "C:\\temp\\miniCRAN"
    ```

5. 서버에 새 R 작업 영역에서 작업 하는 이후를 설치 하는 패키지 목록을도 제공 해야 합니다.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

6. MiniCRAN 리포지토리의 로컬 복사본에 대 한 경로 제공 하는 패키지를 설치 합니다.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath;(source_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE);
    ```

7. 인스턴스 라이브러리에서 다음과 같은 명령을 사용 하 여 설치 된 패키지를 볼 수 있습니다.

    ```R
    installed.packages()
    ```

> [!NOTE] 
> SQL Server에서 패키지를 사용 하는 인스턴스에 사용 되는 기본 라이브러리에 패키지를 설치 합니다. 

## <a name="manually-install-a-single-package-from-a-zipped-file"></a>압축된 된 파일에서 단일 패키지를 수동으로 설치 합니다.

종속 되지 않은 단일 패키지를 설치 하는 하거나 사용할 수 없는 경우 **miniCRAN**, 수동으로 필요한 패키지를 다운로드할 수 있습니다. 이 작업을 수행 하는 관리자 또는 서버의 유일한 소유자 필요 합니다.

패키지를 다운로드 한 후 압축 된 파일 위치에서 R 패키지를 설치 합니다.

1. 패키지를 압축 된 파일로 다운로드 하 고 있는 로컬 폴더에 저장

2. 해당 폴더에 복사는 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 컴퓨터입니다.

3. 기본 R 명령을 사용 하 여 SQL Server 인스턴스 라이브러리에 패키지를 설치 합니다. 패키지에 아직 설치 되지 않은 종속성을 포함 하지 않으면 설치가 실패할 수 있습니다. 

사용 하 여 SQL Server 2017 년의 인스턴스로 개별 패키지를 업로드할 수도 있습니다는 [외부 라이브러리 만들기 문을](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql)합니다. 이 프로세스는 관리 액세스도 필요합니다.
