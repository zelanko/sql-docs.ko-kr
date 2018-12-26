---
title: SQL Server Machine Learning Services (In-database) Windows에서 설치 | Microsoft Docs
description: SQL Server 또는 SQL Server의 Python에는 R은 Windows에서 SQL Server 2017의 Machine Learning Services를 설치할 때 사용할 수입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/01/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 7f96c2acbca436ff18ccb6a12421d84bda965e4d
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878096"
---
# <a name="install-sql-server-machine-learning-services-on-windows"></a>Windows에 SQL Server Machine Learning를 설치합니다.
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017부터 R 및 Python의 데이터베이스 내 분석은 SQL Server 2016에서 소개된 [SQL Server R Services](../r/sql-server-r-services.md) 의 후속 제품인 SQL Server Machine Learning 서비스에서 제공됩니다. 함수 라이브러리는 R 및 Python에서 사용할 수 있으며 데이터베이스 엔진 인스턴스에서 외부 스크립트로 실행할 수 있습니다.

이 문서에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 실행하고 화면의 지시에 따라 머신 러닝 구성 요소를 설치하는 방법을 설명합니다.

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

+ R, Python 또는 Java 언어 지원을 사용 하 여 Machine Learning 서비스를 설치 하려면 SQL Server 2017 (또는 그 이상) 설치가 필요 합니다. 대신 SQL Server 2016 설치 미디어가 있는 경우 설치할 수 있습니다 [SQL Server 2016 R Services (In-database)](sql-r-services-windows-install.md) R 언어 지원을 받을 수 있습니다.

+ 데이터베이스 엔진 인스턴스를 반드시 입력 해야 합니다. 기존 인스턴스를 증분 방식으로 추가할 수는 있지만 방금 R 또는 Python 기능을 설치할 수 없습니다.

- Machine Learning Services를 설치 *지원 되지 않습니다* SQL Server 2017에서 장애 조치 클러스터입니다. 그러나 그 *는* SQL Server 2019를 사용 하 여 합니다. 
 
+ 도메인 컨트롤러에서 Machine Learning 서비스를 설치 하지 마세요. Machine Learning 서비스에 대 한 부분 설치 하지 못합니다.

+ 설치 하지 마세요 **공유 기능** > **Machine Learning Server (독립 실행형)** 컴퓨터의 동일한 데이터베이스 내 인스턴스를 실행 합니다. 독립 실행형 서버 설치 둘 다의 성능을 저해 하면서 같은 리소스를 경합 합니다.

+ 다른 버전의 R 및 Python을 사용 하 여 side-by-side-설치는 지원 되지만 권장 하지 않습니다. SQL Server 인스턴스는 오픈 소스 R 및 Anaconda 배포의 자체 복사본을 사용 하기 때문에 지원 됩니다. 하지만 다양 한 문제가 발생할 수 있습니다 SQL Server 외부 SQL Server 컴퓨터의 R 및 Python을 사용 하는 코드를 실행 하기 때문에 권장 되지 않습니다.
    
  + 다른 실행 파일을 다른 라이브러리를 사용 하 고 SQL Server에서 실행 하는 경우 보다 서로 다른 결과 가져옵니다.
  + 리소스 경합을 SQL Server에서 외부 라이브러리에서 실행 되는 R 및 Python 스크립트를 관리할 수 없습니다.
  
> [!IMPORTANT]
> 설치가 완료되면 이 문서에서 설명하는 구성 후 단계를 완료해야 합니다. 이러한 단계에는 SQL Server에서 외부 스크립트를 사용하고 사용자 대신 R 및 Python 작업을 실행하기 위해 SQL Server에 필요한 계정을 추가하는 것이 포함됩니다. 구성을 변경하려면 일반적으로 인스턴스를 다시 시작하거나 Launchpad 서비스를 다시 시작해야 합니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2017 설치 마법사를 시작 합니다. 다운로드할 수 있습니다. 
  
2. 에 **설치** 탭을 선택 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.

   ![Machine Learning Services in-database 설치](media/2017setup-installation-page-mlsvcs.PNG)
   
