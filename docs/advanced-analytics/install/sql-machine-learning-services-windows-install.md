---
title: SQL Server Machine Learning Services (In-database) Windows에서 설치 | Microsoft Docs
description: SQL Server 또는 SQL Server의 Python에는 R은 Windows에서 SQL Server 2017의 Machine Learning Services를 설치할 때 사용할 수입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/08/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 285745a36552a0029ae0df383fc629b94632d524
ms.sourcegitcommit: 8008ea52e25e65baae236631b48ddfc33014a5e0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/10/2018
ms.locfileid: "44311653"
---
# <a name="install-sql-server-machine-learning-services"></a>SQL Server Machine Learning 서비스 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 2017부터 R 및 Python에 대 한 지원은 SQL Server Machine Learning 서비스에 대 한 후속 데이터베이스 내 분석을 제공 됩니다 [SQL Server R Services](../r/sql-server-r-services.md) SQL Server 2016에서 도입 되었습니다. 함수 라이브러리 R 및 Python에 사용할 수 있으며 데이터베이스 엔진 인스턴스에서 외부 스크립트 실행. 

이 문서를 실행 하 여 machine learning 구성 요소를 설치 하는 방법에 설명 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사 및 다음을 화면의 지시 합니다.

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

+ SQL Server 2017 설치는 R 및 Python을 사용 하 여 Machine Learning 서비스에 대 한 필요합니다. 대신 SQL Server 2016 설치 미디어가 있는 경우 참조 [SQL Server 2016 R Services 설치](sql-r-services-windows-install.md) R 언어 지원을 받을 수 있습니다.

+ 데이터베이스 엔진 인스턴스를 반드시 입력 해야 합니다. 기존 인스턴스를 증분 방식으로 추가할 수는 있지만 방금 R 또는 Python 기능을 설치할 수 없습니다.

+ 장애 조치 클러스터에서 Machine Learning 서비스를 설치 하지 마세요. R 및 Python 프로세스 격리에 사용 되는 보안 메커니즘을 Windows Server 장애 조치 클러스터 환경과 호환 되지 않습니다.

+ 도메인 컨트롤러에서 Machine Learning 서비스를 설치 하지 마세요. Machine Learning 서비스에 대 한 부분 설치 하지 못합니다.

+ 설치 하지 마세요 **공유 기능** > **Machine Learning Server (독립 실행형)** 컴퓨터의 동일한 데이터베이스 내 인스턴스를 실행 합니다. 독립 실행형 서버 설치 둘 다의 성능을 저해 하면서 같은 리소스를 경합 합니다.

+ 다른 버전의 R 및 Python을 사용 하 여 side-by-side-설치는 지원 되지만 권장 하지 않습니다. SQL Server 인스턴스는 오픈 소스 R 및 Anaconda 배포의 자체 복사본을 사용 하기 때문에 지원 됩니다. 하지만 다양 한 문제가 발생할 수 있습니다 SQL Server 외부 SQL Server 컴퓨터의 R 및 Python을 사용 하는 코드를 실행 하기 때문에 권장 되지 않습니다.
    
  + 다른 실행 파일을 다른 라이브러리를 사용 하 고 SQL Server에서 실행 하는 경우 보다 서로 다른 결과 가져옵니다.
  + 리소스 경합을 SQL Server에서 외부 라이브러리에서 실행 되는 R 및 Python 스크립트를 관리할 수 없습니다.
  
> [!IMPORTANT]
> 설치를 완료 한 후에이 문서에 설명 된 구성 후 단계를 완료 해야 합니다. 외부 스크립트를 사용 하 여 SQL Server를 사용 하도록 설정 하 고 계정 사용자를 대신해 R 및 Python 작업을 실행 하려면 SQL Server에 필요한 추가이 단계에 포함 됩니다. 구성 변경에는 일반적으로 인스턴스를 다시 시작 또는 실행 패드 서비스를 다시 시작 해야합니다.

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

## <a name="bkmk_enableFeature"></a>스크립트 실행 활성화

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

