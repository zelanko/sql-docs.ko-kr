---
title: 만들고 Linux의 SQL Server에 대 한 가용성 그룹 구성
description: 이 자습서에서는 만들고 Linux의 SQL Server에 대 한 가용성 그룹을 구성 하는 방법을 보여 줍니다.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 06/28/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 7bd6f1259989c1cb0286fca546ea9e0410e0837f
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833901"
---
# <a name="create-and-configure-an-availability-group-for-sql-server-on-linux"></a>만들고 Linux의 SQL Server에 대 한 가용성 그룹 구성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 자습서에 대 한 만들기 및 가용성 그룹 (AG) 구성 방법에 설명 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux. 와 달리 [!INCLUDE[sssql15-md](../includes/sssql15-md.md)] 이전에 Windows를 설정할 수 있습니다. Ag 기본 Pacemaker 클러스터를 먼저 만들 유무 및 합니다. 클러스터와의 통합 필요에 따라 수행 되지 않으므로 나중.

이 자습서에는 다음 작업이 포함 됩니다.
 
> [!div class="checklist"]
> * 가용성 그룹을 사용 하도록 설정 합니다.
> * 인증서 및 가용성 그룹 끝점을 만듭니다.
> * 사용 하 여 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) 또는 TRANSACT-SQL을 가용성 그룹을 만듭니다.
> * 만들기는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에 대 한 사용 권한과 로그인 합니다.
> * Pacemaker 클러스터 (외부 형식에만 해당)에서 가용성 그룹 리소스를 만듭니다.

## <a name="prerequisite"></a>사전 요구 사항
- 에 설명 된 대로 Pacemaker 고가용성 클러스터를 배포 [SQL Server on Linux의 Pacemaker 클러스터를 배포](sql-server-linux-deploy-pacemaker-cluster.md)합니다.


## <a name="enable-the-availability-groups-feature"></a>가용성 그룹 기능을 사용 하도록 설정

와 달리, Windows에서 사용할 수 없습니다 PowerShell 또는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Configuration Manager 가용성 그룹 (AG) 기능입니다. Linux를 사용 해야 `mssql-conf` 기능을 사용 하도록 합니다. 가용성 그룹 기능을 사용 하는 방법은 두 가지: 사용 된 `mssql-conf` 유틸리티 또는 편집은 `mssql.conf` 파일을 수동으로.

> [!IMPORTANT]
> 에서도 구성 전용 복제본에 대 한 AG 기능을 사용 하도록 해야 [!INCLUDE[ssexpress-md](../includes/ssexpress-md.md)]합니다.

### <a name="use-the-mssql-conf-utility"></a>Mssql conf 유틸리티 사용

프롬프트에서 다음을 실행 합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
```

### <a name="edit-the-mssqlconf-file"></a>Mssql.conf 파일 편집

수정할 수도 있습니다는 `mssql.conf` 아래에 있는 파일은 `/var/opt/mssql` 폴더에 다음 줄을 추가 합니다.

```
[hadr]

