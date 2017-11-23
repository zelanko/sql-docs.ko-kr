---
title: "설정 및 Python 컴퓨터 학습 서비스에 대 한 구성 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: e3142bcf06fa2ed88ead730d0cc127cf41cfde56
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="set-up-python-machine-learning-services-in-database"></a>Python 컴퓨터 학습 Services (In-database) 설치

  실행 하 여 Python에 대 한 필수 구성 요소를 설치는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 고이 항목에 설명 된 대로 대화형 프롬프트를 따릅니다.

## <a name="machine-learning-options-in-sql-server-setup"></a>기계 학습에서 SQL Server 설치 옵션

선택 된 **컴퓨터 학습 서비스** 기능을 사용 하 고 선택 **Python** 언어로 합니다.

**공유 기능** 섹션에는 별도 설치 옵션이 포함 되어 **학습 Server 컴퓨터 (독립 실행형)**합니다. 이 옵션은 서버 변수가 없는 SQL Server 또는 SQL Server 계산 컨텍스트를 사용 하 여 필요 없는 해결해줍니다 Python 코드의를 지원 합니다. 따라서 것을 권장 합니다 있습니다 *없는* 이 SQL Server 인스턴스와 동일한 컴퓨터에 설치 합니다. 대신 별도 컴퓨터에 학습 Server 컴퓨터 (독립 실행형)를 설치 합니다.

설치가 완료 된 후에 외부 실행 파일을 사용 하는 스크립트의 실행을 허용 하도록 인스턴스를 다시 구성 합니다. 컴퓨터 학습 작업을 지원 하려면 서버에 대 한 추가 변경을 해야 할 수 있습니다. 구성 변경에는 일반적으로 인스턴스를 다시 시작 또는 실행 패드 서비스를 다시 시작 해야합니다.

### <a name="prerequisites"></a>필수 구성 요소

+ SQL Server 2017가 필요 합니다. Python 통합 이전 버전의 SQL Server에서 지원 되지 않습니다.
+ 데이터베이스 엔진을 설치 해야 합니다. SQL Server 인스턴스의 데이터베이스에서 Python 스크립트를 실행 하려면 필요 합니다.
+ 필수 구성 요소는 Python 구성 요소 설치의 일부로 설치 됩니다.
+ 기계 학습 Python 서비스 장애 조치 클러스터에 설치할 수 없습니다. Python 프로세스를 격리 하기 위해 사용 되는 보안 메커니즘 Windows Server 장애 조치 클러스터 환경와 호환 되지 않습니다.
   
  이 문제를 해결 Python 서비스를 사용 하는 독립 실행형 SQL Server 인스턴스에 필요한 테이블을 복사할 복제를 사용할 수 있습니다. 또는 기계 학습 Python AlwaysOn 설정을 사용 하 고 가용성 그룹의 일부는 독립 실행형 컴퓨터에는 서비스와 함께 설치할 수 있습니다.

+ Python의 다른 버전과 함께 설치 하 여 병렬이 SQL Server 인스턴스 Anaconda 배포의 자체 복사본을 사용 하기 때문에 가능 합니다. 그러나 SQL Server 외부 SQL Server 컴퓨터에 Python을 사용 하는 코드를 실행 중인 다양 한 문제가 발생할 수 있습니다.
    + 다른 라이브러리와 다른 실행 파일이 사용 및 SQL Server에서 실행 하는 때 보다 서로 다른 결과 가져옵니다.
    + Python 스크립트 외부 라이브러리에서 실행 중인 SQL server에 리소스 경합을 관리할 수 없습니다.
  
> [!IMPORTANT]
> 설치가 완료 된 후에이 항목에 설명 된 추가 구성 후 단계를 완료 해야 합니다. 여기에 SQL Server 외부 스크립트를 사용 하도록 설정 및 계정에서 사용자 대신 Python 작업을 실행 하는 SQL Server에 필요한 추가 됩니다.

