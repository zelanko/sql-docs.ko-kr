---
title: "SQL Server 컴퓨터 학습 Services (In-database) 설치 | Microsoft Docs"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "SQL Server R Services 설치"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 36
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: f0065068d53517626c7157c9be884549573ae08b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/07/2017

---
# <a name="set-up-sql-server-machine-learning-services-in-database"></a>SQL Server 컴퓨터 학습 Services (In-database) 설치

SQL Server의 컴퓨터 학습 서비스를 사용 하 여 설정 하는 방법에 설명 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설정 마법사입니다.

**적용 대상:** SQL Server 2016 R Services (R에만 해당), SQL Server 2017 컴퓨터 학습 서비스 (예: R 및 Python)

## <a name="machine-learning-options-in-sql-server-setup"></a>기계 학습에서 SQL Server 설치 옵션

SQL Server 설치 프로그램에서는 기계 학습을 설치 하기 위한 다음 옵션을 제공 합니다.

* SQL Server 데이터베이스와 함께 설치 기계 학습

  이 옵션에는 저장된 프로시저를 사용 하 여 Python 또는 R 스크립트를 실행할 수 있습니다. 외부 연결에서 실행 되는 R, Python 스크립트에 대 한 원격 계산 컨텍스트는 SQL Server 컴퓨터를 사용할 수 있습니다.

  설치 하려면이 옵션:
  
  * SQL Server 2016에서 선택 **R Services (In-database)**합니다.
  * SQL Server 2017 선택 **컴퓨터 학습 Services (In-database)**합니다.


* 독립 실행형 컴퓨터 학습 서버 설치

  이 옵션은 기계 학습 필요 하지 않거나 SQL Server를 사용 하는 솔루션을 위한 개발 환경을 만듭니다. 따라서 일반적으로 권장 하나의 호스팅 SQL Server와 다른 컴퓨터에이 옵션을 설치 합니다. 이 옵션에 대 한 자세한 내용은 참조 [독립 실행형 R Server 만들기](../r/create-a-standalone-r-server.md)합니다.

설치 프로세스에서 여러 단계를 일부는 선택 사항 필요 합니다. 선택적 부분은 둘 다에 따라 기계 학습 및 보안 환경 상태를 사용 하려는 방법입니다. 

## <a name="bkmk_prereqs"></a> 필수 구성 요소

*  R 서버 및 R 서비스를 모두 동시에 설치 하지 않습니다. 일반적으로 SQL Server에 R Server (독립 실행형)를 연결 하는 데 사용 하는 데이터 과학자 또는 개발자 하는 환경을 만드는 설치 하는 R 솔루션을 배포 합니다. 따라서 같은 컴퓨터에 둘 다 설치할 필요는 없습니다.

* 모든 이전 버전의 Revolution Analytics 개발 환경 또는 RevoScaleR 패키지를 사용 하는 경우 또는 SQL Server 2016의 시험판 버전을 설치한 경우 제거 해야 있습니다. -병렬 설치에 지원 되지 않습니다. 이전 버전을 제거 하는 도움말을 참조 하십시오. [업그레이드 및 SQL Server R Services에 대 한 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

* 장애 조치 클러스터에 컴퓨터 학습 서비스를 설치할 수 없습니다. 원인은 외부 스크립트 프로세스를 격리 하기 위해 사용 되는 보안 메커니즘 Windows Server 장애 조치 클러스터 환경와 호환 되지 않습니다. 이 문제를 해결 다음 중 하나를 수행할 수 있습니다.
    * 복제를 사용 하 여 R services 독립 실행형 SQL Server 인스턴스에 필요한 테이블을 복사 합니다.
    * 설치 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] AlwaysOn을 사용 하 고 가용성 그룹의 일부는 독립 실행형 컴퓨터에 있습니다.

> [!IMPORTANT]
> 설치가 완료 되 면 기계 학습 기능을 사용 하도록 설정 하려면 몇 가지 추가 단계가 필요 합니다. 있습니다 수도 할 특정 데이터베이스에 대 한 사용자 권한을 부여 하려면 변경 하거나 계정을 구성 또는 원격 데이터 과학 클라이언트 설정 합니다.