hadr.hadrenabled = 1
```

### <a name="restart-includessnoversion-mdincludesssnoversion-mdmd"></a>다시 시작 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]
다시 시작 해야 Windows에서에 따라 가용성 그룹을 사용 하도록 설정한 후 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다. 다음으로 수행할 수 있습니다.

```bash
sudo systemctl restart mssql-server
```

## <a name="create-the-availability-group-endpoints-and-certificates"></a>인증서 및 가용성 그룹 끝점 만들기

가용성 그룹을 통신에 대 한 TCP 끝점을 사용합니다. Linux에서 AG에 대 한 끝점은 경우에 지원 인증서 인증에 사용 됩니다. 즉, 동일한 AG에 참여 하는 복제본 수 있는 다른 모든 인스턴스에 대 한 인스턴스에서 인증서를 복원할 수 해야 합니다. 인증서 과정이 구성 전용 복제본에 대해서도 필요 합니다. 

끝점을 만들고 인증서를 복원만 TRANSACT-SQL을 통해 수행할 수 있습니다. 비-사용할 수 있습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]-인증서도 생성 합니다. 프로세스를 관리 하 고 만료 되는 모든 인증서를 교체 해야 합니다.

> [!IMPORTANT]
> 사용 하려는 경우는 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 경우에 AG를 만들기 위해 마법사를 만들고 Linux의 TRANSACT-SQL을 사용 하 여 인증서를 복원 해야 합니다.

다양 한 명령 (예: 추가 보안)에 대 한 사용 가능한 옵션에서 전체 구문의 경우, 다음을 참조 하세요.

-   [BACKUP CERTIFICATE](../t-sql/statements/backup-certificate-transact-sql.md)
-   [인증서 만들기](../t-sql/statements/create-certificate-transact-sql.md)
-   [CREATE ENDPOINT](../t-sql/statements/create-endpoint-transact-sql.md)

> [!NOTE]
> 끝점의 형식을 사용 하 여 가용성 그룹을 만들어야 합니다 하지만 *FOR DATABASE_MIRRORING*이므로 몇 가지 기본 측면은 이제 사용 되지 않는 기능을 사용 하 여 한 번 공유 합니다.

이 예제에서는 3 개 노드 구성에 대 한 인증서를 만듭니다. 인스턴스 이름을 LinAGN1, LinAGN2, 및 LinAGN3입니다.

1.  다음을 실행 하 여 마스터 키, 인증서 및 끝점을 만들려면 LinAGN1와 인증서를 백업 합니다. 예를 들어 일반적인 TCP 포트 5022의 끝점에 사용 됩니다.
    
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
    
3.  마지막으로 LinAGN3에서 같은 시퀀스를 수행 합니다.
    
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
    
4.  사용 하 여 `scp` 또는 다른 유틸리티에서 인증서의 백업을 AG의 일부가 될 각 노드에 복사 합니다.
    
    이 예제:
    
    - LinAGN2 및 LinAGN3 LinAGN1_Cert.cer 복사
    - LinAGN2_Cert.cer LinAGN1 LinAGN3를 복사 합니다.
    - LinAGN3_Cert.cer LinAGN1 LinAGN2를 복사 합니다.
    
5.  소유권 및 복사한 인증서 파일을 사용 하 여 연결 된 그룹을 변경 `mssql`합니다.
    
    ```bash
    sudo chown mssql:mssql <CertFileName>
    ```
    
6.  인스턴스 수준 로그인 및 LinAGN2 LinAGN1에서 LinAGN3와 연결 된 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
7.  LinAGN2_Cert 및 LinAGN3_Cert LinAGN1에 복원 합니다. 다른 복제본의 인증서는 것이 AG 통신 및 보안의 중요 한 측면입니다.
    
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
    
9.  인스턴스 수준 로그인 및 LinAGN1 LinAGN2에서 LinAGN3와 연결 된 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN3_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN3_User FOR LOGIN LinAGN3_Login;
    
    GO
    ```
    
10. LinAGN1_Cert 및 LinAGN3_Cert LinAGN2에 복원 합니다.
    
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
    
