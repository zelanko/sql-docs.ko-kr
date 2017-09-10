---
title: "miniCRAN을 사용하여 로컬 패키지 리포지토리 만들기 | Microsoft 문서"
ms.custom: 
ms.date: 03/30/2017
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
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e8af93b3e132290eef4b43da568b9381ff8e5a04
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-a-local-package-repository-using-minicran"></a>miniCRAN을 사용하여 로컬 패키지 리포지토리 만들기
이 항목에서는 R 패키지 **miniCRAN**을 사용하여 로컬 R 패키지 리포지토리를 만들 수 있는 방법을 설명합니다. 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스는 일반적으로 인터넷에 연결되지 않은 서버에 있으므로 R 패키지를 설치하는 표준 메서드(R 명령 `install.packages()`)는 패키지 설치 관리자가 CRAN 또는 다른 미러 사이트에 액세스할 수 없어 작동하지 않을 수 있습니다.

로컬 공유 또는 리포지토리에서 패키지를 설치하기 위한 두 가지 옵션은 다음과 같습니다.

+ miniCRAN 패키지를 사용하여 필요한 패키지의 로컬 리포지토리를 만든 다음 이 리포지토리에서 설치합니다. 이 항목에서는 miniCRAN 메서드에 대해 설명합니다.

+ 필요한 패키지 및 해당 종속성을 zip 파일로 다운로드하고 로컬 폴더에 저장한 다음 해당 폴더를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에 복사합니다. 수동 복사 방법에 대한 자세한 내용은 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)를 참조하세요.


## <a name="step-1-install-minicran-and-download-packages"></a>1단계. MiniCRAN 설치 및 패키지 다운로드 


1. 인터넷에 연결된 컴퓨터에 miniCRAN 패키지를 설치합니다.

   ~~~~
   # Install miniCRAN and igraph

   if(!require("miniCRAN")) install.packages("miniCRAN")
   if(!require("igraph")) install.packages("igraph")
   library(miniCRAN)

   # Define the package source: a CRAN mirror, or an MRAN snapshot
   CRAN_mirror <- c(CRAN = "https://mran.microsoft.com/snapshot/2016-04-01")

   # Define the local download location
   local_repo <- "~/miniCRAN"
   ~~~~

2. 다음 R 스크립트를 사용하여 필요한 패키지를 이 컴퓨터에 다운로드하거나 설치합니다. 이렇게 하면 나중에 패키지를 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 복사하는 데 필요한 폴더 구조가 생성됩니다.

   ~~~~
   # List the packages to get. Do not specify dependencies.
   pkgs_needed <- c("ggplot2", "ggdendro")
   # Plot the dependency graph 
   plot(makeDepGraph(pkgs_needed)) 
   
   # Create the local repo 
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror) 
   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.2") 

   # List local packages 
   pdb <- as.data.frame( 
     pkgAvail(local_repo, type = "win.binary", Rversion = "3.2"),  
     stringsAsFactors = FALSE) 
   head(pdb) 
   pdb$Package 
   pdb[, c("Package", "Version", "License")] 
   ~~~~


## <a name="step-2-copy-the-minicran-repository-to-the-sql-server-computer"></a>2단계. SQL Server 컴퓨터에 MiniCRAN 리포지토리 복사 

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 인스턴스의 R_SERVICES 라이브러리에 miniCRAN 리포지토리를 복사합니다.

+ SQL Server 2016의 경우 기본 폴더는 `C:/Program Files/Microsoft SQL Server/MSSQL13.MSSQLSERVER/R_SERVICES/library1`입니다.
+ SQL Server 2017 년에 대 한 기본 폴더는 `C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library1`합니다.

명명된 인스턴스를 사용하여 R Services를 설치한 경우 경로에 인스턴스 이름을 포함하여 라이브러리가 올바른 인스턴스에 설치되었는지 확인해야 합니다. 예를 들어 명명된 인스턴스가 RTEST02인 경우 명명된 인스턴스의 기본 경로는 `C:\Program Files\Microsoft SQL Server\MSSQL13.RTEST02\R_SERVICES\library`입니다.

다른 드라이브에 SQL Server를 설치했거나 설치 경로에서 다른 변경을 수행한 경우 해당 변경도 수행해야 합니다.

## <a name="step-3-install-the-packages-on-sql-server-using-the-minicran-repository"></a>3단계. MiniCRAN 리포지토리를 사용하여 SQL Server에 패키지 설치

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 컴퓨터에서 R 명령줄 또는 RGUI를 관리자 권한으로 엽니다. 
  
> [!TIP]
> 컴퓨터에 R 라이브러리가 여러 개 있을 수도 있습니다. 따라서 패키지가 올바른 인스턴스에 설치되었는지 확인하려면 패키지를 설치할 특정 인스턴스와 함께 설치된 RGUI 또는 RTerm 복사본을 사용합니다.
  
리포지토리를 지정하라는 메시지가 나타나면 방금 복사한 파일이 들어 있는 폴더, 즉 로컬 miniCRAN 리포지토리를 선택합니다.

   ~~~~
   # Run this R code as administrator on the SQL Server computer 
   pkgs_needed <- c("ggplot2", "ggdendro") 
   local_repo  <- "~/miniCRAN" 

   # OPTIONAL: If you are not running R from the instance library as recommended, you must specify the path
   #   .libPaths()[1] 
   # "C:/Program Files/Microsoft SQL Server/MSSQL14.MSSQLSERVER/R_SERVICES/library " 
   # lib <- .libPaths()[1]
   
   install.packages(pkgs_needed,  
                    repos = file.path("file://", normalizePath(local_repo, winslash = "/")), 
                    lib = lib, 
                    type = "win.binary", 
                    dependencies = TRUE 
                    ) 
   installed.packages() 
   ~~~~

패키지가 설치되었는지 확인합니다.
   ~~~~
   installed.packages()
   ~~~~



## <a name="acknowledgements"></a>승인

이 정보는 miniCRAN 패키지도 개발한 Andre de Vries가 작성한 이 문서입니다. 자세한 내용과 전체 연습은 [오프라인 SQL Server 2016 인스턴스에 R 패키지를 설치하는 방법](http://blog.revolutionanalytics.com/2016/05/minicran-sql-server.html)을 참조하세요.

