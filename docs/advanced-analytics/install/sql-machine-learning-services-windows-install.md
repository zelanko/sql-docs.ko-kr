---
title: Services (In-database) Windows에서 학습 하는 SQL Server 2017 컴퓨터 설치 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 23fed22efe90a91905c4b36c967ad5fa72717b3f
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2018
ms.locfileid: "34585875"
---
# <a name="install-sql-server-2017-machine-learning-services-in-database-on-windows"></a>Services (In-database) Windows에서 학습 하는 SQL Server 2017 컴퓨터 설치 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server의 컴퓨터 학습 서비스 구성 요소는 데이터베이스에서 예측 분석, 통계 분석, 시각화 및 기계 학습 알고리즘에 추가 합니다. 함수 라이브러리 R 및 Python 사용 가능 하 고 데이터베이스 엔진 인스턴스에서 외부 스크립트로 실행 합니다. 

이 문서에서는 시스템 학습 구성 요소를 실행 하 여 설치 하는 방법에 설명는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사, 그리고 다음의 화면에 나타나는 메시지입니다.

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

+ SQL Server 2017 설치가 R, Python, 또는 둘 다에 대 한 언어 지원으로 컴퓨터 학습 서비스를 설치 하려는 경우 필요 합니다. 설치할 수 대신 SQL Server 2016 설치 미디어를 있으면 [SQL Server 2016 R Services (In-database)](sql-r-services-windows-install.md) R 언어 지원을 받을 수 있습니다.

+ 데이터베이스 엔진 인스턴스는 필수입니다. 방금 R을 설치할 수 없습니다 또는 Python 기능으로, 있지만 추가할 수 있습니다 증분 방식으로 기존 인스턴스.

+ 장애 조치 클러스터에 컴퓨터 학습 서비스를 설치 하지 마십시오. R 및 Python 프로세스를 격리 하기 위해 사용 되는 보안 메커니즘 Windows Server 장애 조치 클러스터 환경와 호환 되지 않습니다.

+ 도메인 컨트롤러에 컴퓨터 학습 서비스를 설치 하지 마십시오. 설치 프로그램의 시스템 학습 서비스 부분 실패 합니다.

+ 설치 하지 마십시오 **공유 기능** > **학습 Server 컴퓨터 (독립 실행형)** 동일한 컴퓨터에 데이터베이스의 인스턴스를 실행 합니다. 독립 실행형 서버 두 설치의 성능을 저해 하면서 동일한 리소스를 경합 합니다.

+ 다른 버전의 R과 Python-나란히 설치는 지원 되지만 하지 것이 좋습니다. SQL Server 인스턴스는 오픈 소스 R 및 Anaconda 배포의 자체 복사본을 사용 하기 때문에 지원 됩니다. 하지만 SQL Server 외부 SQL Server 컴퓨터에 R 및 Python을 사용 하는 코드를 실행 중인 다양 한 문제를 일으킬 수 있으므로 권장 되지 않습니다.
    
  + 다른 라이브러리와 다른 실행 파일이 사용 및 SQL Server에서 실행 하는 때 보다 서로 다른 결과 가져옵니다.
  + 외부 라이브러리를 실행 하는 R 및 Python 스크립트는 SQL server에 리소스 경합을 관리할 수 없습니다.
  
> [!IMPORTANT]
> 설치가 완료 된 후에이 문서에 설명 된 구성 후 단계를 완료 해야 합니다. 이러한 단계에는 외부 스크립트를 사용 하도록 SQL Server를 사용 하도록 설정 하 고 작업을 실행 하려면 R 및 Python에서 사용자 대신 SQL Server에 필요한 계정 추가 포함 됩니다. 구성 변경에는 일반적으로 인스턴스를 다시 시작 또는 실행 패드 서비스를 다시 시작 해야합니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2017에 대 한 설치 마법사를 시작 합니다. 다운로드할 수 있습니다. 
  
2. 에 **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**합니다.

   ![기계 학습 데이터베이스에서 서비스를 설치 합니다.](media/2017setup-installation-page-mlsvcs.PNG)
   