11. LinAGN2의 끝점에 연결할 LinAG1 및 LinAGN3 권한으로 연결 된 로그인 권한을 부여 합니다.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN3_Login;
    
    GO
    ```
    
12. 인스턴스 수준 로그인 및 LinAGN1 LinAGN3에서 LinAGN2와 연결 된 사용자를 만듭니다.
    
    ```SQL
    CREATE LOGIN LinAGN1_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN1_User FOR LOGIN LinAGN1_Login;
    
    GO
    
    CREATE LOGIN LinAGN2_Login WITH PASSWORD = '<StrongPassword>';
    CREATE USER LinAGN2_User FOR LOGIN LinAGN2_Login;
    
    GO
    ```
    
13. LinAGN1_Cert 및 LinAGN2_Cert LinAGN3에 복원 합니다. 
    
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
    
14. LinAGN3의 끝점에 연결할 LinAG1 및 LinAGN2 권한으로 연결 된 로그인 권한을 부여 합니다.
    
    ```SQL
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN1_Login;
    
    GO
    
    GRANT CONNECT ON ENDPOINT::AGEP TO LinAGN2_Login;
    
    GO
    ```

## <a name="create-the-availability-group"></a>가용성 그룹 만들기

이 섹션에서는 사용 하는 방법을 다룹니다 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) 또는 TRANSACT-SQL에 대 한 가용성 그룹을 만들려면 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.

### <a name="use-includessmanstudiofull-mdincludesssmanstudiofull-mdmd"></a>[!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] 사용

이 섹션에서는 SSMS를 사용 하 여 새 가용성 그룹 마법사를 사용 하 여 클러스터 유형이 외부인을 사용 하 여 AG를 만드는 방법.

1.  SSMS에서 확장 **Always On 고가용성**를 마우스 오른쪽 단추로 클릭 **가용성 그룹**를 선택 하 고 **새 가용성 그룹 마법사**합니다.

2.  소개 대화 상자에서 클릭 **다음**합니다.

3.  가용성 그룹 옵션 지정 대화 상자에서 가용성 그룹의 이름을 입력 하 고 드롭다운 목록에서 외부 없거나 클러스터 유형을 선택 합니다. 외부는 Pacemaker를 배포할 때 사용 해야 합니다. None 읽기 확장과 같은 특별 한 시나리오입니다. 데이터베이스 수준 상태 검색에 대 한 옵션을 선택 하는 것은 선택 사항입니다. 이 옵션에 대 한 자세한 내용은 참조 하세요. [가용성 그룹 데이터베이스 수준의 상태 검색 장애 조치 옵션](../database-engine/availability-groups/windows/sql-server-always-on-database-health-detection-failover-option.md)합니다. **다음**을 클릭합니다.

    ![](./media/sql-server-linux-create-availability-group/image3.png)

4.  데이터베이스 선택 대화 상자에서 AG에 참여할 데이터베이스를 선택 합니다. 각 데이터베이스를 AG에 추가할 수 있습니다 전체 백업이 있어야 합니다. **다음**을 클릭합니다.

5.  복제본 지정 대화 상자에서 클릭 **복제본 추가**합니다.

6.  서버 대화 상자에 연결, Linux 인스턴스의 이름을 입력 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 보조 복제본 및 연결 자격 증명이 사용 됩니다. **연결**을 클릭합니다.

7.  에 다른 보조 복제본 또는 구성 전용 복제본을 포함 하는 인스턴스에 대 한 이전 두 단계를 반복 합니다.

8.  이제 세 인스턴스는 모두 복제본 지정 대화 상자에 나열 됩니다. True는 보조 복제본이 될 보조 복제본의 클러스터 유형이 외부인 경우 사용 하는 경우에 일치 주 복제본의 가용성 모드 및 장애 조치 모드가 External로 설정 되어 있는지 확인 합니다. 구성 전용 복제본에 대 한 구성의 가용성 모드를만 선택 합니다.

    다음 예제에서는 두 개의 복제본, 클러스터 유형이 외부인 경우 및 구성 전용 복제본을 사용 하 여 AG를 보여 줍니다.

    ![](./media/sql-server-linux-create-availability-group/image4.png)

    다음 예제에서는 두 개의 복제본 AG, 클러스터 유형이 None, 및 구성 전용 복제본을 보여 줍니다.

    ![](./media/sql-server-linux-create-availability-group/image5.png)

9.  백업 기본 설정을 변경 하려는 경우 백업 기본 설정 탭을 클릭 합니다. Ag 사용 하 여 백업 기본 설정에 대 한 자세한 내용은 참조 하세요. [가용성 복제본에 백업 구성](../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)합니다.

10. 클러스터를 사용 하 여 AG를 만들거나 읽기 가능한 보조 복제본을 사용 하 여 읽기-배율에 대 한 none 입력을 하는 경우 수신기 탭을 선택 하 여 수신기를 만들 수 있습니다. 수신기를 나중에 추가할 수 있습니다. 옵션을 선택 하는 수신기를 만들려면 **가용성 그룹 수신기 만들기** 를 이름, TCP/IP 포트 및 정적 또는 자동으로 할당 된 DHCP IP 주소를 사용할지 여부를 입력 합니다. 클러스터 유형이 없음인는 AG에 대 한 IP 되도록 설정 하 고 정적 기억 주의 IP 주소입니다.

    ![](./media/sql-server-linux-create-availability-group/image6.png)

11. 읽을 수 있는 시나리오에 대 한 수신기를 만든 경우 SSMS 17.3 이상 마법사에서 읽기 전용 라우팅을 만들 수 있습니다. SSMS 또는 TRANSACT-SQL을 통해 나중에 추가할 수도 있습니다. 읽기 전용 라우팅을 이제 추가:

    a.  읽기 전용 라우팅을 탭을 선택 합니다.

    b.  읽기 전용 복제본에 대 한 Url을 입력 합니다. 이러한 Url 끝점 하지 인스턴스 포트를 사용 하는 점을 제외 하 고 끝점와 비슷합니다.

    c.  각 URL을 선택 하 고 맨 아래에서 읽기 가능한 복제본을 선택 합니다. 다중 선택 하려면 SHIFT 또는 클릭 끌기 누른 합니다.

12. **다음**을 클릭합니다.

13. 보조 복제본은 초기화 하는 방법을 선택 합니다. 기본값을 사용 하는 것 [자동 시드](../database-engine/availability-groups/windows/automatically-initialize-always-on-availability-group.md), 동일한 경로 AG에 참여 하는 모든 서버에 필요 합니다. (두 번째 옵션); 복원 마법사 백업, 복사를 수행할 수도 있습니다. 수동으로 백업, 복사, 하 고 복제본에서 데이터베이스를 복원 하는 경우 조인 있습니다 (옵션 3 차); 또는 나중에 데이터베이스 추가 (마지막 옵션). 인증서를 수동으로 백업 하 고 복사 하는 경우와 마찬가지로 백업 파일에 대 한 권한을 다른 복제본에서 설정 해야 합니다. **다음**을 클릭합니다.

14. 유효성 검사 대화 상자에서 모든 돌아오지 않으면 성공으로, 경우 조사 합니다. 일부 경고는 허용 및 치명적이 지 않음, 같은 수신기를 만들지 않도록 하는 경우입니다. **다음**을 클릭합니다.

15. 요약 대화 상자에서 클릭 **완료**합니다. 이제 AG를 만드는 프로세스를 시작 합니다.

16. AG를 만드는 완료 되 면 클릭 **닫기** 결과입니다. 이제 SSMS에서 Always On 고가용성 폴더 및 동적 관리 뷰에서 복제본 AG를 볼 수 있습니다.

### <a name="use-transact-sql"></a>Transact-SQL 사용

이 섹션에서는 TRANSACT-SQL을 사용 하 여 AG를 만드는 방법의 예제를 보여 줍니다. AG 만들어진 후에 수신기 및 읽기 전용 라우팅을 구성할 수 있습니다. 자체 AG를 사용 하 여 수정할 수 있습니다 `ALTER AVAILABILITY GROUP`에서 수행할 수 없는 클러스터 유형을 변경 하지만 [!INCLUDE[sssql17-md](../includes/sssql17-md.md)]합니다. 클러스터 유형이 외부인을 사용 하 여 AG를 만들려는 되지는 않은 경우 삭제 하 고 클러스터 유형이 None을 사용 하 여 다시 만들어야 합니다. 자세한 내용 및 기타 옵션은 다음 링크에서 찾을 수 있습니다.

-   [CREATE AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md)
-   [ALTER AVAILABILITY GROUP(Transact-SQL)](../t-sql/statements/alter-availability-group-transact-sql.md)
-   [가용성 그룹 (SQL Server)에 대 한 읽기 전용 라우팅 구성](../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)
-   [(SQL Server)는 가용성 그룹 수신기 만들기 또는 구성](../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)

#### <a name="example-one---two-replicas-with-a-configuration-only-replica-external-cluster-type"></a>구성 전용 복제본 (외부 클러스터 형식)를 사용 하 여 예제 1-2 복제본

이 예제에는 구성 전용 복제본을 사용 하는 두 개의 복제본 AG를 만드는 방법을 보여 줍니다.

1.  주 복제본 데이터베이스의 완전 읽기/쓰기 복사본을 포함 하 되는 노드에서 실행 합니다. 이 예제에서는 자동 시드를 사용 합니다.

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
    
2.  다른 복제본에 연결 된 쿼리 창에서 AG에 복제본을 조인 하 고 보조 복제본으로 주 데이터베이스에서 시드 프로세스를 시작 하려면 다음을 실행 합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3. 구성 전용 복제본에 연결 된 쿼리 창에서 AG에 조인 합니다.
    
   ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
   ```

