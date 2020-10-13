---
title: Linux의 SQL Server에 대해 가용성 그룹 만들기 및 구성
description: 이 자습서에서는 SQL Server on Linux에 대한 가용성 그룹을 만들고 구성하는 방법과 가용성 그룹 엔드포인트 및 인증서를 만드는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 075a2e7ed11abe0ceadfa4f50ba82ca57ff97f0e
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91785157"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>Linux의 SQL Server에 대해 가용성 그룹 만들기 및 구성

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 자습서에서는 Linux에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 대해 가용성 그룹을 만들고 구성하는 방법을 보여 줍니다. Windows의 [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] 및 이전 버전과 달리 기본 Pacemaker 클러스터를 먼저 만들거나 만들지 않고 AG를 사용하도록 설정할 수 있습니다. 필요에 따라 나중까지 클러스터와 연결되지 않을 수 있습니다.

이 자습서에는 다음 작업이 포함되어 있습니다.
 
> [!div class="checklist"]
> * 가용성 그룹을 사용하도록 설정합니다.
> * 가용성 그룹 엔드포인트 및 인증서를 만듭니다.
> * SSMS([!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]) 또는 Transact-SQL을 사용하여 가용성 그룹을 만듭니다.
> * Pacemaker에 대한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 로그인 및 사용 권한을 만듭니다.
> * Pacemaker 클러스터에서 가용성 그룹 리소스를 만듭니다(외부 형식만 해당).

## <a name="prerequisite"></a>필수 요소
- [Linux의 SQLServer에 대한 Pacemaker 클러스터 배포](sql-server-linux-deploy-pacemaker-cluster.md)에 설명된 대로 Pacemaker 고가용성 클러스터를 배포합니다.


## <a name="enable-the-availability-groups-feature"></a>가용성 그룹 기능 사용

Windows에서와 달리 PowerShell 또는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Configuration Manager를 사용하여 AG(가용성 그룹) 기능을 사용하도록 설정할 수 없습니다. Linux에서는 이 기능을 사용하도록 설정하려면 `mssql-conf`를 사용해야 합니다. 가용성 그룹 기능을 사용하도록 설정하는 방법에는 `mssql-conf` 유틸리티를 사용하거나 `mssql.conf` 파일을 수동으로 편집하는 두 가지 방법이 있습니다.

> [!IMPORTANT]
> AG 기능은 [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]에서도 구성 전용 복제본에 사용하도록 설정해야 합니다.

### <a name="use-the-mssql-conf-utility"></a>mssql-conf 유틸리티 사용

프롬프트에서 다음을 실행합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>mssql.conf 파일 편집

`/var/opt/mssql` 폴더 아래에 있는 `mssql.conf` 파일을 수정하여 다음 줄을 추가할 수도 있습니다.

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-ssnoversion-md"></a>[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 다시 시작
Windows에서와 같이 가용성 그룹을 사용하도록 설정한 후 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 다시 시작해야 합니다. 이러한 작업은 다음을 통해 수행할 수 있습니다.

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>가용성 그룹 엔드포인트 및 인증서 만들기

가용성 그룹은 통신에 TCP 엔드포인트를 사용합니다. Linux에서 AG의 엔드포인트는 인증에 인증서를 사용하는 경우에만 지원됩니다. 즉, 한 인스턴스의 인증서를 동일한 AG에 참여하는 복제본이 될 다른 모든 인스턴스에서 복원해야 합니다. 구성 전용 복제본의 경우에도 인증서 프로세스가 필요합니다. 

