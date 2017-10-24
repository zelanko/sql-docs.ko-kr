---
title: "MiniCRAN를 사용 하 여 로컬 패키지 리포지토리 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 09/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: 1dd7e8f1a0054818849b3b9672a5df6286bdabce
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>MiniCRAN를 사용 하 여 로컬 패키지 리포지토리 만들기

인터넷 연결 되지 않은 서버에 설치에 대 한 R 패키지를 준비할 수 있는 두 가지가 있습니다.

-   [MiniCRAN 패키지를 사용 하 여 단일 로컬 리포지토리 만들기](#bkmk_miniCRAN)

    [miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) CRAN와 유사한 저장소에서 선택 된 패키지의 구성 되는 내부적으로 일관성이 저장소를 만듭니다. 사용자는 원하는 패키지 집합을 지정 하 여 miniCRAN 재귀적으로 이러한 패키지에 대 한 종속성 트리를 읽고 나열 된 패키지만 및 해당 종속성을 다운로드 합니다.

    그런 다음이 로컬 저장소를 서버에 이동한 인터넷을 사용 하지 않고 패키지 설치를 진행 합니다.

-   [수동으로 다운로드 하 여 개별적으로 패키지 복사](#bkmk_manual)

이 문서에서는 두 방법을 사용 하는 R 패키지 리포지토리를 만드는 방법을 설명 하 고 권장의 사용은 **miniCRAN** 패키지 합니다.

## <a name="prepare-packages-using-minicran"></a>MiniCRAN를 사용 하 여 패키지 준비

로컬 패키지 리포지토리를 만드는의 목표는 서버 관리자 또는 조직의 다른 사용자가 인터넷에 연결 되지 않은 서버에 새 R 패키지를 설치 하는 데 사용할 수 있는 단일 위치를 제공 하는 것입니다.

[miniCRAN](https://cran.r-project.org/web/packages/miniCRAN/index.html) 에 의해 작성 되었으므로 R에 대 한 패키지 [Andre de Vries](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html) 를 일관 된 만드는 쉽게 수행할 수 있도록 조직에 대 한 R 패키지 집합을 관리 합니다. 

사용 하 여 miniCRAN 리포지토리를 만들 장점은 다음과 같습니다.

-   **보안**: 많은 R 사용자는에서 다운로드 및 설치가 새 R 패키지 CRAN 또는 해당 미러 사이트의 사이트 중 하나에 익숙해져 있습니다. 그러나 보안상의 이유로 실행 하는 프로덕션 서버에 대 한 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 일반적으로 인터넷에 연결 되어 있지 않습니다.

-   **오프 라인 설치 쉽게**: 오프 라인 서버에 패키지를 설치 하려면 모든 패키지 종속 파일을 다운로드할 수도, 사용 하 여 miniCRAN 더 쉽게 종속성을 가져오려면 모든 올바른 형식이 필요 합니다.

-   **향상 된 버전 관리**: 다중 사용자 환경에는 제한 되지 않은 서버에 여러 패키지 버전 설치를 방지 하기 위해 경우가 있습니다.

저장소를 만든 후에 새 패키지를 추가 하거나 기존 패키지의 버전을 업그레이드 하 여 수정할 수 있습니다.

### <a name="step-1-install-the-minicran-package"></a>1단계. MiniCRAN 패키지 설치

원본으로 사용할 miniCRAN 리포지토리를 만들어서 시작 합니다. 인터넷에 연결 하는 컴퓨터에서이 리포지토리를 만들어야 합니다.

1.  MiniCRAN 패키지 및 필수 설치 **igraph** 패키지 합니다.

    ```R
    if(!require("miniCRAN")) install.packages("miniCRAN") if(!require("igraph"))
    install.packages("igraph") library(miniCRAN)
    ```

### <a name="step-2-define-a-package-source-a-cran-mirror-or-an-mran-snapshot"></a>2단계. 패키지 원본 정의: CRAN 미러 또는 MRAN 스냅숏

1. 패키지를 가져올 수 있는 사용 하도록 미러 사이트를 지정 합니다.

    ```R
    CRAN_mirror \<- c(CRAN = "https://mran.microsoft.com/snapshot/2017-08-01")
    ```

2.  수집 된 패키지를 저장할 로컬 폴더를 나타냅니다. 폴더 miniCRAN; 이름을 필요가 없으며 "GeneticsPackages" 또는 "ClientRPackages1.0.2"와 같은 보다 알기 쉬운 이름 수 있습니다.

    방금 폴더를 미리 만들 해야 합니다. 오류가 발생 하는 경우는 `local_repo` 나중에 R 코드를 실행할 때 폴더가 존재 하지 않습니다.

    ```R
    local_repo <- "~/miniCRAN"
    ```

    결과 해당 하는 환경 변수를 반환 하는 물결표 확장 연산자 `Sys.getenv("R_USER")`합니다.

### <a name="step-3-add-packages-to-the-repository"></a>3단계. 패키지 저장소에 추가

1.  MiniCRAN를 설치한 후 다운로드 하려는 추가 패키지를 지정 하는 목록을 만듭니다.

    이 초기 목록에 종속성을 추가 하지 마십시오 **igraph** miniCRAN에서 사용 하는 패키지를 종속성 목록을 생성 합니다. 이 그래프를 사용 하는 방법에 대 한 자세한 내용은 참조 [miniCRAN를 사용 하 여 패키지 종속성을 식별 하](https://cran.r-project.org/web/packages/miniCRAN/vignettes/miniCRAN-dependency-graph.html)합니다.

    다음 R 스크립트에는 대상 패키지, "zoo" 및 "예상"을 가져오는 방법을 보여 줍니다.

    ```R
    pkgs_needed <- c("zoo", "forecast")

2. Optionally, plot the dependency graph, which can be informative and looks cool.
    
    ```R
    plot(makeDepGraph(pkgs_needed))
    ```

3. 로컬 리포지토리를 만듭니다. 필요한 경우 R 버전을 변경 해야 합니다.

    ```R
    pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror)
    makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.3")
    ```

    이 정보를 miniCRAN 패키지에 패키지를 복사 해야 하는 폴더 구조를 만듭니다는 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 나중입니다.

4. 이 시점에서 패키지를 포함 하는 폴더 있어야 하 고 필요 했던 모든 추가 패키지 합니다.

    MiniCRAN 저장소에 포함 된 패키지를 나열 하려면 다음 코드를 실행할 수 있습니다.

    ```R
    pdb <- as.data.frame(pkgAvail(local_repo, type = "win.binary", Rversion = "3.3"), stringsAsFactors = FALSE)
    head(pdb)
    pdb$Package
    pdb[, c("Package", "Version", "License")]
    ```

### <a name="step-4-use-the-repository-to-add-r-packages-to-the-instance-library"></a>4단계. R 패키지 라이브러리에 추가 하는 인스턴스 저장소를 사용 하 여

저장소를 만들어 있습니다 필요한 패키지를 추가한 후에 서버 컴퓨터에 패키지 리포지토리를 이동 하 고 SQL Server에서 사용 하기 위해 올바른 라이브러리에 R 패키지가 설치 되어 있는지 확인 해야 합니다.

SQL Server의 버전에 따라 가지 SQL Server 인스턴스와 연결 된 R 라이브러리에 새 패키지를 추가 하기 위한 두 가지 옵션이 있습니다.

-   MiniCRAN 리포지토리 및 R 도구를 사용 하 여 인스턴스 라이브러리를 설치 합니다.

-   SQL 데이터베이스에 패키지를 업로드 하 고 외부 라이브러리 만들기 문을 사용 하는 데이터베이스 단위로에 패키지를 설치 합니다. 참조 [SQL Server에 추가 R 패키지 설치](install-additional-r-packages-on-sql-server.md)합니다.

다음 절차에는 R 도구를 사용 하 여 패키지를 설치 하는 방법을 설명 합니다.

1.  MiniCRAN 리포지토리 패키지를 설치할 서버를 전체를 포함 하는 폴더를 복사 합니다.

2.  인스턴스와 연결 된 R 도구를 사용 하 여 R 명령 프롬프트를 엽니다.

    - SQL Server 2017 년에 대 한 기본 폴더는 `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library`합니다.

    - SQL Server 2016의 경우 기본 폴더는 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library`입니다.

    - 명명 된 인스턴스의 경우 기본 경로 것과 같이 설정 해야: `<instance_path>.RTEST/R_SERVICES/library`합니다.

    -  다른 드라이브에 SQL Server를 설치했거나 설치 경로에서 다른 변경을 수행한 경우 해당 변경도 수행해야 합니다.

3.  인스턴스 라이브러리 (경우에는 사용자 디렉터리에 있는)에 대 한 경로 가져오고 라이브러리 경로 목록에 추가 합니다.

    ```R
    .libPaths()[1]  
    lib \<- .libPaths()[1]
    ```

    "C: / Program 파일/Microsoft SQL Server/MSSQL14 인스턴스 경로 반환 해야. MSSQLSERVER/R_SERVICES/라이브러리 "

2.  mininCRAN 리포지토리를 복사한 위치 서버의 위치를 지정 `server_repo`합니다.

    이 예제에서는 저장소 서버에 사용자 폴더에 복사 하는 가정 합니다.

    ```R
    R server_repo <- "C:\\Users\\MyUserName\\miniCRAN"
    ```

3.  서버에 새 R 작업 영역에서 작업 하는 이후를 설치 하는 패키지 목록을도 제공 해야 합니다.

    ```R
    tspackages <- c("zoo", "forecast")
    ```

4.  MiniCRAN 리포지토리의 로컬 복사본에 대 한 경로 사용 하 여 패키지를 설치 합니다.

    ```R
    install.packages(tspackages, repos = file.path("file://", normalizePath(server_repo, winslash = "/")), lib = lib, type = "win.binary", dependencies = TRUE)
    ```

5.  이제 설치 된 패키지를 볼 수 있습니다.

    ```R
    installed.packages()
    ```

> [!NOTE] 
> 
> SQL Server 2017 년 1에서 추가 데이터베이스 역할 및 T-SQL 문을 패키지를 통해 사용 권한을 관리 하는 서버 관리자가 제공 됩니다. 데이터베이스 관리자가 필요한 경우 R 또는 T-SQL을 사용 하 여 패키지를 설치 하는 작업을 소유할 수 있습니다. 그러나 DBA 사용할 수도 역할 자체 패키지를 설치 하는 기능을 사용자에 게 부여 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)합니다.
> 
> SQL Server 2016에서 서버 관리자는 인스턴스에서 사용 하는 기본 라이브러리로 miniCRAN 리포지토리에서 패키지를 설치 해야 합니다. 에 설명 된 대로이 위해 R 도구를 사용는 [섹션 앞에 오는](#bkmk_Rtools)합니다.

## <a name="manually-download-single-packages"></a>단일 패키지를 수동으로 다운로드

MiniCRAN 사용 하지 않을 경우 필요한, 패키지 및 해당 종속성을 수동으로 다운로드할 수 있습니다. 이 작업을 수행 하는 관리자 또는 서버의 유일한 소유자 필요 합니다.

패키지를 다운로드 한 후 압축 된 파일 위치에서 R 패키지를 설치 합니다.

1.  패키지 zip 파일을 다운로드 한 로컬 폴더에 저장

2.  해당 폴더에 복사는 [!INCLUDE [ssNoVersion_md](..\..\includes\ssnoversion-md.md)] 컴퓨터입니다.

3.  SQL Server 인스턴스 라이브러리에 패키지를 설치 합니다.

> [!NOTE]
> R 도구를 사용 하 여 패키지를 설치 하는 인스턴스에 대해 전체적으로 설치 됩니다. 
> 
> 데이터베이스에 패키지를 설치 하 고 데이터베이스 역할을 사용 하 여 사용자와 패키지를 공유 하려는 경우 외부 라이브러리 만들기 문을 사용 하 여 라이브러리를 업로드 해야 합니다. 참조 [SQL Server의 추가 R 패키지를 설치 합니다.](install-additional-r-packages-on-sql-server.md)