#### <a name="example-two---three-replicas-with-read-only-routing-external-cluster-type"></a>예제 2-3 개 복제본 읽기 전용 라우팅을 (외부 클러스터 형식)

이 예제에서는 세 가지 전체 복제본 및 읽기 전용 라우팅 초기 AG 만들기의 일환으로 구성할 수 있습니다.

1.  주 복제본 데이터베이스의 완전 읽기/쓰기 복사본을 포함 하 되는 노드에서 실행 합니다. 이 예제에서는 자동 시드를 사용 합니다.

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
    
    이 구성에 대해 몇 가지 사항은 다음과 같습니다.
    
    - *AGName* 가용성 그룹의 이름입니다.
    - *DBName* 가용성 그룹을 사용 하 여 사용할 데이터베이스의 이름입니다. 쉼표로 구분 된 이름 목록 일 수도 있습니다.
    - *ListenerName* 기본 서버/노드 중 하나가 다른 이름입니다. 와 함께 DNS에 등록 됩니다 *IPAddress*합니다.
    - *IPAddress* 는 연결 된 IP 주소 *ListenerName*합니다. 고유 이기도 동일 하지는 않습니다 서버/노드 중 하나입니다. 응용 프로그램 및 최종 사용자가 사용 됩니다 *ListenerName* 또는 *IPAddress* AG를 연결할 수 있습니다.
    - *SubnetMask* 의 서브넷 마스크 *IPAddress*; 예를 들어 255.255.255.0입니다.

