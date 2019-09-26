---
title: Windows에 SQL Server Machine Learning Services (Python, R) 설치
titleSuffix: ''
description: 이 문서에서는 Windows에 SQL Server Machine Learning Services를 설치 하는 방법을 설명 합니다. Machine Learning Services를 사용 하 여 데이터베이스 내에서 Python 및 R 스크립트를 실행할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/23/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: bdd1a9e20379ae66335baa7d3c415cf68e570d47
ms.sourcegitcommit: 2f56848ec422845ee81fb84ed321a716c677aa0e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/25/2019
ms.locfileid: "71271924"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-windows"></a>Windows에 SQL Server Machine Learning Services (Python 및 R) 설치

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 Windows에 SQL Server Machine Learning Services를 설치 하는 방법을 설명 합니다. Machine Learning Services를 사용 하 여 데이터베이스 내에서 Python 및 R 스크립트를 실행할 수 있습니다.

## <a name="bkmk_prereqs"></a> 사전 설치 검사 목록

+ R 또는 Python 언어 지원으로 Machine Learning Services을 설치 하려면 SQL Server 2017 이상이 필요 합니다. SQL Server 2016 설치 미디어가 있는 경우 [SQL Server R Services (데이터베이스 내)](sql-r-services-windows-install.md) 를 설치 하 여 R 언어 지원을 받을 수 있습니다.

+ 데이터베이스 엔진 인스턴스가 필요 합니다. 기존 인스턴스에 점진적으로 추가할 수는 있지만 R 또는 Python 기능만 설치할 수는 없습니다.

+ 비즈니스 연속성을 위해 [Always On 가용성 그룹이](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) Machine Learning Services에 대해 지원 됩니다. 각 노드에서 Machine Learning Services를 설치 하 고 패키지를 구성 해야 합니다.

+ SQL Server 2017의 장애 조치 (failover) 클러스터에서는 Machine Learning Services 설치가 *지원 되지 않습니다* . 그러나 SQL Server 2019에서 *지원 됩니다* . 
 
+ 도메인 컨트롤러에 Machine Learning Services를 설치 하지 마십시오. 설치 프로그램의 Machine Learning Services 일부가 실패 하 게 됩니다.

+ 데이터베이스 내 인스턴스를 실행 하는 동일한 컴퓨터에 **공유 기능** > **Machine Learning Server (독립 실행형)을 (를)** 설치 하지 마십시오. 독립 실행형 서버는 동일한 리소스에 대해 경쟁 하며 두 설치의 성능을 모두 마이닝 합니다.

+ 다른 버전의 R 및 Python과 함께 설치할 수 있지만 권장 되지는 않습니다. SQL Server 인스턴스가 오픈 소스 R 및 Anaconda 배포의 자체 복사본을 사용 하기 때문에 지원 됩니다. 그러나 SQL Server 외부의 SQL Server 컴퓨터에서 R 및 Python을 사용 하는 코드를 실행 하면 여러 가지 문제가 발생할 수 있으므로 권장 되지 않습니다.
    
  + SQL Server에서 실행 하는 경우와 다른 라이브러리 및 다른 실행 파일을 사용 하 여 다른 결과를 얻을 수 있습니다.
  + 외부 라이브러리에서 실행 되는 R 및 Python 스크립트는 SQL Server로 관리할 수 없으며 리소스 경합이 발생할 수 있습니다.
  
> [!IMPORTANT]
> 설치가 완료되면 이 문서에서 설명하는 구성 후 단계를 완료해야 합니다. 이러한 단계에는 SQL Server에서 외부 스크립트를 사용하고 사용자 대신 R 및 Python 작업을 실행하기 위해 SQL Server에 필요한 계정을 추가하는 것이 포함됩니다. 구성을 변경하려면 일반적으로 인스턴스를 다시 시작하거나 Launchpad 서비스를 다시 시작해야 합니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2017에 대 한 설치 마법사를 시작 합니다. 
  