3. **기능 선택** 페이지에서 다음 옵션을 선택합니다.
  
    -   **데이터베이스 엔진 서비스**
  
         R 및 Python에서을 사용 하려면 SQL Server 데이터베이스 엔진의 인스턴스를 설치 해야 합니다. 기본 인스턴스나 명명 된 인스턴스를 사용할 수 있습니다.
  
    -   **Machine Learning Services(데이터베이스 내)**
  
         이 옵션을 지 원하는 R 데이터베이스 서비스를 설치 하 고 Python 스크립트 실행.

    -   **R**

        Microsoft R 패키지, 인터프리터를와 오픈 소스 오른쪽에 추가 하려면이 옵션을 선택 

    -   **Python**

        Microsoft Python 패키지, Python 3.5 실행 파일을 추가 하려면이 옵션을 확인 하 고 Anaconda 배포에서 라이브러리를 선택 합니다.
        
        ![R 및 Python에 대 한 옵션 기능](media/2017setup-features-page-mls-rpy.png "Python에 대 한 옵션 설정")

        > [!NOTE]
        > 
        > 에 대 한 옵션을 선택 하지 않으면 **학습 Server 컴퓨터 (독립 실행형)** 합니다. 컴퓨터 학습 서버를 설치 하는 옵션 **공유 기능** 별도 컴퓨터에 사용 됩니다.

4. 에 **R 설치를 타고** 페이지에서 **Accept**합니다. Microsoft R Open, 오픈 소스 R 기본 패키지 및 도구는 Microsoft 개발 팀의 연결 공급자 및 고급 R 패키지와 함께 배포를 포함 하는이 사용권 계약에 설명 합니다.

5. 에 **Python 설치에 동의** 페이지에서 **Accept**합니다. Python 오픈 소스 라이선스 계약 Anaconda 및 관련된 도구 외에 Microsoft 개발 팀에서 몇 가지 새로운 Python 라이브러리에 대해서도 설명 합니다.
     
     ![Python 라이선스 계약](media/2017setup-python-license.png "Python에 대 한 계약을 라이선스")
  
    > [!NOTE]
    >  사용 중인 컴퓨터에 인터넷에 연결 하는 경우 설치 관리자를 별도로 다운로드 하도록이 시점에서 일시 중지할 수 있습니다. 자세한 내용은 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소를 설치](../install/sql-ml-component-install-without-internet-access.md)합니다.
  
     선택 **Accept**, 될 때까지 기다렸다가 **다음** 단추가 활성화 되며 선택 **다음**합니다.
  
6. 에 **설치 준비 완료** 페이지에서 이러한 선택 항목에 포함 되어 있는지 확인 하 고 선택 **설치**합니다.
  
    + 데이터베이스 엔진 서비스
    + Machine Learning Services(데이터베이스 내)
    + R, Python, 또는 둘 다

    경로 아래에 있는 폴더의 위치를 기록 `..\Setup Bootstrap\Log` 구성 파일이 저장 됩니다. 설치가 완료 되 면 요약 파일에서 설치 된 구성 요소를 검토할 수 있습니다.

## <a name="restart-the-service"></a>서비스를 다시 시작합니다.

설치가 완료 되 면 스크립트 실행에서 다음 단계로 계속 하기 전에 데이터베이스 엔진을 다시 시작 합니다.

ervice도 자동으로 다시 시작 하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