2.  다른 복제본에 연결 된 쿼리 창에서 AG에 복제본을 조인 하 고 보조 복제본으로 주 데이터베이스에서 시드 프로세스를 시작 하려면 다음을 실행 합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = EXTERNAL);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```
    
3.  세 번째 복제본에 대 한 2 단계를 반복 합니다.

#### <a name="example-three---two-replicas-with-read-only-routing-none-cluster-type"></a>예제에서는 3 개의 복제본 (None 클러스터 유형) 읽기 전용 라우팅을 사용 하 여

이 예제에서는 클러스터 유형이 None을 사용 하 여 두 개의 복제 구성의 생성을 보여 줍니다. 읽기 확장 시나리오에 대 한 장애 조치가 필요한 경우 사용 됩니다. 이 읽기 전용 라우팅, 뿐만 아니라 실제로 주 복제본을 라운드 로빈 기능을 사용 하는 수신기를 만듭니다.

1.  주 복제본 데이터베이스의 완전 읽기/쓰기 복사본을 포함 하 되는 노드에서 실행 합니다. 이 예제에서는 자동 시드를 사용 합니다.

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
    - *DBName* 가용성 그룹을 사용 하 여 사용할 데이터베이스의 이름입니다. 쉼표로 구분 된 이름 목록 일 수도 있습니다.
    - *PortOfEndpoint* 만들어진 끝점에서 사용 하는 포트 번호입니다.
    - *PortOfInstance* 의 인스턴스에서 사용할 포트 번호는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.
    - *ListenerName* 다른 기본 복제본 중 하나 이지만 실제로 사용 되지 것입니다는 이름입니다.
    - *PrimaryReplicaIPAddress* 주 복제본의 IP 주소입니다.
    - *SubnetMask* 의 서브넷 마스크 *IPAddress*합니다. 예를 들어, 255.255.255.0입니다.
    
2.  AG에 보조 복제본을 조인 하 고 자동 시드를 시작 합니다.
    
    ```SQL
    ALTER AVAILABILITY GROUP [<AGName>] JOIN WITH (CLUSTER_TYPE = NONE);
    
    GO
    
    ALTER AVAILABILITY GROUP [<AGName>] GRANT CREATE ANY DATABASE;
    
    GO
    ```

## <a name="create-the-includessnoversion-mdincludesssnoversion-mdmd-login-and-permissions-for-pacemaker"></a>만들기는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 로그인 및 Pacemaker에 대 한 사용 권한

Pacemaker 고가용성 클러스터 내부 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux에 대 한 액세스를 해야 합니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] 자체 가용성 그룹에 대 한 권한 뿐만 아니라 인스턴스. 다음이 단계를 만들고 로그인 Pacemaker 로그인 하는 방법을 알려 주는 파일과 함께 연관된 된 권한을 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)]합니다.

1.  첫 번째 복제본에 연결 된 쿼리 창에서 다음을 실행 합니다.

    ```SQL
    CREATE LOGIN PMLogin WITH PASSWORD ='<StrongPassword>';
    
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
    
    Emacs 편집기에서 열립니다.
    
3.  편집기에 다음 두 줄을 입력 합니다.

    ```
    PMLogin
    <StrongPassword>
    ```
    
4.  CTRL 키를 누른 다음 X 파일을 저장 하 고 종료 한 다음 C 키를 누릅니다.

5.  실행 
    ```bash
    sudo chmod 400 /var/opt/mssql/secrets/passwd
    ```
    
    에 파일을 잠급니다.

