## <a name="prerequisites"></a>필수 구성 요소

가용성 그룹을 만들려면 먼저 다음을 수행해야 합니다.

- 가용성 복제본을 호스팅하는 모든 서버에서 통신할 수 있도록 환경을 설정 합니다.
- SQL Server를 설치합니다.

>[!NOTE]
>Linux 클러스터에서 관리 되는 클러스터 리소스로 추가 하기 전에 가용성 그룹 있습니다 만들어야 합니다. 이 문서에는 가용성 그룹을 만드는 예제가 나옵니다. 클러스터를 만들고 가용성 그룹 클러스터 리소스로 추가 배포 관련 내용은 "다음 단계" 링크를 참조 합니다.

1. 각 호스트에 대 한 컴퓨터 이름을 업데이트 합니다.

   각 SQL Server 이름은 다음과 같아야 합니다.
   
   - 15 자 이하인 합니다.
   - 네트워크 내에서 고유 합니다.
   
   컴퓨터 이름을 설정하려면 `/etc/hostname`을 편집합니다. 다음 스크립트를 사용 하면 편집할 `/etc/hostname` 와 `vi`:

   ```bash
   sudo vi /etc/hostname
   ```

2. 호스트 파일을 구성 합니다.

    >[!NOTE]
    >호스트 이름을 해당 ip를 DNS 서버에 등록 되어 있으면 다음 단계를 수행할 필요가 없습니다. 모든 노드는 가용성 그룹 구성의 포함 않습니다 서로 통신할 수 있는지 확인 합니다. (호스트 이름으로 ping 해당 IP 주소와 함께 응답 해야 합니다.) /Etc/hosts 파일 노드의 호스트 이름으로 로컬 호스트 IP 주소 127.0.0.1을 매핑하는 레코드를 포함 되지 않았는지 확인 합니다.
    >

   모든 서버의 호스트 파일에는 가용성 그룹에 참여할 모든 서버의 IP 주소 및 이름이 포함됩니다. 

   다음 명령은 현재 서버의 IP 주소를 반환합니다.

   ```bash
   sudo ip addr show
   ```

   `/etc/hosts`를 업데이트합니다. 다음 스크립트를 사용 하면 편집할 `/etc/hosts` 와 `vi`:

   ```bash
   sudo vi /etc/hosts
   ```

   다음 예제에서는 **node1**, **node2** 및 **node3**에 대한 항목이 추가된 **node1**의 `/etc/hosts`를 보여 줍니다. 이 문서에서는 **node1** 주 복제본을 호스팅하는 서버를 참조 합니다. 및 **node2** 및 **node3** 보조 복제본을 호스팅하는 서버를 참조 합니다.

    ```
    127.0.0.1   localhost localhost4 localhost4.localdomain4
    ::1       localhost localhost6 localhost6.localdomain6
    10.128.18.12 node1
    10.128.16.77 node2
    10.128.15.33 node3
    ```

### <a name="install-sql-server"></a>SQL Server 설치

SQL Server를 설치합니다. 다음 링크는 다양 한 분포에 대 한 SQL Server 설치 지침을 가리킵니다. 

- [Red Hat Enterprise Linux](../linux/quickstart-install-connect-red-hat.md)
- [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md)
- [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)

## <a name="enable-alwayson-availability-groups-and-restart-mssql-server"></a>AlwaysOn 가용성 그룹을 사용 하도록 설정 하 고 mssql 서버를 다시 시작

SQL Server 인스턴스를 호스팅하는 각 노드에서 AlwaysOn 가용성 그룹을 사용 합니다. 다시 시작 `mssql-server`합니다. 다음 스크립트를 실행합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##  <a name="enable-an-alwaysonhealth-event-session"></a>AlwaysOn_health 이벤트 세션을 사용 하도록 설정 

AlwaysOn 가용성 그룹이 가용성 그룹의 문제를 해결할 때 근본 원인을 진단에 도움이 되도록 확장된 이벤트를 선택적으로 사용할 수 있습니다. SQL Server의 각 인스턴스에 대해 다음 명령을 실행 합니다. 

```SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

이 XE 세션에 대 한 자세한 내용은 참조 [확장 이벤트 AlwaysOn](http://msdn.microsoft.com/library/dn135324.aspx)합니다.

## <a name="create-a-database-mirroring-endpoint-user"></a>한 데이터베이스 미러링 끝점 사용자 만들기

다음 TRANSACT-SQL 스크립트 이라는 로그인을 만듭니다 `dbm_login` 및 라는 사용자 `dbm_user`합니다. 강력한 암호로 스크립트를 업데이트합니다. 데이터베이스 미러링 끝점 사용자를 만들려면 모든 SQL Server 인스턴스에서 다음 명령을 실행 합니다.

```SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>인증서 만들기

