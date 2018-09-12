---
title: SQL Server 2016 R Services (In-database) 설치 | Microsoft Docs
description: SQL Server에서 R는 Windows에서 SQL Server 2016 R Services를 설치할 때 사용할 수 있습니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 4df8391974214452c6b8b3226c3c9a845e4b556b
ms.sourcegitcommit: 8008ea52e25e65baae236631b48ddfc33014a5e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44311683"
---
# <a name="install-sql-server-2016-r-services"></a>SQL Server 2016 R Services 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 설치 및 구성 하는 방법 설명 **SQL Server 2016 R Services**합니다. SQL Server 2016에 있는 경우 SQL Server에서 R 코드의 실행을 사용 하도록 설정 하려면이 기능을 설치 합니다.

SQL Server 2017에서 R 통합으로 제공 됩니다 [Machine Learning Services](../r/r-server-standalone.md), Python의 추가 반영 합니다. R 통합 SQL Server 2017 설치 미디어가 있는 경우, 참조 [SQL Server 2017 Machine Learning Services 설치](sql-machine-learning-services-windows-install.md) 기능을 추가 합니다. 

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

+ 데이터베이스 엔진 인스턴스를 반드시 입력 해야 합니다. 기존 인스턴스에 증분 방식으로 추가할 수는 있지만 방금 R을 설치할 수 없습니다.

+ 장애 조치 클러스터에 R Services를 설치 하지 마세요. R 프로세스 격리에 사용 되는 보안 메커니즘이 Windows Server 장애 조치 클러스터 환경과 호환 되지 않습니다.

+ 도메인 컨트롤러에 R Services를 설치 하지 마십시오. R Services에 대 한 부분 설치 하지 못합니다.

+ 설치 하지 마세요 **공유 기능** > **R Server (독립 실행형)** 컴퓨터의 동일한 데이터베이스 내 인스턴스를 실행 합니다. 

  SQL Server 인스턴스를 오픈 소스 R 및 Anaconda 배포의 자체 복사본을 사용 하기 때문에 다른 버전의 R 및 Python을 사용 하 여 side-by-side-설치를 사용할 수 있습니다. 그러나 SQL Server 외부 SQL Server 컴퓨터의 R 및 Python을 사용 하는 코드를 실행 중인 다양 한 문제가 발생할 수 있습니다.
    
  + 다른 실행 파일을 다른 라이브러리를 사용 하 고 SQL Server에서 실행 하는 경우 보다 서로 다른 결과 가져옵니다.
  + 리소스 경합을 SQL Server에서 외부 라이브러리에서 실행 되는 R 및 Python 스크립트를 관리할 수 없습니다.
  
