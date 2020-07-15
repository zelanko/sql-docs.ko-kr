## <a name="prerequisites"></a>필수 구성 요소

가용성 그룹을 만들려면 먼저 다음을 수행해야 합니다.

- 가용성 복제본을 호스트하는 모든 서버가 통신할 수 있도록 환경을 설정합니다.
- SQL Server를 설치합니다.

>[!NOTE]
>Linux에서는 가용성 그룹을 먼저 만들어야만 클러스터에서 관리할 클러스터 리소스로 추가할 수 있습니다. 이 문서에는 가용성 그룹을 만드는 예제가 나옵니다. 클러스터를 만들고 가용성 그룹을 클러스터 리소스로 추가하는 배포 관련 지침은 “다음 단계”에 있는 링크를 참조하세요.

1. 각 호스트의 컴퓨터 이름을 업데이트합니다.

   각 SQL Server 이름은 다음과 같아야 합니다.
   
   - 15자 이하입니다.
   - 네트워크 내에서 고유합니다.
   
   컴퓨터 이름을 설정하려면 `/etc/hostname`을 편집합니다. 다음 스크립트를 사용하면 `/etc/hostname`를 `vi`로 편집할 수 있습니다.

   ```bash
   sudo vi /etc/hostname
   ```

2. hosts 파일을 구성합니다.

    >[!NOTE]
    >호스트 이름이 DNS 서버에 해당 IP로 등록된 경우 다음 단계를 수행할 필요가 없습니다. 가용성 그룹 구성의 일부로 사용할 모든 노드가 서로 통신할 수 있는지 확인합니다. 호스트 이름에 대한 ping은 해당 IP 주소를 사용하여 회신해야 합니다. 또한 /etc/hosts 파일에 localhost IP 주소 127.0.0.1을 노드의 호스트 이름에 매핑하는 레코드가 포함되어 있지 않아야 합니다.
    >

   모든 서버의 호스트 파일에는 가용성 그룹에 참여할 모든 서버의 IP 주소 및 이름이 포함됩니다. 

   다음 명령은 현재 서버의 IP 주소를 반환합니다.

   ```bash
   sudo ip addr show
   ```

   `/etc/hosts`를 업데이트합니다. 다음 스크립트를 사용하면 `/etc/hosts`를 `vi`로 편집할 수 있습니다.

   ```bash
   sudo vi /etc/hosts
   ```

   다음 예제에서는 **node1**, **node2** 및 **node3**에 대한 항목이 추가된 **node1**의 `/etc/hosts`를 보여 줍니다. 이 문서에서 **node1**은 주 복제본을 호스트하는 서버를 나타냅니다. **node2** 및 **node3**는 보조 복제본을 호스트하는 서버를 참조합니다.

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>SQL Server 설치

SQL Server를 설치합니다. 다음 링크는 다양한 배포에 대한 SQL Server 설치 지침으로 연결됩니다. 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>AlwaysOn 가용성 그룹을 사용하도록 설정하고 mssql-server 다시 시작

SQL Server 인스턴스를 호스트하는 각 노드에서 AlwaysOn 가용성 그룹을 사용하도록 설정합니다. 그런 다음, `mssql-server`를 다시 시작합니다. 다음 스크립트를 실행합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwayson_health-event-session"></a>AlwaysOn_health 이벤트 세션을 사용하도록 설정 

AlwaysOn 가용성 그룹 확장 이벤트를 사용하도록 설정하여 가용성 그룹 문제를 해결할 때 근본적인 원인 진단에 도움을 줄 수도 있습니다. SQL Server의 각 인스턴스에서 다음 명령을 실행합니다. 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

이 XE 세션에 대한 자세한 내용은 [Always On 확장 이벤트](../database-engine/availability-groups/windows/always-on-extended-events.md)를 참조하세요.

## <a name="create-a-certificate"></a>인증서 만들기