2. **설치** 탭에서 **새로 만들기 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 선택 합니다.

   ![새 SQL Server 독립 실행형 설치](media/2017setup-installation-page-mlsvcs.PNG)
   
3. **기능 선택** 페이지에서 다음 옵션을 선택합니다.
  
    -   **데이터베이스 엔진 서비스**
  
         SQL Server에서 R 및 Python을 사용 하려면 데이터베이스 엔진의 인스턴스를 설치 해야 합니다. 기본 또는 명명 된 인스턴스를 사용할 수 있습니다.
  
    -   **Machine Learning Services(데이터베이스 내)**
  
         이 옵션은 R 및 Python 스크립트 실행을 지 원하는 데이터베이스 서비스를 설치 합니다.

    -   **R**

        Microsoft R 패키지, 인터프리터 및 오픈 소스 R을 추가 하려면이 옵션을 선택 합니다. 

    -   **Python**

        Microsoft Python 패키지, Python 3.5 실행 파일을 추가 하 고 Anaconda 배포에서 라이브러리를 선택 하려면이 옵션을 선택 합니다.
        
        ![R 및 Python에 대 한 기능 옵션](media/2017setup-features-page-mls-rpy.png "Python에 대 한 설치 옵션")

        > [!NOTE]
        > 
        > **Machine Learning Server (독립 실행형)** 에 대 한 옵션을 선택 하지 마십시오. **공유 기능** 에 Machine Learning Server를 설치 하는 옵션은 별도의 컴퓨터에서 사용 하기 위한 것입니다.

4. **R을 설치 하는 데 동의** 페이지에서 **동의**를 선택 합니다. 이 사용권 계약은 microsoft 개발 팀의 향상 된 R 패키지 및 연결 공급자와 함께 오픈 소스 R 기본 패키지 및 도구의 배포를 포함 하는 Microsoft R Open에 대해 다룹니다.

5. **Python 설치 동의** 페이지에서 **동의**를 선택 합니다. Python 오픈 소스 라이선스 계약은 Anaconda 및 관련 도구 뿐만 아니라 Microsoft 개발 팀의 몇 가지 새로운 Python 라이브러리에 대해서도 다룹니다.
     
     ![Python 라이선스에 대 한 규약](media/2017setup-python-license.png "Python에 대 한 사용권 계약")
  
    > [!NOTE]
    >  사용 중인 컴퓨터에서 인터넷에 액세스할 수 없는 경우이 시점에서 설치 프로그램을 일시 중지 하 여 설치 관리자를 별도로 다운로드할 수 있습니다. 자세한 내용은 [인터넷에 액세스 하지 않고 machine learning 구성 요소 설치](../install/sql-ml-component-install-without-internet-access.md)를 참조 하세요.
  
     **수락**을 선택 하 고 **다음** 단추가 활성 상태가 될 때까지 기다린 후 **다음**을 선택 합니다.
  
6. **설치 준비 완료** 페이지에서 이러한 선택 항목이 포함 되어 있는지 확인 하 고 **설치**를 선택 합니다.
  
    + 데이터베이스 엔진 서비스
    + Machine Learning Services(데이터베이스 내)
    + R 또는 Python 또는 둘 다

    구성 파일이 저장 되는 경로 `..\Setup Bootstrap\Log` 아래에 있는 폴더의 위치를 적어둡니다. 설치가 완료 되 면 요약 파일에 설치 된 구성 요소를 검토할 수 있습니다.

7. 설치가 완료 되 면 컴퓨터를 다시 시작 하 라는 메시지가 표시 되 면 지금 다시 시작 합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)을 참조하세요.

## <a name="set-environment-variables"></a>환경 변수 설정

