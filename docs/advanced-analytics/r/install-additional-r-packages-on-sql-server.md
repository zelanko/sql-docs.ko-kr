---
title: "SQL Server에 추가 R 패키지를 설치 합니다. | Microsoft Docs"
ms.date: 02/20/2018
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
ms.openlocfilehash: a328b07027f61f50df7e3ca2b6ac12b92508688b
ms.sourcegitcommit: c08d665754f274e6a85bb385adf135c9eec702eb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2018
---
# <a name="install-additional-r-packages-on-sql-server"></a>SQL Server에 추가 R 패키지를 설치 합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 기계 학습 사용 하도록 설정 하는 SQL Server 인스턴스에 새 R 패키지를 설치 하는 방법을 설명 합니다.

SQL Server 버전에 있는 및 인터넷에 연결 되어 있는지에 따라 새 R 패키지를 설치 하기 위한 여러 메서드가 있습니다.

+ [R 도구를 사용 하 여 인터넷에 연결 된 새 패키지를 설치 합니다.](#bkmk_rInstall)

    기본 R 명령을 사용 하 여 인터넷에서 패키지를 설치 합니다. 이 가장 간단한 방법은 아니지만 관리 액세스가 필요한 합니다.

    **적용 대상:**[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)][!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)]합니다.     또한에 필요한 인스턴스의 [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] 패키지 관리 Ddl 통해 설정 되지 않은 합니다.

