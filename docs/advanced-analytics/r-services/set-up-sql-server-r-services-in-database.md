---
title: "SQL Server R Services(In-Database) 설치 | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
keywords: 
  - "SQL Server R Services 설치"
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: 35
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 30
---
# SQL Server R Services(In-Database) 설치
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 이상에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 마법사를 사용하여 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에 관련된 모든 구성 요소를 설치할 수 있습니다.  
 
 
 설치를 완료한 후 R Services 기능을 사용하고, 계정을 구성하고, 특정 데이터베이스에 대한 사용 권한을 사용자에게 부여하기 위해 몇 가지 추가 단계가 필요할 수 있습니다.   
  
설치를 완료한 후 데이터베이스 액세스에 문제가 있거나 이전 버전을 제거해야 하는 경우 [업그레이드 및 설치 FAQ&#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)를 참조하세요.  

> [!NOTE]
> R Services(In-Database)를 설치하려면 기능이 설치되어 있는 드라이브에서 8dot3 표기법을 사용하여 짧은 파일 이름을 만들 수 있도록 지원해야 합니다. 지원하지 않으면 SQL Server에서 R을 시작하는 프로세스를 시작하지 못할 수 있습니다. R Services를 설치하기 전에 볼륨에서 8dot3 표기법을 사용하도록 설정해야 합니다. 이 제한은 향후 릴리스에서 제거됩니다.

  
##  <a name="a-namebkmkinstallrservicesindatabasea-step-1-install-r-services-in-database-on-sql-server-2016-or-later"></a><a name="bkmk_installRServicesInDatabase"></a> 1단계: SQL Server 2016 이상에 R Services(In-Database) 설치  
   
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램을 실행합니다.  
  
    무인 설치를 수행하는 방법에 대한 정보는 [Unattended Installs of SQL Server R Services](../../advanced-analytics/r-services/unattended-installs-of-sql-server-r-services.md)을(를) 참조하십시오.  
  
2.  **설치** 탭에서 **새 SQL Server 독립 실행형 설치 또는 기존 설치에 기능 추가**를 클릭합니다.  
  
    > [!NOTE]  
    >  장애 조치(Failover) 클러스터에는 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치할 수 없습니다. 그러나 Always On을 사용하고 가용성 그룹의 일부인 독립 실행형 컴퓨터에 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치할 수 있습니다. Always On 가용성 그룹에서 R Services를 사용하는 방법에 대한 자세한 내용은 [Always On 가용성 그룹: 상호 운용성](../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)을 참조하세요.  
  
3.  **기능 선택** 페이지에서 다음 옵션을 선택합니다.  
  
    -   **데이터베이스 엔진 서비스**  
  
         [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]을(를) 사용하려면 데이터베이스 엔진 인스턴스가 하나 이상 필요합니다. 기본 인스턴스나 명명된 인스턴스를 사용할 수 있습니다.  
  
    -   **R Services(In-Database)**  
  
         이 옵션은 R 작업에 사용되는 데이터베이스 서비스를 구성하며 외부 스크립트 및 프로세스를 지원하는 확장 프로그램을 설치합니다.  
    > [!NOTE]
    > 
    > [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 R 코드를 실행해야 하는 경우 **[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]**를 설치하세요. 
    > 
    > 이와 달리, Microsoft R Server(독립 실행형)는 SQL Server를 실행하지 않는 Windosw 컴퓨터에서 ScaleR 라이브러리를 사용할 수 있게 해주는 옵션입니다. R 개발에 사용되는 노트북이나 기타 컴퓨터에 Microsoft R Server(독립 실행형)를 설치하여 나중에 R Services(In-Database)를 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 배포할 수 있는 R 솔루션을 만드는 것이 좋습니다.
 
  
4.  **Microsoft R Open 설치에 동의** 페이지에서 **동의**를 클릭합니다.  
  
     이 사용권 계약은 Revolution Analytics의 연결 공급자 및 고급 R 패키지와 함께 오픈 소스 R 기본 패키지 및 도구 배포가 포함된 Microsoft R Open을 다운로드하는 데 필요합니다.  
  
    > [!NOTE]  
    >  사용 중인 컴퓨터가 인터넷에 연결되어 있지 않으면 이 시점에서 설치를 일시 중지하여 [인터넷에 액세스하지 않고 R 구성 요소 설치](../../advanced-analytics/r-services/installing-r-components-without-internet-access.md)의 설명에 따라 설치 관리자를 별도로 다운로드할 수 있습니다.  
  
     **동의**를 클릭하고, **다음** 단추가 활성화될 때까지 클릭한 후 **다음**을 클릭합니다.  
  
5.  **설치 준비 완료** 페이지에서 이러한 선택 사항이 포함되어 있는지 확인하고 **설치**를 클릭합니다.  
  
     **기능**  
  
     데이터베이스 엔진 서비스  
  
     R Services(In-Database)  
  
6.  설치가 완료되면 컴퓨터를 다시 시작합니다.   
  
  
##  <a name="a-namebkmkenablefeaturea-step-2-enable-r-services-and-verify-that-local-r-script-execution-works"></a><a name="bkmk_enableFeature"></a> 2단계: R Services를 사용하도록 설정하고 로컬 R 스크립트 실행이 작동하는지 확인  
  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 엽니다. 아직 설치되지 않은 경우 SQL Server 설치 마법사를 다시 실행하여 다운로드 링크를 열고 설치할 수 있습니다.  
  
2. R Services(In-Database)를 설치한 인스턴스에 연결하고 다음 명령을 실행하여 명시적으로 R Services 기능을 사용하도록 설정합니다. 설정하지 않으면 설치 프로그램을 통해 기능이 설치된 경우에도 R 스크립트를 호출할 수 없습니다.  
  
   ```    
   Exec sp_configure  'external scripts enabled', 1  
   Reconfigure  with override    
   ```  
  
10. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 대한 SQL Server 서비스를 다시 시작합니다. 그러면 관련 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스도 자동으로 다시 시작됩니다. 제어판의 서비스 패널을 사용하거나 SQL Server 구성 관리자를 사용하여 서비스를 다시 시작할 수 있습니다.  
  
9. SQL Server 서비스가 제공된 후 다음 명령을 실행하고 *run_value*가 1로 설정되었는지 확인하여 R 기능을 사용할 수 있는지 확인합니다.  
  
    ```    
    Exec sp_configure  'external scripts enabled'    
    ```  
   필요에 따라 **서비스** 패널을 열고 인스턴스에 대한 실행 패드 서비스가 실행되고 있는지 확인합니다. 각 인스턴스에 해당 실행 패드 서비스가 있습니다.
   
10. 이제 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 다음과 같은 간단한 R 스크립트를 실행할 수 있습니다.  
  
    ```  
    exec sp_execute_external_script  @language =N'R',  
    @script=N'OutputDataSet<-InputDataSet',    
    @input_data_1 =N'select 1 as hello'  
    with result sets (([hello] int not null));  
    go  
    ```  
  
    **Results**  
  
    *hello*  
    *1*   
  
> [!IMPORTANT]  원격 데이터 과학 클라이언트에서 R 명령을 실행하거나 SQL Server 데이터에 액세스해야 하는 경우 몇 가지 추가 단계가 필요합니다. 다음 단계는 이러한 추가 요구 사항을 자세히 설명합니다.
 
  
##  <a name="a-namebkmkconfigureaccountsa-step-3-enable-implied-authentication-for-launchpad-accounts"></a><a name="bkmk_configureAccounts"></a> 3단계: 실행 패드 계정에 암시적 인증 사용  
   
  
설치하는 동안 [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] 서비스의 보안 토큰으로 태스크를 실행하기 위해 새 Windows 사용자 계정 20개가 생성됩니다. 사용자가 외부 클라이언트에서 R 스크립트를 보내면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 사용 가능한 작업자 계정을 활성화하고 호출하는 사용자의 ID에 매핑한 다음 사용자를 대신하여 R 스크립트를 실행합니다. 이는 외부 스크립트의 보안 실행을 지원하는 데이터베이스 엔진의 새로운 서비스이며, *암시적 인증*이라고 합니다. 

Windows 사용자 그룹 **SQLRUserGroup**에서 해당 계정을 볼 수 있습니다.  원격 데이터 과학 클라이언트에서 R 스크립트를 실행해야 하고 Windows 인증을 사용하는 경우 사용자 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 로그인할 수 있는 권한을 이러한 작업자 계정에 부여해야 합니다.  
  
1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 개체 탐색기에서 **보안**을 확장하고 **로그인**을 마우스 오른쪽 단추로 클릭한 다음 **새 로그인**을 선택합니다.  
2. **로그인 - 새로 만들기** 대화 상자에서 **검색**을 클릭합니다.  
3. **개체 유형**을 클릭하고 **그룹**을 선택합니다. 다른 모든 항목의 선택을 취소합니다.  
4. 선택할 개체 이름 입력에서 *SQLRUserGroup*을 입력하고 **이름 확인**을 클릭합니다.  
5. 인스턴스의 실행 패드 서비스와 연결된 로컬 그룹의 이름이 *instancename\SQLRUserGroup*과 같은 이름으로 확인되어야 합니다. **확인**을 클릭합니다.  
6. 기본적으로 로그인은 **public** 역할에 할당되며 데이터베이스 엔진에 연결할 수 있는 권한이 있습니다. 
7. **확인**을 클릭합니다.  
  
> [!NOTE] SQL Server 계산 컨텍스트에서 R 스크립트를 실행하기 위해 SQL 로그인을 사용하는 경우에는 이 추가 단계가 필요하지 않습니다.
  
  
## <a name="step-4-give-non-admin-users-r-script-permissions"></a>4단계: 관리자가 아닌 사용자에게 R 스크립트 사용 권한 부여  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 직접 설치했으며 해당 인스턴스에서 R 스크립트를 실행하는 경우 일반적으로 관리자 권한으로 스크립트를 실행하므로 다양한 작업 및 데이터베이스의 모든 데이터에 대한 암시적 권한이 있으며 새 R 패키지를 설치할 수 있습니다.  
  
그러나 엔터프라이즈 시나리오에서 SQL 로그인을 사용하여 데이터베이스에 액세스하는 사용자를 비롯한 대부분의 사용자에게는 이러한 상승된 권한이 없습니다. 따라서 외부 스크립트를 실행할 각 사용자에 대해 R이 사용될 각 데이터베이스에서 R 스크립트를 실행할 수 있는 권한을 사용자에게 부여해야 합니다.   
  
  
```  
USE <database_name>  
GO  
GRANT EXECUTE ANY EXTERNAL SCRIPT  TO [UserName]  
```  

> [!TIP] 설치와 관련된 도움이 필요하세요? 모든 단계를 실행했는지 확인하고 싶으세요?
>
> 이러한 사용자 지정 보고서를 사용하여 R Services의 설치 상태를 확인합니다. 자세한 내용은 [사용자 지정 보고서를 사용하여 R Services 모니터링](../../advanced-analytics/r-services/monitor-r-services-using-custom-reports-in-management-studio.md)을 참조하세요.    
  
##  <a name="a-namebkmkadditionala-optional-modifications"></a><a name="bkmk_Additional"></a> 선택적 수정  
  
이 섹션에서는 인스턴스 또는 데이터 과학 클라이언트의 구성에서 R 스크립트 실행을 지원하기 위해 추가로 변경할 수 있는 내용을 설명합니다.
  
### <a name="modify-the-number-of-worker-accounts-used-by-includersqllaunchpadtokenrsqllaunchpadmdmd"></a>[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]에서 사용하는 작업자 계정 수 수정
  
R을 많이 사용하거나 여러 사용자가 동시에 스크립트를 실행할 것으로 예상되는 경우 실행 패드 서비스에 할당된 작업자 계정 수를 늘릴 수 있습니다. 자세한 내용은 [SQL Server R Services용 사용자 계정 풀 수정](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)을 참조하세요.  
  
  
### <a name="give-your-r-users-or-logins-read-write-or-ddl-permissions-as-needed-in-additional-databases"></a>추가 데이터베이스에서 필요에 따라 R 사용자 또는 로그인에 읽기, 쓰기 또는 DDL 사용 권한 부여  
  
R 스크립트를 실행하는 동안 사용자 계정이 다른 데이터베이스에서 데이터를 읽고, 결과를 저장할 새 테이블을 만들고, 테이블에 데이터를 써야 할 수도 있습니다. 
     
R 스크립트를 실행할 각 사용자의 사용자 계정에 특정 데이터베이스에 대한 **db_datareader**, **db_datawriter** 또는 **db_ddladmin** 권한이 있는지 확인합니다.   
       
예를 들어 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 *RSamples* 데이터베이스에서 T-SQL 쿼리를 실행할 수 있는 권한을 SQL 로그인 *MySQLLogin*에 부여합니다. 이 문을 실행하려면 SQL 로그인이 서버의 보안 컨텍스트에 이미 있어야 합니다.  
  
```  
USE RSamples  
GO  
EXEC sp_addrolemember 'db_datareader', 'MySQLLogin'  
```  
  
각 역할에 포함된 사용 권한에 대한 자세한 내용은 [데이터베이스 수준 역할](../../relational-databases/security/authentication-access/database-level-roles.md)을 참조하세요.  
  
  
### <a name="create-an-odbc-data-source-for-the-instance-on-your-data-science-client"></a>데이터 과학 클라이언트의 인스턴스에 대한 ODBC 데이터 원본 만들기  
  
데이터 과학 클라이언트 컴퓨터에서 R 솔루션을 만들고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터에 계산 컨텍스트로 연결해야 하는 경우 SQL 로그인 또는 Windows 통합 인증을 사용할 수 있습니다.  
  
SQL 로그인을 사용하는 경우 데이터를 읽을 데이터베이스에 대한 적절한 권한이 로그인에 있는지 확인합니다. 이렇게 하려면 *연결* 및 *SELECT* 권한을 추가하거나 로그인을 **db_datareader** 역할에 추가합니다. 개체를 만들어야 하는 경우 **DDL_admin** 권한이 필요합니다.  테이블에 데이터를 저장하려면 **db_datawriter** 역할에 로그인을 추가합니다.  
  
Windows 인증을 사용하는 경우 데이터 과학 클라이언트에서 해당 인스턴스 이름 및 기타 연결 정보를 지정하는 ODBC 데이터 원본을 구성해야 합니다.  
  
자세한 내용은 [ODBC 데이터 원본 관리자 사용](http://windows.microsoft.com/windows/using-odbc-data-source-administrator)을 참조하세요.  
  
### <a name="optimize-the-server-for-r"></a>R에 맞게 서버 최적화  

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 대한 기본 설정은 데이터베이스 엔진에서 지원하는 다양한 서비스에 맞게 서버의 균형을 최적화하기 위한 것입니다. 이러한 서비스에는 ETL 프로세스, 보고, 감사 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 사용하는 응용 프로그램이 포함될 수 있습니다. 따라서 기본 설정을 사용할 경우, 특히 메모리를 많이 사용하는 작업에서는 R 작업에 대한 리소스가 제한될 수도 있습니다.  
  
 R 태스크에 적절한 우선 순위와 리소스가 지정되도록 리소스 관리자를 사용하여 R 작업과 관련된 외부 리소스 풀을 구성하는 것이 좋습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 엔진에 할당된 메모리 크기를 변경하거나 [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] 서비스에서 실행되는 계정 수를 늘릴 수도 있습니다.  
  
-   외부 리소스 관리를 위해 리소스 풀 구성  
  
     [CREATE EXTERNAL RESOURCE POOL&#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md)  
  
-   데이터베이스 엔진에 예약된 메모리 양 변경  
  
     [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md)  
  
-   [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]에서 시작할 수 있는 R 계정 수 변경  
  
     [SQL Server R Services용 사용자 계정 풀 수정](../../advanced-analytics/r-services/modify-the-user-account-pool-for-sql-server-r-services.md)  
  
### <a name="get-the-r-source-code-optional"></a>R 소스 코드 가져오기(선택 사항)  

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]에는 오픈 소스 R 기본 패키지 배포가 포함되어 있습니다.  
  
필요에 따라 다음 링크 중 하나를 클릭하여 수정된 GPL/LGPL 소스 코드 다운로드를 즉시 시작합니다. 소스 코드는 GNU General Public License에 따라 제공되지만 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]를 설치하거나 사용하는 데 필요하지는 않습니다.  
  
-   RC2와 호환: [rre-gpl-src.8.0.2.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786770) 보관 파일 다운로드 
  
-   RC3과 호환: [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkId=786771) 보관 파일 다운로드 

-   RTM과 호환: [rre-gpl-src.8.0.3.tar.gz](http://go.microsoft.com/fwlink/?LinkID=786771) 보관 파일 다운로드
  
## <a name="troubleshooting"></a>문제 해결  
 문제가 발생하나요? [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시험판 버전을 설치할 때 발생하는 일반적인 문제 목록을 참조하세요.  
  
 [업그레이드 및 설치 FAQ&#40;SQL Server R Services&#41;](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md)  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 과학 클라이언트 설정](../../advanced-analytics/r-services/set-up-a-data-science-client.md)   
 [독립 실행형 R 서버 만들기](../../advanced-analytics/r-services/create-a-standalone-r-server.md)  
  
  