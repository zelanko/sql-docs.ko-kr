---
title: "SQL Server에 추가 R 패키지를 설치 합니다. | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 10/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 29122bdf543e82c1f429cf401b5fe1d8383515fc
ms.openlocfilehash: a7afdf4230bd27505afff271a6b4782214eedfb3
ms.contentlocale: ko-kr
ms.lasthandoff: 10/10/2017

---
# <a name="install-additional-r-packages-on-sql-server"></a>SQL Server에 추가 R 패키지를 설치 합니다.

이 문서에서는 기계 학습 사용 하도록 설정 하는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다.

> [!IMPORTANT]
> 새 패키지를 추가 하기 위한 프로세스를 실행 하는 SQL Server 및 사용 하는 도구의 버전에 따라 달라 집니다. 

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="overview-of-package-installation-process"></a>패키지 설치 프로세스의 개요

1.  패키지의 Windows 버전 인지 확인: [올바른 패키지 버전 및 형식 가져오기](#packageVersion)

2.  서버에 인터넷에 액세스 하는 경우 이진을 사전에 다운로드: [zip 파일 다운로드](#bkmk_zipPreparation)

    패키지 종속성을 확인 하 고 설치 하는 동안 필요할 수 있는 모든 관련된 패키지를 가져올 해야 합니다. 패키지 및 해당 종속성의 컬렉션을 준비 하려면는 [miniCRAN 패키지](#bkmk_packageDependencies)합니다.

3.  서버에 인터넷 액세스를 있는지 여부와 SQL Server 버전에서 패키지 설치 방법에 따라 다릅니다. 권장 되는 프로세스는 다음과 같습니다.

    **SQL Server 2016에 대 한 패키지 설치**
    
    1. 데이터 과학자는 프로젝트 또는 팀에 필요한 패키지를 제공 합니다. 사용 하 여 [miniCRAN](create-a-local-package-repository-using-minicran.md) 종속성과 함께 패키지의 컬렉션을 준비 합니다.

    2. 데이터베이스 관리자는 R 도구를 사용 하 여 인스턴스 라이브러리에는 패키지를 설치 합니다.

    **SQL Server 2017에 대 한 패키지 설치**

    1. 데이터베이스 관리자는 인스턴스에서 패키지 관리를 사용 하도록 설정 하 고 새 패키지 관리 역할에 사용자를 추가 합니다.

    2. 데이터 과학자는 프로젝트 또는 팀에 필요한 패키지를 제공 합니다. 사용 하 여 [miniCRAN](create-a-local-package-repository-using-minicran.md) 종속성과 함께 패키지의 컬렉션을 준비 합니다.

    3. 패키지는 외부 라이브러리 만들기 문을 사용 하 여 SQL Server 인스턴스에 업로드 됩니다.
    
    4. 적절 한 권한이 있는 모든 사용자는 R 스크립트 실행 되는에서 R 코드를 호출 하 여 데이터베이스에 패키지를 설치할 수 인스턴스에 패키지를 추가한 후 `sp_execute_external_script`합니다.
    
    5. 또한 적절 한 권한이 있는 사용자가 설치 하거나 새 RevoScaleR 함수를 사용 하 여 패키지 관리에 대 한 원격 R 클라이언트에서 패키지를 찾을 수 있습니다.

## <a name="install-new-packages"></a>새 패키지 설치

이 섹션에서는 다음 키 패키지 설치 시나리오에 대해 자세히 설명 합니다. 사용할 수 있는 가장 좋은 방법은 이러한 factores에 따라 다릅니다.

- 사용 하는 SQL Server 버전

- 인스턴스의 유일한 소유자 및 여부 데이터베이스 역할을 사용 하 여 여러 사용자에 대 한 mamaneg 패키지 하려고 합니다.

- 종속성이 있는 여러 패키지 또는 한 패키지를 설치는 하는지 여부

**SQL Server 패키지 관리를 사용 하 여**

인스턴스에 패키지 관리 기능을 지 원하는 경우 T-SQL 또는 기존 R 도구를 사용할 수 있습니다.

-  패키지 관리 및 패키지 역할 기반 액세스를 SQL Server에 업로드 R 패키지를 사용할 수 있습니다. 사용자는 다음 T-SQL을 사용 하 여 패키지를 설치 합니다.

    [외부 라이브러리 만들기를 사용 하 여 패키지를 설치 합니다.](#bkmk_sqlInstall)

- 원격 R 클라이언트를 사용 하 여 서버에 새 패키지를 추가 합니다. SQL Server 2017 필요합니다. 패키지 관리 서버에서 사용 해야 합니다. 

    [R을 사용 하 여 패키지 관리를 사용 하는 경우 서버에서 패키지를 설치 하려면](#bkmk_rAddPackage)

- 여러 패키지의 종속성과 함께 포함 된 외부 라이브러리를 만들기와 함께 사용할 패키지 라이브러리를 준비 합니다.

    [MiniCRAN 리포지토리에서 여러 패키지 설치](#bkmk_minicran)

**기본 R rools 사용**

이전 버전의 SQL Server R services 사용 하는 경우 기존 R 도구를 사용 하 여 패키지를 설치 하려면 다음이 지침을 따릅니다. 필요에 따라 miniCRAN을 사용 하 여 설치에 대 한 패키지의 컬렉션을 준비 합니다.

-  R 도구를 사용 하 여 기본 인스턴스 라이브러리에는 R 패키지를 설치 합니다. 관리 액세스가 필요합니다.

    [패키지를 설치 하는 R 도구를 사용 하 여 인스턴스 라이브러리](#bkmk_rInstall)

- 여러 패키지 및 해당 종속성을 간편한 설치를 지원 하기 위해 패키지의 공유 컬렉션을 만듭니다.

    [MiniCRAN를 사용 하 여 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)

### <a name="bkmk_sqlInstall"></a>SQL Server 도구를 사용 하 여 패키지를 설치 합니다.

1. 외부 라이브러리 관리 기능에 SQL Server 2017 인스턴스에서 설정한 있는지 확인 합니다.

    [사용 하도록 설정 하거나 패키지 관리를 사용 하지 않도록 설정 하는 방법](r-package-how-to-enable-or-disable.md)

2. 이 항목에 설명 된 지원 되는 데이터베이스 역할 중 하나를 사용 하 여 새 패키지를 설치할 수 있는 권한이 있는 계정을 사용 하 여 서버에 연결: [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)

3.  같은 서버 컴퓨터에 있는 폴더를 설치 하려면 R 패키지가 포함 된 압축된 파일을 복사 하면 **사용자** 또는 **문서** 폴더입니다. 클라이언트 컴퓨터의 폴더 또는 네트워크 드라이브에서 패키지를 추가할 수 없습니다. 패키지 저장소를 만드는 miniCRAN를 사용한 경우 복사할 패키지 리포지토리 전체에서 서버의 모든 로컬 폴더: 즉, 네트워크 드라이브에 없습니다.

    서버에 있는 모든 폴더에 액세스할 없으면 이진 형식으로 패키지 콘텐츠를 전달할 수 있습니다. 참조 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 예에 대 한 합니다.

4.  패키지를 사용 하려면 데이터베이스에서 실행 된 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 문.

    이 예에서는 사용자 계정에 서버에 새 패키지를 업로드 하 고 데이터베이스에 공유 범위에 설치할 수 있는 권한이 있습니다.

    릴리스 버전을 추가 하는 다음 문에서 [zoo](https://cran.r-project.org/web/packages/zoo/index.html) 패키지 로컬 파일 공유에서 현재 데이터베이스 컨텍스트를 합니다.

    ```SQL
    CREATE EXTERNAL LIBRARY zoo
    FROM (CONTENT = 'C:\Temp\RPackages\zoo_1.8-0.zip')
    WITH (LANGUAGE = 'R');
    ```

    데이터베이스 소유자 (dbo 역할의 멤버)가 있는 계정을 사용 하 여 연결 하는 경우 패키지에서 사용할 수 **공유** 범위: 즉, 구성원 인 모든 사용자가 설치할 수의 `rpkgs-users` 역할입니다.

    에 액세스할 수 있는 계정을 사용 하 여 패키지를 업로드 하는 경우 **개인** 범위만 패키지를 설치할 수 있습니다.

4.  인스턴스에서 사용 하는 기본 R 라이브러리에 패키지를 설치 하는 R을 실행할 `library()` 저장된 프로시저 sp_execute_external_script 내에서 명령을 합니다.

    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # load the binaries in zoo
    library(zoo)'
    ```

    성공 하면는 **메시지** "'zoo' 패키지가 성공적으로 압축을 풀 및 MD5 합계 검사"와 같은 창 메시지를 보고 해야 합니다. 필수 패키지가 이미 설치 되어 설치 프로세스에서 연결 하 고 필요한 패키지를 로드 합니다.

    > [!NOTE]
    > 필수 패키지를 사용할 수 없는 경우 오류가 반환 됩니다. "라는 없는 패키지는 \<required_package\>" 합니다. 
    > 
    > 먼저 패키지 종속성을 확인 하거나 miniCRAN를 사용 하 여 실행 하기 전에 단일 압축 된 파일에 필요한 모든 패키지를 수집할 좋습니다 오류를 방지 하려면 `CREATE EXTERNAL LIBRARY`합니다.

### <a name="bkmk_rAddPackage"></a>R을 사용 하 여 패키지 관리를 사용 하는 경우 서버에서 패키지를 설치 하려면

패키지 관리 인스턴스에서 이미 사용 하는 경우 원격 클라이언트로부터 R, RevoScaleR 함수를 사용 하 여 패키지 관리에 대 한 새 R 패키지를 설치할 수 있습니다.

1. 시작 하기 전에 이러한 조건이 충족 되어 있는지 확인 합니다.

    + R 클라이언트가 RevoScale의 최신 버전을 있습니다. 시험판 버전에는 일부 패키지 관리 기능이 포함 되지 않았습니다.
    + 패키지 관리 및 데이터베이스 인스턴스에 대해 사용 하도록 설정 합니다.
    + 데이터베이스 관리 역할 중 하나에 권한이 있습니다.

2. 문자열 변수에서 설치 하려는 패키지를 나열 합니다.

    ```R
    packageList <- c("e1071")

3. Define a connection string to the instance and database where package management is enabled, and use the connection string to create a SQL Server compute context.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```

4. 호출 `rxInstallPackages` 계산 컨텍스트 및 패키지 이름이 포함 된 문자열 변수를 전달 합니다.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    종속 패키지 필요한 경우 또한 다운로드 됩니다.
    
    이 예제에서는 패키지 소유자 및 범위를 지정 하지 않아 연결을 수행 하는 사용자의 자격 증명을 사용 하 여 패키지를 설치 하 고 패키지는 해당 사용자에 대 한 기본 범위를 사용 하 여 설치 됩니다.

### <a name="bkmk_rInstall"></a>패키지를 설치 하는 R 도구를 사용 하 여 인스턴스 라이브러리

SQL Server 2016 및 SQL Server 2017 둘 다에 새 패키지를 설치 하려면 R 도구를 사용할 수 있습니다. 그러나 이렇게 하려면 관리자 여야 합니다.

1.  서버에 인터넷에 액세스 하는 경우 보다 앞선 시간 패키지를 다운로드 합니다.

    패키지 저장소를 사용 하 여 오프 라인 패키지의 컬렉션을 준비 하는 것이 좋습니다. 자세한 내용은 참조 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리를 만들](create-a-local-package-repository-using-minicran.md)합니다.

2.  인스턴스에 대 한 R 라이브러리를 설치할 서버의 폴더로 이동 합니다.

    > [!IMPORTANT] 
    > 현재 인스턴스와 연결 된 기본 라이브러리에 패키지를 설치 해야 합니다. 사용자 디렉터리에 패키지를 설치 하지 않습니다. 기본 라이브러리를 찾는 방법에 대해 지침은 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)합니다.

    패키지를 실행 하면 각 인스턴스에 대해 별도 패키지의 복사본을 설치 합니다. 패키지는 인스턴스 간에 공유할 수 없습니다.

4.  관리자 권한으로 R 명령 프롬프트를 엽니다.

    예를 들어 Windows 명령 프롬프트를 사용 하는 경우 다음과 같이 RTerm.Exe 또는 RGui.exe 파일이 있는 디렉터리로 이동 합니다. 

    **기본 인스턴스**

    SQL Server 2017:`C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016의 경우:`C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **명명된 인스턴스**

    SQL Server 2017:`C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016의 경우:`C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

5.  R 명령 실행 `install.packages` 패키지를 설치 합니다.

    구문을은 인터넷 또는 로컬 압축 된 파일에서 패키지를 가져오는 방법는 여부에 따라 달라 집니다. 

    **인터넷 연결을 사용 하 여 패키지를 설치 합니다.**

    예를 들어 다음 문은 인기 있는 e1071 패키지를 설치합니다. 큰따옴표는 언제나 패키지 이름에 대 한 필요 합니다.

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    미러 사이트에 대 한 메시지가 표시 되 면 사용자의 위치에 편리한 모든 사이트를 선택 합니다.

    대상 패키지가 추가 패키지에 따라 달라지는 경우 R 설치 관리자가 자동으로 종속성을 다운로드하고 설치합니다.

    **인터넷에 연결 된 패키지를 수동으로 또는 컴퓨터에 설치**

    설치하려는 패키지에 종속성이 있는 경우 필요한 패키지를 미리 가져와 다른 패키지 압축 파일과 함께 폴더에 추가합니다. 참조는 [설치 팁](#bkmk_tips) 패키지 준비에 대 한 도움말 섹션.

    R 명령 프롬프트에서 다음 명령을 입력하여 설치할 패키지의 경로 및 이름을 지정합니다.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    이 명령은 디렉터리의 복사본을 저장 했다고 가정할 때 해당 로컬 압축 된 파일에서 단일 R 패키지를 추출 `C:\Temp\Downloaded packages`, 로컬 컴퓨터의 R 라이브러리 (종속성)과 함께 패키지를 설치 하 고 있습니다.

### <a name="bkmk_minicran"></a>MiniCRAN 리포지토리에서 여러 패키지 설치

MiniCRAN 리포지토리에서 패키지를 설치 하는 경우 전반적인 프로세스는 단일 압축 된 파일에서 패키지를 설치와 매우 비슷합니다. 그러나 압축 된 형식으로 개별 패키지를 업로드 하는 대신 miniCRAN 저장소 포함으로 대상 패키지 관련된 필요한 패키지 합니다.

1.  MiniCRAN 저장소를 준비 하 고 압축 된 파일 서버에서 로컬 폴더로 복사 합니다.

2.  관리자가 T-SQL 문 실행 T-SQL을 사용 하는 경우 `CREATE EXTERNAL LIBRARY` 압축 된 패키지 컬렉션 데이터베이스에 업로드 합니다.

    예를 들어 다음 문은 randomForest 패키지 및 해당 종속성을 포함 하는 miniCRAN 리포지토리를 참조 합니다.

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

3. SQL Server와 함께 사용 하기 위해 패키지를 설치 하려면 저장된 프로시저에서 R 코드의 일환으로 다음 명령을 실행 합니다.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    성공 하면는 **메시지** "MD5 요약과 패키지 'randomForest' 압축을 풀 성공적으로 검사"도 "마침 연결 된 실행"와 같은 창 메시지를 보고 해야 합니다.

## <a name="package-installation-tips"></a>패키지 설치 팁

이 섹션에서는 분류 된 팁 및 SQL Server에서 R 패키지 설치와 관련 된 예제 코드를 제공 합니다. 

###  <a name="packageVersion"></a>올바른 패키지 버전 및 형식 가져오기

R 패키지에 대한 여러 출처가 있으며 특히 CRAN 및 Bioconductor가 가장 널리 알려져 있습니다. R 언어 공식 사이트(<https://www.r-project.org/>)에 다양한 리소스가 나와 있습니다. 많은 패키지는 소스 코드를 가져올 수 있는 GitHub에도 게시됩니다. 그러나 회사의 누군가가 개발한 R 패키지가 지정되었을 수도 있습니다.

소스에 관계 없이 패키지를 설치 하려면 Windows 플랫폼에 대 한 이진 형식에 있는지 확인 해야 합니다. 그렇지 않은 경우 다운로드 한 패키지는 SQL Server 환경에서 실행할 수 없습니다.

또한 패키지 SQL Server에서 실행 되는 R의 버전과 호환 되는지 여부를 결정 해야 합니다.

### <a name="bkmk_zipPreparation"></a>압축 된 파일로 패키지를 다운로드 합니다.

인터넷 연결 되지 않은 서버에서 설치에 대 한 오프 라인 설치에 대 한 압축 된 파일의 형식에 있는 패키지의 복사본을 다운로드 합니다. 패키지를 압축을 풉니다지 않습니다.

다음 절차의 올바른 버전을 설명 하는 예를 들어는 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 패키지는 컴퓨터가 인터넷에 액세스 하는 것으로 가정 Bioconductor에서 합니다.

1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.

2.  에 대 한 링크를 마우스 오른쪽 단추로 클릭는 합니다. ZIP 파일을 선택 **으로 대상 저장**합니다.

3.  압축 된 패키지를 저장 된와 클릭 로컬 폴더로 이동 **저장**합니다.

이 프로세스는 패키지의 로컬 복사본을 만듭니다. 그런 다음 패키지를 설치 하거나 인터넷에 연결 하지 않은 서버에 압축된 된 패키지를 복사할 수 있습니다.

R 패키지를 만드는 방법 및 zip 파일 형식의 콘텐츠에 대한 자세한 내용은 [Freidrich Leisch: Creating R Packages](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)(Freidrich Leisch: R 패키지 만들기) 자습서를 참조하세요. 이 자습서는 R 사이트에서 PDF 형식으로 다운로드할 수 있습니다.

### <a name="bkmk_packageDependencies"></a>패키지 종속 파일 가져오기

R 패키지는 자주 중 일부는 사용 하지 못할 인스턴스에서 사용 하는 기본 R 라이브러리에서 다른 여러 패키지에 따라 다릅니다. 또는 패키지를 이미 설치 되어 있는 종속 패키지의 다른 버전을 필요로 하는 경우도 있습니다.

올바른 패키지 유형 및 버전을 갖게 조직의 모든 사용자를 또는 여러 패키지를 설치 해야 할 경우 miniCRAN 패키지를 사용 하 여 여러 사용자 또는 컴퓨터 간에 공유할 수 있는 로컬 저장소를 만드는 것이 좋습니다. 자세한 내용은 참조 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리를 만들](create-a-local-package-repository-using-minicran.md)합니다.

### <a name="permissions"></a>Permissions

숙련된 된 R 사용자 인 경우 특별 한 권한이 또는 미리 다운로드 하지 않고 명령줄에서 패키지 설치에 익숙한 수 있습니다. 그러나, 대부분의 서버는 인터넷이 연결을 권한이 없습니다. 또한 파일 공유에 대 한 액세스 또는 저장소 제한 될 수 있습니다.

이 섹션에서는 다양 한 SQL Server 2016 및 SQl Server 2017에서 패키지를 설치 하는 데 필요한 사용 권한 수준에 설명 합니다. 설치를 수행할 수 있습니다 R tools 또는 SQL Server를 사용 하는 프로세스 및 사용 권한을 약간 다릅니다.

-   SQL Server 2016

    이 릴리스에서 컴퓨터의 관리자만 필요한 위치에 패키지를 설치할 수 있습니다. 표준 R 도구를 사용 하 여 패키지를 설치 하지만 관리자로 실행 하 고 인스턴스와 연결 된 R 도구를 사용 해야 합니다.

-   SQL Server 2017

    이 릴리스에서 데이터베이스 관리자가 사용자에 게 패키지 설치를 위임할 수 있는 새로운 기능을 제공 합니다. DBA는 패키지 관리 기능에는 인스턴스별로 사용 하도록 설정 해야 합니다. 이 기능을 사용 하도록 설정한 후 DBA 수 필요에 따라 패키지를 설치 하거나 데이터베이스 단위로에 있는 패키지를 공유 하는 기능은 개별 사용자에 게 데이터베이스 역할을 사용 합니다.

    자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)합니다.


> [!IMPORTANT]
> 
> 숙련 된 R 사용자가 사용자 라이브러리에 패키지를 설치 하 고 다음 파일 경로 지정 하 여 R 솔루션의 일부로 해당 폴더에 패키지를 참조 하는 데 익숙한 합니다. 그러나이 방법은 SQL Server에서 지원 되지 않습니다. 자세한 내용 및 해결 방법에 대 한 참조 [사용자 라이브러리에 패키지를 사용 하는 방법을](packages-installed-in-user-libraries.md)합니다.

### <a name="comparing-package-management-methods"></a>패키지 관리 방법 비교

이 섹션을 사용할 수 있는 패키지 설치 방법을 비교 하 고 몇 가지 추가 고려 사항 및 적절 한 패키지 관리 및 설치 전략을 결정 하기 위한 팁을 나열 합니다.

#### <a name="using-sql-server-package-management-features"></a>SQL Server 패키지 관리 기능을 사용 하 여

패키지 관리를 사용 하도록 설정 하면 특정 데이터베이스에 대 한 패키지를 설치 합니다. 패키지를 사용 하는 모든 데이터베이스에서 R 스크립트 사용 하도록 설정 해야 할 경우에 각 데이터베이스에 설치 해야 합니다.

그러나 되기 때문에 SQL Server에 패키지를 사용할 수 있는 권한이 있는 사용자에 대 한 정보를 관리, 사용자와 데이터베이스 간에 패키지에 대 한 정보를 복사 하는 보다 쉽게. 인스턴스 간에 이동할 때 또는 사용자 또는 데이터베이스를 복원 하는 경우 여러 사용자에 대 한 작업 패키지 세트를 다시 작성 하는 것도 쉽습니다.

설치 하거나 R 패키지를 실행할 여러 데이터베이스 사용자가 있을 때마다 T-SQL 및 패키지 관리 기능을 사용 하 여 SQL Server 2017에 것이 좋습니다.

이 기능은 SQL Server 2017부터 사용할 수 있습니다.

#### <a name="using-r-tools-to-install-packages-for-the-sql-server-instance"></a>R 도구를 사용 하 여 SQL Server 인스턴스에 대 한 패키지를 설치 하려면

이 방법을 사용 하면 인스턴스에 대 한 설치 된 패키지를 모든 데이터베이스 에서도 사용할 수 있습니다. 그러나 패키지를 파일 시스템에 직접 설치 되어 있으므로 SQL Server 외부 관리 되어야 합니다. 패키지 백업 되거나 복원 될 수 없습니다. 또한 R 도구를 사용 하는 데이터베이스 관리자 배워야 합니다.

그러나이 솔루션은 데이터베이스의 유일한 소유자 인 경우 가장 간단한 것입니다.

#### <a name="managing-multiple-packages-and-multiple-versions-of-the-same-package"></a>여러 패키지 및 여러 버전의 동일한 패키지 관리

사용 하 여 로컬 저장소를 설정 하는 R 패키지의 오프 라인 설치를 수행 해야 할 경우 [miniCRAN](https://mran.revolutionanalytics.com/package/miniCRAN/) 패키지를 공유 하 고 조직에서 사용 하기 위해 사용할 수 있는 버전을 관리할 수 있습니다.

#### <a name="establish-a-single-mirror-site-as-standard"></a>표준으로 단일 미러 사이트를 설정 합니다.

새 패키지를 추가할 때마다 미러 사이트를 선택할 필요가 없도록 하려면 언제나 같은 리포지토리를 사용하도록 R 개발 환경을 구성할 수 있습니다. 이렇게 하려면 글로벌 R 설정 파일 편집 **합니다. Rprofile**, 다음 줄을 추가 합니다.

`options(repos=structure(c(CRAN="<mirror site URL>")))`

현재 CRAN 미러의에 나열 된 [이 사이트](https://cran.r-project.org/mirrors.html)합니다.

기본 설정 및 R 런타임이 시작 될 때 로드 된 다른 파일에 대 한 자세한 정보에 대 한 R 콘솔에서이 명령을 실행 합니다.`?Startup`

#### <a name="know-which-library-you-are-using-for-installation"></a>상위 라이브러리를 설치에 사용 하는 것을 알고 있습니다

일시 중지는 잠시 아무것도 설치 하기 전에 이전에 컴퓨터의 R 환경을 수정 하는 경우 R 환경 변수를 확인 하 고 `.libPath` 하나의 경로 사용 합니다.

이 경로 인스턴스에 대 한 R_SERVICES 폴더를 가리켜야 합니다. 자세한 내용은 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)합니다.

#### <a name="side-by-side-installation-with-r-server"></a>R server-side-by-side 설치

SQL Server 컴퓨터 학습 서비스 외에도 Microsoft 컴퓨터 학습 Server (독립 실행형)를 설치한 경우 컴퓨터 모두에 대 한 각, R 도구 및 라이브러리의 중복 항목을 별도 R 설치 과정 있어야 합니다.

> [!IMPORTANT]
> 
> R_SERVER 라이브러리에 설치 된 패키지 Microsoft R Server 에서만 사용 되 고 SQL Server에서 액세스할 수 없습니다.
> 
> 사용 하 여 `R_SERVICES` SQL Server에서 사용 하려는 패키지를 설치할 때 라이브러리입니다.