3. **기능 선택** 페이지에서 다음 옵션을 선택합니다.
  
    -   **데이터베이스 엔진 서비스**
  
         SQL Server에서 R 및 Python 사용 하려면 데이터베이스 엔진의 인스턴스를 설치 해야 합니다. 기본 또는 명명된 된 인스턴스 중 하나를 사용할 수 있습니다.
  
    -   **Machine Learning Services(데이터베이스 내)**
  
         이 옵션은 R을 지원 되는 데이터베이스 서비스를 설치 및 Python 스크립트 실행 합니다.

    -   **R**

        Microsoft R 패키지, 인터프리터 및 오픈 소스 R을 추가 하려면이 옵션을 선택 

    -   **Python**

        Python 3.5 실행 파일을 Microsoft Python 패키지를 추가 하려면이 옵션을 선택 하 고 Anaconda 배포에서 라이브러리를 선택 합니다.
        
        ![R 및 Python에 대 한 옵션 기능](media/2017setup-features-page-mls-rpy.png "Python에 대 한 옵션 설정")

        > [!NOTE]
        > 
        > 에 대 한 옵션을 선택 하지 마세요 **Machine Learning Server (독립 실행형)** 합니다. 아래에서 Machine Learning Server를 설치 하는 옵션이 **공유 기능** 별도 컴퓨터에서 사용 됩니다.

4. 에 **R 설치에 동의** 페이지에서 **Accept**합니다. 이 사용권 계약에서는 Microsoft R Open, 도구, Microsoft 개발 팀의 연결 공급자 및 고급 R 패키지와 함께 확인 하 고 오픈 소스 R 기본 패키지의 배포를 포함 하는 설명 합니다.

5. 에 **python 설치 동의** 페이지에서 **Accept**합니다. Python 오픈 소스 라이선스 규약 Anaconda와 관련된 도구, Microsoft 개발 팀에서 몇 가지 새로운 Python 라이브러리에 대해서도 다룹니다.
     
     ![Python 사용권 계약이](media/2017setup-python-license.png "Python에 대 한 계약을 라이선스")
  
    > [!NOTE]
    >  사용 중인 컴퓨터가 인터넷에 없는 경우에이 시점에서 설치 관리자를 별도로 다운로드 하려면 설치 프로그램을 중지할 수 있습니다. 자세한 내용은 [인터넷에 액세스 하지 않고 기계 학습 구성 요소 설치](../install/sql-ml-component-install-without-internet-access.md)합니다.
  
     선택 **Accept**, 될 때까지 대기 합니다 **다음** 버튼 활성 및 선택한 후 **다음**.
  
6. 에 **설치할 준비가** 페이지에서 이러한 선택 항목에 포함 되는지 확인 선택한 **설치**합니다.
  
    + 데이터베이스 엔진 서비스
    + Machine Learning Services(데이터베이스 내)
    + R 또는 Python

    경로 아래에 있는 폴더의 위치를 기록 `..\Setup Bootstrap\Log` 구성 파일이 저장 됩니다. 설치가 완료 되 면 요약 파일에 설치 된 구성 요소를 검토할 수 있습니다.

7. 설치가 완료 되 면 컴퓨터를 다시 시작 하 라는 메시지가 표시 되는 경우 지금 합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)을 참조하세요.

<a name="bkmk_enableFeature"></a>