모든 이전 버전의 Revolution Analytics 개발 환경 또는 RevoScaleR 패키지를 사용 하는 경우, SQL Server 2016의 시험판 버전을 설치한 경우 소프트웨어를 제거 해야 합니다. RevoScaleR 및 다른 전용 패키지의 이전 버전과 새 버전을 실행 하는 것은 지원 되지 않습니다. 이전 버전을 제거 하는 도움말을 참조 하세요 [업그레이드 및 설치 FAQ에 대 한 SQL Server Machine Learning Services](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

> [!IMPORTANT]
> 설치를 완료 한 후에이 문서에 설명 된 추가 사후 구성 단계를 완료 해야 합니다. 외부 스크립트를 사용 하 여 SQL Server를 사용 하도록 설정 하 고 계정 사용자를 대신해 R 작업을 실행 하려면 SQL Server에 필요한 추가이 단계에 포함 됩니다. 구성 변경에는 일반적으로 인스턴스를 다시 시작 또는 실행 패드 서비스를 다시 시작 해야합니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 패치 설치 요구 사항 

Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  

## <a name="bkmk2016top"></a>설치 프로그램을 실행된

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2016 설치 마법사를 시작 합니다.

2. 에 **설치** 탭을 선택 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.
    
   ![R Services (In-database) 설치](media/2016-setup-installation-rsvcs.png "R Services를 사용 하 여 데이터베이스 엔진의 설치를 시작 합니다.")
   
3. 에 **기능 선택** 페이지에서 다음 옵션을 선택 합니다.

   - 선택 **데이터베이스 엔진 서비스**합니다. Machine learning을 사용 하는 각 인스턴스에 데이터베이스 엔진이 필요 합니다.
   - 선택 **R Services (In-database)** 합니다. R입니다. 데이터베이스의 사용을 위해 설치 지원
    
     ![R Services 기능 선택](media/2016setup-rsvcs-features.png "이러한 기능에 대 한 R Services In-database 선택")

    > [!IMPORTANT]
    > 동시에 R Server 및 R Services를 설치 하지 마세요. 일반적으로 R Server (독립 실행형) 연결 하는 데 사용 하는 데이터 과학자 또는 개발자는 environment를 만드는 SQL Server를 설치 하는 R 솔루션을 배포 합니다. 따라서 같은 컴퓨터에 둘 다 설치할 필요는 없습니다.

4.  에 **Microsoft R Open 설치에 동의** 페이지에서 클릭 **Accept**합니다.
  
    본 사용권 계약서는 Microsoft R Open, 도구, Microsoft R 개발 팀의 연결 공급자 및 고급 R 패키지와 함께 확인 하 고 오픈 소스 R 기본 패키지의 배포를 포함 하는 다운로드 해야 합니다.
  
5. 사용권 계약을 수락한 후 경우 잠깐 일시 중지 된 설치 관리자는 준비 하는 동안 클릭 **다음** 때 단추를 사용할 수 있습니다.

6. 에 **설치할 준비가** 페이지에서 다음 항목이 포함 되며 선택한 **설치**합니다.

   + 데이터베이스 엔진 서비스
   + R Services(In-database)

    경로 아래에 있는 폴더의 위치를 기록 `..\Setup Bootstrap\Log` 구성 파일이 저장 됩니다. 설치가 완료 되 면 요약 파일에 설치 된 구성 요소를 검토할 수 있습니다.

7. 설치가 완료 되 면 컴퓨터를 다시 시작 하 라는 메시지가 표시 되는 경우 지금 합니다. 설치가 끝나면 설치 마법사에 표시되는 메시지를 읽어야 합니다. 자세한 내용은 [View and Read SQL Server Setup Log Files](https://docs.microsoft.com/sql/database-engine/install-windows/view-and-read-sql-server-setup-log-files)을 참조하세요.


##  <a name="bkmk_enableFeature"></a>스크립트 실행 활성화

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 

    > [!TIP]
    > 다운로드 하 고이 페이지에서 적절 한 버전을 설치할 수 있습니다: [SQL Server Management Studio (SSMS 다운로드)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.
    > 
    > Preview 릴리스의 아웃 보십시오 [SQL Operations Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is), 관리 작업 및 SQL Server에 대 한 쿼리를 지 합니다.
  
2. Machine Learning 서비스를 설치한 인스턴스에 연결, 클릭 **새 쿼리** 쿼리 창을 열고 다음 명령을 실행 합니다.

   ```SQL
   sp_configure
   ```
    이때 속성 값 `external scripts enabled`는 **0**이어야 합니다. 기능을 기본적으로 해제 되어 있으므로입니다. R 또는 Python 스크립트를 실행 하기 전에 기능 관리자가 명시적으로 설정 해야 합니다.
     
3. 외부 스크립팅 기능을 사용 하려면 다음 문을 실행 합니다.
  
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
  
## <a name="restart-the-service"></a>서비스를 다시 시작합니다.

설치가 완료 되 면, 다음 스크립트 실행을 사용 하도록 설정 하기 전에 데이터베이스 엔진을 다시 시작 합니다.

관련 된 다시 시작 서비스를 자동으로 다시 시작 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

마우스를 사용 하 여 서비스를 다시 시작할 수 있습니다 **다시 시작** SSMS에서 또는 사용 하 여 인스턴스에 대 한 명령을 합니다 **Services** 제어판 또는 사용 하 여 패널 [SQL Server 구성 관리자 ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>설치 확인

외부 스크립트를 실행 하는 데 사용 하는 모든 구성 요소가 실행 되 고 있는지 확인 하려면 다음 단계를 사용 합니다.

1. SQL Server Management studio에서 새 쿼리 창을 열고 다음 명령을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    이제 **run_value**가 1로 설정되어야 합니다.

2. 열기는 **서비스** 패널 또는 SQL Server 구성 관리자를 확인 하 고 **SQL Server 실행 패드 서비스** 실행. R에 있는 모든 데이터베이스 엔진 인스턴스에 대해 하나의 서비스 해야 하거나 Python 설치 합니다. 서비스에 대 한 자세한 내용은 참조 하세요. [Extensibility framework](../concepts/extensibility-framework.md)합니다.

7. 실행 패드를 실행 하는 경우에 외부 스크립팅 런타임을 SQL Server와 통신할 수 있는지 확인 하려면 간단한 R을 실행할 수 있어야 합니다. 

    새 **쿼리** 창에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 다음과 같은 스크립트를 실행 하 고:
    
    ```SQL
    EXEC sp_execute_external_script  @language =N'R',
    @script=N'
    OutputDataSet <- InputDataSet;
    ',
    @input_data_1 =N'SELECT 1 AS hello'
    WITH RESULT SETS (([hello] int not null));
    GO
    ```

    스크립트를 처음으로 실행 하려면 외부 스크립트 런타임에 로드 되는 동안 잠시 걸릴 수 있습니다. 결과 다음과 같이 해야 합니다.

    | hello |
    |----|
    | 1|

## <a name="bkmk_FollowUp"></a> 기타 고려 사항

외부 스크립트 확인 단계를 성공적으로 수행 되었으면 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 Python 명령을 실행할 수 있습니다.

명령을 실행할 때 오류가 발생 하면이 섹션의 추가 구성 단계를 검토 합니다. 서비스 또는 데이터베이스에 추가 적절 한 구성을 확인 해야 합니다.

추가 변경 해야 하는 일반적인 시나리오에는 다음이 포함 됩니다.

* [인바운드 연결에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [추가 네트워크 프로토콜을 사용 하도록 설정](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [원격 연결을 사용 하도록 설정](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [원격 사용자에 게 기본 제공 권한 확장](#bkmk_configureAccounts)
* [외부 스크립트를 실행 하는 권한 부여](#bkmk_AllowLogon)
* [개별 데이터베이스에 액세스 권한 부여](#permissions-db)

> [!NOTE]
> 나열 된 모든 변경 내용이 필요 하 고 none 필요할 수 있습니다. 요구 사항 보안 스키마를 설치한 SQL Server 및 데이터베이스에 연결 하 여 외부 스크립트를 실행 하는 사용자를 예상 하는 방법에 따라 달라 집니다. 추가 문제 해결 팁을 여기서 확인할 수 있습니다: [업그레이드 및 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)

### <a name="bkmk_configureAccounts"></a>실행 패드 계정 그룹에 대 한 암시적된 인증 사용

설치 중의 보안 토큰으로 태스크를 실행 하는 것에 대 한 일부 새로운 Windows 사용자 계정은 만들어집니다는 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스입니다. 사용자가 외부 클라이언트에서 R 스크립트를 보내면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용 가능한 작업자 계정을 활성화 하 고 호출 하는 사용자의 id로 매핑합니다 사용자를 대신 하 여 R 스크립트를 실행 합니다. 데이터베이스 엔진의이 새로운 서비스 보안 이라는 외부 스크립트 실행을 지원 *묵시적된 인증*합니다.

이러한 계정은 Windows 사용자 그룹에 볼 수 있습니다 **SQLRUserGroup**합니다. 기본적으로 R을 실행 충분히 보다 더 많은 작업은 일반적으로 20 개의 작업자 계정이 생성 됩니다.

그러나 원격 데이터 과학 클라이언트에서 R 스크립트를 실행 해야 하 고 Windows 인증을 사용 하는 경우 권한을 부여 해야 이러한 작업자 계정에 로그인 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 귀하를 대신해 인스턴스.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.
2. 에 **로그인-신규** 대화 상자에서 **검색**합니다.
3. 선택 합니다 **개체 유형** 하 고 **그룹** 확인란을 선택한 다른 모든 확인란의 선택을 취소 합니다.
4. 클릭 **Advanced**를 클릭 한 다음 확인 하 고 현재 컴퓨터를 검색할 위치 인지 확인 **지금 찾기**합니다.
5. 그룹 계정 하나부터 찾을 때까지 서버에서 목록 스크롤하여 `SQLRUserGroup`합니다.
    
    + 에 대 한 실행 패드 서비스와 연결 된 그룹의 이름을 합니다 _기본 인스턴스_ 것은 항상 **SQLRUserGroup**합니다. 기본 인스턴스에 대해서만이 계정을 선택 합니다.
    + 사용 중인 경우는 _명명 된 인스턴스로_, 인스턴스 이름이 기본 이름에 추가 됩니다 `SQLRUserGroup`합니다. 따라서 인스턴스 이름이 "MLTEST" 인 경우이 인스턴스에 대 한 기본 사용자 그룹 이름을 것 **SQLRUserGroupMLTest**합니다.
5. 클릭 **확인** 를 고급 검색 대화 상자를 닫고 인스턴스에 대 한 올바른 계정을 선택 했는지 확인 합니다. 각 인스턴스는 자체 실행 패드 서비스에만 및 해당 서비스에 대해 만든 그룹에 사용할 수 있습니다.
6. 클릭 **확인** 한 번 더 클릭 하 여 닫습니다 합니다 **사용자 또는 그룹 선택** 대화 상자.
7. 에 **로그인-신규** 대화 상자, 클릭 **확인**합니다. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다.

### <a name="bkmk_AllowLogon"></a>외부 스크립트를 실행 하도록 사용자 권한 부여

> [!NOTE]
> SQL Server 계산 컨텍스트에서 R 스크립트를 실행 하는 것에 대 한 SQL 로그인을 사용 하는 경우이 단계가 필요 하지 않습니다.

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고유한 경우 일반적으로 실행 하는 스크립트 관리자 또는 데이터베이스 소유자는 최소한 다양 한 작업, 데이터베이스 및 새 패키지를 설치 하는 기능에 대 한 모든 데이터에 대 한 암시적 권한이 있으므로 반복 합니다.

그러나 엔터프라이즈 시나리오에서 SQL 로그인을 사용 하 여 데이터베이스에 액세스 하는 사용자를 포함 한 대부분의 사용자 없습니다 이러한 권한. 따라서 R 스크립트를 실행할 각 사용자에 대 한 외부 스크립트를 사용 하는 각 데이터베이스에서 스크립트를 실행 하는 사용자 권한을 부여 해야 합니다.

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!TIP]
> 설치와 관련된 도움이 필요하세요? 모든 단계를 실행했는지 확인하고 싶으세요? 설치 상태를 확인 하 고 추가 단계를 실행 하려면 이러한 사용자 지정 보고서를 사용 합니다. 
> 
> [사용자 지정 보고서를 사용 하 여 Machine Learning Services 모니터링](../r/monitor-r-services-using-custom-reports-in-management-studio.md)합니다.

### <a name="permissions-db"></a> 에 사용자에 게 읽기, 쓰기 또는 DDL 권한이 데이터베이스에 제공 합니다.

R 실행에 사용 되는 사용자 계정 수 필요 다른 데이터베이스에서 데이터를 읽을를 결과 저장할 새 테이블 만들고 테이블로 데이터를 작성 합니다. 따라서 R 스크립트를 실행 하는 각 사용자에 대 한 사용자 데이터베이스에서 적절 한 권한이 있는지를 확인 합니다. *db_datareader*를 *db_datawriter*, 또는 *db_ddladmin*.

예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *RSamples* 데이터베이스에서 T-SQL 쿼리를 실행할 수 있는 권한을 SQL 로그인 *MySQLLogin* 에 부여합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE RSamples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 하세요. [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)입니다.


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기

데이터 과학 클라이언트 컴퓨터에서 R 솔루션을 만들고 SQL Server 컴퓨터에 계산 컨텍스트로 사용 하 여 코드를 실행 해야 하는 경우에 SQL 로그인 또는 통합된 Windows 인증을 사용할 수 있습니다.

* SQL 로그인의 경우: 데이터를 읽을 데이터베이스에 대한 적절한 권한이 로그인에 있는지 확인합니다. 추가 하 여 이렇게 수 있습니다 *연결할* 및 *선택* 권한 또는 로그인을 추가 하 여 합니다 *db_datareader* 역할입니다. 개체를 만들어야 하는 로그인에 대 한 추가 *DDL_admin* 권한. 테이블에 데이터를 저장 해야 하는 로그인에 대 한 로그인을 추가 합니다 *db_datawriter* 역할입니다.

* Windows 인증을 위해: 인스턴스 이름 및 기타 연결 정보를 지정 하는 데이터 과학 클라이언트에서 ODBC 데이터 소스를 구성 해야 할 수 있습니다. 자세한 내용은 [ODBC 데이터 원본 관리자](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)합니다.

## <a name="suggested-optimizations"></a>제안 된 최적화

모든 작업을 수행 해야 했으므로 기계 학습을 지원 하도록 서버를 최적화할 수도 있습니다 또는 미리 학습 된 모델 설치 합니다.

### <a name="add-more-worker-accounts"></a>더 많은 작업자 계정을 추가 합니다.

R을 많이 사용할 수 있습니다 하는 것이 생각 또는 스크립트를 실행할 동시에 많은 사용자가 예상 하는 경우 실행 패드 서비스에 할당 된 작업자 계정 수를 늘릴 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에 대 한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

### <a name="bkmk_optimize"></a>외부 스크립트 실행에 대 한 서버를 최적화 합니다.

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다양 한 추출, 변환 및 로드 (ETL) 프로세스를 보고, 감사에 포함 될 수 있는 데이터베이스 엔진에 의해 지원 되는 서비스에 대 한 서버의 균형을 최적화 하려는 설치 하 고 사용 하는 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다. 따라서 기본 설정에서 machine learning 위한 리소스는 경우에 따라 제한 또는 제한, 특히 메모리 사용량이 많은 작업을 찾을 수 있습니다.

Machine learning 작업 우선 순위와 정보를 적절 하 게 되도록 SQL Server 리소스 관리자를 사용 하 여 외부 리소스 풀을 구성 하는 것이 좋습니다. 에 할당 된 메모리 양을 변경할 수도 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 되는 계정의 수를 늘리거나 데이터베이스 엔진는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

- 외부 리소스를 관리 하기 위한 리소스 풀을 구성 하려면 참조 [외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)합니다.
  
- 데이터베이스에 대해 예약 된 메모리 양을 변경 하려면 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)합니다.
  
- 가 시작할 수 있는 R 계정의 수를 변경 하려면 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]를 참조 하세요 [machine learning 위한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

동적 관리 뷰 (Dmv) 및 확장 이벤트 뿐만 아니라 Windows 이벤트 모니터링을 R에서 사용 되는 서버 리소스를 관리할 수 있도록 Standard Edition을 사용 하는 리소스 관리자가 없는 경우 사용할 수 있습니다. 자세한 내용은 [모니터링 및 R Services를 관리](../r/managing-and-monitoring-r-solutions.md)합니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지 설치

SQL Server에 대 한 만든 R 솔루션은 기본 R 함수, 타사 R 패키지 및 SQL Server와 함께 설치 되는 전용 패키지에서 함수를 SQL Server로 설치 하는 오픈 소스 R의 버전과 호환으로 호출할 수 있습니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에서 R의 별도 설치를 수행한 경우, 사용자 라이브러리에 패키지를 설치한 경우에 T-SQL에서 해당 패키지를 사용할 수 없습니다.

R 패키지 설치 및 관리에 대 한 프로세스는 SQL Server 2016 및 SQL Server 2017에서 다릅니다. SQL Server 2016에서 데이터베이스 관리자는 사용자에 게 필요한 R 패키지를 설치 해야 합니다. SQL Server 2017에서 데이터베이스별 수준에서 패키지를 공유 하도록 사용자 그룹을 설정할 수도 있고 사용자가 자신의 패키지를 설치할 수 있도록 하려면 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 [새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.


## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드를 사용 하 여 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대 한 답변을 다음 문서를 참조 하세요.

* [업그레이드 및 설치 FAQ-Machine Learning 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 R을 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: T-SQL에서 R 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.


