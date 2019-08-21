---
title: Sqlmlutils를 사용 하 여 새 R 패키지 설치
description: Sqlmlutils를 사용 하 여 SQL Server Machine Learning Services 또는 SQL Server R Services 인스턴스에 새 R 패키지를 설치 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a0be3f1f9039f30043eb5275c49c5b4db4ccfbca
ms.sourcegitcommit: 632ff55084339f054d5934a81c63c77a93ede4ce
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2019
ms.locfileid: "69641190"
---
# <a name="install-new-r-packages-with-sqlmlutils"></a>Sqlmlutils를 사용 하 여 새 R 패키지 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 문서에서는 [**sqlmlutils**](https://github.com/Microsoft/sqlmlutils) 패키지의 함수를 사용 하 여 SQL Server Machine Learning Services 또는 SQL Server R Services 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다. 설치 하는 패키지는 T-sql [sp-s q s](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) -transact-sql 문을 사용 하 여 데이터베이스 내에서 실행 되는 R 스크립트에서 사용할 수 있습니다.

> [!NOTE]
> SQL Server에서 r `install.packages` 패키지를 추가 하는 데는 표준 r 명령이 권장 되지 않습니다. 대신이 문서에 설명 된 대로 **sqlmlutils** 를 사용 합니다.

## <a name="prerequisites"></a>사전 요구 사항

- SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에 [R](https://www.r-project.org) 및 [rstudio Desktop](https://www.rstudio.com/products/rstudio/download/) 을 설치 합니다. 스크립트를 실행 하기 위해 R IDE를 사용할 수 있지만이 문서에서는 RStudio를 가정 합니다.

- SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에 SSMS ( [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) 또는 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms) (SSMS)를 설치 합니다. 다른 데이터베이스 관리 또는 쿼리 도구를 사용할 수 있지만이 문서에서는 Azure Data Studio 또는 SSMS를 가정 합니다.

### <a name="other-considerations"></a>기타 고려 사항

- SQL Server에서 실행 되는 R 스크립트는 기본 인스턴스 라이브러리에 설치 된 패키지만 사용할 수 있습니다. 라이브러리는 동일한 컴퓨터에 있는 경우에도 외부 라이브러리에서 패키지를 로드할 수 SQL Server. 여기에는 다른 Microsoft 제품과 함께 설치 된 R 라이브러리가 포함 됩니다.

- 강화 된 SQL Server 환경에서는 다음을 방지 해야 할 수 있습니다.
  - 네트워크 액세스가 필요한 패키지
  - 관리자 권한으로 파일 시스템에 액세스 해야 하는 패키지
  - 웹 개발에 사용 되는 패키지 또는 SQL Server 내에서 실행 하 여 이점을 제공 하지 않는 기타 작업

## <a name="install-sqlmlutils-on-the-client-computer"></a>클라이언트 컴퓨터에 sqlmlutils 설치

**Sqlmlutils**를 사용 하려면 먼저 SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에 설치 해야 합니다.

**Sqlmlutils** 패키지는 **rodbcext** 패키지에 종속 되며 **rodbcext** 는 여러 다른 패키지에 종속 됩니다. 다음 절차에서는 이러한 패키지를 모두 올바른 순서로 설치 합니다.

### <a name="install-sqlmlutils-online"></a>온라인으로 sqlmlutils 설치

클라이언트 컴퓨터에서 인터넷에 액세스할 수 있는 경우 **sqlmlutils** 및 해당 종속 패키지를 온라인으로 다운로드 하 여 설치할 수 있습니다.

1. 에서 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 클라이언트 컴퓨터로 최신 **sqlmlutils** zip 파일을 다운로드 합니다. 파일의 압축을 풀어야 합니다.

1. **명령 프롬프트** 를 열고 다음 명령을 실행 하 여 **Sqlmlutils** 및 **rodbcext**패키지를 설치 합니다. 전체 경로를 다운로드 한 **sqlmlutils** zip 파일로 대체 합니다 .이 예제에서는 파일이 문서 폴더에 있다고 가정 합니다. 온라인 및 설치 된 **Rodbcext** 패키지를 찾을 수 있습니다.

   ```console
   R -e "install.packages('RODBCext', repos='https://cran.microsoft.com')"
   R CMD INSTALL %UserProfile%\Documents\sqlmlutils_0.7.1.zip
   ```

### <a name="install-sqlmlutils-offline"></a>Sqlmlutils 오프 라인 설치

클라이언트 컴퓨터가 인터넷에 연결 되어 있지 않은 경우 인터넷에 액세스할 수 있는 컴퓨터를 사용 하 여 **sqlmlutils** 및 **Rodbcext** 패키지를 미리 다운로드 해야 합니다. 그런 다음 클라이언트 컴퓨터의 폴더에 파일을 복사 하 고 오프 라인으로 패키지를 설치할 수 있습니다.

**Rodbcext** 패키지에는 많은 종속 패키지가 있으며 패키지에 대 한 모든 종속성을 식별 하는 것은 복잡 합니다. [**MiniCRAN**](https://andrie.github.io/miniCRAN/) 를 사용 하 여 모든 종속 패키지를 포함 하는 패키지에 대 한 로컬 리포지토리 폴더를 만드는 것이 좋습니다.
자세한 내용은 [miniCRAN를 사용 하 여 로컬 R 패키지 리포지토리 만들기](../r/create-a-local-package-repository-using-minicran.md)를 참조 하세요.

**Sqlmlutils** 패키지는 클라이언트 컴퓨터에 복사 하 여 설치할 수 있는 단일 zip 파일로 구성 되어 있습니다.

인터넷에 액세스할 때 사용 되는 컴퓨터:

1. **MiniCRAN**를 설치 합니다. 자세한 내용은 [Install miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) 를 참조 하세요.

1. RStudio에서 다음 R 스크립트를 실행 하 여 **Rodbcext**패키지의 로컬 리포지토리를 만듭니다. 이 예제에서는 폴더 `c:\downloads\rodbcext`에 리포지토리를 만듭니다.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
   local_repo <- "c:/downloads/rodbcext"
   pkgs_needed <- "RODBCext"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end

   `Rversion` 값에 대해 SQL Server에 설치 된 R 버전을 사용 합니다. 설치 된 버전을 확인 하려면 다음 T-sql 명령을 사용 합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 에서 https://github.com/Microsoft/sqlmlutils/tree/master/R/dist 최신 **sqlmlutils** zip 파일을 다운로드 합니다 (파일의 압축을 풀어야 함). 예를 들어 파일을로 `c:\downloads\sqlmlutils_0.7.1.zip`다운로드 합니다.

1. 전체 **rodbcext** 리포지토리 폴더 (`c:\downloads\rodbcext`) 및 **sqlmlutils** zip 파일 (`c:\downloads\sqlmlutils_0.7.1.zip`)을 클라이언트 컴퓨터에 복사 합니다. 예를 들어 클라이언트 컴퓨터의 폴더 `c:\temp\packages` 에 복사 합니다.

SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에서 명령 프롬프트를 열고 다음 명령을 실행 하 여 **Rodbcext** 를 설치한 다음 **sqlmlutils**를 설치 합니다.

```console
R -e "install.packages('RODBCext', repos='c:\temp\packages\rodbcext')"
R CMD INSTALL c:\temp\packages\sqlmlutils_0.7.1.zip
```

## <a name="add-an-r-package-on-sql-server"></a>SQL Server에서 R 패키지 추가

다음 예제에서는 SQL Server에 [**glue**](https://cran.r-project.org/web/packages/glue/) 패키지를 추가 합니다.

### <a name="add-the-package-online"></a>온라인으로 패키지 추가

SQL Server에 연결 하는 데 사용 하는 클라이언트 컴퓨터에서 인터넷에 액세스할 수 있는 경우 **sqlmlutils** 를 사용 하 여 인터넷을 통해 **glue** 패키지와 종속성을 찾은 다음 원격으로 SQL Server 인스턴스에 패키지를 설치할 수 있습니다.

1. 클라이언트 컴퓨터에서 RStudio를 열고 새 **R 스크립트** 파일을 만듭니다.

1. 다음 R 스크립트를 사용 하 여 **sqlmlutils**를 사용 하 여 **glue** 패키지를 설치 합니다. 사용자 고유의 SQL Server 데이터베이스 연결 정보를 대체 합니다.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC")
   ```

   > [!TIP]
   > **범위** 는 **공용** 또는 **개인**중 하나일 수 있습니다. 공용 범위는 데이터베이스 관리자가 모든 사용자가 사용할 수 있는 패키지를 설치 하는 데 유용 합니다. 전용 범위는 패키지를 설치 하는 사용자만 패키지를 사용할 수 있도록 합니다. 범위를 지정 하지 않는 경우 기본 범위는 **PRIVATE**입니다.

### <a name="add-the-package-offline"></a>오프 라인으로 패키지 추가

클라이언트 컴퓨터가 인터넷에 연결 되어 있지 않은 경우 **miniCRAN** 를 사용 하 여 인터넷에 액세스할 수 있는 컴퓨터를 사용 하 여 **glue** 패키지를 다운로드할 수 있습니다. 그런 다음 패키지를 오프 라인으로 설치할 수 있는 클라이언트 컴퓨터에 복사 합니다.
**MiniCRAN**설치에 대 한 자세한 내용은 [Install miniCRAN](../r/create-a-local-package-repository-using-minicran.md#install-minicran) 를 참조 하세요.

인터넷에 액세스할 때 사용 되는 컴퓨터:

1. 다음 R 스크립트를 실행 하 여 **glue**의 로컬 리포지토리를 만듭니다. 이 예에서는에서 `c:\downloads\glue`리포지토리 폴더를 만듭니다.

   ::: moniker range=">=sql-server-2016||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "win.binary", Rversion = "3.5");
   ```

   ::: moniker-end

   ::: moniker range=">=sql-server-linux-ver15||=sqlallproducts-allversions"

   ```R
   CRAN_mirror <- c(CRAN = "https://cran.cnr.berkeley.edu")
   local_repo <- "c:/downloads/glue"
   pkgs_needed <- "glue"
   pkgs_expanded <- pkgDep(pkgs_needed, repos = CRAN_mirror);

   makeRepo(pkgs_expanded, path = local_repo, repos = CRAN_mirror, type = "source", Rversion = "3.5");
   ```

   ::: moniker-end


   `Rversion` 값에 대해 SQL Server에 설치 된 R 버전을 사용 합니다. 설치 된 버전을 확인 하려면 다음 T-sql 명령을 사용 합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'print(R.version)'
   ```

1. 전체 **glue** repository 폴더 (`c:\downloads\glue`)를 클라이언트 컴퓨터에 복사 합니다. 예를 들어 폴더 `c:\temp\packages\glue`에 복사 합니다.

클라이언트 컴퓨터에서 다음을 수행합니다.

1. RStudio를 열고 새 **R 스크립트** 파일을 만듭니다.

1. 다음 R 스크립트를 사용 하 여 **sqlmlutils**를 사용 하 여 **glue** 패키지를 설치 합니다. 사용자 고유의 SQL Server 데이터베이스 연결 정보를 대체 합니다.

   ```R
   library(sqlmlutils)
   connection <- connectionInfo(
     server= "yourserver",
     database = "yourdatabase",
     uid = "yoursqluser",
     pwd = "yoursqlpassword")
   localRepo = "c:/temp/packages/glue"

   sql_install.packages(connectionString = connection, pkgs = "glue", verbose = TRUE, scope = "PUBLIC", repos=paste0("file:///",localRepo))
   ```

   > [!TIP]
   > **범위** 는 **공용** 또는 **개인**중 하나일 수 있습니다. 공용 범위는 데이터베이스 관리자가 모든 사용자가 사용할 수 있는 패키지를 설치 하는 데 유용 합니다. 전용 범위는 패키지를 설치 하는 사용자만 패키지를 사용할 수 있도록 합니다. 범위를 지정 하지 않는 경우 기본 범위는 **PRIVATE**입니다.

## <a name="use-the-package"></a>패키지 사용

**Glue** 패키지가 설치 되 면 t-sql **sp_execute_external_script** 명령을 사용 하 여 SQL Server의 R 스크립트에서 사용할 수 있습니다.

1. Azure Data Studio 또는 SSMS를 열고 SQL Server 데이터베이스에 연결 합니다.

1. 다음 명령을 실행합니다.

   ```sql
   EXECUTE sp_execute_external_script @language = N'R'
       , @script = N'
   library(glue)

   name <- "Fred"
   birthday <- as.Date("2020-06-14")
   text <- glue(''My name is {name} '',
   ''and my birthday is {format(birthday, "%A, %B %d, %Y")}.'')

   print(text)
         ';
   ```

    **결과**

    ```text
    My name is Fred and my birthday is Sunday, June 14, 2020.
    ```

## <a name="remove-the-package"></a>패키지 제거

**Glue** 패키지를 제거 하려면 다음 R 스크립트를 실행 합니다. 앞에서 정의한 것과 동일한 **연결** 변수를 사용 합니다.

```R
sql_remove.packages(connectionString = connection, pkgs = "glue", scope = "PUBLIC")
```

## <a name="next-steps"></a>다음 단계

- 설치 된 R 패키지에 대 한 자세한 내용은 [r 패키지 정보 가져오기](r-package-information.md) 를 참조 하세요.
- R 패키지 사용에 [대 한 도움말은 r 패키지 사용을 위한 팁](../r/packages-installed-in-user-libraries.md) 을 참조 하세요.
- Python 패키지 설치에 대 한 자세한 내용은 [pip를 사용 하 여 python 패키지 설치](install-additional-python-packages-on-sql-server.md) 를 참조 하세요.
- Machine Learning Services SQL Server에 대 한 자세한 내용은 [SQL Server Machine Learning Services (Python 및 R)](../what-is-sql-server-machine-learning.md) 를 참조 하세요.