Linux의 SQL Server 서비스는 인증서를 사용하여 미러링 엔드포인트 간의 통신을 인증합니다. 

다음 Transact-SQL 스크립트는 마스터 키와 인증서를 만듭니다. 그런 다음, 인증서를 백업하고 프라이빗 키로 파일을 보호합니다. 강력한 암호로 스크립트를 업데이트합니다. 기본 SQL Server 인스턴스에 연결합니다. 인증서를 만들려면 다음 Transact-SQL 스크립트를 실행합니다.

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

이제 기본 SQL Server 복제본은 `/var/opt/mssql/data/dbm_certificate.cer`에 인증서, `var/opt/mssql/data/dbm_certificate.pvk`에 프라이빗 키가 있습니다. 이러한 두 파일을 가용성 복제본을 호스트할 모든 서버의 동일한 위치로 복사합니다. mssql 사용자를 사용하거나 mssql 사용자에게 이러한 파일에 액세스할 수 있는 권한을 부여합니다. 

예를 들어 원본 서버에서 다음 명령은 파일을 대상 컴퓨터에 복사합니다. `**<node2>**` 값을 복제본을 호스트할 SQL Server 인스턴스의 이름으로 바꿉니다. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

각 대상 서버에서 mssql 사용자에게 인증서에 액세스할 수 있는 권한을 부여합니다.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>보조 서버에서 인증서 만들기

다음 Transact-SQL 스크립트는 기본 SQL Server 복제본에 대해 만든 백업을 사용하여 마스터 키와 인증서를 만듭니다. 강력한 암호로 스크립트를 업데이트합니다. 해독 암호는 이전 단계에서 .pvk 파일을 만들 때 사용한 암호와 동일합니다. 인증서를 만들려면 모든 보조 서버에서 다음 스크립트를 실행합니다.

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>모든 복제본에서 데이터베이스 미러링 엔드포인트 만들기

데이터베이스 미러링 엔드포인트는 TCP(전송 제어 프로토콜)를 사용하여 데이터베이스 미러링 세션에 참여하거나 가용성 복제본을 호스트하는 서버 인스턴스 간에 메시지를 보내고 받습니다. 데이터베이스 미러링 엔드포인트는 고유의 TCP 포트 번호에서 수신합니다. 

다음 Transact-SQL 스크립트는 가용성 그룹에 대해 수신하는 엔드포인트 `Hadr_endpoint`를 만듭니다. 이 스크립트는 엔드포인트를 시작하고 만든 인증서에 대해 연결 권한을 부여합니다. 스크립트를 실행하기 전에 `**< ... >**` 사이의 값을 바꿉니다. 필요에 따라 IP 주소 `LISTENER_IP = (0.0.0.0)`을 포함할 수 있습니다. 수신기 IP 주소는 IPv4 주소여야 합니다. 또한 `0.0.0.0`을 사용할 수 있습니다. 

모든 SQL Server 인스턴스에서 환경에 대한 다음 Transact-SQL 스크립트를 업데이트합니다. 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

>[!NOTE]
>한 노드에서 SQL Server Express Edition을 사용하여 구성 전용 복제본을 호스트하는 경우 `ROLE`의 유효한 값은 `WITNESS`뿐입니다. SQL Server Express Edition에서 다음 스크립트를 실행합니다.

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_PORT = **<5022>**)
    FOR DATABASE_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
```

방화벽의 TCP 포트를 수신기 포트용으로 열어 두어야 합니다.



>[!IMPORTANT]
>SQL Server 2017 릴리스의 경우 데이터베이스 미러링 엔드포인트에 지원되는 인증 방법은 `CERTIFICATE`뿐입니다. `WINDOWS` 옵션은 향후 릴리스에서 사용할 수 있습니다.

자세한 내용은 [데이터베이스 미러링 엔드포인트(SQL Server)](https://msdn.microsoft.com/library/ms179511.aspx)를 참조하세요.


