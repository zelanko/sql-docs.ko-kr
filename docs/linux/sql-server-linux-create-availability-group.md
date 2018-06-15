---
title: 만들기 및 Linux에서 SQL Server에 대 한 가용성 그룹 구성 | Microsoft Docs
description: 이 자습서에는 만들고 Linux에서 SQL Server에 대 한 가용성 그룹을 구성 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.date: 12/11/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 549b34aa918f65da20c3398e1d38491841b5c6fc
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/19/2018
ms.locfileid: "34323884"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>만들기 및 Linux에서 SQL Server에 대 한 가용성 그룹 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 자습서에서는 가용성 그룹 (AG) 만들기 및 구성 하는 방법에 설명 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux. 와 달리 [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] 이전 버전 windows에서 사용할 수 있습니다 Ag 또는 먼저 기반이 되는 Pacemaker 클러스터를 만들지 않고도 합니다. 클러스터와의 통합 필요에 따라 수행 되지 않으므로 나중에 다시.

이 자습서에는 다음 작업이 포함 됩니다.
 
> [!div class="checklist"]
> * 가용성 그룹을 사용 하도록 설정 합니다.
> * 인증서 및 가용성 그룹 끝점을 만듭니다.
> * 사용 하 여 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) 또는 가용성 그룹을 만드는 TRANSACT-SQL입니다.
> * 만들기는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에 대 한 권한과 로그인 합니다.
> * (외부 형식에만 해당) Pacemaker 클러스터에서 가용성 그룹 리소스를 만듭니다.

## <a name="prerequisite"></a>사전 요구 사항
- 에 설명 된 대로 Pacemaker 고가용성 클러스터를 배포 [Pacemaker 클러스터 Linux에서 SQL Server에 대 한 배포](sql-server-linux-deploy-pacemaker-cluster.md)합니다.


## <a name="enable-the-availability-groups-feature"></a>가용성 그룹 기능을 사용 하도록 설정

와 달리 windows에서는 사용할 수 없습니다 PowerShell 또는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 가용성을 사용할 수 있도록 Configuration Manager (AG) 기능을 그룹화 합니다. Linux를 사용 해야 `mssql-conf` 기능을 활성화 합니다. 가용성 그룹 기능을 활성화 하는 방법은 두 가지가: 사용 하 여는 `mssql-conf` 유틸리티 또는 편집은 `mssql.conf` 파일을 수동으로 백업 합니다.

> [!IMPORTANT]
> 에 구성 전용 복제본에 대 한 AG 기능을 사용할 수 해야 [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]합니다.

### <a name="use-the-mssql-conf-utility"></a>Mssql conf 유틸리티를 사용 하 여

프롬프트에서 다음을 실행 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Mssql.conf 파일 편집

수정할 수도 있습니다는 `mssql.conf` 아래에 있는 파일의 `/var/opt/mssql` 다음 줄을 추가할 폴더:

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>다시 시작 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
다시 시작 해야 windows에서는 가용성 그룹을 사용 하도록 설정한 후 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 다음으로 수행할 수 있습니다.

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>가용성 그룹 끝점을 만들고 인증서

가용성 그룹 통신에 TCP 끝점을 사용합니다. Linux, AG에 대 한 끝점 인증서 인증에 사용 됩니다 하는 경우 지원만 됩니다. 즉, 동일한 AG에 참여 하는 복제본 수 있는 다른 모든 인스턴스에 대 한 인스턴스에서 인증서를 복원할 수 있어야 합니다. 인증서가 구성 전용 복제도 필요 합니다. 