## <a name="additional-configuration"></a>기타 고려 사항

외부 스크립트 확인 단계를 성공적으로 수행 되었으면 SQL Server Management Studio, Visual Studio Code 또는 T-SQL 문을 서버로 보낼 수 있는 다른 모든 클라이언트에서 Python 명령을 실행할 수 있습니다.

명령을 실행할 때 오류가 발생 하면이 섹션의 추가 구성 단계를 검토 합니다. 서비스 또는 데이터베이스에 추가 적절 한 구성을 확인 해야 합니다.

추가 변경 해야 하는 일반적인 시나리오에는 다음이 포함 됩니다.

* [인바운드 연결에 대 한 Windows 방화벽 구성](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)
* [추가 네트워크 프로토콜을 사용 하도록 설정](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)
* [원격 연결을 사용 하도록 설정](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)
* [원격 사용자에 게 기본 제공 권한 확장](#bkmk_configureAccounts)
* [외부 스크립트를 실행 하는 권한 부여](#permissions-external-script)
* [개별 데이터베이스에 액세스 권한 부여](#permissions-db)

> [!NOTE]
> 나열 된 모든 변경 내용이 필요 하 고 none 필요할 수 있습니다. 요구 사항 보안 스키마를 설치한 SQL Server 및 데이터베이스에 연결 하 여 외부 스크립트를 실행 하는 사용자를 예상 하는 방법에 따라 달라 집니다. 추가 문제 해결 팁을 여기서 확인할 수 있습니다: [업그레이드 및 설치 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)

###  <a name="bkmk_configureAccounts"></a> 실행 패드 계정 그룹에 대 한 암시적된 인증 사용

설치하는 동안 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스의 보안 토큰으로 태스크를 실행하기 위해 많은 새 Windows 사용자 계정이 생성됩니다. 사용자가 외부 클라이언트에서 Python 또는 R 스크립트를 보내면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 사용 가능한 작업자 계정을 활성화 합니다. 그런 다음 호출 하는 사용자의 id로 매핑합니다 하 고 사용자를 대신 하 여 스크립트를 실행 합니다.

이 이라고 *묵시적된 인증*에 데이터베이스 엔진의 서비스 및 합니다. 이 서비스는 SQL Server 2016 및 SQL Server 2017의 외부 스크립트의 보안 실행을 지원합니다.

Windows 사용자 그룹 **SQLRUserGroup**에서 해당 계정을 볼 수 있습니다. 기본적으로 외부 스크립트 실행을 위한 충분 한 보다 자세한 작업은 일반적으로 20 개의 작업자 계정이 생성 됩니다.

> [!IMPORTANT]
> 작업자 그룹 이름은 **SQLRUserGroup** R 또는 Python을 설치 하는 여부에 관계 없이 합니다. 각 인스턴스에 대 한 단일 그룹이 있습니다.

원격 데이터 과학 클라이언트에서 스크립트를 실행 해야 하는 경우 Windows 인증을 사용 하는 추가 고려 사항이 있습니다. 이러한 작업자 계정에 로그인 하는 권한을 지정 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 귀하를 대신해 인스턴스.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]개체 탐색기에서를 확장 하 고 **보안**합니다. 마우스 오른쪽 단추로 클릭 **로그인**, 선택한 **새 로그인**합니다.
2. 에 **로그인-신규** 대화 상자에서 **검색**합니다.
3. 선택 **개체 유형**, 선택한 **그룹**합니다. 다른 모든 항목의 선택을 취소 합니다.
4. **선택할 개체 이름 입력**, 형식 *SQLRUserGroup*를 선택한 **이름 확인**합니다.
5. 인스턴스의 실행 패드 서비스와 연결된 로컬 그룹의 이름이 *instancename\SQLRUserGroup*과 같은 이름으로 확인되어야 합니다. **확인**을 선택합니다.
6. 기본적으로 그룹에 할당 합니다 **공용** 역할, 데이터베이스 엔진에 연결할 수 있는 권한이 있고.
7. **확인**을 선택합니다.

> [!NOTE]
> 사용 하는 경우는 **SQL 로그인** SQL Server 계산 컨텍스트에서 스크립트 실행을 위해이 추가 단계가 필요 하지 않습니다.

### <a name="permissions-external-script"></a> 외부 스크립트를 실행 하도록 사용자 권한 부여

설치한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고 사용자가 직접 인스턴스를 직접에서 R 또는 Python 스크립트를 실행 중인, 일반적으로 관리자 권한으로 스크립트를 실행 합니다. 따라서 권한이 암시적 다양 한 작업 및 데이터베이스의 모든 데이터입니다.

그러나 대부분의 사용자가 이러한 권한 없습니다. 예를 들어 SQL 로그인을 사용 하 여 일반적으로 데이터베이스에 액세스 하는 조직에서 사용자에는 관리자 권한이 없습니다. 따라서 R 또는 Python을 사용 하는 각 사용자에 대 한 권한을 부여 해야 Machine Learning Services의 사용자는 언어를 사용 하는 각 데이터베이스에서 외부 스크립트를 실행 합니다. 다음은 어떻게:

```SQL
USE <database_name>
GO
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]
```

> [!NOTE]
> 권한은 지원 되는 스크립트 언어에 적용 됩니다. 즉, Python 스크립트 및 R 스크립트에 대해 별도 사용 권한 수준이 하지 않습니다. 이러한 언어에 대 한 별도 사용 권한을 유지 해야 할 경우 별도 인스턴스에서 R 및 Python을 설치 합니다.

### <a name="permissions-db"></a> 사용자 읽기, 쓰기 또는 데이터 정의 언어 (DDL) 권한을 데이터베이스 제공

사용자 스크립트를 실행 하는 동안 다른 데이터베이스에서 데이터를 읽는 사용자 필요할 수 있습니다. 사용자 테이블로 데이터를 쓰고 결과 저장할 새 테이블을 만드는 해야 할 수 있습니다.

각 Windows 사용자 계정 또는 R 또는 Python 스크립트를 실행 하는 SQL 로그인에 대 한 권한이 있는지 확인 하는 적절 한 특정 데이터베이스에서: `db_datareader`하십시오 `db_datawriter`, 또는 `db_ddladmin`합니다.

다음 예를 들어 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 SQL 로그인을 제공 *MySQLLogin* T-SQL 쿼리를 실행할 수 있는 권한을 합니다 *ML_Samples* 데이터베이스. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.

```SQL
USE ML_Samples
GO
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'
```

각 역할에 포함 된 사용 권한에 대 한 자세한 내용은 참조 하세요. [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)입니다.


### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기

Machine learning 데이터 과학 클라이언트 컴퓨터에서 솔루션을 만들 수 있습니다. SQL Server 컴퓨터에 계산 컨텍스트로 사용 하 여 코드를 실행 하는 경우 두 가지 옵션이 있습니다:는 Windows를 사용 하 여 계정 또는 SQL 로그인을 사용 하 여 인스턴스에 액세스 합니다.

+ SQL 로그인에 대 한: 로그인 위치 데이터를 읽을 데이터베이스에 적절 한 권한이 있는지 확인 합니다. 추가 하 여이 수행할 수 있습니다 *연결할* 하 고 *선택* 권한 또는 로그인을 추가 하 여는 `db_datareader` 역할. 할당 개체를 만들려면 `DDL_admin` 권한. 데이터 테이블을 저장 해야 하는 경우에 추가 된 `db_datawriter` 역할입니다.

+ Windows 인증을 위해: 인스턴스 이름 및 기타 연결 정보를 지정 하는 데이터 과학 클라이언트에서 ODBC 데이터 소스를 만들려면 해야 할 수 있습니다. 자세한 내용은 [ODBC 데이터 원본 관리자](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator)합니다.

## <a name="suggested-optimizations"></a>제안 된 최적화

모든 작업을 수행 해야 했으므로 기계 학습을 지원 하도록 서버를 최적화할 수도 있습니다 또는 미리 학습 된 모델 설치 합니다.

### <a name="add-more-worker-accounts"></a>더 많은 작업자 계정을 추가 합니다.

스크립트를 동시에 실행 하 여 많은 사용자를 예상 하는 경우에 실행 패드 서비스에 할당 된 작업자 계정 수를 늘릴 수 있습니다. 자세한 내용은 [SQL Server Machine Learning Services에 대 한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

### <a name="optimize-the-server-for-script-execution"></a>스크립트 실행에 대 한 서버를 최적화 합니다.

에 대 한 기본 설정을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 다양 한 추출, 변환 및 로드 (ETL) 프로세스를 보고, 감사에 포함 될 수 있는 데이터베이스 엔진에 의해 지원 되는 서비스에 대 한 서버의 균형을 최적화 하려는 설치 하 고 사용 하는 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터입니다. 따라서 기본 설정에서 machine learning 위한 리소스는 경우에 따라 제한 또는 제한, 특히 메모리 사용량이 많은 작업을 찾을 수 있습니다.

Machine learning 작업 우선 순위와 정보를 적절 하 게 되도록 SQL Server 리소스 관리자를 사용 하 여 외부 리소스 풀을 구성 하는 것이 좋습니다. 에 할당 된 메모리 양을 변경할 수도 있습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 실행 되는 계정의 수를 늘리거나 데이터베이스 엔진는 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스입니다.

- 외부 리소스를 관리 하기 위한 리소스 풀을 구성 하려면 참조 [외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)합니다.
  
- 데이터베이스에 대해 예약 된 메모리 양을 변경 하려면 [서버 메모리 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)합니다.
  
- 가 시작할 수 있는 R 계정의 수를 변경 하려면 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]를 참조 하세요 [machine learning 위한 사용자 계정 풀 수정](../r/modify-the-user-account-pool-for-sql-server-r-services.md)합니다.

Standard Edition을 사용 하는 리소스 관리자가 없는 경우 동적 관리 뷰 (Dmv) 및 확장 이벤트 뿐만 아니라 Windows 이벤트 모니터링, 서버 리소스를 관리 하는 데 사용할 수 있습니다. 자세한 내용은 참조 하세요. [모니터링 및 R Services를 관리](../r/managing-and-monitoring-r-solutions.md) 하 고 [모니터링 서비스 및 관리 Python](../python/managing-and-monitoring-python-solutions.md)합니다.

### <a name="install-additional-r-packages"></a>추가 R 패키지 설치

SQL Server에 대 한 만든 R 솔루션은 기본 R 함수, 타사 R 패키지 및 SQL Server와 함께 설치 되는 전용 패키지에서 함수를 SQL Server로 설치 하는 오픈 소스 R의 버전과 호환으로 호출할 수 있습니다.

SQL Server에서 사용할 패키지는 인스턴스에서 사용되는 기본 라이브러리에 설치되어야 합니다. 컴퓨터에서 R의 별도 설치를 수행한 경우, 사용자 라이브러리에 패키지를 설치한 경우에 T-SQL에서 해당 패키지를 사용할 수 없습니다.

R 패키지 설치 및 관리에 대 한 프로세스는 SQL Server 2016 및 SQL Server 2017에서 다릅니다. SQL Server 2016에서 데이터베이스 관리자는 사용자에 게 필요한 R 패키지를 설치 해야 합니다. SQL Server 2017에서 데이터베이스별 수준에서 패키지를 공유 하도록 사용자 그룹을 설정할 수도 있고 사용자가 자신의 패키지를 설치할 수 있도록 하려면 데이터베이스 역할을 구성할 수 있습니다. 자세한 내용은 [SQL Server에서 새 R 패키지 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.


## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드를 사용 하 여 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대 한 답변을 다음 문서를 참조 하세요.

* [업그레이드 및 설치 FAQ-Machine Learning 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 R을 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: T-SQL에서 R 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는 이러한 자습서를 수행 하 여 SQL Server를 사용 하 여 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: t-sql로 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스 내 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.