## <a name="enable-script-execution"></a>스크립트 실행 활성화

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 

    > [!TIP]
    > 다운로드 하 고이 페이지에서 적절 한 버전을 설치할 수 있습니다: [SQL Server Management Studio (SSMS 다운로드)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.
    > 
    > 미리 보기 릴리스도 사용할 수 있는 [Azure Data Studio](../../azure-data-studio/what-is.md), 관리 작업 및 SQL Server에 대 한 쿼리를 지 합니다.
  
2. Machine Learning 서비스를 설치한 인스턴스에 연결, 클릭 **새 쿼리** 쿼리 창을 열고 다음 명령을 실행 합니다.

   ```SQL
   sp_configure
   ```

    이때 속성 값 `external scripts enabled`는 **0**이어야 합니다. 기능을 기본적으로 해제 되어 있으므로입니다. R 또는 Python 스크립트를 실행 하기 전에 기능 관리자가 명시적으로 설정 해야 합니다.
    
3.  외부 스크립팅 기능을 사용 하려면 다음 문을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    R 언어에 대 한 기능을 이미 설정한 경우 ě Python에 대 한 두 번째 시간을 다시 구성 합니다. 기본 확장성 플랫폼 두 언어를 지원합니다.

## <a name="restart-the-service"></a>서비스를 다시 시작합니다.

설치가 완료 되 면, 다음 스크립트 실행을 사용 하도록 설정 하기 전에 데이터베이스 엔진을 다시 시작 합니다.

관련 된 다시 시작 서비스를 자동으로 다시 시작 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

마우스를 사용 하 여 서비스를 다시 시작할 수 있습니다 **다시 시작** SSMS에서 또는 사용 하 여 인스턴스에 대 한 명령을 합니다 **Services** 제어판 또는 사용 하 여 패널 [SQL Server 구성 관리자 ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>설치 확인

인스턴스의 설치 상태를 확인 [사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md) 또는 로그를 설치 합니다.

외부 스크립트를 실행 하는 데 사용 하는 모든 구성 요소가 실행 되 고 있는지 확인 하려면 다음 단계를 사용 합니다.

1. SQL Server Management studio에서 새 쿼리 창을 열고 다음 명령을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    이제 **run_value**가 1로 설정되어야 합니다.
    
2. 열기는 **서비스** 패널 또는 SQL Server 구성 관리자를 확인 하 고 **SQL Server 실행 패드 서비스** 실행. R에 있는 모든 데이터베이스 엔진 인스턴스에 대해 하나의 서비스 해야 하거나 Python 설치 합니다. 서비스에 대 한 자세한 내용은 참조 하세요. [Extensibility framework](../concepts/extensibility-framework.md)합니다. 
   
3. 실행 패드를 실행 하는 경우 외부 스크립팅 런타임을 SQL Server와 통신할 수 있는지 확인 하려면 간단한 R 및 Python 스크립트를 실행할 수 있어야 합니다.

   새 **쿼리** 창에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 다음과 같은 스크립트를 실행 하 고:
    
    + R에 대 한
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    + Python 용
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'
    OutputDataSet = InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

 **결과**

    스크립트를 처음으로 실행 하려면 외부 스크립트 런타임에 로드 되는 동안 잠시 걸릴 수 있습니다. 결과 다음과 같이 해야 합니다.

    | hello |
    |----|
    | 1|


> [!NOTE]
> 열 또는 Python 스크립트에서 사용 되는 머리글 반환 되지 않습니다 기본적입니다. 출력 열 이름에 추가 하려면 반환 된 데이터 집합에 대 한 스키마를 지정 해야 합니다. 이 작업을 수행 하 여의 열 명명 및 SQL 데이터 형식을 지정 하는 저장된 프로시저를 사용 하 여 결과 매개 변수를 사용 합니다.
> 
> 예를 들어는 임의의 열 이름을 생성 하려면 다음 줄을 추가할 수 있습니다. `WITH RESULT SETS ((Col1 AS int))`

<a name="apply-cu"></a>

## <a name="apply-updates"></a>업데이트를 적용 합니다.

데이터베이스 엔진 및 기계 학습 구성 요소 모두에 최신 누적 업데이트를 적용 하는 것이 좋습니다.

인터넷에 연결 된 장치에서 누적 업데이트는 Windows Update를 통해 일반적으로 적용 됩니다 있지만 제어 되는 업데이트에 대 한 아래 단계를 사용할 수도 있습니다. 데이터베이스 엔진에 대 한 업데이트를 적용 하면 설치는 동일한 인스턴스를 설치한 모든 R 또는 Python 기능에 대 한 누적 업데이트를 가져옵니다. 

연결이 끊어진된 서버에 추가 단계가 필요 합니다. 자세한 내용은 [인터넷 액세스 없이 컴퓨터에 설치 > 누적 업데이트를 적용할](sql-ml-component-install-without-internet-access.md#apply-cu)합니다.

1. 이미 설치 된 기본 인스턴스를 시작 합니다: SQL Server 2017 초기 릴리스

2. 누적 업데이트 목록으로 이동: [SQL Server 2017 업데이트](https://sqlserverupdates.com/sql-server-2017-updates/)

3. 최신 누적 업데이트를 선택 합니다. 실행 파일 다운로드 되어 자동으로 추출 합니다.

4. 설치 프로그램을 실행합니다. 라이선스 조건에 동의 하 고 기능 선택 페이지의 누적 업데이트 적용 되는 기능을 검토 합니다. Machine learning 기능을 포함 하 여 현재 인스턴스에 대해 설치 된 모든 기능에 표시 됩니다. 모든 기능을 업데이트 하는 데 필요한 CAB 파일이 다운로드 됩니다.

  ![](media/cumulative-update-feature-selection.png)

5. R 및 Python 배포에 대 한 라이선스 조건에 동의 하 여 마법사를 진행 합니다. 

## <a name="additional-configuration"></a>기타 고려 사항

외부 스크립트 확인 단계를 성공적으로 수행 되었으면 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 R 또는 Python 명령을 실행할 수 있습니다.

명령을 실행할 때 오류가 발생 하면이 섹션의 추가 구성 단계를 검토 합니다. 서비스 또는 데이터베이스에 추가 적절 한 구성을 확인 해야 합니다.

인스턴스 수준에서 추가 구성이 포함 될 수 있습니다.

* [SQL Server Machine Learning Services에 대 한 방화벽 구성](../../advanced-analytics/security/firewall-configuration.md)
* [추가 네트워크 프로토콜을 사용 하도록 설정](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [원격 연결을 사용 하도록 설정](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)

<a name="bkmk_configureAccounts"></a> 
<a name="permissions-external-script"></a> 

데이터베이스에서 다음 구성을 업데이트 해야 합니다.

* [SQL Server Machine Learning Services 하도록 사용자 권한 부여](../../advanced-analytics/security/user-permission.md)
* [SQLRUserGroup을 데이터베이스 사용자로 추가](../../advanced-analytics/security/add-sqlrusergroup-to-database.md)

> [!NOTE]
> 추가 구성이 필요한 지 여부를 보안 스키마를 설치한 SQL Server 및 데이터베이스에 연결 하 여 외부 스크립트를 실행 하는 사용자를 예상 하는 방법에 따라 달라 집니다.

## <a name="suggested-optimizations"></a>제안 된 최적화

모든 작업을 수행 해야 했으므로 기계 학습을 지원 하도록 서버를 최적화할 수도 있습니다 또는 미리 학습 된 모델 설치 합니다.

### <a name="add-more-worker-accounts"></a>더 많은 작업자 계정을 추가 합니다.

스크립트를 동시에 실행 하 여 많은 사용자를 예상 하는 경우에 실행 패드 서비스에 할당 된 작업자 계정 수를 늘릴 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에 대 한 사용자 계정 풀 수정](../administration/modify-user-account-pool.md)합니다.

### <a name="optimize-the-server-for-script-execution"></a>스크립트 실행에 대 한 서버를 최적화 합니다.

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다양 한 추출, 변환 및 로드 (ETL) 프로세스를 보고, 감사에 포함 될 수 있는 데이터베이스 엔진에 의해 지원 되는 서비스에 대 한 서버의 균형을 최적화 하려는 설치 하 고 사용 하는 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다. 따라서 기본 설정에서 machine learning 위한 리소스는 경우에 따라 제한 또는 제한, 특히 메모리 사용량이 많은 작업을 찾을 수 있습니다.

Machine learning 작업 우선 순위와 정보를 적절 하 게 되도록 SQL Server 리소스 관리자를 사용 하 여 외부 리소스 풀을 구성 하는 것이 좋습니다. 에 할당 된 메모리 양을 변경할 수도 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 되는 계정의 수를 늘리거나 데이터베이스 엔진는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

- 외부 리소스를 관리 하기 위한 리소스 풀을 구성 하려면 참조 [외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)합니다.
  
- 데이터베이스에 대해 예약 된 메모리 양을 변경 하려면 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)합니다.
  
- 가 시작할 수 있는 R 계정의 수를 변경 하려면 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]를 참조 하세요 [machine learning 위한 사용자 계정 풀 수정](../administration/modify-user-account-pool.md)합니다.

Standard Edition을 사용 하는 리소스 관리자가 없는 경우 동적 관리 뷰 (Dmv) 및 확장 이벤트 뿐만 아니라 Windows 이벤트 모니터링, 서버 리소스를 관리 하는 데 사용할 수 있습니다. 자세한 내용은 참조 하세요. [모니터링 및 R Services를 관리](../r/managing-and-monitoring-r-solutions.md) 하 고 [모니터링 서비스 및 관리 Python](../python/managing-and-monitoring-python-solutions.md)합니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지 설치

SQL Server에 대 한 만든 R 솔루션은 기본 R 함수, 타사 R 패키지 및 SQL Server와 함께 설치 되는 전용 패키지에서 함수를 SQL Server로 설치 하는 오픈 소스 R의 버전과 호환으로 호출할 수 있습니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에서 R의 별도 설치를 수행한 경우, 사용자 라이브러리에 패키지를 설치한 경우에 T-SQL에서 해당 패키지를 사용할 수 없습니다.

R 패키지 설치 및 관리에 대 한 프로세스는 SQL Server 2016 및 SQL Server 2017에서 다릅니다. SQL Server 2016에서 데이터베이스 관리자는 사용자에 게 필요한 R 패키지를 설치 해야 합니다. SQL Server 2017에서 데이터베이스별 수준에서 패키지를 공유 하도록 사용자 그룹을 설정할 수도 있고 사용자가 자신의 패키지를 설치할 수 있도록 하려면 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 [SQL Server에서 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.


## <a name="next-steps"></a>다음 단계

R 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 R을 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: T-SQL에서 R 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 이러한 자습서를 수행 하 여 SQL Server를 사용 하 여 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: t-sql로 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.