Linux의 SQL Server 서비스는 인증서를 사용하여 미러링 끝점 간의 통신을 인증합니다. 

다음 TRANSACT-SQL 스크립트에는 마스터 키와 인증서를 만듭니다. 인증서를 백업 하 고 개인 키가 있는 파일을 보호 합니다. 강력한 암호로 스크립트를 업데이트합니다. 기본 SQL Server 인스턴스에 연결 합니다. 인증서를 만들려면 다음 Transact SQL 스크립트를 실행 합니다.

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

이 시점에서 기본 SQL Server 복제 데이터베이스에 인증서가에서 `/var/opt/mssql/data/dbm_certificate.cer` 및 개인 키 at `var/opt/mssql/data/dbm_certificate.pvk`합니다. 이러한 두 파일을 가용성 복제본을 호스트할 모든 서버의 동일한 위치로 복사합니다. Mssql 사용자를 사용 하거나 이러한 파일에 액세스 하려면 mssql 사용자에 게 권한을 부여 합니다. 

예를 들어 원본 서버에서 다음 명령을 대상 컴퓨터에 파일 복사합니다. 대체는 `**<node2>**` 는 복제본을 호스팅하는 SQL Server 인스턴스 이름 사용 하 여 값입니다. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

각 대상 서버에서 인증서에 액세스할 mssql 사용자에 게 권한을 부여 합니다.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>보조 서버에서 인증서 만들기

다음 TRANSACT-SQL 스크립트 기본 SQL Server 복제 데이터베이스에 만든 백업에서 마스터 키와 인증서를 만듭니다. 이 명령은 사용자에게 인증서에 액세스할 권한도 부여합니다. 강력한 암호로 스크립트를 업데이트합니다. 해독 암호는 이전 단계에서 .pvk 파일을 만들 때 사용한 암호와 동일합니다. 인증서를 만들려면 모든 보조 서버에서 다음 스크립트를 실행 합니다.

```SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>모든 복제본에서 데이터베이스 미러링 끝점 만들기

데이터베이스 미러링 끝점 (TCP (Transmission Control Protocol)를 사용 하 여 데이터베이스 미러링 세션에에서 참여 하거나 가용성 복제본을 호스팅하는 서버 인스턴스 간에 메시지를 주고받을 수 있습니다. 데이터베이스 미러링 끝점은 고유의 TCP 포트 번호에서 수신합니다. TCP 수신기 수신기 IP 주소가 필요합니다. 수신기 IP 주소는 IPv4 주소 여야 합니다. 사용할 수도 있습니다 `0.0.0.0`합니다. 

다음 TRANSACT-SQL 스크립트 라는 수신 대기 끝점을 만듭니다 `Hadr_endpoint` 가용성 그룹에 대 한 합니다. 끝점을 시작 하 고 만든 사용자에 게 연결 권한을 부여 합니다. 스크립트를 실행하기 전에 `**< ... >**` 사이의 값을 바꿉니다.

모든 SQL Server 인스턴스에서 사용자 환경에 대해 다음 TRANSACT-SQL 스크립트를 업데이트 합니다. 

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = ALL,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

>[!NOTE]
>SQL Server Express Edition 한 노드에서 구성 전용 복제본에 대 한 유일한 유효 값을 호스팅하는 데 사용 하는 경우 `ROLE` 은 `WITNESS`합니다. SQL Server Express Edition에서 다음 스크립트를 실행 합니다.

```SQL
CREATE ENDPOINT [Hadr_endpoint]
    AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = **<5022>**)
    FOR DATA_MIRRORING (
        ROLE = WITNESS,
        AUTHENTICATION = CERTIFICATE dbm_certificate,
        ENCRYPTION = REQUIRED ALGORITHM AES
        );
ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login];
```

방화벽에서 TCP 포트에 대 한 수신기 포트가 열려 있어야 합니다.



>[!IMPORTANT]
>SQL Server 2017 릴리스에 대 한 데이터베이스 미러링 끝점에 대 한 지원 되는 유일한 인증 방법은 `CERTIFICATE`합니다. `WINDOWS` 이후 버전에서 옵션 설정 됩니다.

자세한 내용은 참조 [데이터베이스 미러링 끝점 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)합니다.