##  <a name="bkmk_installExt"></a>1 단계: 확장 기능을 설치 하 고 기계 학습 언어를 선택 합니다.

기계 학습을 사용 하려면 SQL Server 2016 이상의 버전을 설치 해야 합니다. 사용 하도록 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 데이터베이스 엔진의 인스턴스를 하나 이상 있어야 합니다. 기본 인스턴스나 명명된 인스턴스를 사용할 수 있습니다.

1. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.
  
    무인된 설치를 수행 하는 방법에 대 한 정보를 참조 하십시오. [의 SQL Server R Services 무인 설치](../r/unattended-installs-of-sql-server-r-services.md)합니다.
  
2. 에 **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.
   
3. 에 **기능 선택** 페이지에서 R에서 사용 하는 데이터베이스 서비스를 설치 하려면 작업 및 외부 스크립트 및 프로세스를 지 원하는, 다음 옵션을 선택 하는 확장을 설치 합니다.
   
   **SQL Server 2016**
   - 선택 **데이터베이스 엔진 서비스**합니다.
   - 선택 **R Services (In-database)**합니다.

   **SQL Server 2017**
   - 선택 **데이터베이스 엔진 서비스**합니다.
   - 선택 **기계 학습 Services (In-database)**합니다.
   - 사용할 수 있도록 언어 학습 컴퓨터를 하나 이상 선택 합니다. R만 선택 하거나 R 및 Python 모두 추가할 수 있습니다.
   
   > [!NOTE]
   > Python 또는 R 언어 옵션을 선택 하지 않으면 설치 마법사 설치만 확장성 프레임 워크, SQL Server 신뢰할 수 있는 실행 패드를 포함 하는 하지만 모든 언어별 구성 요소를 설치 하지 않습니다. 이 옵션은 Microsoft 최신 수명 주기 정책의 일부로 R, Python에는 SQL Server 인스턴스를 바인딩 됩니다. 자세한 내용은 참조 [R Services의 인스턴스를 업그레이드 하려면 사용 하 여 SqlBindR](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

4.  에 **Microsoft R Open 설치에 동의** 페이지에서 **Accept**합니다.
  
     Microsoft R Open, 오픈 소스 R 기본 패키지 및 도구, 고급 R 패키지 및 Microsoft R 개발 팀의 연결 공급자와 함께 배포를 포함 하는 다운로드 하려면이 사용권 계약에 필요 합니다.
  
    > [!NOTE]
    >  이 시점에 설명 된 대로 별도로 설치 관리자를 다운로드 하려면 설치 프로그램을 일시 중지할 수 사용 중인 컴퓨터에 인터넷에 연결 하는 경우 [설치 R components without](installing-ml-components-without-internet-access.md)합니다.
  
5. **다음**을 선택합니다.

6. 에 **설치 준비 완료** 페이지에서 다음 항목은 포함 되어 있으며 다음 선택 **설치**합니다.

   **SQL Server 2016**
   - 데이터베이스 엔진 서비스
   - R Services(In-Database)

   **SQL Server 2017**
   - 데이터베이스 엔진 서비스
   - Machine Learning Services(데이터베이스 내)
   - R, Python, 또는 둘 다
    
7. 설치가 완료 되 면 컴퓨터를 다시 시작 합니다.

##  <a name="bkmk_enableFeature"></a>2 단계: 외부 스크립트 서비스를 사용 합니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 아직 설치되지 않은 경우 SQL Server 설치 마법사를 다시 실행하여 다운로드 링크를 열고 설치할 수 있습니다.
  
2. 기계 학습을 설치한 인스턴스에 연결 하 고 다음 명령을 실행 합니다.

   ```SQL
   sp_configure
   ```

    에 대 한 값의 **사용 하도록 설정 하는 외부 스크립트** 속성 있어야 **0**합니다. 기능을 노출 영역을 줄이기 위해 기본적으로 꺼져 있으며 관리자가 명시적으로 활성화 해야 때문입니다.
     
3. 외부 스크립팅 기능을 사용 하도록 설정 하려면 다음 문을 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 SQL Server 서비스를 다시 시작합니다. SQL Server 서비스가 자동으로 다시 시작 하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

    사용 하 여 서비스를 다시 시작할 수는 **서비스** 제어판 또는 SQL Server 구성 관리자를 사용 하 여 패널입니다.

## <a name="bkmk_TestScript"></a>3 단계: 스크립트 실행 로컬로 작동 하는지 확인

외부 스크립트 실행 서비스 활성화 되어 있는지 확인 합니다.

1. SQL Server Management Studio를 열고 새 **쿼리** 창을 닫은 후 다음 명령 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```
    이제 **run_value**가 1로 설정되어야 합니다.
    
2. 열기는 **서비스** 패널 및 실행 패드 서비스 인스턴스에 대 한 실행 되 고 있는지 확인 합니다. 여러 인스턴스를 설치할 경우 각 인스턴스에는 자체 실행 패드 서비스가 있습니다.
   
3. 새 **쿼리** 창을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 고 다음과 같은 간단한 R 스크립트를 실행 합니다.
  
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```
  
    **결과**
  
    *hello* *1*
  
   명령이 오류 없이 실행 되는 경우 다음 단계로 이동 합니다. 목록이 몇 가지 일반적인 문제에 대 한 오류가 발생 하면 참조 [업그레이드 및 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

## <a name="bkmk_FollowUp"></a>4 단계: 추가 구성

R 또는 Python에 대 한 사용 사례에 따라 서버, 방화벽, 서비스 또는 데이터베이스 사용 권한을 사용 하는 계정에 대 한 추가 변경을 해야 할 수 있습니다. 대/소문자에 따라 다른 변경 해야 합니다.

추가로 변경 해야 하는 일반적인 시나리오는 다음과 같습니다.

* SQL Server에 대 한 인바운드 연결을 허용 하도록 방화벽 규칙을 변경 합니다.
* 추가 네트워크 프로토콜을 사용 하도록 설정 합니다.
* 서버에서 원격 연결을 지원 하는지 확인 합니다.
* 사용 하도록 설정 *암시 된 인증이*, 사용자가 원격 R 개발 터미널에서 SQL Server 데이터 액세스 RODBC 패키지 또는 다른 Microsoft ODBC Open Database Connectivity () 공급자를 사용 하 여 R 코드를 실행 하는 경우.
* R 스크립트를 실행 하거나 데이터베이스를 사용 하 여 사용자에 게 권한을 부여 합니다.
* 실행 패드 서비스와의 통신을 방해 하는 보안 문제를 수정 합니다.
* 사용자가 R 코드를 실행 하거나 패키지를 설치할 수 있는 권한을 확인 합니다.

> [!NOTE]
> 나열 된 일부 변경 해야 할 수 있습니다. 그러나 시나리오에 적용 가능한 지 확인 하는 모든 항목을 검토 하는 것이 좋습니다.

### <a name="bkmk_configureAccounts"></a>실행 패드 계정 그룹에 대 한 묵시적된 인증을 사용 하도록 설정

설치 하는 동안의 보안 토큰에서 작업 실행을 위해 몇 가지 새로운 Windows 사용자 계정이 만들어집니다는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스입니다. 외부 클라이언트에서 R 스크립트를 보낼 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용 가능한 작업자 계정을 활성화 하 고 호출 하는 사용자의 id로 매핑합니다 사용자를 위해 R 스크립트를 실행 합니다. 데이터베이스 엔진의이 새로운 서비스 보안 이라는 외부 스크립트 실행을 지원 *암시 된 인증이*합니다.

이러한 계정은 Windows 사용자 그룹에 볼 수 있습니다 **SQLRUserGroup**합니다. 기본적으로 R을 실행 하기 위한 충분 한 더 많은 작업은 일반적으로 20 작업자 계정이 생성 됩니다.

그러나 원격 데이터 과학 클라이언트에서 R 스크립트를 실행 해야 하 고 Windows 인증을 사용 하는 경우 권한을 부여 해야 이러한 작업자 계정에 로그인 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 대신 인스턴스.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.
2. 에 **로그인-신규** 대화 상자에서 **검색**합니다.
3. 선택 된 **개체 유형** 및 **그룹** 확인란을 선택한 다른 모든 확인란의 선택을 취소 합니다. 
4. **선택할 개체 이름을 입력**, 형식 **SQLRUserGroup**를 선택한 후 **이름 확인**합니다.  
    인스턴스의 실행 패드 서비스와 관련 된 로컬 그룹의 이름이 같은 값으로 확인 되어야 *instancename\SQLRUserGroup*합니다. 
5. **확인**을 선택합니다.
6. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.
7. **확인**을 선택합니다.

### <a name="bkmk_AllowLogon"></a>사용자 한 외부 스크립트를 실행 하는 권한 부여

> [!NOTE]
> SQL Server 계산 컨텍스트에서에서 R 스크립트를 실행 하기 위한 SQL 로그인을 사용 하는 경우에이 단계가 필요 하지 않습니다.

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 인스턴스를 직접에서 R 스크립트를 실행 하는, 관리자는 스크립트를 실행할 일반적으로 또는 데이터베이스 소유자는 최소한가지고 다양 한 작업, 데이터베이스 및 수의 모든 데이터에 대 한 암시적 사용 권한 으로 새 R 패키지를 설치 하려면 필요 합니다.

그러나 엔터프라이즈 시나리오에서 SQL 로그인을 사용 하 여 데이터베이스를 액세스 하는 사용자를 포함 한 대부분의 사용자 없는 이러한 승격 된 권한입니다. 따라서, Python 또는 R 스크립트를 실행할 각 사용자에 대해 각 데이터베이스에서 스크립트를 실행 한 외부 스크립트 사용될지 사용자 권한을 부여 해야 합니다.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 설치와 관련된 도움이 필요하세요? 모든 단계를 실행했는지 확인하고 싶으세요? 이러한 사용자 지정 보고서를 사용하여 R Services의 설치 상태를 확인합니다. 자세한 내용은 [사용자 지정 보고서를 사용하여 R Services 모니터링](monitor-r-services-using-custom-reports-in-management-studio.md)을 참조하세요.

### <a name="ensure-that-the-sql-server-computer-supports-remote-connections"></a>SQL Server 컴퓨터에서 원격 연결을 지원 하는지 확인 하십시오.

원격 컴퓨터에서 연결할 수 없는 경우 서버에서 원격 연결 허용 되는지 여부를 확인 합니다. 원격 연결이 기본적으로 비활성화 하는 경우가 있습니다.

또한 방화벽 SQL Server에 대 한 액세스를 허용 하는지 여부를 확인 하려면 확인 합니다. 기본적으로 SQL Server에서 사용 되는 포트는 종종 방화벽에 의해 차단 됩니다. Windows 방화벽을 사용 하는 경우 참조 [데이터베이스 엔진 액세스에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)합니다.

### <a name="give-your-users-read-write-or-ddl-permissions-to-the-database"></a>사용자의 읽기, 쓰기 또는 데이터베이스에 DDL 사용 권한을 부여 합니다.

R 스크립트를 실행 중인 사용자 계정 또는 SQL 로그인 수 할 다른 데이터베이스에서 데이터를 읽는 결과 저장 하기 위한 새 테이블 만들고 테이블에 데이터를 쓸 합니다.

각 사용자 계정 또는 R 스크립트를 실행 하는 SQL 로그인에 대해 해당 계정이 나 로그인에 데이터베이스에 적절 한 권한이 있는지 수: *db_datareader*, *db_datawriter*, 또는  *db_ddladmin*합니다.

예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *RSamples* 데이터베이스에서 T-SQL 쿼리를 실행할 수 있는 권한을 SQL 로그인 *MySQLLogin* 에 부여합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)합니다.

### <a name="use-machine-learning-in-an-azure-vm"></a>기계 학습을 사용 하 여 Azure VM에서

Azure 가상 컴퓨터에서 컴퓨터 학습 서비스 (또는 R Services)를 설치한 경우 몇 가지 추가 기본값을 변경 해야 합니다. 자세한 내용은 참조 [Azure 가상 컴퓨터에서 SQL Server 기계 학습 설치](installing-sql-server-r-services-on-an-azure-virtual-machine.md)합니다.

### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기

데이터 과학 클라이언트 컴퓨터에서 R 솔루션을 만들고 계산 컨텍스트로 써 SQL Server 컴퓨터를 사용 하 여 코드를 실행 해야 하는 경우에 SQL 로그인 또는 Windows 통합된 인증을 사용할 수 있습니다.

* SQL 로그인의 경우: 데이터를 읽을 데이터베이스에 대한 적절한 권한이 로그인에 있는지 확인합니다. 추가 하 여 그렇게 할 수 *연결할* 및 *선택* 사용 권한 또는 로그인을 추가 하 여는 *db_datareader* 역할입니다. 개체를 만들어야 하는 로그인에 대 한 추가 *DDL_admin* 권한. 테이블에 데이터를 저장 해야 하는 로그인에 대 한 로그인을 추가 *db_datawriter* 역할입니다.

* Windows 인증을 위해: 인스턴스 이름 및 기타 연결 정보를 지정 하는 데이터 과학 클라이언트에 ODBC 데이터 소스를 구성 해야 할 수도 있습니다. 자세한 내용은 참조 [ODBC 데이터 원본 관리자](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)합니다.

## <a name="next-steps"></a>다음 단계

SQL Server에서 스크립트 실행 기능이 작동 하는지 확인 한 후에 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 R 및 Python 명령을 실행할 수 있습니다.

그러나 다음 새 R 패키지를 추가 또는 기계 학습의 사용을 지원 하도록 시스템 구성에 대 한 일부 변경 하는 것이 좋습니다.

이 섹션에서는 기계 학습을 지원 하기 위한 몇 가지 일반적인 수정 작업을 나열 합니다.

### <a name="add-more-worker-accounts"></a>작업자 계정을 더 추가 합니다.

R을 많이, 사용할 수 있다고 생각 되 면 또는 많은 사용자를 동시에 실행 중인 스크립트 상태가 될 것으로 예상한 경우에 실행 패드 서비스에 할당 된 작업자 계정의 수를 늘릴 수 있습니다. 자세한 내용은 참조 [SQL Server R Services에 대 한 사용자 계정 풀 수정](modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

### <a name="bkmk_optimize"></a>외부 스크립트 실행에 대 한 서버를 최적화 합니다.

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 다양 한 추출, 변환 및 로드 하는 ETL 프로세스를 보고, 감사를 데이터베이스 엔진에서 지원 되는 서비스에 대 한 서버의 균형을 최적화 하는 데 사용 됩니다 하 고 사용 하는 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다. 따라서, 기본 설정에서 기계 학습에 대 한 리소스는 제한 또는 제한 하 여 메모리 집중형 작업에 특히 경우가 있을 수 있습니다.

을 보장 하기 위해 컴퓨터 학습 작업 우선 순위를 지정 하 고 적절 하 게 리소스는 외부 리소스 풀을 구성 하려면 SQL Server 리소스 관리자를 사용 하는 것이 좋습니다. 에 할당 된 메모리 양을 변경할 수도 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진, 또는에서 실행 되는 계정 수가 증가 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

- 외부 리소스 관리를 위해 리소스 풀을 구성 하려면 참조 [외부 리소스 풀을 만들](../../t-sql/statements/create-external-resource-pool-transact-sql.md)합니다.
  
- 데이터베이스에 대해 예약 된 메모리의 크기를 변경 하려면 참조 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)합니다.
  
- 에 의해 시작 될 수 있는 R 계정의 수를 변경 하려면 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], 참조 [기계 학습에 대 한 사용자 계정 풀 수정](modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

동적 관리 뷰 (Dmv) 및 확장 이벤트 뿐 아니라 Windows 이벤트 모니터링, 오른쪽에서 사용 되는 서버 리소스를 관리할 수 있도록 Standard Edition을 사용 하는 리소스 관리자를 갖지 않는 경우 사용할 수 있습니다. 자세한 내용은 참조 [모니터링 및 R 서비스 관리](managing-and-monitoring-r-solutions.md)합니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지를 설치 합니다.

사용할 수 있는 추가 R 패키지를 설치 하려면 몇 분을 걸립니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에서 R의 별도 설치 하는 경우 또는 사용자 라이브러리에 패키지를 설치한 경우에 T-SQL에서 이러한 패키지를 사용할 수 없습니다. 자세한 내용은 참조 [SQL Server에 추가 R 패키지 설치](../../advanced-analytics/r-services/install-additional-r-packages-on-sql-server.md)합니다.

데이터베이스 수준에서 패키지를 공유 하려면 사용자 그룹을 설정 하거나 사용자가 자신의 패키지를 설치할 수 있도록 데이터베이스 역할을 구성할 수도 있습니다. 자세한 내용은 참조 [관리 패키지](r-package-management-for-sql-server-r-services.md)합니다.

### <a name="upgrade-the-machine-learning-components"></a>기계 학습 구성 요소를 업그레이드 합니다.

SQL Server 2016을 사용 하 여 R Services를 설치 하면 릴리스 나 서비스 팩을 게시할 때 최신 했던의 R 구성 요소 버전을 가져올 수 있습니다. 서버를 업그레이드 하거나 패치 때마다 컴퓨터 학습 구성 요소의 업그레이드 됩니다.

하지만 기계 학습가 지 원하는 것 보다 더 빠른 일정에 따라 구성 요소를 업그레이드할 수 있습니다 SQL Server 릴리스에서 Microsoft R Server를 설치 하 고 인스턴스를 바인딩. 를 업그레이드 하면 Microsoft R Server의 최신 릴리스에서 지원 되는 다음과 같은 새로운 기능을 얻게:

* 포함 하 여 새 R 패키지 [sqlrutils](https://docs.microsoft.com/r-server/r-reference/sqlrutils/sqlrutils), [olapR](https://docs.microsoft.com/r-server/r-reference/olapr/olapr), 및 [MicrosoftML](https://docs.microsoft.com/r-server/r-reference/microsoftml/microsoftml-package)합니다.
* [모델을 미리 학습 된](https://docs.microsoft.com/r-server/install/microsoftml-install-pretrained-models) 이미지 분류 및 텍스트 분석에 대 한 합니다.

SQL Server 2016 인스턴스를 업그레이드 하는 방법에 대 한 정보를 참조 하십시오. [바인딩을 통해 업그레이드 R 구성 요소](use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.

어떤 버전의 R는 인스턴스와 연결 된 확실 하지 않은 경우에 다음과 같은 명령을 실행할 수 있습니다.

```SQL
EXEC sp_execute_external_script  @language =N'R',
@script=N'
myvar <- version$version.string
OutputDataSet <- as.data.frame(myvar);'
```

> [!NOTE]
> 바인딩 프로세스를 통해 업그레이드에 대 한 SQL Server 2017도 지원 됩니다. 그러나 현재 SQL Server 2016 인스턴스에 대해서만 업그레이드가 지원 됩니다.

### <a name="tutorials"></a>자습서

몇 가지 간단한 예제 시작 하 고 SQL Server R 작동 하는 방법의 기본 사항 참조 [TRANSACT-SQL에서 사용 하 여 R 코드](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.

### <a name="troubleshooting"></a>문제 해결

문제가 발생하나요? 업그레이드 하려는? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](monitor-r-services-using-custom-reports-in-management-studio.md)