### <a name="unattended-installation"></a>무인된 설치

무인된 설치를 수행 하려면 SQL Server 설치 프로그램 및 Python 특정 인수에 대 한 명령줄 옵션을 사용 합니다. 자세한 내용은 참조 [Unattended Python 컴퓨터 학습 서비스를 사용 하 여 SQL server 설치](unattended-installs-of-sql-server-python-services.md)합니다.

##  <a name="bkmk_installPythonInDatabase"></a>1 단계: 기계 학습에서 SQL Server Services (In-database) 설치

1. SQL Server 2017에 대 한 설치 마법사를 실행 합니다.
  
2. 에 **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.

    ![데이터베이스에서 Python 설치](media/2017setup-installation-page-mlsvcs.PNG)
   
3. **기능 선택** 페이지에서 다음 옵션을 선택합니다.
  
    -   **데이터베이스 엔진 서비스**
  
         Python에서 SQL Server를 사용 하려면 데이터베이스 엔진의 인스턴스를 설치 해야 합니다. 기본 인스턴스나 명명 된 인스턴스를 사용할 수 있습니다.
  
    -   **기계 학습 Services (In-database)**
  
         이 옵션에서는 Python 스크립트 실행을 지 원하는 데이터베이스 서비스를 설치 합니다.

    -   **Python** Python 3.5 실행 파일을 가져오고 Anaconda 배포에서 라이브러리를 선택 하려면이 옵션을 선택 합니다. 인스턴스당 하나의 언어를 설치 합니다.
        
        ![Python에 대 한 옵션 기능](media/ml-svcs-features-python-highlight.png "Python에 대 한 옵션 설정")

        > [!NOTE]
        > 
        > 에 대 한 옵션을 선택 하지 않으면 **학습 Server 컴퓨터 (독립 실행형)**합니다. 컴퓨터 학습 서버를 설치 하는 옵션 **공유 기능** 별도 컴퓨터에 사용 됩니다. 예를 들어 다음 동일한 버전의 기계 학습 데이터 과학자의 랩톱 등의 프로젝트 개발에 사용 되는 다른 컴퓨터에 구성 요소를 설치 하는 것이 좋습니다.

4. 에 **Python 설치에 동의** 페이지에서 **Accept**합니다.
  
     이 사용권 계약은 실행 파일인 Python Anaconda에서 Python 패키지를 다운로드 해야 합니다.
     
     ![Python 라이선스 계약](media/ml-svcs-license-python.png "Python에 대 한 계약을 라이선스")
  
    > [!NOTE]
    >  사용 중인 컴퓨터에 인터넷에 연결 하는 경우 설치 관리자를 별도로 다운로드 하도록이 시점에서 일시 중지할 수 있습니다. 자세한 내용은 참조 [인터넷 연결 되지 않은 구성 요소 설치](../r/installing-ml-components-without-internet-access.md)합니다.
  
     선택 **Accept**, 될 때까지 기다렸다가 **다음** 단추가 활성화 되며 선택 **다음**합니다.
  
5. 에 **설치 준비 완료** 페이지에서 이러한 선택 항목에 포함 되어 있는지 확인 하 고 선택 **설치**합니다.
  
     + 데이터베이스 엔진 서비스
     + Machine Learning Services(데이터베이스 내)
     + Python
  
    이러한 선택 항목으로 Python을 사용 하는 데 필요한 최소 구성을 나타냅니다 [!INCLUDE[ssnoversion](../../includes/ssnoversion.md)]합니다.
    
    ![Python 설치 준비 완료](media/ready-to-install-python.png "Python 설치에 대 한 필수 구성 요소")

    필요에 따라 경로 아래에 있는 폴더의 위치를 기록해 `..\Setup Bootstrap\Log` 구성 파일이 저장 됩니다. 설치가 완료 되 면 요약 파일에서 설치 된 구성 요소를 검토할 수 있습니다.