R 기능 통합의 경우에는 **MKL_CBWR** 환경 변수를 설정 하 여 Intel Mkl (Math Kernel Library) 계산과 일관 되 게 [출력 되도록](https://software.intel.com/articles/introduction-to-the-conditional-numerical-reproducibility-cnr) 해야 합니다.

1. 제어판에서 **시스템 및 보안** > **시스템** > **고급 시스템 설정** > **환경 변수**를 클릭 합니다.

2. 새 사용자 또는 시스템 변수를 만듭니다. 

  + 변수 이름 설정`MKL_CBWR`
  + 변수 값을로 설정 합니다.`AUTO`

이 단계를 수행 하려면 서버를 다시 시작 해야 합니다. 스크립트 실행을 사용 하도록 설정 하려는 경우 모든 구성 작업이 완료 될 때까지 다시 시작에 대 한 정보를 유지할 수 있습니다.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>스크립트 실행 사용

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 

    > [!TIP]
    > 이 페이지에서 적절 한 버전을 다운로드 하 여 설치할 수 있습니다. [SSMS(SQL Server Management Studio) 다운로드합니다](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
    > 
    > SQL Server에 대 한 관리 작업 및 쿼리를 지 원하는 [Azure Data Studio](../../azure-data-studio/what-is.md)를 사용할 수도 있습니다.
  
2. Machine Learning Services을 설치한 인스턴스에 연결 하 고 **새 쿼리** 를 클릭 하 여 쿼리 창을 열고 다음 명령을 실행 합니다.

    ```sql
    sp_configure
    ```

    이때 속성 값 `external scripts enabled`는 **0**이어야 합니다. 기능이 기본적으로 해제 되어 있기 때문입니다. R 또는 Python 스크립트를 실행 하려면 먼저 관리자가이 기능을 명시적으로 사용 하도록 설정 해야 합니다.
    
3.  외부 스크립팅 기능을 사용 하도록 설정 하려면 다음 문을 실행 합니다.
    
    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    R 언어에 대 한 기능을 이미 사용 하도록 설정한 경우 Python에 대해 다시 구성을 실행 하지 마세요. 기본 확장성 플랫폼은 두 언어를 모두 지원 합니다.

## <a name="restart-the-service"></a>서비스를 다시 시작합니다.

설치가 완료 되 면 다음 단계를 계속 하기 전에 데이터베이스 엔진을 다시 시작 하 여 스크립트 실행을 사용 하도록 설정 합니다.

서비스를 다시 시작 하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스도 자동으로 다시 시작 됩니다.

SSMS에서 인스턴스에 대해 마우스 오른쪽 단추 **를 클릭 하거나** 제어판의 **서비스** 패널을 사용 하거나 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)를 사용 하 여 서비스를 다시 시작할 수 있습니다.

## <a name="verify-installation"></a>설치 확인

[사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 또는 설치 로그에서 인스턴스의 설치 상태를 확인 합니다.

외부 스크립트를 시작 하는 데 사용 되는 모든 구성 요소가 실행 중인지 확인 하려면 다음 단계를 사용 합니다.

1. SQL Server Management Studio에서 새 쿼리 창을 열고 다음 명령을 실행 합니다.
    
    ```sql
    EXEC sp_configure  'external scripts enabled'
    ```

    이제 **run_value**가 1로 설정되어야 합니다.
    
2. **서비스** 패널 또는 SQL Server 구성 관리자를 열고 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 합니다. R 또는 Python이 설치 된 모든 데이터베이스 엔진 인스턴스에 대해 하나의 서비스가 있어야 합니다. 서비스에 대 한 자세한 내용은 [확장성 프레임 워크](../concepts/extensibility-framework.md)를 참조 하세요. 
   
3. 실행 패드를 실행 하는 경우 간단한 R 및 Python 스크립트를 실행 하 여 외부 스크립팅 런타임이 SQL Server와 통신할 수 있는지 확인할 수 있어야 합니다.

   에서[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]새 **쿼리** 창을 열고 다음과 같은 스크립트를 실행 합니다.
    
    + R의 경우
    
    ```sql
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Python의 경우
    
    ```sql
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    **결과**

    외부 스크립트 런타임이 처음 로드 될 때 스크립트를 실행 하는 데 약간의 시간이 걸릴 수 있습니다. 결과는 다음과 같습니다.

    | hello |
    |----|
    | 1|

> [!NOTE]
> Python 스크립트에서 사용 되는 열 또는 머리글은 의도적으로 반환 되지 않습니다. 출력에 대 한 열 이름을 추가 하려면 반환 데이터 집합에 대 한 스키마를 지정 해야 합니다. 저장 프로시저의 WITH RESULTS 매개 변수를 사용 하 여 열의 이름을 지정 하 고 SQL 데이터 형식을 지정 하 여이 작업을 수행 합니다.
> 
> 예를 들어 다음 줄을 추가 하 여 임의의 열 이름을 생성할 수 있습니다.`WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>업데이트 적용

데이터베이스 엔진과 machine learning 구성 요소 모두에 최신 누적 업데이트를 적용 하는 것이 좋습니다.

인터넷에 연결 된 장치에서 누적 업데이트는 일반적으로 Windows 업데이트를 통해 적용 되지만 제어 되는 업데이트에 대해 아래 단계를 사용할 수도 있습니다. 데이터베이스 엔진에 대 한 업데이트를 적용 하는 경우 설치 프로그램은 동일한 인스턴스에 설치 된 R 또는 Python 기능의 누적 업데이트를 가져옵니다. 

연결 되지 않은 서버에서는 추가 단계가 필요 합니다. 자세한 내용은 [인터넷 액세스가 없는 컴퓨터에 설치 > 누적 업데이트 적용](sql-ml-component-install-without-internet-access.md#apply-cu)을 참조 하세요.

1. 이미 설치 된 기본 인스턴스를 사용 하 여 시작: SQL Server 2017 초기 릴리스

2. 누적 업데이트 목록으로 이동 합니다. [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 최신 누적 업데이트를 선택 합니다. 실행 파일이 자동으로 다운로드 되 고 추출 됩니다.

4. 설치 프로그램을 실행합니다. 사용 조건에 동의 하 고 기능 선택 페이지에서 누적 업데이트가 적용 되는 기능을 검토 합니다. 기계 학습 기능을 포함 하 여 현재 인스턴스에 대해 설치 된 모든 기능이 표시 되어야 합니다. 설치 프로그램은 모든 기능을 업데이트 하는 데 필요한 CAB 파일을 다운로드 합니다.

  ![설치 된 기능 요약](media/cumulative-update-feature-selection.png)

5. R 및 Python 배포에 대 한 사용 조건에 동의 하 여 마법사를 계속 진행 합니다. 

## <a name="additional-configuration"></a>기타 고려 사항

외부 스크립트 확인 단계가 성공한 경우 SQL Server Management Studio, Visual Studio Code 또는 T-sql 문을 서버에 보낼 수 있는 다른 모든 클라이언트에서 R 또는 Python 명령을 실행할 수 있습니다.

명령을 실행할 때 오류가 발생 하는 경우이 섹션의 추가 구성 단계를 검토 합니다. 서비스 또는 데이터베이스에 적절 한 구성을 추가로 만들어야 할 수도 있습니다.

인스턴스 수준에서 추가 구성에는 다음이 포함 될 수 있습니다.

* [SQL Server Machine Learning Services에 대 한 방화벽 구성](../../advanced-analytics/security/firewall-configuration.md)
* [추가 네트워크 프로토콜 사용](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [원격 연결 사용](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [SQLRUserGroup에 대 한 로그인 만들기](../../advanced-analytics/security/create-a-login-for-sqlrusergroup.md)
* 디스크 공간을 확보 하는 작업을 실행 하는 외부 스크립트를 방지 하는 [디스크 할당량 관리](https://docs.microsoft.com/windows/desktop/fileio/managing-disk-quotas)

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
Windows의 SQL Server 2019에서는 격리 메커니즘이 변경 되었습니다. 이는 **SQLRUserGroup**, 방화벽 규칙, 파일 사용 권한 및 묵시적 인증에 영향을 줍니다. 자세한 내용은 [Machine Learning Services에 대 한 격리 변경 내용](sql-server-machine-learning-services-2019.md)을 참조 하세요.
::: moniker-end

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

데이터베이스에서 다음 구성 업데이트가 필요할 수 있습니다.

* [사용자에 게 SQL Server Machine Learning Services 사용 권한 부여](../../advanced-analytics/security/user-permission.md)

> [!NOTE]
> 추가 구성이 필요한 지 여부는 SQL Server 설치 된 보안 스키마와 사용자가 데이터베이스에 연결 하 여 외부 스크립트를 실행 하는 방법을 결정 합니다.

## <a name="suggested-optimizations"></a>제안 된 최적화

모든 작업을 수행 했으므로 이제 기계 학습을 지원 하도록 서버를 최적화 하거나 미리 학습 된 모델을 설치할 수도 있습니다.

::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
### <a name="add-more-worker-accounts"></a>작업자 계정 추가

많은 사용자가 스크립트를 동시에 실행 하는 것으로 간주 되는 경우 실행 패드 서비스에 할당 된 작업자 계정 수를 늘릴 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services 사용자 계정 풀 수정](../administration/modify-user-account-pool.md)을 참조 하세요.
::: moniker-end

### <a name="optimize-the-server-for-script-execution"></a>스크립트 실행을 위해 서버 최적화

설치 프로그램에 대 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 한 기본 설정은 데이터베이스 엔진에서 지원 되는 다양 한 서비스에 대 한 서버의 균형을 최적화 하기 위한 것입니다. 여기에는 ETL (추출, 변환 및 로드) 프로세스, 보고, 감사 및이 포함 될 수 있습니다. 데이터를 사용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하는 응용 프로그램입니다. 따라서 기본 설정에 따라 특히 메모리를 많이 사용 하는 작업에서 기계 학습에 대 한 리소스가 제한 되거나 제한 되는 것을 알 수 있습니다.

Machine learning 작업의 우선 순위를 지정 하 고 리소스를 적절 하 게 지정 하려면 SQL Server Resource Governor를 사용 하 여 외부 리소스 풀을 구성 하는 것이 좋습니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에 할당 된 메모리 양을 변경 하거나 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스에서 실행 되는 계정 수를 늘릴 수 있습니다.

- 외부 리소스 관리를 위해 리소스 풀을 구성 하려면 [외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)를 참조 하세요.
  
- 데이터베이스에 예약 된 메모리 양을 변경 하려면 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)을 참조 하세요.
  
- 에서 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]시작할 수 있는 R 계정 수를 변경 하려면 [machine learning에 대 한 사용자 계정 풀 수정](../administration/modify-user-account-pool.md)을 참조 하세요.

Standard Edition을 사용 중이 고 Resource Governor 없는 경우 Dmv (동적 관리 뷰) 및 확장 이벤트 뿐만 아니라 Windows 이벤트 모니터링을 사용 하 여 서버 리소스를 쉽게 관리할 수 있습니다. 자세한 내용은 [R Services 모니터링 및 관리](../r/managing-and-monitoring-r-solutions.md) 및 [Python 서비스 모니터링 및 관리](../python/managing-and-monitoring-python-solutions.md)를 참조 하세요.

### <a name="install-additional-r-packages"></a>추가 R 패키지 설치

SQL Server에 대해 만드는 R 솔루션은 기본 R 함수, SQL Server 설치 된 소유 패키지의 함수 및 SQL Server에서 설치한 오픈 소스 R 버전과 호환 되는 타사 R 패키지를 호출할 수 있습니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에 R을 별도로 설치 하거나 사용자 라이브러리에 패키지를 설치한 경우 T-sql에서 해당 패키지를 사용할 수 없습니다.

R 패키지를 설치 하 고 관리 하려면 사용자 그룹을 설정 하 여 데이터베이스 수준에서 패키지를 공유 하거나 사용자가 자신의 패키지를 설치할 수 있도록 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 [SQL Server에 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)를 참조 하세요.

## <a name="next-steps"></a>다음 단계

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [자습서: T-SQL에서 R 사용](../tutorials/quickstart-r-create-script.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [자습서: Python 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)를 참조하세요.
