## <a name="prerequisites"></a>필수 구성 요소

전에 가용성 그룹을 만들 필요가 있습니다.

- 가용성 복제본을 호스팅하는 모든 서버에서 통신할 수 있도록 사용자 환경 설정
- SQL Server 설치

>[!NOTE]
>Linux 클러스터에서 관리 되는 클러스터 리소스로 추가 하기 전에 가용성 그룹을 만들어야 합니다. 이 문서에는 가용성 그룹을 만드는 예제를 제공 합니다. 배포에 대 한 구체적인 지침 클러스터를 만들고를 클러스터 리소스로 가용성 그룹을 추가 하는 링크를 참조 [다음 단계](#next-steps)합니다.

1. **각 호스트에 대 한 컴퓨터 이름을 업데이트합니다**

   각 SQL Server 이름 이어야 합니다.
   
   - 15 자 이하의
   - 네트워크 내에서 고유
   
   컴퓨터 이름을 설정 하려면 편집 `/etc/hostname`합니다. 다음 스크립트를 사용 하면 편집할 `/etc/hostname` 와 `vi`합니다.

   ```bash
   sudo vi /etc/hostname
   ```

1. **호스트 파일 구성**

>[!NOTE]
>호스트 이름에 등록 된 DNS 서버에 해당 IP를 경우 아래 단계를 수행할 필요가 없습니다. 가용성 그룹 구성의 일부로는 모든 노드 (호스트 이름을 해당 IP 주소와 함께 응답 해야을 ping) 서로 통신할 수 있는지 확인 합니다. 또한 해당 /etc/hosts 파일에 포함 된 노드의 호스트 이름으로 로컬 호스트 IP 주소 127.0.0.1을 매핑하는 레코드를 확인 합니다.


   모든 서버에 호스트 파일의 IP 주소 및 가용성 그룹에 참여할 모든 서버 이름을 포함 합니다. 

   다음 명령은 현재 서버의 IP 주소를 반환합니다.

   ```bash
   sudo ip addr show
   ```

   업데이트 `/etc/hosts`합니다. 다음 스크립트를 사용 하면 편집할 `/etc/hosts` 와 `vi`합니다.

   ```bash
   sudo vi /etc/hosts
   ```

   다음 예제와 `/etc/hosts` 에 **node1** 추가 대 한 내용은 **node1** 및 **node2**합니다. 이 문서에서 **node1** 기본 SQL Server 복제 데이터베이스를 가리킵니다. **node2** 보조 SQL Server를 가리킵니다.;


   ```
   127.0.0.1   localhost localhost4 localhost4.localdomain4
   ::1       localhost localhost6 localhost6.localdomain6
   10.128.18.128 node1
   10.128.16.77 node2
   ```

### <a name="install-sql-server"></a>SQL Server 설치

SQL Server를 설치 합니다. 다음 링크는 다양 한 분포에 대 한 SQL Server 설치 지침을 가리킵니다. 

- [Red Hat Enterprise Linux](..\linux\sql-server-linux-setup-red-hat.md)

- [SUSE Linux Enterprise Server](..\linux\sql-server-linux-setup-suse-linux-enterprise-server.md)

- [Ubuntu](..\linux\sql-server-linux-setup-ubuntu.md)

## <a name="enable-always-on-availability-groups-and-restart-sqlserver"></a>Always On 가용성 그룹을 사용 하도록 설정 하 고 sql server를 다시 시작

SQL Server 서비스를 호스팅하는 각 노드에서 Always On 가용성 그룹을 설정한 다음 다시 시작 `mssql-server`합니다.  다음 스크립트를 실행합니다.

```bash
sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled  1
sudo systemctl restart mssql-server
```

##    <a name="enable-alwaysonhealth-event-session"></a>AlwaysOn_health 이벤트 세션을 사용 하도록 설정 

Optionaly enable Always On 가용성 그룹 특정 확장 이벤트는 가용성 그룹의 문제를 해결할 때 근본 원인을 진단에 도움이 되도록 할 수 있습니다.

```Transact-SQL
ALTER EVENT SESSION  AlwaysOn_health ON SERVER WITH (STARTUP_STATE=ON);
GO
```

이 XE 세션에 대 한 자세한 내용은 참조 [항상에서 확장 이벤트](http://msdn.microsoft.com/library/dn135324.aspx)합니다.

## <a name="create-db-mirroring-endpoint-user"></a>끝점 사용자 미러링 db 만들기

다음 TRANSACT-SQL 스크립트 이라는 로그인을 만듭니다 `dbm_login`, 및 라는 사용자 `dbm_user`합니다. 강력한 암호를 가진 스크립트를 업데이트 합니다. 모든 SQL server 데이터베이스 미러링 끝점 사용자를 만들려면 다음 명령을 실행 합니다.

```Transact-SQL
CREATE LOGIN dbm_login WITH PASSWORD = '**<1Sample_Strong_Password!@#>**';
CREATE USER dbm_user FOR LOGIN dbm_login;
```

## <a name="create-a-certificate"></a>인증서 만들기

Linux에서 SQL Server 서비스를 미러링 끝점 간 통신을 인증 인증서를 사용 합니다. 

다음 TRANSACT-SQL 스크립트는 마스터 키와 인증서를 만듭니다. 그런 다음 인증서를 백업 하 고 개인 키가 있는 파일을 보호 합니다. 강력한 암호를 가진 스크립트를 업데이트 합니다. 기본 SQL Server에 연결 하 고 인증서를 만드는 다음 Transact SQL을 실행 합니다.

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
BACKUP CERTIFICATE dbm_certificate
   TO FILE = '/var/opt/mssql/data/dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '**<Private_Key_Password>**'
       );
```

이 시점에서 기본 SQL Server 복제 데이터베이스에 인증서가에서 `/var/opt/mssql/data/dbm_certificate.cer` 및 개인 키 at `var/opt/mssql/data/dbm_certificate.pvk`합니다. 가용성 복제본을 호스팅하는 모든 서버에서 같은 위치에이 두 파일을 복사 합니다. Mssql 사용자를 사용 하거나 이러한 파일에 액세스 하려면 mssql 사용자에 게 권한을 부여 합니다. 

예를 들어 원본 서버에서 다음 명령을 대상 컴퓨터에 파일 복사합니다. 대체는  **<node2>**  는 복제본을 호스팅하는 SQL Server 인스턴스 이름 사용 하 여 값입니다. 

```bash
cd /var/opt/mssql/data
scp dbm_certificate.* root@**<node2>**:/var/opt/mssql/data/
```

대상 서버에서 인증서에 액세스할 mssql 사용자에 게 권한을 부여 합니다.

```bash
cd /var/opt/mssql/data
chown mssql:mssql dbm_certificate.*
```

## <a name="create-the-certificate-on-secondary-servers"></a>보조 서버에서 인증서 만들기

다음 TRANSACT-SQL 스크립트 기본 SQL Server 복제 데이터베이스에 만든 백업에서 마스터 키와 인증서를 만듭니다. 명령에는 인증서에 액세스할 사용자 권한을 부여 합니다. 강력한 암호를 가진 스크립트를 업데이트 합니다. 해독 암호는 이전 단계에서 (.pvk) 파일을 만드는 데 사용한 암호와 동일 합니다. 인증서를 만드는 모든 보조 서버에서 다음 스크립트를 실행 합니다.

```Transact-SQL
CREATE MASTER KEY ENCRYPTION BY PASSWORD = '**<Master_Key_Password>**';
CREATE CERTIFICATE dbm_certificate   
    AUTHORIZATION dbm_user
    FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
    WITH PRIVATE KEY (
    FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
    DECRYPTION BY PASSWORD = '**<Private_Key_Password>**'
            );
```

## <a name="create-the-database-mirroring-endpoints-on-all-replicas"></a>데이터베이스 미러링 끝점에서 모든 복제본 만들기

데이터베이스 미러링 끝점은 TCP(전송 제어 프로토콜)를 사용하여 데이터베이스 미러링 세션에 참여하거나 가용성 복제본을 호스팅하는 서버 인스턴스 간에 메시지를 보내고 받습니다. 데이터베이스 미러링 끝점은 고유의 TCP 포트 번호에서 수신합니다. 

다음 TRANSACT-SQL 라는 수신 대기 끝점을 만듭니다 `Hadr_endpoint` 가용성 그룹에 대 한 합니다. 끝점을 시작한 연결 권한이 만든 사용자에 게 제공 합니다. 스크립트를 실행 하기 전에 사이의 값을 대체 `**< ... >**`합니다.


>[!NOTE]
>이 릴리스에 대 한 수신기 IP에 대 한 다른 IP 주소를 사용 하지 마십시오. 이 문제에 대 한 수정 작업 하지만 지금은 사용 가능한 값은 '0.0.0.0'.

모든 SQL Server 인스턴스에서 사용자 환경에 대 한 다음 TRANSACT-SQL을 업데이트 합니다. 

```Transact-SQL
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

>[!IMPORTANT]
>방화벽에서 TCP 포트에 대 한 수신기 포트가 열려 있어야 합니다.

자세한 내용은 참조 [데이터베이스 미러링 끝점 (SQL Server)](http://msdn.microsoft.com/library/ms179511.aspx)합니다.