6. 설치가 완료되면 컴퓨터를 다시 시작합니다.

##  <a name="bkmk_enableFeature"></a>2 단계: Python 스크립트 실행을 사용 하도록 설정

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 아직 설치 되지 않은 경우 다운로드 링크를 열도록 하 고 설치를 다시 SQL Server 설치 마법사를 실행할 수 있습니다.
  
2. 컴퓨터 학습 서비스를 설치한 인스턴스에 연결 하 고 다음 명령을 실행 합니다.

   ```SQL
   sp_configure
   ```

    이때 속성 값 `external scripts enabled`는 **0**이어야 합니다. 기본적으로는 기능이 꺼져 때문입니다. Python 또는 R 스크립트를 실행 하기 전에 기능 관리자가 명시적으로 활성화 해야 합니다.
    
3.  외부 스크립팅 기능을 지 원하는 Python을 사용 하도록 설정 하려면 다음 문을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    R 언어에 대 한 기능을 이미 사용 하는 경우 실행할 필요가 없습니다 Python에 대 한를 두 번째로 다시 구성 합니다. 기본 확장성 플랫폼 언어를 모두 지원 합니다.

4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 SQL Server 서비스를 다시 시작합니다. SQL Server 서비스가 자동으로 다시 시작 하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

    사용 하 여 서비스를 다시 시작할 수는 **서비스** 제어판에서 또는 사용 하 여 패널 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)합니다.

## <a name="step-3-verify-that-the-external-script-execution-feature-is-running"></a>3 단계: 외부 스크립트 실행 기능 실행 되 고 있는지 확인 하십시오.

잠시 Python 스크립트를 실행 하는 데 사용 하는 모든 구성 요소가 실행 되 고 있는지 확인 합니다.

1. SQL Server Management Studio에서 새 쿼리 창을 열고 다음 명령을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    이제 **run_value**가 1로 설정되어야 합니다.
    
2. 열기는 **서비스** 패널 또는 SQL Server 구성 관리자는 실행 패드 서비스 인스턴스에 대 한 실행 되 고 있는지 확인 합니다. 실행 패드를 실행 하지 않는 경우 서비스를 다시 시작 합니다.
  
    SQL Server의 여러 인스턴스를 설치한 경우 사용 하도록 설정 하는 Python 또는 R 권한이 있는 모든 인스턴스는 실행 패드 서비스는 자체에 있습니다.

    단일 인스턴스에서 모두 R 및 Python을 설치 하는 경우에 하나의 실행 패드 설치 됩니다. 각 언어에 대 한 별도, 언어별 launcher DLL 추가 됩니다. 자세한 내용은 참조 [Python의 통합을 지원 하려면 구성 요소가](new-components-in-sql-server-to-support-python-integration.md)합니다. 
   