마우스를 사용 하 여 서비스를 다시 시작할 수 **다시 시작** SSMS 또는 사용 하 여 인스턴스에 대 한 명령을 **서비스** 제어판에서 또는 사용 하 여 패널 [SQL Server 구성 관리자 ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="bkmk_enableFeature"></a>외부 스크립트 실행을 사용 하도록 설정

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 

    > [!TIP]
    > 다운로드 하 고이 페이지에서 적절 한 버전을 설치할 수 있습니다: [다운로드 SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)합니다.
    > 
    > 미리 보기 릴리스도 볼 수 있습니다 [SQL 작업 Studio](https://docs.microsoft.com/sql/sql-operations-studio/what-is)를 지 원하는 관리 작업 및 SQL Server에 대 한 쿼리 합니다.
  
2. 컴퓨터 학습 서비스를 설치한 인스턴스에 연결을 클릭 **새 쿼리** 쿼리 창을 열고 다음 명령을 실행 합니다.

   ```SQL
   sp_configure
   ```

    이때 속성 값 `external scripts enabled`는 **0**이어야 합니다. 기본적으로는 기능이 꺼져 때문입니다. Python 또는 R 스크립트를 실행 하기 전에 기능 관리자가 명시적으로 활성화 해야 합니다.
    
3.  외부 스크립팅 기능을 사용 하도록 설정 하려면 다음 문을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    ```
    
    R 언어에 대 한 기능을 이미 사용 하는 경우 실행 하지 마십시오 Python에 대 한를 두 번째로 다시 구성 합니다. 기본 확장성 플랫폼 언어를 모두 지원 합니다.

4. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 SQL Server 서비스를 다시 시작합니다. SQL Server 서비스가 자동으로 다시 시작 하면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

    마우스를 사용 하 여 서비스를 다시 시작할 수 **다시 시작** SSMS 또는 사용 하 여 인스턴스에 대 한 명령을 **서비스** 제어판에서 또는 사용 하 여 패널 [SQL Server 구성 관리자 ](../../relational-databases/sql-server-configuration-manager.md).

## <a name="verify-installation"></a>설치 확인

다음 단계를 사용 하 여 외부 스크립트를 실행 하는 데 사용 하는 모든 구성 요소가 실행 되 고 있는지 확인 합니다.

1. SQL Server Management Studio에서 새 쿼리 창을 열고 다음 명령을 실행 합니다.
    
    ```SQL
    EXEC sp_configure  'external scripts enabled'
    ```

    이제 **run_value**가 1로 설정되어야 합니다.
    
2. 열기는 **서비스** 패널 또는 SQL Server 구성 관리자를 확인 하 고 **SQL Server 실행 패드 서비스** 실행 합니다. R 있는 모든 데이터베이스 엔진 인스턴스에 대해 하나의 서비스 있어야 또는 Python 설치 합니다. 실행 되지 않는 경우 서비스를 다시 시작 합니다. 자세한 내용은 참조 [Python의 통합을 지원 하려면 구성 요소가](../python/new-components-in-sql-server-to-support-python-integration.md)합니다. 
   
3. 실행 패드를 실행 하는 경우 외부 스크립팅 런타임 SQL Server와 통신할 수 있는지 확인 하려면 간단한 R 및 Python 스크립트를 실행할 수 있습니다.

   새 **쿼리** 창을 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], 고 다음과 같은 스크립트를 실행 합니다.
    
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

    + Python에 대 한
    
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

    스크립트를 처음으로 실행 하려면 외부 스크립트 런타임을 로드 되는 동안 약간 걸릴 수 있습니다. 결과 코드는 다음과 같아야 합니다.

    | hello |
    |----|
    | 1|


> [!NOTE]
> 열 또는 Python 스크립트에 사용 되는 머리글은을 반환 하지를 디자인 합니다. 출력에 대 한 열 이름을 추가 하려면 반환 된 데이터 집합에 대 한 스키마를 지정 해야 합니다. 이 작업을 수행 하 여 열 이름을 지정 하 고 SQL 데이터 형식 지정, 저장된 프로시저의 결과와 매개 변수를 사용 합니다.
> 
> 예를 들어 임의의 열 이름을 생성 하려면 다음 줄을 추가할 수 있습니다. `WITH RESULT SETS ((Col1 AS int))`

## <a name="additional-configuration"></a>기타 고려 사항

외부 스크립트 확인 단계에 성공한 경우에 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 Python 명령을 실행할 수 있습니다.

오류가 발생 하면 명령을 실행할 때,이 섹션의 추가 구성 단계를 검토 합니다. 서비스 또는 데이터베이스에 적절 한 구성 작업 추가 수행 해야 합니다.

추가로 변경 해야 하는 일반적인 시나리오는 다음과 같습니다.

* [인바운드 연결에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [추가 네트워크 프로토콜을 사용 하도록 설정](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [원격 연결 설정](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [원격 사용자에 게 기본 제공 권한 확장](#bkmk_configureAccounts)
* [외부 스크립트를 실행할 수 있는 권한을 부여 합니다.](#permissions-external-script)
* [개별 데이터베이스에 액세스 권한 부여](#permissions-db)

> [!NOTE]
> 나열 된 모든 변경 내용이 필요 하 고 none 필요할 수 있습니다. 요구 사항은 보안 스키마를 설치한 SQL Server 및 데이터베이스에 연결 하 고 외부 스크립트를 실행 하는 사용자를 예상 하는 방법에 따라 달라 집니다. 추가 문제 해결 정보를 볼 수 있습니다: [업그레이드 및 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> 실행 패드 계정 그룹에 대 한 묵시적된 인증을 사용 하도록 설정

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

### <a name="permissions-external-script"></a> 사용자 한 외부 스크립트를 실행 하는 권한 부여

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , 직접 고 실행할 Python 또는 R 스크립트에서 인스턴스를 직접, 일반적으로 관리자 권한으로 스크립트를 실행 합니다. 따라서 다양 한 작업 및 데이터베이스의 모든 데이터를 통해 암시적 사용 권한이 있는 합니다.

그러나 대부분 사용자에 게 이러한 승격 된 권한 없는 합니다. 예를 들어 조직의 사용자에 게 데이터베이스에 액세스 하는 일반적으로 SQL 로그인을 사용 하는 승격 된 권한이 없는 합니다. 따라서 R, Python을 사용 하는 각 사용자에 대해 부여 해야 컴퓨터 학습 서비스의 사용자가 해당 언어가 사용은 각 데이터베이스에서 외부 스크립트를 실행할 수 있는 권한이. 다음은 방법:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 권한은 지원 되는 스크립트 언어에 적용 됩니다. 즉, Python 스크립트와 R 스크립트에 대 한 별도 권한 수준이 되지 됩니다. 이러한 언어에 대 한 별도 사용 권한을 유지 해야 할 경우 별도 인스턴스에 R 및 Python을 설치 합니다.

### <a name="permissions-db"></a> 데이터베이스 언어 (DDL) 사용 권한을 부여 하 여 사용자가 읽기, 쓰기 또는 데이터 정의

사용자 스크립트를 실행 중인 동안에 다른 데이터베이스에서 데이터를 읽는 사용자 해야 합니다. 사용자 결과 저장 하 고 데이터를 테이블에 기록 하기 위한 새 테이블을 만들려고 할 수도 있습니다.

각 Windows 사용자 계정 또는 Python 또는 R 스크립트를 실행 하는 SQL 로그인에 대 한 특정 데이터베이스에 적절 한 권한을 보유 확인: `db_datareader`, `db_datawriter`, 또는 `db_ddladmin`합니다.

예를 들어, 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 SQL 로그인 *MySQLLogin* T-SQL 쿼리를 실행할 수 있는 권한을 *ML_Samples* 데이터베이스입니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)합니다.


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기

기계 학습 데이터 과학 클라이언트 컴퓨터에서 솔루션을 만들 수 있습니다. 계산 컨텍스트로 써 SQL Server 컴퓨터를 사용 하 여 코드를 실행 해야 할 경우 두 가지 옵션이 있습니다: Windows를 사용 하 여 계정 또는 SQL 로그인을 사용 하 여 인스턴스에 액세스 합니다.

+ SQL 로그인에 대 한: 로그인 데이터를 읽는 데이터베이스에서 적절 한 권한이 있는지 확인 합니다. 추가 하 여 수행할 수 있습니다 *연결할* 및 *선택* 사용 권한 또는 로그인을 추가 하 여는 `db_datareader` 역할입니다. 할당 개체를 만들려는 `DDL_admin` 권한. 테이블에 데이터를 저장 해야 하는 경우에 추가 된 `db_datawriter` 역할입니다.

+ Windows 인증을 위해: 인스턴스 이름 및 기타 연결 정보를 지정 하는 데이터 과학 클라이언트에는 ODBC 데이터 원본을 만들 해야 할 수 있습니다. 자세한 내용은 참조 [ODBC 데이터 원본 관리자](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)합니다.

## <a name="suggested-optimizations"></a>제안 된 최적화

모든 작업을가지고 기계 학습을 지원 하도록 서버를 최적화할 수도 있습니다 또는 모델을 미리 학습 된 설치 합니다.

### <a name="add-more-worker-accounts"></a>작업자 계정을 더 추가 합니다.

많은 사용자를 동시에 스크립트를 실행 하려는 경우에 실행 패드 서비스에 할당 된 작업자 계정의 수를 늘릴 수 있습니다. 자세한 내용은 참조 [SQL Server 컴퓨터 학습 서비스에 대 한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

### <a name="optimize-the-server-for-script-execution"></a>서버 스크립트 실행을 위해 최적화

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램은 다양 한 추출, 변환 및 로드 하는 ETL 프로세스를 보고, 감사를 데이터베이스 엔진에서 지원 되는 서비스에 대 한 서버의 균형을 최적화 하는 데 사용 됩니다 하 고 사용 하는 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다. 따라서, 기본 설정에서 기계 학습에 대 한 리소스는 제한 또는 제한 하 여 메모리 집중형 작업에 특히 경우가 있을 수 있습니다.

을 보장 하기 위해 컴퓨터 학습 작업 우선 순위를 지정 하 고 적절 하 게 리소스는 외부 리소스 풀을 구성 하려면 SQL Server 리소스 관리자를 사용 하는 것이 좋습니다. 에 할당 된 메모리 양을 변경할 수도 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진, 또는에서 실행 되는 계정 수가 증가 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

- 외부 리소스 관리를 위해 리소스 풀을 구성 하려면 참조 [외부 리소스 풀을 만들](../../t-sql/statements/create-external-resource-pool-transact-sql.md)합니다.
  
- 데이터베이스에 대해 예약 된 메모리의 크기를 변경 하려면 참조 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)합니다.
  
- 에 의해 시작 될 수 있는 R 계정의 수를 변경 하려면 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], 참조 [기계 학습에 대 한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

Standard Edition을 사용 하는 리소스 관리자를 갖지 않는 경우 서버 리소스를 관리할 수 있도록 모니터링 되는 Windows 이벤트 뿐만 아니라 동적 관리 뷰 (Dmv) 및 확장 이벤트를 사용할 수 있습니다. 자세한 내용은 참조 [모니터링 및 R 서비스 관리](../r/managing-and-monitoring-r-solutions.md) 및 [모니터링 서비스 및 관리 Python](../python/managing-and-monitoring-python-solutions.md)합니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지를 설치 합니다.

SQL Server에 대 한 만드는 R 솔루션 기본 R 함수, SQL Server 및 SQL Server로 설치 되는 오픈 소스 R의 버전과 호환 제 3 자 R 패키지와 함께 설치 된 properietary packes에서 함수를 호출할 수 있습니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에서 R의 별도 설치 하는 경우 또는 사용자 라이브러리에 패키지를 설치한 경우에 T-SQL에서 이러한 패키지를 사용할 수 없습니다.

설치 및 R 패키지를 관리 하기 위한 프로세스는 SQL Server 2016 및 SQL Server 2017에서 다릅니다. SQL Server 2016에서 데이터베이스 관리자는 사용자가 필요로 하는 R 패키지를 설치 해야 합니다. SQL Server 2017 년 데이터베이스 수준에서 패키지 공유 사용자 그룹을 설정할 수도 있고 사용자가 자신의 패키지를 설치할 수 있도록 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 참조 [새 R 패키지를 SQL Server에에서 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.


## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드로 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자 몇 가지 간단한 예제 차별화할 수 및 R SQL Server와 함께 작동 하는 방법에 대 한 기본 사항을 설명 합니다. 다음 단계에서는 다음 링크 참조:

+ [자습서: T-SQL에서 R을 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는이 자습서를 수행 하 여 SQL Server와 함께 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.