+ [사용 하 여 서버에 새 R 패키지 설치 **없는** 인터넷 액세스](#bkmk_offlineInstall)

    서버에 인터넷 액세스 몇 가지 추가 단계는 패키지를 준비 해야 합니다. 이 섹션에서는 패키지 및 종속성의 설치에 필요한 파일을 준비 하는 방법을 설명 합니다.

+ [외부 라이브러리 만들기 문을 사용 하 여 패키지 설치](#bkmk_createlibrary) 

    외부 라이브러리 만들기 문은 dba Python 또는 R 코드를 직접 실행 하지 않고 패키지 라이브러리를 만들 수 있도록 SQL Server 2017에 제공 됩니다. 그러나이 방법은 필요한 모든 패키지를 미리 준비 해야 합니다.  

    **적용 대상:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]; 기타 제한이 적용  

## <a name="bkmk_rInstall"></a> 인터넷을 사용 하 여 새 R 패키지 설치

SQL Server 2016 또는 SQL Server 2017의 인스턴스에서 새 패키지를 설치 하려면 표준 R 도구를 사용할 수 있습니다. 이 프로세스는 컴퓨터에서 관리자가 필요 합니다.

> [!IMPORTANT] 
> 현재 인스턴스와 연결 된 기본 라이브러리에 패키지를 설치 해야 합니다. 사용자 디렉터리에 패키지를 설치 하지 않습니다.

이 절차에서는 관리자 권한;를 사용 하 여 패키지를 설치 하는 방법을 설명합니다 그러나 rterm이 또는 다른 R 명령줄 도구 상승 된 액세스를 지 원하는 사용할 수 있습니다.

### <a name="install-a-package-using-rgui-or-rterm"></a>관리자 권한 또는 rterm이 사용 하 여 패키지 설치

1. 인스턴스에 대 한 R 라이브러리를 설치할 서버의 폴더로 이동 합니다.

  **기본 인스턴스**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **명명된 인스턴스**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

  바인딩 기계 학습 구성 요소 업그레이드를 사용 하 여 경로 변경 수 있습니다. 항상 새 패키지를 설치 하기 전에 인스턴스 경로 확인 합니다. 

2. RGui.exe를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.

    필요한 사용 권한이 없는 경우 데이터베이스 관리자에 게 문의 하 고 필요한 패키지의 목록을 제공 합니다.

3. 명령줄에서 패키지 이름을 알고 있으면 입력할 수 있습니다: `install.packages("the_package-name")` 큰따옴표는 패키지 이름에 필요 합니다.

4. 미러 사이트에 대 한 메시지가 표시 되 면 사용자의 위치에 편리한 모든 사이트를 선택 합니다.

5. 대상 패키지가 추가 패키지에 의존 하는 경우 R 설치 관리자 자동으로 종속성을 다운로드 하 고 설치 합니다.

6. 패키지를 사용 해야 하는 각 인스턴스에 대해 개별적으로 설치를 실행 합니다. 패키지는 인스턴스 간에 공유할 수 없습니다.

## <a name = "bkmk_offlineInstall"></a> R 도구를 사용 하 여 오프 라인 설치

R 패키지를 인터넷에 연결 되지 않은 서버에 설치 하려면 다음을 수행 해야 합니다.

+ 사전에 종속성을 분석 합니다.
+ 인터넷에 연결 된 컴퓨터에는 대상 패키지를 다운로드 합니다.
+ 동일한 컴퓨터에 필요한 패키지를 다운로드 하 고 단일 패키지 보관 파일의 모든 패키지를 배치 합니다.
+ 아직 않은 압축 된 형태로 표시 하는 경우 아카이브를 압축 합니다.
+ 패키지 보관 서버의 위치에 복사 합니다.
+ 원본으로 보관 파일을 지정 하는 대상 패키지를 설치 합니다.

> [!IMPORTANT] 
> > 모든 종속성을 분석 해야 하 고 다운로드 **모든** 패키지 필요한 **하기 전에** 설치를 시작 합니다. 권장 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 이 프로세스에 대 한 합니다. 이 R 패키지는 패키지를 설치할 종속성을 분석 하 고 압축 된 파일을 모두 가져옵니다 목록을 사용 합니다. 그런 다음 miniCRAN 서버 컴퓨터에 복사할 수 있는 단일 저장소를 만듭니다.
> 
> 자세한 내용은 참조 하세요. [miniCRAN를 사용 하 여 로컬 패키지 리포지토리 만들기](create-a-local-package-repository-using-minicran.md)

이 절차에서는 압축 된 형식에 필요한 서버에 복사를 준비 하는 모든 패키지를 준비한 가정 합니다.

1. 복사 패키지 파일을 압축 또는 대 한 여러 패키지의 모든 패키지를 포함 하는 전체 저장소 압축 형식으로 서버에 액세스할 수 있는 위치에 있습니다.

2. 인스턴스에 대 한 R 라이브러리를 설치할 서버에서 폴더를 엽니다. 예를 들어 Windows 명령 프롬프트를 사용 하는 경우 RGui.exe 또는 RTerm.Exe가 있는 디렉터리를 이동 합니다.

  **기본 인스턴스**

    SQL Server 2017: `C:\Program Files\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program Files\MSSQL13.MSSQLSERVER\R_SERVICES\bin\x64`

  **명명된 인스턴스**

    SQL Server 2017: `C:\Program files\MSSQL14.<instanceName>\R_SERVICES\bin\x64`
    
    SQL Server 2016: `C:\Program files\MSSQL13.<instanceName>\R_SERVICES\bin\x64`

3. 관리자 권한 또는 명령 프롬프트를 마우스 오른쪽 단추로 클릭 하 고 선택 **관리자 권한으로 실행**합니다.

4. R 명령 실행 `install.packages` 패키지 또는 저장소 이름 및 압축 된 파일의 위치를 지정 합니다.

    ```R
    install.packages("C:\\Temp\\Downloaded packages\\mynewpackage.zip", repos=NULL)
    ```

    이 명령은 R 패키지를 추출 `mynewpackage` 복사 디렉터리에 저장 했다고 가정할 때 해당 로컬 압축 된 파일에서 `C:\Temp\Downloaded packages`, 로컬 컴퓨터에 패키지를 설치 합니다. 패키지에 경우 모든 종속 파일을 라이브러리에서 기존 패키지에 대 한 설치 관리자를 확인 합니다. 종속성을 포함 하는 리포지토리를 만든 경우 설치 관리자는 데 필요한 패키지를 설치 합니다.

    필요한 패키지 인스턴스 라이브러리에 표시 되지 않으며 압축 된 파일에서 찾을 수 없습니다, 대상 패키지의 설치가 실패 합니다.

## <a name="bkmk_createlibrary"></a> DDL 문을 사용 하 여 패키지를 설치 하려면 

SQL Server 2017 년 1에서 사용할 수 있습니다는 [외부 라이브러리 만들기](https://docs.microsoft.com/sql/t-sql/statements/create-external-library-transact-sql) 인스턴스 또는 특정 데이터베이스에 패키지 또는 패키지 집합을 추가 하는 문입니다. 이 DDL 문이 및 지원 데이터베이스 역할은 않습니다 패키지의 설치 및 관리를 용이 하 게 한 BA 하 여 Python 또는 R 도구를 사용 하지 않고도.

이 프로세스는 일반적인 R, Python 메서드를 사용 하 여 패키지 설치에 비해 몇 가지 준비가 필요 합니다.

+ 인터넷에서 다운로드 하는 대신 로컬 파일을 압축으로 사용할 수 있는 모든 패키지를 여야 합니다.

    서버에서 파일 시스템에 액세스할 수 없는 경우 전달할 수도 있습니다는 완전 한 패키지 변수를 이진 형식을 사용 하 여 합니다. 자세한 내용은 참조 [외부 라이브러리 만들기](../../t-sql/statements/create-external-library-transact-sql.md)합니다.

+ 문이 필요한 패키지를 사용할 수 없는 경우 실패 합니다. 설치 하 고 패키지 서버 및 데이터베이스에 업로드 되 고 있는지 확인 하려는 패키지의 종속성을 분석 해야 합니다. 사용 하는 것이 좋습니다 **miniCRAN** 또는 **igraph** 패키지 종속성을 분석에 대 한 합니다.

### <a name="prepare-the-packages-in-archive-format"></a>보관 파일 형식으로 패키지 준비

1. 단일 패키지를 설치 하는 경우 압축 된 형식의 패키지를에서 다운로드 합니다. 

2. 패키지는 다른 패키지에 필요한 경우 필요한 패키지를 사용할 수 있는지 확인 해야 합니다. 대상 패키지를 분석 하 고 모든 해당 종속성을 확인할 miniCRAN를 사용할 수 있습니다. 

3. 압축 된 파일 또는 서버에서 로컬 폴더에 모든 패키지가 포함 된 miniCRAN 리포지토리 복사 합니다.

4. 열기는 **쿼리** 창에서 관리자 권한을 가진 계정을 사용 합니다.

5. T-SQL 문 실행 `CREATE EXTERNAL LIBRARY` 압축 된 패키지 컬렉션 데이터베이스에 업로드 합니다.

    예를 들어, 다음 문은 이름이 패키지 원본으로 포함 하는 miniCRAN 리포지토리는 **randomForest** 종속 항목과 함께 패키지 됩니다. 

    ```R
    CREATE EXTERNAL LIBRARY randomForest
    FROM (CONTENT = 'C:\Temp\Rpackages\randomForest_4.6-12.zip')
    WITH (LANGUAGE = 'R');
    ```

    임의의 이름을; 사용할 수 없습니다. 외부 라이브러리 이름에는 로드 하거나 패키지를 호출할 때 사용 되는 동일한 이름을 가져야 합니다.

6. 라이브러리 정상적으로 작성 하는 경우에 저장 프로시저 호출 하 여 SQL Server에서 패키지를 실행할 수 있습니다.
    
    ```SQL
    EXEC sp_execute_external_script
    @language =N'R',
    @script=N'
    library(randomForest)'
    ```

### <a name="known-issues-with-create-external-library"></a>외부 라이브러리 만들기의 알려진된 문제

외부 라이브러리 만들기 이러한 조건에서 사용할 수 있습니다.

+ 단일 패키지를 설치 하는 종속성이 없는 합니다.
+ 패키지 종속성을 설치 하는 한 모든 패키지를 미리 준비 된 있습니다. 

누락 된 모든 패키지 종속성 DDL 문은 실패 합니다. 예를 들어 설치 프로세스는 이러한 경우 실패 하도록 알려져 있습니다.

+ 두 번째 수준 종속성이 포함 된 패키지를 설치 하 고 분석 2-수준 패키지를 확장 하지 않았습니다. 예를 들어 설치 하려는 **gglot2**, 및 매니페스트에 나열 된 모든 패키지를 식별; 그러나 해당 패키지 설치 되지 않은 다른 종속성.
+ 지원 패키지의 다른 버전을 필요로 하는 패키지를 설치 했으며 서버 버전이 잘못 되었습니다.

## <a name="package-installation-tips"></a>패키지 설치 팁

이 섹션에서는 다양 한 팁과 SQL Server에서 R 패키지 설치와 관련 된 일반적인 질문을 제공 합니다.

###  <a name="packageVersion"></a> 올바른 패키지 버전 및 형식 가져오기

R 패키지, 특히 CRAN 및 Bioconductor 등의 여러 원본 있습니다. R 언어에 대 한 공식 사이트 (<https://www.r-project.org/>) 많은이 리소스를 나열 합니다. 많은 패키지는 소스 코드를 가져올 수 있는 GitHub에 게시 됩니다. 마지막으로 수 수 있게 된 회사의 누군가가 개발한 R 패키지가 하거나 작성 한 사용자 지정 패키지를 해야 합니다.

소스에 관계 없이 패키지를 설치 하기 전에 Windows 플랫폼에 대 한 이진 형식을 가져온를 확인 합니다. 

### <a name="bkmk_zipPreparation"></a> 패키지를 압축 된 파일로 다운로드

인터넷 연결 되지 않은 서버에서 설치에 대 한 오프 라인 설치에 대 한 압축된 된 파일 형식으로 패키지의 복사본을 다운로드 해야 합니다. **패키지를 압축을 풉니다지 않습니다.**

다음 절차의 올바른 버전을 설명 하는 예를 들어는 [FISHalyseR](http://bioconductor.org/packages/release/bioc/html/FISHalyseR.html) 패키지는 컴퓨터가 인터넷에 액세스 하는 것으로 가정 Bioconductor에서 합니다.

1.  **패키지 보관** 목록에서 **Windows 이진** 버전을 찾습니다.

2.  에 대 한 링크를 마우스 오른쪽 단추로 클릭는 합니다. ZIP 파일을 선택 **으로 대상 저장**합니다.

3.  압축 된 패키지를 저장 된와 클릭 로컬 폴더로 이동 **저장**합니다.

    이 프로세스는 패키지의 로컬 복사본을 만듭니다. 

4. 다운로드 오류가 발생 하면 다른 미러 사이트를 시도 합니다.

5. 패키지 보관을 다운로드 한 후 패키지를 설치 하거나 인터넷에 연결 하지 않은 서버에 압축된 된 패키지를 복사 수 있습니다.

> [!TIP]
> 실수로 이진 파일을 다운로드 하는 대신 패키지를 설치 하면 다운로드 된 압축된 파일의 복사본은 컴퓨터에도 저장 됩니다. 파일 위치를 확인할 패키지가 설치 되어 상태 메시지를 감시 합니다. 인터넷에 연결 하지 않은 서버에는 압축 된 파일을 복사할 수 있습니다.
> 
> 그러나이 메서드를 사용 하 여 패키지를 얻을 때 종속성 포함 되지 않습니다. 

### <a name="bkmk_packageDependencies"></a> 필수 패키지 가져오기

R 패키지는 자주 중 일부는 사용 하지 못할 인스턴스에서 사용 하는 기본 R 라이브러리에서 다른 여러 패키지에 따라 다릅니다. 경우에 따라 패키지에 이미 설치 되어 있는 종속 패키지의 다른 버전이 필요 합니다.

올바른 패키지 유형 및 버전을 갖게 조직의 모든 사용자를 또는 여러 패키지를 설치 해야 할 경우 사용 하는 것이 좋습니다는 [miniCRAN](https://mran.microsoft.com/package/miniCRAN) 전체 종속성 체인을 분석 하는 패키지입니다. minicRAN 여러 사용자 또는 컴퓨터 간에 공유할 수 있는 한 로컬 저장소를 만듭니다. 자세한 내용은 참조 [miniCRAN를 사용 하 여 로컬 패키지 리포지토리를 만들](create-a-local-package-repository-using-minicran.md)합니다.


### <a name="know-which-library-you-are-using-for-installation"></a>상위 라이브러리를 설치에 사용 하는 것을 알고 있습니다

일시 중지는 잠시 아무것도 설치 하기 전에 이전에 컴퓨터의 R 환경을 수정 하는 경우 R 환경 변수를 확인 하 고 `.libPath` 하나의 경로 사용 합니다.

이 경로 인스턴스에 대 한 R_SERVICES 폴더를 가리켜야 합니다. 자세한 내용은 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)합니다.

### <a name="side-by-side-installation-with-r-server"></a>R server-side-by-side 설치

SQL Server 컴퓨터 학습 서비스 외에도 Microsoft 컴퓨터 학습 Server (독립 실행형)를 설치한 경우 컴퓨터에 R 도구 및 라이브러리의 중복 항목을 각각에 대 한 별도 설치 R의 있어야 합니다.

R_SERVER 라이브러리에 설치 된 패키지 Microsoft R Server 에서만 사용 되 고 SQL Server에서 액세스할 수 없습니다. 사용 하 여 `R_SERVICES` SQL Server에서 사용 하려는 패키지를 설치할 때 라이브러리입니다.

### <a name="how-to-determine-which-packages-are-already-installed"></a>어떤 패키지가 이미 설치 되어 있는지 확인 하는 방법

 참조 [SQL Server와 함께 설치 된 R 패키지](installing-and-managing-r-packages.md)