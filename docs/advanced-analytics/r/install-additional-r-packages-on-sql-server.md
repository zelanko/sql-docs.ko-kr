---
title: "SQL Server에 추가 R 패키지를 설치 합니다. | Microsoft Docs"
ms.date: 01/04/2018
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 21456462-e58a-44c3-9d3a-68b4263575d7
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 530745918dfd4808694b401be55e40bac00f3cce
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>SQL Server에 추가 R 패키지를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 기계 학습 사용 하도록 설정 하는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다.

**적용 대상:** 
+ [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]
+ [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="prerequisites"></a>필수 구성 요소

+ 패키지의 Windows 버전 인지 확인: [올바른 패키지 버전 및 형식 가져오기](#packageVersion)

+ Windows 이진을 사전에 다운로드 해야는 서버에 인터넷 액세스가 없는 경우: [zip 파일 다운로드](#bkmk_zipPreparation)

+ 패키지 종속성을 식별 합니다. 

    - 서버에서 인터넷에 액세스할 경우 종속성;에 대해 걱정할 필요가 없습니다. 필요한 모든 패키지를 자동으로 설치할 수 있습니다.

    - 서버가 수행 하는 경우 **하지** 인터넷에 액세스할 모든 종속성을 식별 하 고 압축 된 형식으로 사전에 필요한 패키지를 다운로드 해야 합니다. 이 작업을 수행 하는 쉬운 방법을 사용 하는 것 [miniCRAN](create-a-local-package-repository-using-minicran.md) 모든 종속성을 사용 하 여 패키지의 컬렉션을 준비 합니다. 이 저장소는 다음 서버 컴퓨터에 복사할 수 있습니다.

+ 패키지 호환성을 확인 합니다. 패키지는 SQL Server에서 실행 되는 R의 버전과 호환 되어야 합니다.

    또한 패키지 (또는 필요한 모든 패키지)을 SQL Server에서 또는 정책에 의해 차단 될 수 있는 기능이 포함 되어 있는지 여부를 확인 합니다. 예를 들어 특정 패키지는 강화 된 SQL Server 환경에 대 한 저하 적합 합니다. 이러한 패키지는 Java 또는 대개는 SQL Server 환경 또는 높은 파일 시스템 액세스를 필요로 하는 패키지에서 사용 되지 다른 프레임 워크를 사용 하는 네트워크에 액세스 하는 패키지를 포함할 수 있습니다.

+ Permissions

    SQL Server를 실행 하는 컴퓨터에 관리자 권한이 있어야 합니다.

    또한 SQL Server를 실행 하려면 현재 인스턴스와 연결 되는 기본 라이브러리에서 패키지를 설치 되어야 합니다. 기본 라이브러리를 찾는 방법에 대해 지침은 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)합니다.
    
    숙련된 된 R 사용자 인 경우 특별 한 권한이 또는 미리 다운로드 하지 않고 명령줄에서 패키지 설치에 익숙한 수 있습니다. 그러나이 메서드는 SQL Server에서 작동 하지 않습니다. 대부분의 경우 SQL Server에에서 없는 컴퓨터는 인터넷에 연결 합니다. 또한 서버 파일에 대 한 액세스 또는 외부 저장 제한 될 수 있습니다. 사용자 라이브러리에 설치 된 패키지를 SQL Server의 R 작업 runnign 하 여 액세스할 수 없습니다. 

    SQL Server 컴퓨터에 관리자 권한이 없으면 데이터베이스 관리자를를 패키지 설치에 대 한 도움말을 찾습니다.

+ 패키지를 사용 해야 하는 각 인스턴스에 대해 개별적으로 설치를 실행 합니다.

     패키지는 인스턴스 간에 공유할 수 없습니다. 동일한 압축 된 파일 원본을 사용 하 여 인스턴스를 구분 하 여 패키지를 설치 하지만 각 인스턴스 라이브러리에는 별도 패키지의 복사본 추가 됩니다.

## <a name="install-packages"></a>패키지 설치

이 섹션에서는 다음과 같은 시나리오에 대 한 패키지 설치 단계를 제공 합니다.

+ [인터넷에 연결 된 서버에 새 패키지를 설치 합니다.](#bkmk_rInstall)
+ [패키지의 오프 라인 설치를 사용 하 여 서버에서 수행 **없는** 인터넷 액세스](#bkmk_offlineInstall)
+ [RevoScaleR을 사용 하 여 SQL Server 계산 컨텍스트에서에 패키지를 설치 합니다.](#bkmk_rAddPackage)
+ [외부 라이브러리 만들기 문을 사용 하 여 패키지 설치](#bkmk_createlibrary) (SQL Server 2017만; 기타 제한 사항 적용)

### <a name="bkmk_rInstall"></a>R 도구를 사용 하 여 온라인 설치

SQL Server 2016 또는 SQL Server 2017의 인스턴스에서 새 패키지를 설치 하려면 표준 R 도구를 사용할 수 있습니다. 그러나 이렇게 하려면 관리자 여야 합니다.

1.  인스턴스에 대 한 R 라이브러리를 설치할 서버의 폴더로 이동 합니다.

    > [!IMPORTANT] 
    > 현재 인스턴스와 연결 된 기본 라이브러리에 패키지를 설치 해야 합니다. 사용자 디렉터리에 패키지를 설치 하지 않습니다.

    필요한 사용 권한이 없는 경우 데이터베이스 관리자에 게 문의 하 고 필요한 패키지의 목록을 제공 합니다.

2.  관리자 권한으로 R 명령 프롬프트를 엽니다.

    예를 들어 Windows 명령 프롬프트를 사용 하는 경우 RGui.exe 또는 RTerm.Exe가 있는 디렉터리를 이동 합니다. 

    **기본 인스턴스**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **명명된 인스턴스**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

    바인딩 기계 학습 구성 요소 업그레이드를 사용 하 여 경로 변경 수 있습니다. 항상 새 패키지를 설치 하기 전에 인스턴스 경로 확인 합니다. 

3.  R 명령 실행 `install.packages` 패키지를 설치 합니다. 예를 들어 다음 문은 인기 있는 e1071 패키지를 설치합니다. 

    ```R
    install.packages("e1071", lib = lib.SQL)
    ```

    큰따옴표는 패키지 이름에 필요 합니다.

4. 미러 사이트에 대 한 메시지가 표시 되 면 사용자의 위치에 편리한 모든 사이트를 선택 합니다.

5. 대상 패키지가 추가 패키지에 의존 하는 경우 R 설치 관리자 자동으로 종속성을 다운로드 하 고 설치 합니다.

> [!IMPORTANT]
> 패키지를 사용 해야 하는 각 인스턴스에 대해 개별적으로 설치를 실행 합니다. 패키지는 인스턴스 간에 공유할 수 없습니다.

### <a name = "bkmk_offlineInstall"></a>R 도구를 사용 하 여 오프 라인 설치 

패키지를 설치 하려는 경우에 종속성이 준비 **모든** 미리 패키지 필요 합니다.  참조는 [설치 팁](#bkmk_tips) 패키지 준비에 대 한 도움말 섹션.

> [!IMPORTANT]
>  때마다 인터넷에 액세스할 수 있는 서버에 패키지를 설치 하는 것이 중요 전체 종속성을 사전에 분석 하 고 필요한 모든 패키지를 다운로드 했는지 확인 **전에** 설치를 시작 합니다. 권장 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 이 프로세스에 대 한 합니다. 이 R 패키지는 패키지를 설치할 종속성을 분석 하 고 압축 된 파일을 모두 가져옵니다 목록을 사용 합니다. 그런 다음 miniCRAN 서버 컴퓨터에 복사할 수 있는 단일 저장소를 만듭니다.
> 
> 자세한 내용은 참조 하세요. [miniCRAN를 사용 하 여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)

1. 패키지 또는 저장소 압축 된 형식으로 로컬 공유 또는 서버에 액세스할 수 있는 기타 위치에 복사 합니다.

2.  인스턴스에 대 한 R 라이브러리를 설치할 서버에서 폴더를 찾습니다.

    예를 들어 Windows 명령 프롬프트를 사용 하는 경우 RGui.exe 또는 RTerm.Exe가 있는 디렉터리를 이동 합니다.

    **기본 인스턴스**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

    **명명된 인스턴스**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. 관리자 권한으로 R 명령 프롬프트를 엽니다.

4.  R 명령 실행 `install.packages` 패키지 또는 저장소 이름 및 압축 된 파일의 위치를 지정 합니다.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    이 명령은 R 패키지를 추출 `mynewpackage` 복사 디렉터리에 저장 했다고 가정할 때 해당 로컬 압축 된 파일에서 `C:\Temp\Downloaded packages`, 로컬 컴퓨터에 패키지를 설치 합니다. 패키지에 경우 모든 종속 파일을 라이브러리에서 기존 패키지에 대 한 설치 관리자를 확인 합니다. 종속성을 포함 하는 리포지토리를 만든 경우 requireed 패키지도 설치 관리자를 설치 합니다.

    필요한 패키지 인스턴스 라이브러리에 표시 되지 않으며 압축 된 파일에서 찾을 수 없습니다, 대상 패키지의 설치가 실패 합니다.

### <a name="bkmk_rAddPackage"></a>R 원격 클라이언트에서 서버에 R 패키지 설치

최신 버전의 [R 서버 또는 컴퓨터 학습 서버](https://docs.microsoft.com/machine-learning-server/rebranding-microsoft-r-server), RevoScaleR 함수를 지 원하는 SQL Server 계산 컨텍스트에서에 새 R 패키지를 설치에 포함 됩니다. 

1. 시작 하기 전에 이러한 조건이 충족 되어 있는지 확인 합니다.

    + 클라이언트에 RevoScale 9.0.1 이상.
    + SQL Server 인스턴스에서 RevoScaleR의 해당 버전을 설치한 합니다.
    + [패키지 관리 기능](..\r\r-package-how-to-enable-or-disable.md) 인스턴스에서 사용 되었습니다.
    + 지정 된 인스턴스 및 ddatabase에 패키지 공유에서 또는 prvate 컨텍스트를 설치할 수 있도록 데이터베이스 역할의 멤버인 사용자가 있습니다.

2. R 명령줄에서 인스턴스 및 데이터베이스를 연결 문자열을 정의 하 고 연결 문자열을 사용 하 여는 [RxInSqlServer](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinsqlserver) 를 SQL Server 계산 컨텍스트를 만드는 생성자입니다.

    ```R
    sqlcc <- RxInSqlServer(connectionString = myConnString, shareDir = sqlShareDir, wait = sqlWait, consoleOutput = sqlConsoleOutput)
    ```
3. 설치 하 여 문자열 변수에 목록을 저장 제거할 패키지의 목록을 만듭니다.

    ```R
    packageList <- c("e1071", "mice")
    ```

4. 호출 [rxInstallPackages](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxinstallpackages) 계산 컨텍스트 및 패키지 이름이 포함 된 문자열 변수를 전달 합니다.

    ```R
    rxInstallPackages(pkgs = packageList, verbose = TRUE, computeContext = sqlcc)
    ```

    종속 패키지 필요한 경우 또한 설치 하기 인터넷 연결을 사용할 수 있는 것으로 가정 합니다.
    
    이 예제에서는 소유자 및 범위 지정 되지 않았기 때문에 설치 된 패키지가 해당 사용자의 기본 범위에 연결 하는 사용자의 자격 증명.

### <a name="bkmk_createlibrary"></a>MiniCRAN 저장소 및 외부 라이브러리 만들기를 사용 하 여 패키지를 설치 하려면 

SQL Server 2017 설치 및 T-SQL을 사용 하 여 R 패키지를 관리 하기 위한 새로운 기능을 제공 합니다. 그러나이 프로세스는 로컬 인터넷에서 다운로드 하지 않고 파일을 압축 하는 대로 패키지 사용할 수 있어야 합니다. 모든 패키지가 미리 준비 되지 않았는지 문은 실패 합니다.

외부 라이브러리 만들기 이러한 조건에서 사용할 수 있습니다.

+ 단일 패키지를 설치 하는 종속성이 없는
+ 설치 하는 여러 패키지 또는 패키지, 종속성이 있는 한 모든 패키지를 미리 준비 된 있습니다. 

**단계**

1.  압축 된 형식으로 패키지 준비 또는 패키지 및 해당 종속성을 포함 하는 miniCRAN 리포지토리 만들기.  

2. 압축 된 파일 또는 리포지토리에서 서버에서 로컬 폴더로 복사 합니다.

     > [!IMPORTANT]
     > 소스는 대상 패키지 뿐만 아니라 모든 관련된 필수 패키지가 있어야 합니다. 항목으로 지정 된 파일입니다.

3. 관리자로 서 T-SQL 문 실행 `CREATE EXTERNAL LIBRARY` 압축 된 패키지 컬렉션 데이터베이스에 업로드 합니다.

    예를 들어 다음 문은 randomForest 패키지 및 해당 종속성을 포함 하는 miniCRAN 리포지토리를 참조 합니다. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Downloads\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    CREATE 문에서; 임의의 이름을 사용할 수 없습니다. 외부 라이브러리 이름에는 로드 하거나 패키지를 호출할 때 사용 되는 동일한 이름을 가져야 합니다.

4. 저장된 프로시저 내부에서 코드를 실행 하 여 SQL Server와 함께 사용 하기 위해 패키지를 설치 합니다.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    # install randomForest and its dependencies
    library(randomForest)'
    ```

    성공 하면는 **메시지** "MD5 요약과 패키지 'randomForest' 압축을 풀 성공적으로 검사" 및 "마침 연결 된 실행"와 같은 창 메시지를 보고 해야 합니다.

    설치가 실패할 경우에 모든 패키지 설치 실패 하 고를 패키지 설치를 설치 하면 실패할 수,이 메시지와. 

    "오류: rxSqlPkgInstallPackages... 자세한 내용은 로그를 검토 하십시오.-패키지를 설치 하지 못했습니다. "

## <a name="package-installation-tips-and-frequently-asked-questions-faq"></a>패키지 설치 팁 및 질문과 대답 (FAQ)

이 섹션에서는 다양 한 팁과 SQL Server에서 R 패키지 설치와 관련 된 일반적인 질문을 제공 합니다.

###  <a name="packageVersion"></a>올바른 패키지 버전 및 형식 가져오기

R 패키지에 대한 여러 출처가 있으며 특히 CRAN 및 Bioconductor가 가장 널리 알려져 있습니다. R 언어 공식 사이트(<https://www.r-project.org/>)에 다양한 리소스가 나와 있습니다. 많은 패키지는 소스 코드를 가져올 수 있는 GitHub에 게시 됩니다. 그러나 있습니다 수 받은 회사의 누군가가 개발한 R 패키지가 있습니다.

소스에 관계 없이 패키지를 설치 하려면 Windows 플랫폼에 대 한 이진 형식에 있는지 확인 해야 합니다. 그렇지 않은 경우 다운로드 한 패키지는 SQL Server 환경에서 실행할 수 없습니다.

### <a name="bkmk_zipPreparation"></a>패키지를 압축 된 파일로 다운로드

인터넷 연결 되지 않은 서버에서 설치에 대 한 오프 라인 설치에 대 한 압축된 된 파일 형식으로 패키지의 복사본을 다운로드 해야 합니다. 패키지를 압축을 풉니다지 않습니다.

다음 절차의 올바른 버전을 설명 하는 예를 들어는 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 패키지는 컴퓨터가 인터넷에 액세스 하는 것으로 가정 Bioconductor에서 합니다.

1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.

2.  에 대 한 링크를 마우스 오른쪽 단추로 클릭는 합니다. ZIP 파일을 선택 **으로 대상 저장**합니다.

3.  압축 된 패키지를 저장 된와 클릭 로컬 폴더로 이동 **저장**합니다.

    이 프로세스는 패키지의 로컬 복사본을 만듭니다. 다운로드 오류가 발생 하면 다른 미러 사이트를 시도 합니다.

4. 패키지 보관을 다운로드 한 후 패키지를 설치 하거나 인터넷에 연결 하지 않은 서버에 압축된 된 패키지를 복사 수 있습니다.

> [!TIP]
> 실수로 이진 파일을 다운로드 하는 대신 패키지를 설치 하면 다운로드 된 압축된 파일의 복사본은 컴퓨터에도 저장 됩니다. 파일 위치를 확인할 패키지가 설치 되어 상태 메시지를 감시 합니다. 인터넷에 연결 하지 않은 서버에는 압축 된 파일을 복사할 수 있습니다.
> 이 메서드를 사용 하 여 패키지를 다운로드 하는 경우에 패키지 종속 파일 포함 되지 않습니다. 

Zip 파일 형식 및 R 패키지를 만드는 방법의 내용에 대 한 자세한 내용은이 자습서에서는 R 프로젝트 사이트에서 PDF 형식으로 다운로드할 수 있는 권장: [R 패키지를 만드는](http://cran.r-project.org/doc/contrib/Leisch-CreatingPackages.pdf)합니다.

### <a name="bkmk_packageDependencies"></a>패키지 종속 파일 가져오기

R 패키지는 자주 중 일부는 사용 하지 못할 인스턴스에서 사용 하는 기본 R 라이브러리에서 다른 여러 패키지에 따라 다릅니다. 경우에 따라 패키지에 이미 설치 되어 있는 종속 패키지의 다른 버전이 필요 합니다.

올바른 패키지 유형 및 버전을 갖게 조직의 모든 사용자를 또는 여러 패키지를 설치 해야 할 경우 사용 하는 것이 좋습니다는 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 공유할 수 있는 로컬 저장소를 만드는 패키지 여러 사용자 또는 컴퓨터 간에 자세한 내용은 참조 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리를 만들](create-a-local-package-repository-using-minicran.md)합니다.

### <a name="permissions"></a>Permissions

이 섹션에서는 다양 한 SQL Server 2016 및 SQL Server 2017에서 패키지를 설치 하는 데 필요한 사용 권한 수준에 설명 합니다. 설치를 수행할 수 있습니다 R tools 또는 SQL Server를 사용 하는 프로세스 및 사용 권한을 약간 다릅니다.

-   SQL Server 2016

    이 릴리스에서 컴퓨터의 관리자만 필요한 위치에 패키지를 설치할 수 있습니다. 표준 R 도구를 사용 하 여 패키지를 설치 하지만 관리자로 실행 하 고 인스턴스와 연결 된 R 도구를 사용 해야 합니다.

-   SQL Server 2017

    관리 권한이 있는 경우에 R 도구를 사용 하 여는 인스턴스 전체에서 패키지를 설치할 수 있습니다.

    데이터베이스 소유자 인 경우에 대 한 연결을 정의 하 고 RxInSqlServer를 사용 하 여 인스턴스에 연결 하는 경우 원격 클라이언트에서 R 패키지를 설치할 수 있습니다.
    
    이 릴리스의 이후 릴리스에서 데이터베이스 관리자가 R, Python 패키지 관리를 지원 하도록 새로운 기능이 있습니다. 이 기능을 사용 하려면 DBA 패키지 관리 기능에는 인스턴스별로 사용 하도록 설정 먼저 해야 합니다. 이 기능을 설정 하면 개별 사용자가 데이터베이스 역할에 따라 특정 데이터베이스에 패키지를 설치할 수 있습니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리를 사용할지](../r/r-package-how-to-enable-or-disable.md)합니다.

> [!IMPORTANT]
> 
> 숙련 된 R 사용자가 사용자 라이브러리에 패키지를 설치 하 고 다음 파일 경로 지정 하 여 R 솔루션의 일부로 해당 폴더에 패키지를 참조 하는 데 익숙한 합니다. 그러나이 방법은 SQL Server에서 지원 되지 않습니다. 자세한 내용 및 해결 방법에 대 한 참조 [사용자 라이브러리에 패키지를 사용 하는 방법을](packages-installed-in-user-libraries.md)합니다.

### <a name="establish-a-single-mirror-site-as-standard"></a>표준으로 단일 미러 사이트를 설정 합니다.

새 패키지를 추가할 때마다 미러 사이트를 선택할 필요가 없도록 하려면 언제나 같은 리포지토리를 사용하도록 R 개발 환경을 구성할 수 있습니다. 이렇게 하려면 글로벌 R 설정 파일 편집 **합니다. Rprofile**, 다음 줄을 추가 합니다.

`options(repos=structure(c(CRAN="<mirror site URL>")))`

현재 CRAN 미러의에 나열 된 [이 사이트](https://cran.r-project.org/mirrors.html)합니다.

기본 설정 및 R 런타임이 시작 될 때 로드 된 다른 파일에 대 한 자세한 정보에 대 한 R 콘솔에서이 명령을 실행 합니다.`?Startup`

### <a name="know-which-library-you-are-using-for-installation"></a>상위 라이브러리를 설치에 사용 하는 것을 알고 있습니다

일시 중지는 잠시 아무것도 설치 하기 전에 이전에 컴퓨터의 R 환경을 수정 하는 경우 R 환경 변수를 확인 하 고 `.libPath` 하나의 경로 사용 합니다.

이 경로 인스턴스에 대 한 R_SERVICES 폴더를 가리켜야 합니다. 자세한 내용은 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)합니다.

### <a name="side-by-side-installation-with-r-server"></a>R server-side-by-side 설치

SQL Server 컴퓨터 학습 서비스 외에도 Microsoft 컴퓨터 학습 Server (독립 실행형)를 설치한 경우 컴퓨터에 R 도구 및 라이브러리의 중복 항목을 각각에 대 한 별도 설치 R의 있어야 합니다.

> [!IMPORTANT]
> 
> R_SERVER 라이브러리에 설치 된 패키지 Microsoft R Server 에서만 사용 되 고 SQL Server에서 액세스할 수 없습니다.
> 
> 사용 하 여 `R_SERVICES` SQL Server에서 사용 하려는 패키지를 설치할 때 라이브러리입니다.

### <a name="how-to-determine-which-packages-are-already-installed"></a>어떤 패키지가 이미 설치 되어 있는지 확인 하는 방법

 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)