엔드포인트를 만들고 인증서를 복원하는 작업은 Transact-SQL을 통해서만 수행할 수 있습니다. [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 생성하지 않은 인증서도 사용할 수 있습니다. 또한 만료되는 인증서를 관리하고 바꾸는 프로세스도 필요합니다.

> [!IMPORTANT]
> [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 마법사를 사용하여 AG를 만들려는 경우에도 Linux에서 Transact-SQL을 사용하여 인증서를 만들고 복원해야 합니다.

다양한 명령에 사용할 수 있는 옵션의 전체 구문(예: 추가 보안)에 대해서는 다음을 참조하세요.

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [CREATE CERTIFICATE](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 가용성 그룹을 만드는 경우에도 일부 기본 측면이 현재는 더 이상 사용되지 않는 기능과 공유되므로 해당 엔드포인트 유형은 *FOR DATABASE_MIRRORING*을 사용합니다.

이 예제에서는 3개 노드 구성을 위한 인증서를 만듭니다. 인스턴스 이름은 LinAGN1, LinAGN2 및 LinAGN3입니다.

1.  LinAGN1에서 다음을 실행하여 마스터 키, 인증서 및 엔드포인트를 만들고 인증서를 백업합니다. 이 예제에서는 일반적인 TCP 포트 5022이 엔드포인트에 사용됩니다.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN1_Cert
    WITH SUBJECT = 'LinAGN1 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN1_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN1_Cert,
        ROLE = ALL);
    
    GO
    ```
    
2.  LinAGN2에 대해 동일한 작업을 수행합니다.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    WITH SUBJECT = 'LinAGN2 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN2_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN2_Cert,
        ROLE = ALL);
    
    GO
    ```
    
3.  마지막으로 LinAGN3에서 동일한 시퀀스를 수행합니다.
    
    ```SQL
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<StrongPassword>';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    WITH SUBJECT = 'LinAGN3 AG Certificate';
    
    GO
    
    BACKUP CERTIFICATE LinAGN3_Cert
    TO FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
    CREATE ENDPOINT AGEP
    STATE = STARTED
    AS TCP (
        LISTENER_PORT = 5022,
        LISTENER_IP = ALL)
    FOR DATABASE_MIRRORING (
        AUTHENTICATION = CERTIFICATE LinAGN3_Cert,
        ROLE = ALL);
    
    GO
    ```
    
4.  `scp` 또는 다른 유틸리티를 사용하여 AG에 포함될 각 노드에 인증서의 백업을 복사합니다.
    
    이 예제에서는 다음과 같이 복사합니다.
    
    - LinAGN1_Cert.cer을 LinAGN2 및 LinAGN3에 복사합니다.
    - LinAGN2_Cert.cer을 LinAGN1 및 LinAGN3에 복사합니다.
    - LinAGN3_Cert.cer을 LinAGN1 및 LinAGN2에 복사합니다.
    
5.  복사한 인증서 파일과 관련된 소유권 및 그룹을 `mssql`로 변경합니다.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  LinAGN1에서 LinAGN2 및 LinAGN3과 연결된 인스턴스 수준 로그인 및 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  LinAGN1에서 LinAGN2_Cert 및 LinAGN3_Cert를 복원합니다. 다른 복제본의 인증서를 유지하는 것이 AG 통신 및 보안의 중요한 측면입니다.
    
    ```SQL
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
8.  Grant the logins associated with LinAG2 and LinAGN3 permission to connect to the endpoint on LinAGN1.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
9.  LinAGN2에서 LinAGN1 및 LinAGN3과 연결된 인스턴스 수준 로그인 및 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. LinAGN2에서 LinAGN1_Cert 및 LinAGN3_Cert를 복원합니다.
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    ```
    
11. LinAGN2의 엔드포인트에 연결하기 위한 LinAG1 및 LinAGN3 권한과 관련된 로그인을 부여합니다.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. LinAGN3에서 LinAGN1 및 LinAGN2와 연결된 인스턴스 수준 로그인 및 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. LinAGN3에서 LinAGN1_Cert 및 LinAGN2_Cert를 복원합니다. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    ```
    
14. LinAGN3의 엔드포인트에 연결하기 위한 LinAG1 및 LinAGN2 권한과 관련된 로그인을 부여합니다.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>가용성 그룹 만들기

이 섹션에서는 SSMS([!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]) 또는 Transact-SQL을 사용하여 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 대한 가용성 그룹을 만드는 방법을 설명합니다.

### <a name="use-ssmanstudiofull-md"></a>[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 사용

이 섹션에서는 새 가용성 그룹 마법사에서 SSMS를 사용하여 외부 클러스터 유형의 AG를 만드는 방법을 보여 줍니다.

1.  SSMS에서 **Always On 고가용성**을 확장하고 **가용성 그룹** 을 마우스 오른쪽 단추로 클릭한 후 **새 가용성 그룹 마법사**를 선택합니다.

2.  소개 페이지에서 **다음**을 클릭합니다.

3.  가용성 그룹 옵션 지정 대화 상자에서 가용성 그룹의 이름을 입력하고 드롭다운에서 클러스터 유형으로 외부 또는 없음을 선택합니다. Pacemaker를 배포하는 경우 외부를 사용해야 합니다. 읽기 확장과 같은 특수한 시나리오의 경우에는 없음을 사용합니다. 데이터베이스 수준 상태 검색 옵션을 선택하는 것은 선택 사항입니다. 이 옵션에 대한 자세한 내용은 [가용성 그룹 데이터베이스 수준의 상태 검색 장애 조치(failover) 옵션](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)을 참조하세요. **다음**을 클릭합니다.

    ![가용성 그룹 만들기 03](./media/sql-server-linux-create-availability-group/image3.png)

4.  데이터베이스 선택 대화 상자에서 AG에 참여할 데이터베이스를 선택합니다. 각 데이터베이스를 AG에 추가하려면 먼저 전체 백업이 있어야 합니다. **다음**을 클릭합니다.

5.  복제본 지정 대화 상자에서 **복제본 추가**를 클릭합니다.

6.  서버에 연결 대화 상자에서 보조 복제본이 될 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 Linux 인스턴스 이름과 연결할 자격 증명을 입력합니다. **연결**을 클릭합니다.

7.  구성 전용 복제본 또는 다른 보조 복제본을 포함할 인스턴스에 대해 앞의 두 단계를 반복합니다.

8.  이제 세 개의 인스턴스가 모두 복제본 지정 대화 상자에 나열됩니다. 클러스터 유형으로 외부를 사용하는 경우 진정한 보조 복제본을 사용될 보조 복제본에 대해, 가용성 모드가 주 복제본의 가용성 모드와 일치하는지와 장애 조치(failover) 모드가 외부로 설정되어 있는지 확인합니다. 구성 전용 복제본의 경우 구성 전용 가용성 모드를 선택합니다.

    다음 예제에서는 클러스터 유형이 외부인 두 개의 복제본과 구성 전용 복제본이 있는 AG를 보여 줍니다.

    ![가용성 그룹 만들기 04](./media/sql-server-linux-create-availability-group/image4.png)

    다음 예제에서는 클러스터 유형이 없음인 두 개의 복제본과 구성 전용 복제본이 있는 AG를 보여 줍니다.

    ![가용성 그룹 만들기 05](./media/sql-server-linux-create-availability-group/image5.png)

9.  백업 기본 설정을 변경하려면 백업 기본 설정 탭을 클릭합니다. AG의 백업 기본 설정에 대한 자세한 내용은 [가용성 복제본에 백업 구성](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)을 참조하세요.

10. 읽을 수 있는 보조 복제본을 사용하거나 읽기 확장을 위해 클러스터 유형이 없음인 AG를 만드는 경우 수신기 탭을 선택하여 수신기를 만들 수 있습니다. 수신기를 나중에 추가할 수도 있습니다. 수신기를 만들려면 **가용성 그룹 수신기 만들기** 옵션을 선택하고 이름, TCP/IP 포트를 입력하고, 고정 DHCP IP 주소 또는 자동으로 할당된 DHCP IP 주소 중 어떤 주소를 사용할지 지정합니다. 클러스터 유형이 없음인 AG의 경우 IP는 고정이어야 하고, 기본 IP 주소로 설정되어야 합니다.

    ![가용성 그룹 만들기 06](./media/sql-server-linux-create-availability-group/image6.png)

11. 읽을 수 있는 시나리오에 대해 수신기를 만드는 경우 SSMS 17.3 이상에서 마법사를 통해 읽기 전용 라우팅을 만들 수 있습니다. SSMS 또는 Transact-SQL을 통해 나중에 추가할 수도 있습니다. 지금 읽기 전용 라우팅을 추가하려면

    a.  읽기 전용 라우팅 탭을 선택합니다.

    b.  읽기 전용 복제본의 URL을 입력합니다. 이러한 URL은 엔드포인트가 아니라 인스턴스의 포트를 사용한다는 점을 제외하고 엔드포인트와 비슷합니다.

    다.  각 URL을 선택하고 아래쪽에서 읽을 수 있는 복제본을 선택합니다. 여러 개를 선택하려면 Shift 키를 누른 채 선택하거나 클릭하여 끕니다.

12. **다음**을 클릭합니다.

13. 보조 복제본을 초기화하는 방법을 선택합니다. 기본값은 AG에 참여하는 모든 서버에서 동일한 경로를 필요로 하는 [자동 시드](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md)를 사용하는 것입니다. 마법사에서 백업, 복사 및 복원을 수행하거나(두 번째 옵션), 복제본에서 데이터베이스를 수동으로 백업, 복사 및 복원한 경우 조인하거나(세 번째 옵션), 나중에 데이터베이스를 추가합니다(마지막 옵션). 인증서를 사용할 때와 마찬가지로 수동으로 백업 및 복사하는 경우 백업 파일에 대한 사용 권한을 다른 복제본에 대해 설정해야 합니다. **다음**을 클릭합니다.

14. 유효성 검사 대화 상자에서 모든 결과가 성공이 아니면 조사합니다. 수신기를 만들지 않는 경우처럼, 일부 경고는 치명적이지 않고 허용되는 수준입니다. **다음**을 클릭합니다.

15. 요약 페이지에서 **마침**을 클릭합니다. 이제 AG를 만드는 프로세스가 시작됩니다.

16. AG 만들기가 끝나면 결과에서 **닫기**를 클릭합니다. 이제 동적 관리 뷰 뿐만 아니라 SSMS의 Always On 고가용성 폴더 아래에서도 복제본에 대한 AG를 확인할 수 있습니다.

### <a name="use-transact-sql"></a>Transact-SQL 사용

이 섹션에서는 Transact-SQL을 사용하여 AG를 만드는 예를 보여 줍니다. AG를 만든 후에 수신기와 읽기 전용 라우팅을 구성할 수 있습니다. AG 자체는 `ALTER AVAILABILITY GROUP`을 사용하여 수정할 수 있지만 클러스터 유형 변경은 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]에서 수행할 수 없습니다. 클러스터 유형으로 외부를 사용하여 AG를 만들지 않은 경우 삭제한 후 클러스터 유형이 없음을 사용하여 다시 만들어야 합니다. 추가 정보 및 기타 옵션은 다음 링크에서 찾을 수 있습니다.

-   [CREATE AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [가용성 그룹에 대한 읽기 전용 라우팅 구성(SQL Server)](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [가용성 그룹 수신기 만들기 또는 구성(SQL Server)](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>예제 1 - 구성 전용 복제본을 포함하는 두 개의 복제본(외부 클러스터 유형)

이 예제에서는 구성 전용 복제본을 사용하는 두 개의 복제본 AG를 만드는 방법을 보여 줍니다.

1.  데이터베이스의 전체 읽기/쓰기 복사본을 포함하는 주 복제본이 될 노드에서 작업을 실행합니다. 이 예제에서는 자동 시드를 사용합니다.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1' WITH (
       ENDPOINT_URL = N' TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       SEEDING_MODE = AUTOMATIC),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       AVAILABILITY_MODE = CONFIGURATION_ONLY);
       
    GO
    ```
    
2.  다른 복제본에 연결된 쿼리 창에서 다음을 실행하여 AG에 복제본을 조인하고 주 복제본에서 보조 복제본으로의 시드 프로세스를 시작합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. 구성 전용 복제본에 연결된 쿼리 창에서 AG에 조인합니다.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>예제 2 - 읽기 전용 라우팅을 사용하는 3개의 복제본(외부 클러스터 유형)

이 예제에서는 세 개의 전체 복제본과 읽기 전용 라우팅을 초기 AG 생성의 일부로 구성할 수 있는 방법을 보여 줍니다.

1.  데이터베이스의 전체 읽기/쓰기 복사본을 포함하는 주 복제본이 될 노드에서 작업을 실행합니다. 이 예제에서는 자동 시드를 사용합니다.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = EXTERNAL)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN2.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:1433')),
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN3.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN2.FullyQualified.Name:1433')),
    N'LinAGN3' WITH (
       ENDPOINT_URL = N'TCP://LinAGN3.FullyQualified.Name:5022',
       FAILOVER_MODE = EXTERNAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = SYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN3.FullyQualified.Name:1433'))
    LISTENER '<ListenerName>' (WITH IP = ('<IPAddress>', '<SubnetMask>'), Port = 1433);
    
    GO
    ```
    
    이 구성에 대해 유의해야 할 몇 가지 사항은 다음과 같습니다.
    
    - *AGName*은 가용성 그룹의 이름입니다.
    - *DBName*은 가용성 그룹에 사용되는 데이터베이스의 이름입니다. 쉼표로 구분된 이름 목록일 수도 있습니다.
    - *ListenerName*은 기본 서버/노드의 이름과는 다른 이름입니다. *IPAddress*와 함께 DNS에 등록됩니다.
    - *IPAddress*는 *ListenerName*과 연결된 IP 주소입니다. 또한 고유하며, 서버/노드의 IP 주소와 동일하지 않습니다. 애플리케이션 및 최종 사용자는 *ListenerName* 또는 *IPAddress*를 사용하여 AG에 연결합니다.
    - *SubnetMask*는 *IPAddress*의 서브넷 마스크입니다(예: 255.255.255.0).

2.  다른 복제본에 연결된 쿼리 창에서 다음을 실행하여 AG에 복제본을 조인하고 주 복제본에서 보조 복제본으로의 시드 프로세스를 시작합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  세 번째 복제본에 대해 2단계를 반복합니다.

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>예제 3 - 읽기 전용 라우팅을 사용하는 2개의 복제본(없음 클러스터 유형)

이 예제에서는 클러스터 유형 없음을 사용하여 두 개의 복제본 구성을 만드는 방법을 보여 줍니다. 장애 조치(failover)가 필요하지 않은 읽기 확장 조정 시나리오에 사용됩니다. 이 예제에서는 왕복 기능을 사용하여 읽기 전용 라우팅 뿐만 아니라 실제로 주 복제본에 해당하는 수신기를 만듭니다.

1.  데이터베이스의 전체 읽기/쓰기 복사본을 포함하는 주 복제본이 될 노드에서 작업을 실행합니다. 이 예제에서는 자동 시드를 사용합니다.

    ```SQL
    CREATE AVAILABILITY GROUP [<AGName>]
    WITH (CLUSTER_TYPE = NONE)
    FOR DATABASE <DBName>
    REPLICA ON N'LinAGN1'
    WITH (
       ENDPOINT_URL = N'TCP://LinAGN1.FullyQualified.Name: <PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name'.'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL = N'TCP://LinAGN1.FullyQualified.Name:<PortOfInstance>'));
    N'LinAGN2' WITH (
       ENDPOINT_URL = N'TCP://LinAGN2.FullyQualified.Name:<PortOfEndpoint>',
       FAILOVER_MODE = MANUAL,
       SEEDING_MODE = AUTOMATIC,
       AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
       PRIMARY_ROLE (ALLOW_CONNECTIONS = READ_WRITE, READ_ONLY_ROUTING_LIST = (('LinAGN1.FullyQualified.Name', 'LinAGN2.FullyQualified.Name'))),
       SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL, READ_ONLY_ROUTING_URL =N'TCP://LinAGN2.FullyQualified.Name:<PortOfInstance>'));
    LISTENER '<ListenerName>' (WITH IP = ('<PrimaryReplicaIPAddress>', '<SubnetMask>'), Port = <PortOfListener>);
    
    GO
    ```
    
    Where
    - *AGName*은 가용성 그룹의 이름입니다.
    - *DBName*은 가용성 그룹에 사용되는 데이터베이스의 이름입니다. 쉼표로 구분된 이름 목록일 수도 있습니다.
    - *PortOfEndpoint*는 생성된 엔드포인트에서 사용하는 포트 번호입니다.
    - *PortOfInstance*는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]의 인스턴스에서 사용되는 포트 번호입니다.
    - *ListenerName*은 기본 복제본과는 다른 이름이지만 실제로는 사용되지 않습니다.
    - *PrimaryReplicaIPAddress*는 주 복제본의 IP 주소입니다.
    - *SubnetMask*는 *IPAddress*의 서브넷 마스크입니다. 예를 들면 255.255.255.0과 같습니다.
    
2.  AG에 보조 복제본을 가입하고 자동 시드를 시작합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-ssnoversion-md-login-and-permissions-for-pacemaker"></a>Pacemaker에 대한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 로그인 및 사용 권한 만들기

Linux의 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]를 기준으로 하는 Pacemaker 고가용성 클러스터는 가용성 그룹 자체에 대한 권한 뿐만 아니라 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 인스턴스에 대한 액세스 권한이 필요합니다. 이러한 단계를 수행하면 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 로그인하는 방법을 Pacemaker에 알려주는 파일과 함께 로그인 및 관련 사용 권한이 만들어집니다.

1.  첫 번째 복제본에 연결된 쿼리 창에서 다음을 실행합니다.

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  노드 1에서 다음 명령을 입력합니다. 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    그러면 Emacs 편집기가 열립니다.
    
3.  쿼리 창에서 다음 두 줄을 입력합니다.

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  Ctrl 키를 누른 상태에서 X, C를 차례로 눌러 종료하고 파일을 저장합니다.

5.  Execute 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    파일을 잠급니다.

6.  복제본 역할을 할 다른 서버에서 1-5단계를 반복합니다.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Pacemaker 클러스터에서 가용성 그룹 리소스를 만듭니다(외부만 해당).

클러스터 유형으로 외부를 지정하고 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에서 가용성 그룹을 만든 후에는 Pacemaker에서 해당 리소스를 만들어야 합니다. AG와 연결된 두 가지 리소스는 AG 자체와 IP 주소입니다. 수신기 기능을 사용하지 않는 경우 IP 주소 리소스를 구성하는 것이 좋지만 권장 사항입니다.

만든 AG 리소스는 복제본이라는 특수한 종류의 리소스입니다. AG 리소스는 기본적으로 각 노드에 복사본이 있으며, 마스터라는 하나의 제어 리소스가 있습니다. 마스터는 주 복제본을 호스트하는 서버와 연결됩니다. 다른 리소스는 보조 복제본(일반 또는 구성 전용)을 호스트하며 장애 조치(failover) 시 마스터로 승격될 수 있습니다.

[!INCLUDE [bias-sensitive-term-t](../includes/bias-sensitive-term-t.md)]

1.  다음 구문을 사용하여 AG 리소스를 만듭니다.

    **RHEL(Red Hat Enterprise Linux) 및 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >RHEL 7.4에서는 --master를 사용할 때 경고가 발생할 수 있습니다. 이를 방지하려면 `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`를 사용합니다.
   
    **SUSE Linux Enterprise Server(SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
    meta failure-timeout=60s \
    op start timeout=60s \
    op stop timeout=60s \
    op promote timeout=60s \
    op demote timeout=10s \
    op monitor timeout=60s interval=10s \
    op monitor timeout=60s interval=11s role="Master" \
    op monitor timeout=60s interval=12s role="Slave" \
    op notify timeout=60s
    ms ms-ag_cluster <NameForAGResource> \
    meta master-max="1" master-node-max="1" clone-max="3" \
    clone-node-max="1" notify="true" \
    commit
    ```
    
    여기서 *NameForAGResource*는 AG에 대해 이 클러스터 리소스에 지정된 고유한 이름이고, *AGName*은 생성된 AG의 이름입니다.
 
2.  수신기 기능과 연결될 AG의 IP 주소 리소스를 만듭니다.

    **RHEL 및 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForIPResource> ocf:heartbeat:IPaddr2 ip=<IPAddress> cidr_netmask=<Netmask>
    ```

    **SLES**
    
    ```bash
    crm configure \
    primitive <NameForIPResource> \
       ocf:heartbeat:IPaddr2 \
       params ip=<IPAddress> \
          cidr_netmask=<Netmask>
    ```
    
    여기서 *NameForIPResource*는 IP 리소스의 고유한 이름이고 *IPAddress*는 리소스에 할당된 고정 IP 주소입니다. SLES에서는 네트워크 마스크도 제공해야 합니다. 예를 들어, 255.255.255.0은 *네트워크 마스크* 값이 24입니다.
    
3.  IP 주소와 AG 리소스가 동일한 노드에서 실행되고 있는지 확인하려면 공동 배치 제약 조건을 구성해야 합니다.

    **RHEL 및 Ubuntu**
    
    ```bash
    sudo pcs constraint colocation add <NameForIPResource> <NameForAGResource>-master INFINITY with-rsc-role=Master
    ```

    **SLES**
    
    ```bash
    crm configure <NameForConstraint> inf: \
    <NameForIPResource> <NameForAGResource>:Master 
    commit
    ```
    
    여기서 *NameForIPResource*는 는 IP 리소스의 이름이고, *NameForAGResource*는 AG 리소스의 이름이고, SLES의 경우 *NameForConstraint*는 제약 조건의 이름입니다.

4.  AG 리소스가 IP 주소보다 먼저 가동 상태가 되도록 하려면 정렬 제약 조건을 만듭니다. 공동 배치 제약 조건은 정렬 제약 조건을 암시하지만 정렬 제약 조건이 적용됩니다.

    **RHEL 및 Ubuntu**
    
    ```bash
    sudo pcs constraint order promote <NameForAGResource>-master then start <NameForIPResource>
    ```
    
    **SLES**
    
    ```bash
    crm configure \
    order <NameForConstraint> inf: <NameForAGResource>:promote <NameForIPResource>:start
    commit
    ```
    
    여기서 *NameForIPResource*는 는 IP 리소스의 이름이고, *NameForAGResource*는 AG 리소스의 이름이고, SLES의 경우 *NameForConstraint*는 제약 조건의 이름입니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 Linux에서 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]에 대해 가용성 그룹을 만들고 구성하는 방법을 살펴보았습니다. 구체적으로 다음 작업 방법을 알아보았습니다.
> [!div class="checklist"]
> * 가용성 그룹을 사용하도록 설정합니다.
> * AG 엔드포인트 및 인증서를 만듭니다.
> * SSMS([!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)]) 또는 Transact-SQL을 사용하여 AG를 만듭니다.
> * Pacemaker에 대한 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 로그인 및 사용 권한을 만듭니다.
> * Pacemaker 클러스터에서 AG 리소스를 만듭니다.

업그레이드 및 장애 조치(failover)를 비롯한 대부분의 AG 관리 작업에 대해서는 다음을 참조하세요.

> [!div class="nextstepaction"]
> [Linux의 SQL Server에 대해 HA 가용성 그룹 작동](sql-server-linux-availability-group-failover-ha.md)