끝점을 만들고 인증서를 복원만 Transact SQL을 통해 수행할 수 있습니다. 비-같이 사용할 수 있습니다.[!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-인증서도 생성 합니다. 프로세스를 관리 하 고 만료 되는 모든 인증서를 대체 해야 합니다.

> [!IMPORTANT]
> 사용 하려는 경우는 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 경우에 AG을 만드는 마법사를 만들고 linux TRANSACT-SQL을 사용 하 여 인증서를 복원 해야 합니다.

다양 한 명령 (예: 추가 보안)에 사용할 수 있는 옵션에 전체 구문에 대 한 참조.

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [인증서 만들기](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 끝점의 형식을 사용 하 여 가용성 그룹을 만들 수는, 있지만 *FOR DATABASE_MIRRORING*일부 기본 측면 이제 사용 되지 않는 기능을 한 번 공유 된 때문에 있습니다.

이 예제에서는 3 개의 노드로 구성에 대 한 인증서를 만듭니다. 인스턴스 이름은 LinAGN1, LinAGN2, 및 LinAGN3는.

1.  다음을 실행 하 여 마스터 키, 인증서 및 끝점을 만들려면 LinAGN1 뿐 아니라 인증서를 백업 합니다. 이 예에서는 일반적인 TCP 포트 5022의 끝점에 대해 사용 됩니다.
    
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
    
2.  LinAGN2에서 동일한 작업을 수행 합니다.
    
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
    
3.  마지막으로 LinAGN3에서 동일한 절차를 수행 합니다.
    
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
    
4.  사용 하 여 `scp` 또는 AG의 일부가 될 각 노드에 인증서의 백업을 복사 하는 다른 유틸리티입니다.
    
    에 대 한 설명은이 다음과 같습니다.
    
    - 복사 LinAGN1_Cert.cer LinAGN2 및 LinAGN3
    - LinAGN1 및 LinAGN3 LinAGN2_Cert.cer 복사 합니다.
    - LinAGN1 및 LinAGN2 LinAGN3_Cert.cer 복사 합니다.
    
5.  소유권과 복사한 인증서 파일을와 연결 된 그룹 변경 `mssql`합니다.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  인스턴스 수준 로그인과 LinAGN2 및 LinAGN3 LinAGN1에 연결 된 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  LinAGN2_Cert 및 LinAGN3_Cert LinAGN1에 복원 합니다. 다른 복제본의 인증서를 중요 한 부분은 AG 통신 및 보안 합니다.
    
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
    
9.  인스턴스 수준 로그인과 LinAGN1 및 LinAGN3 LinAGN2에 연결 된 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10.  LinAGN1_Cert 및 LinAGN3_Cert LinAGN2에 복원 합니다. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN3_Cert
    AUTHORIZATION LinAGN3_User
    FROM FILE = '/var/opt/mssql/data/LinAGN3_Cert.cer';
    
    GO
    
11.  Grant the logins associated with LinAG1 and LinAGN3 permission to connect to the endpoint on LinAGN2.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12.  인스턴스 수준 로그인과 LinAGN1 및 LinAGN2 LinAGN3에 연결 된 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13.  LinAGN1_Cert 및 LinAGN2_Cert LinAGN3에 복원 합니다. 
    
    ```SQL
    CREATE CERTIFICATE LinAGN1_Cert
    AUTHORIZATION LinAGN1_User
    FROM FILE = '/var/opt/mssql/data/LinAGN1_Cert.cer';
    
    GO
    
    CREATE CERTIFICATE LinAGN2_Cert
    AUTHORIZATION LinAGN2_User
    FROM FILE = '/var/opt/mssql/data/LinAGN2_Cert.cer';
    
    GO
    
14.  Grant the logins associated with LinAG1 and LinAGN2 permission to connect to the endpoint on LinAGN3.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>가용성 그룹 만들기

이 섹션에서는 사용 하는 방법을 설명 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) 또는 가용성 그룹을 만드는 데 TRANSACT-SQL [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 사용

이 섹션 SSMS를 사용 하 여 새 가용성 그룹 마법사와 외부의 클러스터 유형 AG를 만드는 방법을 보여 줍니다.

1.  SSMS에서 **Always On 고가용성**를 마우스 오른쪽 단추로 클릭 **가용성 그룹**를 선택 하 고 **새 가용성 그룹 마법사**합니다.

2.  소개 대화 상자에서 클릭 **다음**합니다.

3.  가용성 그룹 옵션 지정 대화 상자에서 가용성 그룹에 대 한 이름을 입력 하 고 클러스터 유형의 외부 웹 서비스 또는 드롭다운 목록에서 없음을 선택 합니다. Pacemaker 배포 될 때 외부를 사용 해야 합니다. None 읽기 확장과 같은 특수 한 시나리오에 대 한이입니다. 데이터베이스 수준 상태 검색에 대 한 옵션을 선택 하면 선택 사항입니다. 이 옵션에 대 한 자세한 내용은 참조 하십시오. [가용성 그룹 데이터베이스 수준 상태 검색 장애 조치 옵션](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)합니다. **다음**을 클릭합니다.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  데이터베이스 선택 대화 상자에서 AG에 참여할 데이터베이스를 선택 합니다. AG에 추가할 수 있습니다 각 데이터베이스는 전체 백업이 있어야 합니다. **다음**을 클릭합니다.

5.  복제본 지정 대화 상자에서 **Add Replica**합니다.

6.  서버 연결 대화 상자, Linux 인스턴스의 이름을 입력 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 보조 복제본과 연결 하려면 자격 증명이 사용 됩니다. **연결**을 클릭합니다.

7.  복제 구성 전용 데이터베이스 또는 다른 보조 복제본을 포함할 인스턴스에 대 한 이전 두 단계를 반복 합니다.

8.  이제 세 인스턴스는 모두 복제본 지정 대화 상자에 나열 됩니다. True 보조 복제본이 될 보조 복제본에 대 한 외부, 클러스터 유형을 사용 해야 하는 경우 주 복제본의 가용성 모드 일치 하 고 장애 조치 모드가 외부로 설정 됩니다. 구성 전용 복제본에 대 한만 구성의 가용성 모드를 선택 합니다.

    다음 예제에서는 두 개의 복제본, 외부, 사용 되는 클러스터 유형의와 구성 전용 복제본 AG 보여 줍니다.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    다음 예제에서는과 2 개의 복제본 AG, None, 및 구성 전용 복제본의 클러스터 유형을 보여 줍니다.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  백업 기본 설정을 변경 하려는 경우는 백업 기본 설정 탭을 클릭 합니다. Ag와 백업 기본 설정에 대 한 자세한 내용은 참조 하십시오. [가용성 복제본에 백업 구성](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)합니다.

10. 읽기 가능한 보조 복제본을 사용 하 여 클러스터를 사용 하 여 AG 만들기 또는 none 읽기 눈금에 대 한 입력 수신기 탭을 선택 하 여 수신기를 만들 수 있습니다. 수신기를 나중에 추가할 수도 있습니다. 옵션을 선택 된 수신기를 만들려면 **가용성 그룹 수신기를 만드는** 이름, TCP/IP 포트 및 정적 또는 자동으로 할당 된 DHCP IP 주소를 사용할 것인지를 입력 합니다. None 클러스터 유형 AG에 대 한 IP 되도록 정적 및 설정 기억 주의 IP 주소입니다.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 를 읽을 수 있는 시나리오에 대 한 수신기를 만드는 경우 17.3 또는 그 이후 버전의 SSMS는 마법사에서 읽기 전용 라우팅의 만들 수 있습니다. SSMS 또는 TRANSACT-SQL을 통해 나중에 추가할 수도 있습니다. 추가 하려면 읽기 전용 라우팅 이제:

    a.  읽기 전용 라우팅 탭을 선택 합니다.

    b.  읽기 전용 복제본에 대 한 Url을 입력 합니다. 이러한 Url 끝점 하지 인스턴스 포트를 사용할 점을 제외 하 고 끝점을와 비슷합니다.

    c.  각 URL을 선택 하 고 아래에서 읽기 가능한 복제본을 선택 합니다. 다중 선택 하려면 SHIFT 또는 클릭 한 후 드래그 누른 합니다.

12. **다음**을 클릭합니다.

13. 보조 복제본은 초기화 하는 방법을 선택 합니다. 기본값은 사용 하도록 [자동 시드](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), AG에 참여 하는 모든 서버에서 동일한 경로 필요 합니다. 마법사를 백업, 복사 및 복원 (두 번째 옵션); 할 수도 있습니다. 수동으로 백업, 복사, 하 고는 복제본에서 데이터베이스를 복원 하는 경우 조인 된 (옵션 3 차); 또는 나중에 데이터베이스 추가 (마지막 옵션). 인증서를 수동으로 백업 하 고 복사 하는 경우와 마찬가지로 백업 파일에 대 한 권한을 다른 복제본에 설정 해야 합니다. **다음**을 클릭합니다.

14. 유효성 검사 대화 상자에서 모든 내용을 가져오지 않은 경우 다시 성공으로를 조사 합니다. 몇 가지 경고가 허용 되지 치명적와 같은 수신기를 만들지 않으면 합니다. **다음**을 클릭합니다.

15. 요약 대화 상자에서 클릭 **마침**합니다. 이제 AG를 만드는 프로세스를 시작 합니다.

16. AG 만들기 완료 되 면 클릭 **닫기** 결과에 있습니다. 이제 SSMS에서 Always On 고가용성 폴더 및 동적 관리 뷰에서 복제본에는 AG를 볼 수 있습니다.

### <a name="use-transact-sql"></a>TRANSACT-SQL 사용

이 섹션에서는 TRANSACT-SQL을 사용 하 여 AG를 만드는 예제를 보여 줍니다. AG 만들어진 후에 수신기 및 읽기 전용 라우팅을 구성할 수 있습니다. 자체 AG으로 수정할 수 `ALTER AVAILABILITY GROUP`에서 수행할 수 없고 클러스터 유형을 변경 하지만 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]합니다. AG 외부 클러스터 유형 만들려는 되지는 않은 경우에 삭제 하 고 none 클러스터 유형 다시 만들어야 합니다. 다음 링크에서 자세한 정보 및 기타 옵션을 찾을 수 있습니다.

-   [CREATE AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [가용성 그룹 (SQL Server)에 대 한 읽기 전용 라우팅 구성](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [(SQL Server)는 가용성 그룹 수신기 만들기 또는 구성](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one--two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>예제 1-2 복제본 함께 구성 전용 복제 (외부 클러스터 유형)

이 예제에는 구성 으로만 이동 가능한 복제본을 사용 하는 두 개의 복제본 AG를 만드는 방법을 보여 줍니다.

1.  데이터베이스의 완전 하 게 읽기/쓰기 복사본을 포함 하는 주 복제본이 될 노드에서 실행 합니다. 이 예제에서는 자동 시드를 사용 합니다.

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
    
2.  다른 복제본에 연결 하는 쿼리 창에서 AG에 복제본을 조인 하 고 보조 복제본에 주 데이터베이스에서 시드 프로세스를 시작 하려면 다음을 실행 합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  구성만 복제본에 연결 하는 쿼리 창에서 AG에 조인 합니다.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two--three-replicas-with-read-only-routing-external-cluster-type"></a>예제 2-3 개의 복제본이 읽기 전용 라우팅 (외부 클러스터 유형) 함께

이 예제에서는 세 개의 전체 복제본과 어떻게 읽기 전용 라우팅 초기 AG 만들기의 일부로 구성할 수 있습니다.

1.  데이터베이스의 완전 하 게 읽기/쓰기 복사본을 포함 하는 주 복제본이 될 노드에서 실행 합니다. 이 예제에서는 자동 시드를 사용 합니다.

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
    
    몇 가지가이 구성에 대 한 참고 사항:
    
    - *AGName* 가용성 그룹의 이름입니다.
    - *DBName* 가용성 그룹에 사용 될 데이터베이스의 이름입니다. 쉼표로 구분 된 이름 목록 일 수도 있습니다.
    - *ListenerName* 는 기본 서버/노드 중 하나가 다른 이름입니다. 와 함께 DNS에 등록 됩니다 *IPAddress*합니다.
    - *IPAddress* 와 연결 된 IP 주소가 *ListenerName*합니다. 고유 이기도 및 서버/노드 중 하나가와 동일 합니다. 응용 프로그램 및 최종 사용자는 사용 하 여 *ListenerName* 또는 *IPAddress* AG에 연결 하 합니다.
    - *서브넷 마스크* 의 서브넷 마스크는 *IPAddress*예: 255.255.255.0입니다.

2.  다른 복제본에 연결 하는 쿼리 창에서 AG에 복제본을 조인 하 고 보조 복제본에 주 데이터베이스에서 시드 프로세스를 시작 하려면 다음을 실행 합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  세 번째 복제본에 대 한 2 단계를 반복 합니다.

#### <a name="example-three--two-replicas-with-read-only-routing-none-cluster-type"></a>(None 유형 클러스터) 읽기 전용 라우팅을 사용 하 여 예 3-2 복제본

이 예제는 클러스터 유형의 None을 사용 하 여 2 복제본 구성의 생성을 보여줍니다. 장애 조치가 필요한, 읽기 크기 조정 시나리오에 사용 됩니다. 이 메서드는 읽기 전용 라우팅을, 뿐만 아니라 주 복제본 실제로 라운드 로빈 기능을 사용 하는 수신기를 만듭니다.

1.  데이터베이스의 완전 하 게 읽기/쓰기 복사본을 포함 하는 주 복제본이 될 노드에서 실행 합니다. 이 예제에서는 자동 시드를 사용 합니다.

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
    
    위치
    - *AGName* 가용성 그룹의 이름입니다.
    - *DBName* 가용성 그룹에 사용 될 데이터베이스의 이름입니다. 쉼표로 구분 된 이름 목록 일 수도 있습니다.
    - *PortOfEndpoint* 만든 끝점에서 사용 하는 포트 번호입니다.
    - *PortOfInstance* 의 인스턴스에 사용 되는 포트 번호는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.
    - *ListenerName* 이름인 기본 복제본이 다른 하지만 실제로 사용 되지 것입니다.
    - *PrimaryReplicaIPAddress* 주 복제본의 IP 주소입니다.
    - *서브넷 마스크* 의 서브넷 마스크는 *IPAddress*합니다. 예를 들어 255.255.255.0입니다.
    
2.  AG에 보조 복제본을 조인 하 고 자동 시드를 시작 합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>만들기는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에 대 한 권한과 로그인

Pacemaker 고가용성 클러스터 기본 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux에 액세스 해야 하는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 자체 가용성 그룹에 대 한 권한 뿐만 아니라 인스턴스를 합니다. 다음이 단계를 만들고 로그인 Pacemaker에 로그인 하는 방법을 알려 주는 파일과 함께 연결 된 사용 권한이 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.

1.  첫 번째 복제본에 연결 하는 쿼리 창에서 다음을 실행 합니다.

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD '<StrongPassword>';
    
    GO
    
    GRANT VIEW SERVER STATE TO PMLogin;
    
    GO
    
    GRANT ALTER, CONTROL, VIEW DEFINITION ON AVAILABILITY GROUP::<AGThatWasCreated> TO PMLogin;
    
    GO
    ```
    
2.  노드 1에서 명령을 입력합니다 
    ```bash
    sudo emacs /var/opt/mssql/secrets/passwd
    ```
    
    그러면 Emacs 편집기가 열립니다.
    
3.  편집기에 다음 두 줄을 입력 합니다.

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  CTRL 키를 누른 다음 X, 파일을 저장 하 고 종료 한 다음 C 키를 누릅니다.

5.  Parameter 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    에 파일 잠글 수 있습니다.

6.  복제본 역할을 수행 하는 다른 서버에서 1-5 단계를 반복 합니다.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>(외부에만 해당) Pacemaker 클러스터에서 가용성 그룹 리소스 만들기

후 가용성 그룹에 만들어집니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], 해당 리소스에에서 만들어야 Pacemaker, 외부 클러스터 종류를 지정 합니다. AG와 관련 된 두 개의 리소스: 자체 AG 및 IP 주소입니다. IP 주소 리소스 구성은 선택 사항 경우 수신기 기능을 사용 하지 않는 것이 좋습니다.

만들어지는 AG 리소스는 복제를 호출 하는 리소스의 특수 한 종류입니다. 각 노드에 기본적으로 받은 복사본 AG 리소스 이며 마스터 라는 하나의 제어 리소스입니다. 마스터 주 복제본을 호스팅하는 서버에 연결 됩니다. 보조 복제본 (정기적으로 또는 구성 전용) 슬레이브가 것으로 간주 됩니다 및 승격 될 수는 장애 조치에서 마스터입니다.

1.  다음 구문을 사용 하 여 AG 리소스를 만듭니다.

    **Red Hat Enterprise Linux (RHEL) 및 Ubuntu**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> --master meta notify=true
    ```

    >[!NOTE]
    >RHEL 7.4-마스터의를 사용 하 여 경고를 발생할 수 있습니다. 이 문제를 방지 하려면 사용 `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> master notify=true`
   
    **SUSE Linux Enterprise Server(SLES)**
    
    ```bash
    primitive <NameForAGResource> \
    ocf:mssql:ag \
    params ag_name="<AGName>" \
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
    
    여기서 *NameForAGResource* AG에 대해이 클러스터 리소스를 지정 하는 고유 이름입니다 및 *AGName* 만든 AG 이름입니다.
 
2.  기능 수신기와 연결 될 AG에 대 한 IP 주소 리소스를 만듭니다.

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
    
    여기서 *NameForIPResource* IP 리소스에 대 한 고유 이름 및 *IPAddress* 는 고정 IP 주소 리소스에 할당 합니다. SLES에 네트워크 마스크를 제공 해야 합니다. 예를 들어 255.255.255.0 값이에 대 한 24 갖기 *네트워크 마스크입니다.*
    
3.  AG 리소스와 IP 주소는 동일한 노드에서 실행을 보장 하려면 공동 배치 제약 조건 구성 되어야 합니다.

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
    
    여기서 *NameForIPResource* IP 리소스에 대 한 이름 *NameForAGResource* SLES, AG 리소스에 대 한 이름을 *NameForConstraint* 이름에 대 한는 제약 조건입니다.

4.  AG 리소스가를 확인 하도록 제약 조건을 순서 지정 및 실행 전에 IP 주소를 만듭니다. 공동 배치 제약 조건 의미는 정렬 제약 하는 동안이 적용 합니다.

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
    
    여기서 *NameForIPResource* IP 리소스에 대 한 이름 *NameForAGResource* SLES, AG 리소스에 대 한 이름을 *NameForConstraint* 이름에 대 한는 제약 조건입니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 만들고에 대 한 가용성 그룹을 구성 하는 방법을 배웠습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux. 방법에 대해 배웠습니다에:
> [!div class="checklist"]
> * 가용성 그룹을 사용 하도록 설정 합니다.
> * 인증서 및 만들기 AG 끝점입니다.
> * 사용 하 여 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) 또는 TRANSACT-SQL AG 만들려고 합니다.
> * 만들기는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에 대 한 권한과 로그인 합니다.
> * AG 리소스 Pacemaker 클러스터를 만듭니다.

대부분 AG 관리 작업을 업그레이드를 포함 하 고 들어 장애 조치에 대 한 참조.

> [!div class="nextstepaction"]
> [Linux에서 SQL Server에 대 한 HA 가용성 그룹 동작](sql-server-linux-availability-group-failover-ha.md)