3. 다음과 같은 간단한 Python 스크립트를 실행할 수 있어야 실행 패드를 실행 중인 경우 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'Python',
    @script=N'OutputDataSet = InputDataSet',
    @input_data_1 = N'SELECT 1 AS col'
    ```
    
    **결과**
    
    *<code>&nbsp;&nbsp;</code>* *1*

> [!NOTE]
> 열 또는 Python 스크립트에 사용 되는 머리글은을 반환 하지를 디자인 합니다. 출력에 대 한 열 이름을 추가 하려면 반환 된 데이터 집합에 대 한 스키마를 지정 해야 합니다. 이 작업을 수행 하 여 열 이름을 지정 하 고 SQL 데이터 형식 지정, 저장된 프로시저의 결과와 매개 변수를 사용 합니다.
> 
> 예를 들어 임의의 열 이름을 생성 하려면 다음 줄을 추가할 수 있습니다.`WITH RESULT SETS ((Col1 AS int))`

## <a name="step-4-additional-configuration"></a>4 단계: 추가 구성

이전 명령이 성공 하면 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 Python 명령을 실행할 수 있습니다.

오류가 발생 하면 명령을 실행할 때, 경우에 다음 목록을 검토 합니다. 서비스 또는 데이터베이스에 적절 한 구성 작업 추가 수행 해야 합니다.

> [!NOTE]
> 
> 나열 된 모든 변경 내용이 필요 하 고 none 필요할 수 있습니다. 요구 사항은 보안 스키마를 설치한 SQL Server 및 데이터베이스에 연결 하 고 외부 스크립트를 실행 하는 사용자를 예상 하는 방법에 따라 달라 집니다.

###  <a name="bkmk_configureAccounts"></a>실행 패드 계정 그룹에 대 한 묵시적된 인증을 사용 하도록 설정

설치하는 동안 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스의 보안 토큰으로 태스크를 실행하기 위해 많은 새 Windows 사용자 계정이 생성됩니다. 외부 클라이언트에서 Python 또는 R 스크립트를 보낼 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 가능한 작업자 계정을 활성화 합니다. 다음 호출 하는 사용자의 id로 매핑합니다 하 고 사용자를 대신 하 여 스크립트를 실행 합니다.

라고 *암시 된 인증이*, 며 데이터베이스 엔진의 서비스입니다. 이 서비스는 SQL Server 2016 및 SQL Server 2017의 외부 스크립트의 보안 실행을 지원합니다.

Windows 사용자 그룹 **SQLRUserGroup**에서 해당 계정을 볼 수 있습니다. 기본적으로 외부 스크립트 실행을 위한 충분 한 더 많은 작업은 일반적으로 20 작업자 계정이 생성 됩니다.

> [!IMPORTANT]
> 작업자 그룹 이름은 **SQLRUserGroup** R, Python 설치 여부에 관계 없이 합니다. 각 인스턴스에 대 한 단일 그룹이 됩니다.

원격 데이터 과학 클라이언트에서 스크립트를 실행 해야 하는 경우 Windows 인증을 사용 하는 추가 고려 사항 사항이 있습니다. 이러한 작업자 계정 로그인 할 사용 권한이 부여 해야는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 대신 인스턴스.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]개체 탐색기에서 확장 **보안**합니다. 마우스 오른쪽 단추로 클릭 한 다음 **로그인**를 선택 하 고 **새 로그인**합니다.
2. 에 **로그인-신규** 대화 상자에서 **검색**합니다.
3. 선택 **개체 유형**를 선택 하 고 **그룹**합니다. 다른 모든 항목의 선택을 취소 합니다.
4. **선택할 개체 이름을 입력**, 형식 *SQLRUserGroup*를 선택 하 고 **이름 확인**합니다.
5. 인스턴스의 실행 패드 서비스와 연결된 로컬 그룹의 이름이 *instancename\SQLRUserGroup*과 같은 이름으로 확인되어야 합니다. **확인**을 선택합니다.
6. 기본적으로 그룹에 할당 된 **공용** 역할을 데이터베이스 엔진에 연결할 수 있는 권한이 있으며 합니다.
7. **확인**을 선택합니다.

> [!NOTE]
> 사용 하는 경우는 **SQL 로그인** SQL Server 계산 컨텍스트에서 스크립트를 실행 하는 데이 추가 단계가 필요 하지 않습니다.

### <a name="give-users-permission-to-run-external-scripts"></a>사용자 한 외부 스크립트를 실행 하는 권한 부여

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 직접 고 실행할 Python 스크립트에서 인스턴스를 직접, 일반적으로 관리자 권한으로 스크립트를 실행 합니다. 따라서 다양 한 작업 및 데이터베이스의 모든 데이터를 통해 암시적 사용 권한이 있는 합니다.

그러나 대부분 사용자에 게 이러한 승격 된 권한 없는 합니다. 예를 들어 조직의 사용자에 게 데이터베이스에 액세스 하는 일반적으로 SQL 로그인을 사용 하는 승격 된 권한이 없는 합니다. 따라서 Python을 사용 하는 각 사용자에 대해 부여 해야 컴퓨터 학습 서비스의 사용자가 Python을 사용 하는 각 데이터베이스에서 외부 스크립트를 실행할 수 있는 권한이 있습니다. 다음은 방법:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 권한은 지원 되는 스크립트 언어에 적용 됩니다. 즉, Python 스크립트와 R 스크립트에 대 한 별도 권한 수준이 되지 됩니다. 이러한 언어에 대 한 별도 사용 권한을 유지 해야 할 경우 별도 인스턴스에 R 및 Python을 설치 합니다.

### <a name="give-your-users-read-write-or-data-definition-language-ddl-permissions-to-databases"></a>데이터베이스 언어 (DDL) 사용 권한을 부여 하 여 사용자가 읽기, 쓰기 또는 데이터 정의

사용자 스크립트를 실행 중인 동안에 다른 데이터베이스에서 데이터를 읽는 사용자 해야 합니다. 사용자 결과 저장 하 고 데이터를 테이블에 기록 하기 위한 새 테이블을 만들려고 할 수도 있습니다.

각 Windows 사용자 계정 또는 Python 또는 R 스크립트를 실행 하는 SQL 로그인에 대 한 특정 데이터베이스에 적절 한 권한을 보유 확인: `db_datareader`, `db_datawriter`, 또는 `db_ddladmin`합니다.

예를 들어, 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 SQL 로그인 *MySQLLogin* T-SQL 쿼리를 실행할 수 있는 권한을 *ML_Samples* 데이터베이스입니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)합니다.

### <a name="ensure-that-the-sql-server-installation-supports-remote-connections"></a>설치 된 SQL Server 원격 연결을 지원 하는지 확인

원격 컴퓨터에서 연결할 수 없는 경우 방화벽 SQL Server에 대 한 액세스를 허용 하는지 여부를 확인 합니다. 기본 설치에 대 한 원격 연결을 사용할 수 또는 SQL Server에서 사용 되는 특정 포트를 방화벽에 의해 차단 될 수 있습니다. 자세한 내용은 참조 [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)합니다.

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기

기계 학습 데이터 과학 클라이언트 컴퓨터에서 솔루션을 만들 수 있습니다. 계산 컨텍스트로 써 SQL Server 컴퓨터를 사용 하 여 코드를 실행 해야 할 경우 두 가지 옵션이 있습니다: Windows를 사용 하 여 계정 또는 SQL 로그인을 사용 하 여 인스턴스에 액세스 합니다.

+ SQL 로그인에 대 한: 로그인 데이터를 읽는 데이터베이스에서 적절 한 권한이 있는지 확인 합니다. 추가 하 여 수행할 수 있습니다 *연결할* 및 *선택* 사용 권한 또는 로그인을 추가 하 여는 `db_datareader` 역할입니다. 할당 개체를 만들려는 `DDL_admin` 권한. 테이블에 데이터를 저장 해야 하는 경우에 추가 된 `db_datawriter` 역할입니다.

+ Windows 인증을 위해: 인스턴스 이름 및 기타 연결 정보를 지정 하는 데이터 과학 클라이언트에는 ODBC 데이터 원본을 만들 해야 할 수 있습니다. 자세한 내용은 참조 [ODBC 데이터 원본 관리자](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)합니다.

## <a name="additional-optimizations"></a>추가 최적화

모든 작업을가지고 기계 학습을 지원 하도록 서버를 최적화할 수도 있습니다 또는 모델을 미리 학습 된 설치 합니다.

### <a name="add-more-worker-accounts"></a>작업자 계정을 더 추가 합니다.

많은 사용자를 동시에 스크립트를 실행 하려는 경우에 실행 패드 서비스에 할당 된 작업자 계정의 수를 늘릴 수 있습니다. 자세한 내용은 참조 [SQL Server 컴퓨터 학습 서비스에 대 한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

### <a name="optimize-the-server-for-script-execution"></a>서버 스크립트 실행을 위해 최적화

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 다양 한 서비스에 대 한 서버의 균형을 최적화 합니다. 이러한 서비스에는 ETL 프로세스, 보고, 감사 및 사용 하는 응용 프로그램 포함 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다.

기본 설정을 사용 하는 경우에 외부 스크립트를 실행 하기 위한 자원을 제한 하거나 제한 하 여 메모리 집중형 작업에 특히 있는지를 확인할 수 있습니다. 우선 순위를 기계 학습을 사용 하는 경우에 외부 스크립트 작업 우선 순위를 지정 하 고 적절 하 게 리소스는 기본 데이터베이스 설정을 변경 합니다. 이러한 변경 내용이 포함할 수 있습니다.

+ 에 할당 된 메모리의 양을 줄이거나는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진입니다.
+ 실행 중인 계정 수를 늘리면는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다. 이 리소스의 수를 증가 하지 않고 하지만 동시에 실행할 수 있는 스크립트의 수 증가 합니다.

SQL Server Enterprise Edition의 경우 Python에 대 한 외부 리소스 풀을 구성 하려면 리소스 관리자를 사용 합니다. 자세한 내용은 다음 문서를 참조하세요.

-   외부 리소스 관리를 위해 리소스 풀 구성
  
     [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)
  
-   데이터베이스 엔진에 예약된 메모리 양 변경
  
     [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)
  
-   에 의해 시작 될 수 있는 작업자 계정의 수를 변경 합니다.[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]
  
     [SQL Server R Services에 대 한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)

SQL Server Standard Edition을 사용 하는 리소스 관리자를 갖지 않는 경우 서버 리소스를 관리할 수 있도록 동적 관리 뷰 및 확장된 이벤트를 사용할 수 있습니다. 이 목적을 위해 Windows 이벤트 모니터링을 사용할 수 있습니다. 자세한 내용은 참조 [모니터링 및 R 서비스 관리](../r/managing-and-monitoring-r-solutions.md)합니다.

### <a name="upgrade-the-machine-learning-components"></a>기계 학습 구성 요소를 업그레이드 합니다.

SQL Server 2017을 사용 하 여 컴퓨터 학습 서비스를 설치 하면 릴리스를 게시 하는 시간에 구성 요소 버전을 가져옵니다. 패치 또는 SQL Server 인스턴스를 업그레이드할 때마다 컴퓨터 학습 구성 요소의 업그레이드 됩니다.

기계 학습가 지 원하는 것 보다 더 빠른 일정에 따라 구성 요소를 업그레이드할 수 Microsoft 컴퓨터 학습 서버를 설치 하 여 SQL Server 릴리스에서 합니다. 이렇게 하면을 같은 컴퓨터 학습 서버의 최신 버전에서 지원 되는 새로운 기능 볼 수도 있습니다.

+ 에 대 한 Python 패키지에 대 한 업데이트 [revoscalepy](https://docs.microsoft.com/r-server/python-reference/revoscalepy/revoscalepy-package) 및 [Python에 대 한 microsoftml](https://docs.microsoft.com/r-server/python-reference/microsoftml/microsoftml-package)합니다.
+ [모델을 미리 학습 된](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) 이미지 분류 및 텍스트 분석에 대 한 합니다.

인스턴스를 업그레이드 하는 방법에 대 한 정보를 참조 하십시오. [바인딩을 통해 업그레이드 R 구성 요소](..\r\use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

### <a name="tutorials"></a>자습서

Python SQL Server와 함께 사용 하 여 빌드 컴퓨터 학습 솔루션을 배포 하는 방법을의 몇 가지 예에 대 한 다음 자습서를 참조 하십시오.

[Python을 사용 하 여 T-SQL에서](../tutorials/run-python-using-t-sql.md)

[Revoscalepy를 사용 하 여 Python 모델 만들기](../tutorials/use-python-revoscalepy-to-create-model.md)
