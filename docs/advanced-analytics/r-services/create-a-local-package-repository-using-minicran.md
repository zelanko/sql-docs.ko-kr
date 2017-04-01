---
title: "사용 하 여 로컬 패키지 저장소 miniCRAN 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "05/27/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27f2a1ce-316f-4347-b206-8a1b9eebe90b
caps.latest.revision: 4
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 4
---
# 사용 하 여 로컬 패키지 저장소 miniCRAN 만들기
이 항목에서는 R 패키지를 사용 하 여 로컬 R 패키지 리포지토리를 만드는 방법을 설명 **miniCRAN**합니다. 

때문에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스 일반적으로 인터넷에 연결 하면 표준 메서드로 R 패키지를 설치 하지 않은 서버에 있는 (R 명령 `install.packages()`) 작동 하지 않을 수, 패키지 설치 관리자는 CRAN 또는 다른 미러 사이트에 액세스할 수 없습니다.

가지 로컬 공유 또는 리포지토리 로부터 패키지를 설치 하기 위한 두 가지 옵션이 있습니다.

+ MiniCRAN 패키지를 사용 하 여 필요한 다음이 저장소에서 설치 패키지의 로컬 리포지토리를 만듭니다. 이 항목에서는 miniCRAN 메서드를 설명 합니다.

+ 필요한 패키지 및 해당 종속성을 zip 파일로 다운로드 하 고 로컬 폴더에 저장 한 후 다음에 해당 폴더를 복사는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터입니다. 수동 복사 방법에 대 한 자세한 내용은 참조 하십시오. [SQL Server에 추가 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)합니다.


## 1단계. MiniCRAN를 설치 하 고 패키지를 다운로드 합니다. 


1. 인터넷에 연결 하는 컴퓨터에서 miniCRAN 패키지를 설치 합니다.

   ~~~~
   # Install miniCRAN ---------------------------------------------------

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. 다운로드 하거나이 컴퓨터에 필요한 패키지를 설치 합니다. 패키지를 복사 해야 하는 폴더 구조를 만들 것이 고 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 나중입니다.

   ~~~~
   # List the packages you need 
   # Do not specify dependencies
   pkgs_needed <- c("ggplot2", "ggdendro")
   ~~~~

3. 기록 중 복사 miniCRAN 저장소 R_SERVICES 라이브러리에는 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스.

## 2단계. SQL Server 컴퓨터에 패키지를 설치 합니다. 

4. 에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] R 명령을 실행 하는 컴퓨터  `install.packages()`합니다. 과 함께 설치 된 R 도구 중 하나를 사용 하면 [!INCLUDE[rsql_productname_md](../../includes/rsql-productname-md.md)], 와 같은 Rgui.exe, 또는 있습니다의 일환으로 명령을 실행할 수는 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 저장 프로시저입니다.
5. 저장소를 지정 하려면 프롬프트에서; 복사 된 파일을 포함 하는 폴더 선택 즉, 로컬 miniCRAN 저장소입니다.

   ~~~~
   pkgs_needed <- c("ggplot2", "ggdendro")
   local_repo  <- "~/miniCRAN"
   
   .libPaths()[1]
   "C:/Program Files/Microsoft SQL Server/130/R_SERVER/library"

   lib <- .libPaths()[1]

   install.packages(pkgs_needed, 
                 repos = file.path("file://", normalizePath(local_repo, winslash = "/")),
                 lib = lib,
                 type = "win.binary",
                 dependencies = TRUE
                 )
   ~~~~

6. 이 R 코드를 실행 하 여 패키지 설치 되었는지 확인 합니다.
   ~~~~
   installed.packages()
   ~~~~



## 승인

이 정보에 대 한 기사에서 Andre de Vries 또한 miniCRAN 패키지를 개발 하 여이 문서입니다. 세부 정보 및 완벽 한 연습에 대 한 참조  [오프 라인으로 SQL Server 2016 인스턴스에서 패키지를 R을 설치 하는 방법](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)