6.  복제본으로 사용할 다른 서버에서 1 ~ 5 단계를 반복 합니다.

## <a name="create-the-availability-group-resources-in-the-pacemaker-cluster-external-only"></a>Pacemaker 클러스터 (외부에만 해당)의 가용성 그룹 리소스 만들기

가용성 그룹이 만들어진 후에 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)], 외부 클러스터 유형이 지정 된 경우 Pacemaker에 해당 리소스를 생성 해야 합니다. AG와 관련 된 두 개의 리소스가 있습니다: 자체 AG와 IP 주소입니다. 수신기 기능을 사용 하지 않지만 권장 되는 데 사용 되는 경우 IP 주소 리소스를 구성 합니다. 선택 사항입니다.

만든 AG 리소스는 복제본을 호출 하는 리소스의 특별 한 합니다. 기본적으로 복사본이 각 노드에서 AG 리소스가 되며 마스터 라는 하나의 제어 리소스. 마스터 주 복제본을 호스팅하는 서버를 사용 하 여 연결 됩니다. 보조 복제본 (일반 또는 구성 전용) 슬레이브 것으로 간주 됩니다 및 승격 될 수 있습니다 (failover)에서 마스터입니다.

1.  다음 구문을 사용 하 여 AG 리소스를 만듭니다.

    **Ubuntu 및 Red Hat Enterprise Linux (RHEL)**
    
    ```bash
    sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failure-timeout=30s --master meta notify=true
    ```

    >[!NOTE]
    >RHEL 7.4에서 사용 하 여-마스터 경고가 발생할 수 있습니다. 이 문제를 방지 하려면 사용 `sudo pcs resource create <NameForAGResource> ocf:mssql:ag ag_name=<AGName> meta failover-timeout=30s master notify=true`
   
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
    
    여기서 *NameForAGResource* AG에 대해이 클러스터 리소스에 지정 된 고유 이름 및 *AGName* 만든 AG의 이름입니다.
 
2.  수신기 기능과 관련 된 AG에 대해 IP 주소 리소스를 만듭니다.

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
    
    여기서 *NameForIPResource* IP 리소스에 대 한 고유 이름 및 *IPAddress* 고정 IP 주소 리소스에 할당 됩니다. SLES에서의 네트워크 마스크를 제공 해야 합니다. 예를 들어, 255.255.255.0 값이에 대 한 24 해야 *네트워크 마스크입니다.*
    
3.  을 보장 하기 위해 IP 주소 및 AG 리소스가 동일한 노드에서 실행 되는 공동 배치 제약 조건을 구성 되어야 합니다.

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
    
    여기서 *NameForIPResource* IP 리소스에 대 한 이름 *NameForAGResource* AG 리소스 및 SLES에서의 이름인 *NameForConstraint* 의 이름인는 제약 조건입니다.

4.  AG 리소스가 구성 되었는지 확인 하도록 제약 조건을 순서 지정 및 실행 전에 IP 주소를 만듭니다. 공동 배치 제약 조건을 정렬 제약 조건을 의미 하는 동안이 적용 됩니다.

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
    
    여기서 *NameForIPResource* IP 리소스에 대 한 이름 *NameForAGResource* AG 리소스 및 SLES에서의 이름인 *NameForConstraint* 의 이름인는 제약 조건입니다.

## <a name="next-steps"></a>다음 단계

이 자습서에서는 만들고 가용성 그룹을 구성 하는 방법을 배웠습니다 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] linux. 방법을 배웠습니다에:
> [!div class="checklist"]
> * 가용성 그룹을 사용 하도록 설정 합니다.
> * 인증서 및 끝점 만들기 AG입니다.
> * 사용 하 여 [!INCLUDE[ssmanstudiofull-md](../includes/ssmanstudiofull-md.md)] (SSMS) 또는 TRANSACT-SQL을 AG를 만듭니다.
> * 만들기는 [!INCLUDE[ssnoversion-md](../includes/ssnoversion-md.md)] Pacemaker에 대 한 사용 권한과 로그인 합니다.
> * Pacemaker 클러스터에서 AG 리소스를 만듭니다.

대부분의 AG 관리 등의 작업을 업그레이드 및 장애 조치를 참조 하세요.

> [!div class="nextstepaction"]
> [Linux의 SQL Server에 대 한 HA 가용성 그룹을 작동](sql-server-linux-availability-group-failover-ha.md)

